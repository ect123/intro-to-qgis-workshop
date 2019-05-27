# Intro to GIS with QGIS 3.4

<p align="center">
  <a href="#introduction">Introduction</a>&nbsp;|
</p>

## INTRODUCTION
This is an introductory workshop focusing on the fundamental concepts and skills needed to begin using **QGIS 3** exploring and analyzing spatial data. It is also meant to help you understand how to get started composing a map document for print production. **The instructions below will follow a brief presentation overviewing the QGIS 3 and it's user interface.**

The result of this project will be a choropleth map showing the number of Douglas Firs lining the streets in each of Vancouver's neighbourhoods. We will compose and export this map for print.

---
#### GIS Resources at UBC:
- General Informational website for all things UBC GIS: [gis.ubc.ca](http://gis.ubc.ca/)    
- UBC Library's guide for finding and working with GIS resources: [guides.library.ubc.ca/gis](http://guides.library.ubc.ca/gis)
- UBC's GIS email list (participate or lurk!): [UBC GIS ListServ](https://lists.ubc.ca/scripts/wa.exe?SUBED1=GIS-LIST&A=1)  
- UBC's GIS Slack (create your own channel or lurk!): [ubcgis.slack.com](https://ubcgis.slack.com/)
- Evan Thornberry, GIS Librarian @ UBC Library: evan.thornberry AT ubc.ca
---
#### Download Workshop Data
To get started with this workshop, you'll need to first download the data and files from this GitHub repository. To do this,

![Download the .zip file][download]

[download]: /img/download.png "Download the .zip file."   


1. Save this repository (.**zip**) to your Desktop.
2. Right-click on the .zip file you just downloaded and select **Extract All**...
3. Accept all defaults to extract the file.    

Open the new **Intro-to-ArcGIS-Pro** folder. This is your project folder which contains the files:
- Intro.**gdb**: the geodatabase with data for your map
- Intro.**aprx**: the project file with all the maps
- Intro.**tbx**: a toolbox with analytical tools for your project
- Index: folder with background organizing information

### 0. Start QGIS and get the workshop data and instructions.
Open QGIS 3.4.0 with GRASS. In your browser, download the .zip file of the repository found on this page: **github.com/ect123/intro-to-qgis-workshop**. SAVE the file. The .zip file will now be in your Downloads folder. Move this folder to a locations on your hard drive or flash drive and **extract**. We will use C:\Temp for this workshop.

### 1. Open the QGIS project file (.qgz)
In the Browser Panel, click the C:\Temp folder to expand, and select your newly extracted folder called **intro-to qgis-workshop-master**. Inside you'll see a project file named **vanTreeMap**. Double-click that file to open the project.

### 2. View layer properties
In the Layers Panel, right-click the title of the **vanHoods** layer, and select **Properties**. Observe some of the layer properties and close the window.

### 3. Change the shoreline boundary width and colour
In the Layers Panel, right-click on the title of the **vanShoreline** layer and select **Layer Properties**. In Layer Properties, select the tab for **Symbology**, and change the line width to **1**. Next, change the colour of the line to **blue**. *You should see a slight change in the width of the shoreline and your line should now be blue*.

### 4. Add the tree data
Click on the **Open Data Source Manager** button and select the **Vector** tab. For the vector dataset's source, navigate to your C:\Temp\intro-to-qgis-workshop-master\data folder and select the file named **vanBigTrees.geojson**. Click add, then close. *You should see a new layer named **vanBigTrees** in your Layers Panel.*

### 5. Examine the attributes in your trees layer.
In the Layers Panel, right-click the title for the trees layer, and select **Open Attribute Table**. *You should see your attribute table*. Note that there are several attributes (columns) that describe each feature (rows) in this dataset.

### 6. Select only the Douglas Fir trees.
With your attribute table open, select the **Select features using an expression** button. We will use this tool to query and select only features that have a common name value of "Douglas Fir".

In middle of the window, expand the option for **Fields and Values**, and double-click **COMMN_NAME** so that it is entered in your expression builder (on the left).

Click the **=** button above the expression builder.

With COMMN_NAME selected, click the **All Unique** button. This displays all the unique values in the COMMN_NAME field. Double-click **DOUGLAS FIR**, then click the **Select features** button at the bottom right.

Close the expression builder window and close the attribute table. *You should now see some trees selected on your map - they'll be yellow. These are the Douglas Fir trees*.

### 7. Create a new layer from your Douglas Fir tree selection.
Right-click your **vanBigTrees** layer in the Layers Panel, and select **Export - Save Selected Features As..**.

**Format:** Esri Shapefile    
**File name:** navigate to the location of your project's data and save the file as **vanDougFirs**.

Notice that the option to save only selected features is enabled. Keep the rest of the default settings and click **ok**. You will now see your new layer appear on your map.

In your Layers Panel, deselect the **vanBigTrees** layer to remove it from the display.

### 8. Count the number of Douglas Fir trees in each neighbourhood.
In the Main Menu select **View - Panels - Processing Toolbox**. This is where you can find a large number of analytical and geoprocessing tools.

In the search, type "count points in polygon" and double-click the result.

**Polygons:** vanHoods (your input polygon layer)   
**Points:** vanDougFirs (your input points layer)   
**Count field name:** DougFirs (the name of the attribute that will have Doug Fir counts)

Click **Run**, then **Close** when the process has finished. *You will now have a new layer called **Count***. Take a look at the attribute table for this new layer.

Save this layer to your data folder by right-clicking and selecting **Export - Save Features As..**

**Format:** Esri Shapefile    
**File name:** navigate to the location of your project's data and save the file as **vanHoodsCount**.

### 9. Create a choropleth map showing the number of Douglas Firs in each neighbourhood.

In your layers panel, remove everything except your **vanHoodsCount** and **vanShoreline** layers.

Right-click your **vanHoodsCount** layer and select **Layer Properties**, then click the **Symbology** tab.

At the very top, click **Single Symbol** and change to **Graduated**. This will allow you to display graduated colours representing classes of attribute values.

**Column:** DougFirs    
**Legend Format:** Precision 0, Trim   
**Color Ramp:** pick a color ramp that looks like it would represent the prevalence of Douglas Firs.        
**Mode:** Natural Breaks (Jenks)    
**Classes:** 5    

Click **ok** and close the window.

### 10. Label your neighbourhoods.
Right-click your vanHoodsCount layer, select **Layer Properties**, and click the **Labels** tab. Change **No Labels** to **Single Layers.**

**Label with:** NAME    
**Buffer:** Draw text buffer - this can help with displaying dark text over dark coloured maps.    
**Placement:** Horizontal

Click **Apply** to see your changes, and make any stylistic adjustments. Click **ok** when done.

### 11. Compose your map for print.
Select the **New Print Layout** button at in the Toolbar, and name the layout **Doug Fir Map**.

Right-click on the resulting page and select **Page Properties**. Change the layout to your desired dimension.

Using the **Add new map** button, add a new map to your layout. Drag the map to cover the entire layout. Use the **Move item content** button to fine tune your map's placement.

### 12. Add a legend, scale bar, north arrow, and title.
You'll need to add context to your map using some cartographic elements. Using the **Add legend** button, click and drag a box in the area you would like to place the legend. Right-click your legend and select **Item Properties**. Double-click your layer names and enter more relevant titles.

Using the **Add scale bar** button, add a scale bar to your map.

Using the **Add title** button, add a title **Vancouver's Douglas Firs**.

##### North Arrow
Using the **Add picture** button, select the Arrow folder, then pick whichever arrow you would like. (Alternately, select a custom arrow or any other image).

Then, select the image from the list of items added to the map if it is not already selected.

Under item properties, scroll down until you see Image Rotation. Choose **Sync with map**, then select the map you'd like to sync with. For type of alignment, select **Grid or Magnetic north**.

### 13. Export your map for print.
In the Print Layout Menu, Select the option to **Export as Image**. Save your file as a .jpeg image in your project folder. Now you have a static image of your map.

Close the print layout menu.

### 14. Save your project for later use.
In the main menu, select **Project - Save**.
