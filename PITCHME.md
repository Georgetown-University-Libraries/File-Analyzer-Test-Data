## Generating IIIF Manifests from Repository Metadata and Archival Metadata (EAD)

Terry Brady

Georgetown University Library

https://github.com/terrywbrady/info

![](https://www.library.georgetown.edu/sites/default/files/library-logo.png)

---

## IIIF in DigitalGeorgetown

- March 2018 - First Collection Released
  - [Alliance for Progress Cartoon Book Program in Latin America Collection](https://repository.library.georgetown.edu/handle/10822/1044538#?m=7)
- Reasonably Sized Collection, Visually Interesting
  - Item Metadata in DSpace
- Next Steps
  - Usability Testing
  - Capacity Planning for Future Projects

+++

## Next Steps

- Law Collections Described in EAD
  - Digitized AIDS Papers (on Test Server, VPN Required)
- Difficult to represent as items in DSpace
- EAD Hierarchy to be represented in a manifest
- Instructed our plans

+++

## Possible Future Plans

- Combine digitized content with scholarship to tell a story
- Student newspaper archive

---

## Our Approach

- Re-use metadata wherever possible
- Assemble metadata and image files to facilitate manifest generation
  - Developer intervention not needed!
- Use our [File Analyzer](https://github.com/Georgetown-University-Libraries/File-Analyzer) application for automation 
- Try it yourself!
  - [Tutorial - Generating IIIF Manifests with File Analyzer](https://github.com/Georgetown-University-Libraries/File-Analyzer-Test-Data/blob/master/iiif/README.md)
- We hope this is useful for other institutions
  
+++?image=iiif/overview.png&size=auto 90%

---

## Manifest Generation Property File

@ul

- Root Path to IIIF Server
- Where to write the manifest file
- Construct one manifest or a collection of manifests
- Where to find metadata
- How to assemble/format manifest ranges

@ulend

+++

## Where to find metadata

@ul

- One common property file for all images
- EAD File describing folders and items
- CSV file containing item specific data
- Separate metadata files for each item
- DSpace REST API calls

@ulend

+++

### URL Prefix for Image Resources

    # URL Prefix to prepend to IIIF resource URL's for this project
    IIIFRoot: https://YOUR-IMAGE-SERVER-URL/project-path

+++

### URL Prefix for Manifests within a Collection Manifest

    # URL Prefix to prepend to manifests in a collection manifest
    # ManifestRoot: https://YOUR-IMAGE-SERVER-URL/manifest-path

+++

### Manifest Output Directory

    # Manifest Output Directory
    # If blank, the current dir will be used
    # Enter the path as a linux style path even for windows
    #   \\server\share\path --> //server/share/path
    ManifestOuputDir: //YOUR-SERVER-PATH/IIIF/manifests

+++

### Manifest Output File Name

    # Manifest Output File
    # Name of the top level manifest file that will be generated
    ManifestOuputFile: dog-photos.json

+++

### Directory Separator for subfolders of image assets

    # IIIF Directory Separator.
    #  - "/" (default)
    #  - "%2F" may be needed for Cantaloupe Server.
    #DirectorySeparator: /
    DirectorySeparator: %2F

+++

### Collection manifest configuration

    # Create Collection Manifest - An individual manifest will be generated for each subfolder 
    # and registered in a collection level manifest
    #  - NoCollection: No collection manifest will be created (default)
    #  - OneItemPerFolder: Only one item per folder, use item name for folder name
    #  - ManyItemsPerFolder: Many items will exist per folder
    #CreateCollectionManifest: NoCollection
    #CreateCollectionManifest: OneItemPerFolder
    #CreateCollectionManifest: ManyItemsPerFolder
@[6](On manifest will be created - no collections)
@[7](All assets in a folder will share item metadata)
@[8](Each asset in a folder may have distinct metadata)
   
+++

### 2Page view Setting

    # Set2PageView
    #  - false: do not enable 2 page view (default)
    #  - true: enable 2 page view
    #Set2PageView: true

+++

### Manifest Logo

    # Manifest Logo URL
    # URL to a logo image to embed within the manifest
    ManifestLogoURL: 

+++

### Global metadata file - applies to all items

    # Manifest Metadata 
    # Manifest Metadata Input File
    # - EAD File containing metadata
    # - CSV File for each input directory of resources
    # If blank, this property file will be utilized
    #ManifestMetadataInputFile: 
    #ManifestMetadataInputFile: dogPhotosEAD.xml
    #ManifestMetadataInputFile: dogPhotosEADWithLinkedDAO.xml
    #ManifestMetadataInputFile: metadata.csv

@[6](No master metadata file)
@[7-8](EAD XML file containing metadata)
@[9](CSV file containing metadata for multiple items)

+++

### Global metadata fields

    # Manifest Metadata 
    # - If not defined in another external metadata file
    Title: Sample Manifest File with Dog Photos 
    Attribution: Sample file illustrating File Analyzer functionality
    DateCreated: 2017-12-12
    Creator: Terry Brady, Georgetown University Library
    #Description:
    #Rights: 

+++

###  Item Identifier Calculation

    # Get Item Identifier
    # - ItemMetadataFile - extract metadata from an item-specific file
    #   - mets.xml from DSpace AIP export
    #   - dublin_core.xml from DSpace Simple Archive Format metadata file
    # - FolderName - folder name contains item identifier
    # - FileName - file name contains item identifier
    #GetItemIdentifer: ItemMetadataFile
    #GetItemIdentifier: FolderName
    GetItemIdentifier: FileName

@[7](Item identifier will be defined in a metadata file associated with an image asset)
@[8](Item identifier will be derived from the name of the folder containing an image asset)
@[9](Item identifier will be derived from the file name of the image asset)


+++

### Item Metadata Location

    # Get Item Metadata
    # - ItemMetadataFile - extract metadata from a file
    #   - mets.xml from DSpace AIP export
    #   - dublin_core.xml from DSpace Simple Archive Format metadata file
    # - ManfiestMetadataFile - manifest level file containing metadata for all items
    #   - CSV files
    # - RESTAPI - extract metadata using the DSpace REST API
    # - None - no metadata file exists
    #GetItemMetadata: RESTAPI
    GetItemMetadata: None
    #GetItemMetadata: ItemMetadataFile
    #GetItemMetadata: ManifestMetadataFile 

@[9](Descriptive metadata will be pulled from the DSpace REST API)
@[10](Descriptive metadata will not exist for each asset)
@[11](Descriptive metadata will be pulled from an item specific metadata file)
@[12](Descriptive metadata will be pulled from a a global file applying to all assets)

+++

### Conversion class name - references a java enum class name

    # Manifest Project
    # Name of the Manifest Project (in code) class that will provide custom translation.
    # If blank, a default value will be assigned.
    # The class should be the name of an Enum that implements ManifestProjectTranslateEnum
    #ManifestProject: 

+++

### Looking For Feedback

- What use cases are missing from this model?

---

## Manifest Builder Tutorial Demo

[IIIF Manifest Builder Tutorial](http://georgetown-university-libraries.github.io/File-Analyzer-Test-Data/iiif/)
---
### Prerequisite Software
- IIIF Image Server such as Loris or Cantaloupe to serve 
- Web Server (manifests and universal viewer) 

+++

### Clone Repositories

- Install [File Analyzer](https://github.com/Georgetown-University-Libraries/File-Analyzer)
- Clone [File Analyzer Test Data](https://github.com/Georgetown-University-Libraries/File-Analyzer-Test-Data)

+++

### Sample Images Listing

    ./dog-photos-linked-dao/car.jpg
    ./dog-photos-linked-dao/yawn.jpg
    ./dog-photos/box_01/2006/IMG_0063.jpg
    ./dog-photos/box_01/2010/IMG_1063.jpg
    ./dog-photos/box_01/2010/dog1.jpg
    ./dog-photos/box_01/2013/IMG_3999.jpg
    ./dog-photos/box_01/2015/IMG_2159.jpg
    ./dog-photos/box_02/2006/IMG_1448.jpg
    ./dog-photos/box_02/2009/IMG_0168.jpg
    ./dog-photos/box_02/2014/IMG_5534.jpg
    ./dog-photos/box_02/2015/IMG_3749.jpg
    ./dog-photos/box_03/2009/IMG_0941.jpg
    ./dog-photos/box_03/2014/IMG_4970.jpg
    ./dog-photos/box_03/2017/IMG_0908.jpg
    ./dog-photos/box_04/2006/IMG_1800.jpg
    ./dog-photos/box_04/2009/IMG_0204.jpg
    ./dog-photos/box_04/2013/IMG_4591.jpg
    ./dog-photos/box_04/2015/IMG_5032.jpg
    ./dog-photos/box_04/2016/IMG_9030.jpg

+++

### Sample Images

![Sample Images Gif](iiif/tutorial-screenshots/sampleImages.gif)

+++

### Configure Application for Your Local Environment
- Make a local copy of the Manifest Generator Property 
- Configure the manifestGenerate.prop file for your server


---
### Basic Manifest

![Basic Use Case](iiif/tutorial-screenshots/IIIFScenarios/Slide2.JPG)

+++

### Select "Create IIIF Manifest" from the dropdown on the "Criteria" panel

+++

![Screenshot](iiif/tutorial-screenshots/fa1.png)

+++

![Screenshot](iiif/tutorial-screenshots/fa1.z.png)

+++

### Set "Root Directory" to the dog-photos directory

+++

![Screenshot](iiif/tutorial-screenshots/fa2.png)

+++

![Screenshot](iiif/tutorial-screenshots/fa2.z.png)

+++

### On the "File Test Properties Tab", note the options that exist. 
The "Manifest Generate Property Filename" should match the name of the file that you modified.

+++

![Screenshot](iiif/tutorial-screenshots/fa3.png)

+++

![Screenshot](iiif/tutorial-screenshots/fa3.z.png)

+++

### Click "Analyze"

+++

![Screenshot](iiif/tutorial-screenshots/fa4.png)

+++

### The results will display in a table describing the items found

+++

![Screenshot](iiif/tutorial-screenshots/fa5.png)

+++

![Screenshot](iiif/tutorial-screenshots/fa5.z.png)

+++

### Preview the Manifest in the Universal Viewer

+++

![Screenshot](iiif/tutorial-screenshots/uv1.png)

+++

Note that the image filenames are used as canvas labels.

+++

![Screenshot](iiif/tutorial-screenshots/uv1.z.png)

---

### Generate Manifest with Item Metadata

The Create Manifest Builder is able to merge item metadata into the manifest file as it is being generated.  

+++

![Basic Use Case With Metadata](iiif/tutorial-screenshots/IIIFScenarios/Slide3.JPG)

+++

### Metadata Support

Since this application was built to support content described in DSpace, the following metadata formats are supported.

* DSpace metadata input file: dublin_core.xml
* DSpace AIP export file: mets.xml
* DSpace REST API 

+++
The application is also designed to support the following non-DSpace specific metadata types
* CSV File 
* Embedded metadata within images (future support)

+++

## Step 1: In manifestGenerate.prop, set GetItemMetadata to "ItemMetadataFile"

    # Get Item Metadata
    # - ItemMetadataFile - extract metadata from a file
    GetItemMetadata: ItemMetadataFile

+++

### Step 2: Re-run the Create IIIF Manifest task in File Analyzer (click Analyze)

+++

![Screenshot](iiif/tutorial-screenshots/fa4.png)

+++

### Step 3: Review the results. Note that title information is extacted for each item

+++

![Screenshot](iiif/tutorial-screenshots/fad2.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad2.z.png)

+++

## Step 4: Preview the results in Universal Viewer

Note the descriptive metadata in the right-hand panel.

+++

![Screenshot](iiif/tutorial-screenshots/uv2.png)

+++

![Screenshot](iiif/tutorial-screenshots/uv2.z.png)

+++

Note the descriptive canvas names.

+++

![Screenshot](iiif/tutorial-screenshots/uv2a.png)

+++

![Screenshot](iiif/tutorial-screenshots/uv2a.z.png)

---

### Generate Manifest with Date Ranges

In this example, we will use a special project translation class to sort the images by date created and then generate date ranges for each of the images.

+++

![Index By Date](iiif/tutorial-screenshots/IIIFScenarios/Slide4.JPG)

+++

### Step 1: On the "File Test Properties" tab of "Criteria" tab, set Project Value Translator to "ByCreationDate"

+++

![Screenshot](iiif/tutorial-screenshots/fad3.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad3.z.png)

+++

Note the sequence and range information assigned to each image.

+++

![Screenshot](iiif/tutorial-screenshots/fad3a.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad3a.z.png)

+++

### Step 2: Preview the results in Universal Viewer

Note the date ranges present on the left hand side.

+++

![Screenshot](iiif/tutorial-screenshots/uv3.png)

+++

![Screenshot](iiif/tutorial-screenshots/uv3.z.png)

--- 
### Generate Manifest with Folder Ranges

In this example, we will use a special project translation class to replicate the folder structure as ranges within the manifest.

+++

### Generate Manifest with Folder Ranges

+++

![Index by Folder](iiif/tutorial-screenshots/IIIFScenarios/Slide5.JPG)

+++

### Step 1: On the "File Test Properties" tab of "Criteria" tab, set Project Value Translator to "ByFolderName"

Then click "Analyze"...

+++

![Screenshot](iiif/tutorial-screenshots/fad4.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad4.z.png)

+++
Note the sequence and range information assigned to each image.

+++

![Screenshot](iiif/tutorial-screenshots/fad4a.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad4a.z.png)

+++

### Step 2: Preview the results in Universal Viewer

+++

Note the file system folder structure present on the left hand side.

+++

![Screenshot](iiif/tutorial-screenshots/uv4.png)

+++

![Screenshot](iiif/tutorial-screenshots/uv4.z.png)

---

### Generate Manifest with EAD Subject + Folder Ranges

In this example, we will use use an EAD file to build project metadata and project ranges.  

+++

### Generate Manifest with EAD Subject + Folder Ranges

+++
![Index by EAD and Folder](iiif/tutorial-screenshots/IIIFScenarios/Slide6.JPG)

+++

The named folders of images are linked to EAD components by box and folder numbers.

+++

### Step 1: In manifestGenerate.prop, set ManifestMetadataInputFile to "[dogPhotosEAD.xml]({{site.src_path}}/iiif/dog-photos/dogPhotosEAD.xml)"

    # Manifest Metadata Input File
    ManifestMetadataInputFile: dogPhotosEAD.xml

+++

### Step 2: On the "File Test Properties" tab of "Criteria" tab, set Project Value Translator to "EADFolderMap"

Then click "Analyze"...

+++

![Screenshot](iiif/tutorial-screenshots/fad5.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad5.z.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad5a.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad5a.z.png)

+++

### Step 3: Preview the results in Universal Viewer

Note the EAD hierarchy and file system folder structure present on the left hand side.

+++

![Screenshot](iiif/tutorial-screenshots/uv5.png)

+++

![Screenshot](iiif/tutorial-screenshots/uv5.z.png)

---

### Generate Manifest with EAD Subject Ranges

In this example, we will modify the range listing from the prior example with a different project translator.  

+++

![Index by EAD](iiif/tutorial-screenshots/IIIFScenarios/Slide7.JPG)

+++

The named folders of images are linked to EAD components by box and folder numbers.

+++

### Step 1: On the "File Test Properties" tab of "Criteria" tab, set Project Value Translator to "EADFolderMapSubjectsOnly"

Then click "Analyze"...

+++

![Screenshot](iiif/tutorial-screenshots/fad6.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad6.z.png)

+++

### Step 3: Preview the results in Universal Viewer

Note the EAD hierarchy present on the left hand side.

+++

![Screenshot](iiif/tutorial-screenshots/uv6.png)

---

### Generate Manifest with EAD Subject Ranges and Digital Object References

In this example, we will also include digital objects (DAO's) defined within the EAD into the manifest.

+++

![Index by EAD and DAO](iiif/tutorial-screenshots/IIIFScenarios/Slide8.JPG)

+++

### Step 1: In manifestGenerate.prop, set ManifestMetadataInputFile to "[dogPhotosEADWithLinkedDAO.xml]({{site.src_path}}/iiif/dog-photos/dogPhotosEADWithLinkedDAO.xml#L135-L145)"

+++

    # Manifest Metadata Input File
    ManifestMetadataInputFile: dogPhotosEADWithLinkedDAO.xml

+++

### Step 2: On the "File Test Properties" tab of "Criteria" tab, keep the Project Value Translator to "EADFolderMapSubjectsOnly"

+++

Then click "Analyze"...

+++

![Screenshot](iiif/tutorial-screenshots/fad6.png)

+++

![Screenshot](iiif/tutorial-screenshots/fad6.z.png)

+++

### Step 3: Preview the results in Universal Viewer

+++

Note the additional items that have been imported by Digital Object URL in the EAD.

+++

![Screenshot](iiif/tutorial-screenshots/uv7.png)

+++

![Screenshot](iiif/tutorial-screenshots/uv7.z.png)

+++

![Screenshot](iiif/tutorial-screenshots/uv7a.png)

+++

![Screenshot](iiif/tutorial-screenshots/uv7a.z.png)

---

### Generate Manifest Metadata from a CSV

In this example, we will use a CSV file to populate manifest metdata.

+++

![Use CSV Metadata](iiif/tutorial-screenshots/IIIFScenarios/Slide9.JPG)

+++

### Step 1: In manifestGenerate.prop, set ManifestMetadataInputFile to "[metdata.csv]({{site.src_path}}/iiif/dog-photos/metadata.csv)"

    # Manifest Metadata Input File
    ManifestMetadataInputFile: metadata.csv

+++

### Step 2: In manifestGenerate.prop, set GetItemMetadata to "ManifestMetadataFile"

    # Get Item Metadata
    GetItemMetadata: ManifestMetadataFile

+++

### Step 3: On the "File Test Properties" tab of "Criteria" tab, keep the Project Value Translator to "Default"

+++

Then click "Analyze"...

+++

### Step 4: Preview the results in Universal Viewer

Note that the metadata was pulled from the CSV file (using the filename as a matching key)

+++

![Screenshot](iiif/tutorial-screenshots/uv8.png)

+++

![Screenshot](iiif/tutorial-screenshots/uv8.z.png)

---

### Generate a Collection Manifest

In this example, we will generate a collection of manifests (one per each top level folder).

+++

![Collection Manifest](iiif/tutorial-screenshots/IIIFScenarios/Slide10.JPG)

+++

### Step 1: In manifestGenerate.prop, set CreateCollectionManifest to "ManyItemsPerFolder"

    # Create Collection Manifest - An individual manifest will be generated for each subfolder 
    CreateCollectionManifest: ManyItemsPerFolder

+++

### Step 2: In manifestGenerate.prop, set GetItemMetadata to "ItemMetadataFile"

    # Get Item Metadata
    GetItemMetadata: ItemMetadataFile

+++

### Step 3: On the "File Test Properties" tab of "Criteria" tab, set the Project Value Translator to "ByItemFolderName"

Then click "Analyze"...

+++

### Step 4: Preview the results in Universal Viewer

Note that the images have been broken into individual manifests for each box.

+++

![Screenshot](tutorial-screenshots/uv9collection.gif)

---

### Try it Yourself

Give the [tutorial](http://georgetown-university-libraries.github.io/File-Analyzer-Test-Data/iiif/) and let me know your results

Terry Brady

Georgetown University Library

https://github.com/terrywbrady/info

![](https://www.library.georgetown.edu/sites/default/files/library-logo.png)

