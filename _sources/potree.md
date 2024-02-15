# Sharing Point Clouds with Potree

[Potree](https://github.com/potree/potree) is a free and open source web-based point cloud viewer. The
advantage over Sketchfab is that Potree has a built-in interface to allow interaction with the point cloud.
Potree, however, does not work locally and instead relies on viewing through a web server. A solution is to
upload models to GitHub, but point clouds will have to be subsampled to file sizes below 100 mb.

# Using Potree Converter to Package a Point Cloud

First, download the Potree Converter from <https://github.com/potree/potree>. In the Command Prompt, change
the directory to the Potree Converter folder. Run the following command on your point cloud. For sharing on
GitHub, generate an .html page called index, which will automatically become the home page for your online
point cloud.

```
PotreeConverter.exe "..\input.las" -o "..\destinationFolder" -generate-page index
```

This command will create an .html page that will display your point cloud. However, if you open this .html
file on your local computer, you will not see anything because Potree must be hosted on a web server. GitHub
Pages offers a free and accessible option.

# Editing the HTML

You can directly edit the newly created index.html file to personalize the point cloud. For example, you can 
add a title. Under the line that reads:

```
viewer.setPointBudget(2_000_000);
<!-- INCLUDE SETTINGS HERE -->
```

add the following:

```
document.title = "Your Title Here";
```

Under

```
viewer.loadSettingsFromURL();
```

add the following:

```
viewer.SetDescription("Your Description Here");
```

Potree assumes metric measurements. If your data area not in meters, under the line that reads:

```
viewer.loadSettingsFromURL();
```

add the following:

```
viewer.setLengthUnit('ft');
```

You can adjust other settings, for example:

```
material.pointSizeType = Potree.PointSizeType.FIXED;
material.shape = Potree.PointShape.CIRCLE;
material.activeAttributeName = "rgba";
```

# Uploading the Point Cloud to GitHub

In your GitHub profile, create a new repository, <my-repository-name>. Create a new empty repositoryFolder on your local computer. In the Command Prompt or Bash, run the following command to sync or clone your GitHub repository with your local folder.

```Bash
cd "..\repositoryFolder"
```

```Bash
git clone https://github.com/<my-org>/<my-repository-name>
```

Next, copy the Potree files from ..\destinationFolder into the new folder created in the ..\repositoryFolder.
Change your directory in the Command Prompt to this new folder.

```Bash
cd "..\repositoryFolder\newfolder"
```

The following commands will upload the Potree files to your GitHub repository.

```Bash
git add ./*
```

```Bash
git commit -m "adding"
```

```Bash
git push
```

Go to your GitHub repository settings, scroll to "Pages." Under "Branch," change "None" to "main" and save.
After a few minutes, your GitHub Pages website should be live.

<iframe src="https://whitschroder.github.io/cedarkey" width="640" height="480" title="Cedar Key"></iframe>