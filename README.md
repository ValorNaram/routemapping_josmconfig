# About

This repository gives you the necessary tools to hand to let you organize your mapping team that adds bus routes to [OpenStreetMap](https://www.openstreetmap.org/about) and to validate their work.

It provides you with the ability to

- make it easier for your team to add bus routes to [OpenStreetMap](https://www.openstreetmap.org/about)

- To monitor and validate their work and to do the necessary troubleshooting in case of invalid data

**This repository belongs to the "Trufi - Easier access to public transportation" project run by [Trufi Association](https://www.trufi-association.org/).**

## Table of Content

- The section [Setting up our mapping tool](#setting-up-our-mapping-tool) shows you how you can make adding bus routes to OpenStreetMap easier for your mapping team.

- The section [Setting up our monitoring tool](#setting-up-our-monitoring-tool) shows you how you can monitor the progress of your mapping team and to troubleshoot errors.

# Setting up our mapping tool

Our mapping tool is actually a configuration file which simplifies the [JOSM editor](https://josm.openstreetmap.de) for our purpose. JOSM is complicated so we will show you how to tweak the configuration file to make it easier for your mapping team to [add bus routes to OSM via JOSM](https://mapping-bus-routes.readthedocs.io/en/master/mapping-routes/).

This document does not explain how to [set up JOSM](https://mapping-bus-routes.readthedocs.io/en/master/installing-josm-on-linux/) nor to [link it to your OSM account](https://mapping-bus-routes.readthedocs.io/en/master/oauth-josm/). The hyperlinks will point you to the respective tutorials for that.

![](img/routemapping-look.png)

> **What is JOSM?**
> 
> JOSM is an extensible editor for [OpenStreetMap](https://welcome.openstreetmap.org/what-is-openstreetmap/). OpenStreetMap itself is a project to create a free and editable map for anyone by anyone. JOSM is a highly advantage tool to actually contribute to OSM by letting you add objects that represent real world objects to the database.

## Prepare your workplace

1. Download the [JOSM editor](https://josm.openstreetmap.de) which is available for Linux, Mac and Windows.

2. Fork this repository

3. Clone this repository onto your computer

4. Change into the newly created folder

## Editing `trufi_presets.xml`

This is actually the really important part which will also take the most time.

1. Open XML file `trufi_presets.xml`.

2. The file is documented. You should understand it. But here are some aspects good to know. The following three images show you the schematics of UI creation in preset means. It shows you which part of the preset code does which part of the UI. Study the images carefully:
   
   ![](img/WYSIWYG-01.png)![](img/WYSIWYG-02.png)![](img/WYSIWYG-03.png)
   
   3. A good another way of understanding the file is by understanding its schematics.
      
      ```xml
      <presets author="Author name" link="Url to project this file is for" shortdescription="Short description of what this preset file allows you to do" description="Longer description of what this preset file allows you to do"> <!-- Description of the presets this file contains. This is metadata that is equal for every preset specified in here.-->
          <group name="Name of group" icon="Url to the online resource containing the icon"> <!-- Presets can be grouped to add extra metadata only to preset inside of it -->
              <item name="Name of the preset" type="osm type for which this preset can be used. Seperate multiple types by comma. Supported osm types are 'node', 'way', 'relation'." icon="url to preset icon">
                  <label text="Label 1" /> <!-- It creates a label (read-only text container) in the preset dialog with the content "Label 1"-->
                  <key key="public_transport" value="platform"/> <!-- Tells JOSM to apply the OSM tag "public_transport=platform" to the object this preset is used on. The user cannot prevent that.-->
                  <text key="name" text="Stop name" default="" delete_if_empty="true" /> <!--This shows a textfield prompting the user to specify the value of OSM key "name".-->
                      <!-- XML attribute `key`: The key the user can specify a value for -->
                      <!-- XML attribute `text`: The text to be shown to the user so he/she knows for what he/she is prompted to type in. -->
                      <!-- XML attribute `default`: The default value of the key to apply when the user does not type anything into the textfield. -->
                      <!-- XML attribute `delete_if_empty`: Can have the values "true" (JOSM will not apply the key to the preset when the user did not type anything (leaving the textfield empty)) and "false" (JOSM will also apply the key to the preset when the user did not type anything into the textfield. The value for XML attribute `default` will be applied instead.)-->
                  <combo key="wheelchair" text="Wheelchair accessible?" values="no, yes" default="no" delete_if_empty="true"/> <!-- This shows a combo box (select from a predefined list of values) to the user prompting to decide which value to take for key "wheelchair". -->
                      <!-- XML attribute `key`: The key the user can specify a value for -->
                      <!-- XML attribute `text`: The text to be shown to the user so he/she knows for what he/she is prompted to select a value for. -->
                      <!-- XML attribute `values`: A comma seperated list of values the user can select from. This is the list which will be shown to the user. -->
                      <!-- XML attribute `default`: The default value of the key to apply when the user does not select anything from the list. -->
                      <!-- XML attribute `delete_if_empty`: Can have the values "true" (JOSM will not apply the key to the preset when the user did not type anything (leaving the textfield empty)) and "false" (JOSM will also apply the key to the preset when the user did not select anything from the list. The value for XML attribute `default` will be applied instead.)-->
              </item>
          </group>
      </preset>
      ```

## Preparing preset for production use.

1. Compress the XML file `trufi_presets.xml` into a zip archive.

2. Upload the zip file to the repository on GitHub.

3. Go to GitHub

4. Go to the online repository.

5. Click on the file you uploaded in step 2.

6. Copy the hotlink of the file into your clipboard.

## Editing `josmconfig-trufi-routes.xml`

The XML contains the configuration for JOSM and the plugins to be installed. Editing it is pretty easy because we've done the most work for you.

1. Open XML file `josmconfig-trufi-routes.xml` .

2. Search for the line that looks like:
   
   ```xml
   <tag key="url" value="https://github.com/SamuelRioTz/Trufi-Presets/releases/download/v1.0.5/trufi.zip"/>
   ```

3. Change the value `https://github.com/SamuelRioTz/Trufi-Presets/releases/download/v1.0.5/trufi.zip` to the url pointing to the zip file you uploaded into your repository on GitHub by inserting the new value from your clipboard e.g. `https://github.com/trufi-association/routemapping_josmconfig/raw/master/trufi_presets.zip`

4. Save your work and close your text editor.

## Finishing up

Upload all your changes to the forked GitHub repository and follow the tutorial [here](https://mapping-bus-routes.readthedocs.io/en/master/installing-mapping-tool/) in order to activate your customized version of our tool in JOSM. Distribute the customized file `josmconfig-trufi-routes.xml` (not our original one but the one in your forked repo you changed e.g. `https://github.com/username/routemapping_josmconfig/josmconfig-trufi-routes.xml`) and nothing else to your community. Point them also to the tutorial on [how to install your customized version of our tool for mapping bus routes in JOSM](https://mapping-bus-routes.readthedocs.io/en/master/installing-mapping-tool/) so they know what to do. You should also consider pointing them to [our comprehensive guide on using JOSM for mapping bus routes](https://mapping-bus-routes.readthedocs.io/en/master/).

# Setting up our monitoring tool

Our monitoring tool lets you monitor the progress of your mapping team and lets you troubleshoot errors.

## Preparing your workspace

1. Fork the repository [containing our monitoring tool](https://github.com/SamuelRioTz/GeoJSON-Bolivia-Cochabamba) to your GitHub account.

2. Clone the forked version to your computer.

3. Change to the local directory of your forked version of the repository.

4. Open a terminal there.

5. Install the program [Node.js](https://nodejs.org/en/) e.g. `apt install nodejs`.

6. Install the node module installer `npm` e.g. `apt install npm`.

7. Execute the command `npm install osm-public-transport-export` . It installs the necessary node package needed by our monitoring tool.

8. Leave the terminal open.

**Don't hestitate to reach out to us in case of problems. We're here to help you :) Please use our channel for this.**

## Modifying our monitoring tool

1. Open the file `index.js`  located in the root of the directory in your favourite text editor and head over to the following code piece
   
   ```js
    bounds: {
           south: -17.57727,
           west: -66.376555,
           north: -17.276198,
           east: -65.96397,
       }
   ```

2. Replace the numbers with their respective respresentation for your city. This is the boundingbox you need to specify for your city/region you want to monitor.
   
   1. Go to https://boundingbox.klokantech.com/
   
   2. Go to the region you want to monitor
   
   3. Drag and resize the boundingbox to reach the boundaries of the region (e.g. city) you want to monitor changes of routes in the OSM database for.
   
   4. On the bottom left side of the map click on the dropdown field (right under `Copy & Paste`) with text `MARC` and select `CSV` from the opening list.
   
   5. The content of the textfield next to it on the right side changes to something in the format `west,south,east,north`. Values are seperated by comma.
   
   6. Copy the first number (representing the west border of the boundingbox) and **replace `-66.376555` with it**.
   
   7. Copy the second number (representing the south border of the boundingbox) and **replace `-17.57727` with it.**
   
   8. Copy the third number (representing the east border of the boundingbox) and **replace `-65.96397` with it.**
   
   9. Copy the last number (representing the north border of the boundingbox) and **replace `-17.276198` with it.**
   
   10. At the end it should look like (e.g. for Addis Ababa, Ethiopia)
       
       ```js
       bounds: {
        south: 8.829865,
        west: 38.652136,
        north: 9.101212,
        east: 38.913422,
        }
       ```

3. Save the file and close your editor.

4. Now go back to the terminal and type in `node index.js` to start the script. (You still need to be in the root directory of the repository you cloned locally).

## Finishing up

The script generates a table you can find in the `README.md` file in your local repository. Upload it - together with the `out` directory -  to your forked GitHub manually or by running the following script `upload.sh`.

Now you can close the terminal :)

Then point your mapping team to the README.md file and say them, with this list they can validate their work. You should consider rerunning the script regulary on your computer locally to update the README.md in order to update the monitoring results used by you and your mapping team for troubleshooting. You can also show them how they can run the script themselves so they can trigger updates according to their needs.
