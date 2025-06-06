# Workshop Activity

Google Earth Engine provides an interface to process large amounts of spatial imagery with a few lines of code. Rather than searching for and downloading many raster files, Google Earth Engine processes imagery in the cloud. In this lab, students will learn how to conduct a supervised land classification in Google Earth Engine using JavaScript.

After creating your Google Earth Engine account, go to <https://code.earthengine.google.com>. Then, create a new script.

## Import Landsat Data

The first step is to define a region. The simplest approach is to use the tools in the map area to create a marker (point). This marker will appear in the Imports section at the top of the script as a variable called geometry. Change the name of this variable to point. Optionally, you can create a rectangle or polygon to define your area of interest, which you can later use to clip your data (change the name of this variable to poly). Next, we will import Landsat 8 imagery. Under Search places and datasets..., type Landsat 8, and select USGS Landsat 8 Level 2, Collection 2, Tier 1 and click the Import button. Change the name of the variable under Imports to ls8_sr. We can also import elevation data. Search for SRTM, and import NASA SRTM Digital Elevation 30m. Rename this variable to srtm.

The following code will center the map over your point when the code is run.

```JavaScript
Map.centerObject(point, 7);
```

Now we can add the SRTM to the map.

```JavaScript
Map.addLayer(srtm, {min:0, max:3000}, 'SRTM DEM');
```

Alternatively, we can clip to our region of interest if defined as a polygon:

```JavaScript
var srtm_clip = srtm.clip(poly);

Map.addLayer(srtm_clip, {min:2250, max:3000}, 'SRTM DEM');
```

We can create and view a hillshade of the same elevation surface:

```JavaScript
var hillshade = ee.Terrain.hillshade(srtm_clip, 315, 45);
Map.addLayer(hillshade, null, 'Hillshade');
```

## Generate a Cloud Free Composite

Next we will define some variables, including a date range and amount of cloud cover.

```JavaScript
var start = '2023-01-01';
var end = '2023-12-31';

var cloud_max = 50;
```

Imagery will now be filtered to dates within the year 2023 with less than 50% cloud cover using the following code.

```JavaScript
var ls8filtered = ls8_sr
  .filterDate(start,end)
  .filterBounds(poly)
  .filterMetadata('CLOUD_COVER','less_than',cloud_max);
```

We can print the new image collection to determine the size of our data:

```JavaScript
print(ls8filtered);
```

We now define several functions to rescale the imagery and to apply the cloud mask.

```JavaScript
//function to rescale LS8 in GEE
var apply_offset = function(image){
  return image.toFloat().multiply(0.0000275).add(-0.2).set('system:time_start',image.get('system:time_start'));
};

//define LS8 cloud mask function based on QA band
var L8CloudMask_fun = function (image) {
  // Bits 3 and 5 are cloud shadow and cloud, respectively.
  var cloudShadowBitMask = 1 << 3;
  var cloudsBitMask = 1 << 5;

// Get the pixel QA band.
  var qa = image.select('QA_PIXEL');

 // Both flags should be set to zero, indicating clear conditions.
  var mask = qa.bitwiseAnd(cloudShadowBitMask).eq(0)
      .and(qa.bitwiseAnd(cloudsBitMask).eq(0));

// Return the masked image, scaled to reflectance, without the QA bands.
  return image.updateMask(mask)
      .select('SR_B1', 'SR_B2','SR_B3', 'SR_B4', 'SR_B5', 'SR_B6', 'SR_B7').rename('B1','B2','B3','B4','B5','B6','B7')
      .set('system:time_start',image.get('system:time_start'))
}

//apply cloud mask function and offset function
var LS8_masked = ls8filtered.map(L8CloudMask_fun).map(apply_offset);
print(LS8_masked);
```

Finally, we can display the filtered, masked, and rescaled imagery. Defining the bands as B4, B3, B2 creates a true color composite.

```JavaScript
//create LS8 median composite and display
var composite = LS8_masked.median().clip(poly);
Map.addLayer(composite, {bands: ['B4', 'B3', 'B2'], min: 0, max: 0.15}, 'Landsat 8 composite');
```

## Import Sentinel Data

The process for importing Sentinel data is similar to importing Landsat data, but some of the metadata are labeled differently. First, import Harmonized Sentinel-2 MSI: MultiSpectral Instrument, Level-2A (SR), and rename as sentinel.

To create a cloud free composite:

```JavaScript
function maskS2clouds(image) {
  var qa = image.select('QA60');

  // Bits 10 and 11 are clouds and cirrus, respectively.
  var cloudBitMask = 1 << 10;
  var cirrusBitMask = 1 << 11;

  // Both flags should be set to zero, indicating clear conditions.
  var mask = qa.bitwiseAnd(cloudBitMask).eq(0)
      .and(qa.bitwiseAnd(cirrusBitMask).eq(0));

  return image.updateMask(mask).divide(10000);
}

var S2_filtered = sentinel
  .filterDate(start,end)
  .filterBounds(poly)
  .filterMetadata('CLOUDY_PIXEL_PERCENTAGE','less_than',cloud_max)
  .map(maskS2clouds);
  
print(S2_filtered);

//create Sentinel-2 median composite and display
var S2composite = S2_filtered.median().clip(poly);
Map.addLayer(S2composite, {bands: ['B4', 'B3', 'B2'], min: 0, max: 0.15}, 'Sentinel 2 composite');
```

The code in the following sections will pertain only to Landsat, but refer to the [band combinations for Sentinel-2](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR_HARMONIZED#bands) if you choose to use Sentinel-2 data.

## Visualizing False Color Composites

We can visualize any combination of bands in a similar fashion by defining a new variable with our chosen band composite. The following code will display a color infrared composite:

```JavaScript
Map.addLayer(composite, {bands: ['B5', 'B3', 'B2'], min: 0, max: 0.15}, 'Landsat 8 false color composite');
```

## Band Ratios

We can use simple map algebra to display band ratios in Google Earth Engine. The following code divides Band 4 from Band 5 and displays the result.

```JavaScript
var b5 = composite.select("B5");
var b4 = composite.select("B4");
var b5divb4 = b5.divide(b4).rename('B5/B4');

Map.addLayer(b5divb4, {min:0, max:1, palette: ["white", "green"]} , "NDVI");
```

## Calculate NDVI

Using the 2023 composite imagery, we can also calculate the Normalized Difference Vegetation Index.

```JavaScript
var b5 = composite.select("B5");
var b4 = composite.select("B4");
var ndvi = b5.subtract(b4).divide(b5.add(b4)).rename('NDVI');

Map.addLayer(ndvi, {min:0, max:1, palette: ["white", "green"]} , "NDVI");
```

## Supervised Land Cover Classification

We will now conduct a supervised land cover classification using the Landsat 8 composite, SRTM DEM, and NDVI.

In a similar fashion to how the study area was defined with a point, we can define training polygons by selecting Draw a shape or Draw a rectangle in the lower map section. We will define 4 land cover classes: forest, cultivated, urban, and water. In the map section add a new layer for each of these classes and choose a suitable color. Import as a FeatureCollection and add a property called landcover. Assign forest a landcover value of 0, cultivated 1, urban 2, and water 3.

We will now merge these polygons.

```JavaScript
//Create training polygons

var polygons = forest.merge(cultivated).merge(urban).merge(water);
```

Next, we define the composite imagery, combining our 2023 Landsat 8 composite with the SRTM DEM and the NDVI.

```JavaScript
var compositeFin = composite.addBands(srtm).addBands(ndvi);
print (compositeFin, 'final composite');


//define prediction bands
var bands = ['B1','B2','B3','B4','B5','B6','B7', 'elevation', 'NDVI'];
```

The next step trains the classifier using a random forest algorithm. We also separate the training data into 70% for training and 30% for validation.

```JavaScript
//Train the classifier
var sample = compositeFin.sampleRegions({  
  // Get the sample from the polygons FeatureCollection.
  collection: polygons, //converts each pixel into a feature and extracts the 'landcover' value for each pixel
  // Keep this list of properties from the polygons.
  properties: ['landcover'],
  // Set the scale to get Landsat pixels in the polygons.
  scale: 30
}).randomColumn('random');

print(sample.first(), 'sample')

//split the sample data into training and validation 
var split = 0.7;  // Roughly 70% training, 30% validation.
var training = sample.filter(ee.Filter.lt('random', split)); 
//--> Use the training sample to train your model
var validation = sample.filter(ee.Filter.gte('random', split));
//--> we will use this validation sample later to evaluate the accuracy of our model
print('Samples n =', sample.aggregate_count('.all'));
print('Training n =', training.aggregate_count('.all'));
print('Validation n =', validation.aggregate_count('.all'));

//define the classifier --> this is the classification method you want to use
//along with any of ther parameters you would like to define
var classifier = ee.Classifier.smileRandomForest({
      numberOfTrees: 50
});

//Train the classifier
var trained = classifier.train(training, 'landcover', bands);
print (trained, 'trained')

//Classify the image
var classified = compositeFin.select(bands).classify(trained);
 
Map.addLayer(classified, {min: 0, max: 3, palette: ['green', 'yellow', 'white', 'blue']}, 'Classified');

//Calculate Accuracy

//classify each point in the validation dataset
var validated = validation.classify(trained);
print(validated.first(), 'validated')

// Get a confusion matrix representing expected accuracy.
var testAccuracy = validated.errorMatrix('landcover', 'classification');
print('Validation error matrix: ', testAccuracy);
print('Validation overall accuracy: ', testAccuracy.accuracy());
```

We can now view the land cover classification in the map section, and we can view a confusion matrix of the validation data. We can further refine the classification by altering and adding training polygons.

## Export Imagery

We can also export any imagery generated in Google Earth Engine to our local drive for additional processing or data presentation. Depending on the size of the data (more than 1,000,000,000 pixels), you may need to import a grid and export data in smaller chunks.

```JavaScript
Export.image.toDrive({
  image: classified,
  description: 'classified',
  maxPixels:1e9,
});
```

Once you have run the code, go to the Tasks section and run the unsubmitted tasks. Here you can set the resolution and other parameters. By default, the imagery will be exported to your Google Drive main folder where you can then download locally.

## Additional Links

To develop more skills in Google Earth Engine, additional code is available at the following links:

[Remote Sensing with Google Earth Engine](https://calekochenour.github.io/remote-sensing-textbook/introduction.html)

[Remotely Sensing Cities and Environments](https://andrewmaclachlan.github.io/CASA0023/5_GEE_I.html)

## References

Alders, W., Davis, D.S. & Haines, J.J. 2024. Archaeology in the Fourth Dimension: Studying Landscapes with Multitemporal PlanetScope Satellite Data. Journal of Archaeological Method and Theory 31:1588–1621. <https://doi.org/10.1007/s10816-024-09644-x>

Alcover Firpi, Omar A. 2016. Satellite Data for All? Review of Google Earth Engine 
for Archaeological Remote Sensing. Internet Archaeology 42. 
<https://doi.org/10.11141/ia.42.10>

Herndon, Kelsey, Robert Griffin, Whittaker Schroder, Timothy Murtha, Charles Golden,
Daniel A. Contreras, Emil Cherrington, Luwei Wang, Alexandra Bazarsky, G. Van Kollias,
and Omar Alcover Firpi. 2023. Google Earth Engine for Archaeologists: An Updated
Look at the Progress and Promise of Remotely Sensed Big Data. Journal of Archaeological
Science: Reports 50:104094. <https://doi.org/10.1016/j.jasrep.2023.104094>

Orengo, H.A., A. Garcia-Molsosa. 2019. A Brave New World for Archaeological Survey:
Automated Machine Learning-Based Potsherd Detection Using High-Resolution Drone Imagery. 
Journal of Archaeological Science 112: 105013. <https://doi.org/10.1016/j.jas.2019.105013>