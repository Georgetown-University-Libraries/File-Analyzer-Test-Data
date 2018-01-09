# Setup: Generating IIIF Manifests with File Analyzer

[Main Menu](README.md) | [Next](demo1.md) 
------------------------- | ------------------------- 

## Directory Overview

* dog-photos
  * This is the directory to scan with File Analyzer
  * Images are grouped into boxes and then year created
  * Item metadata exists in dublin_core.xml in each folder
* dog-photos-linked-dao
  * iiif assets that will be referenced directly in the EAD

## Step 1: Install File Analyzer
* [File Analyzer Overview](https://github.com/Georgetown-University-Libraries/File-Analyzer)
* [File Analyzer Installation](https://github.com/Georgetown-University-Libraries/File-Analyzer/wiki/Installation-instructions)

## Step 2: Clone File Analyzer Test Data
* Clone the [File Analyzer Test Data Repo](https://github.com/Georgetown-University-Libraries/File-Analyzer-Test-Data)
* Make the [IIIF test data](https://github.com/Georgetown-University-Libraries/File-Analyzer-Test-Data/tree/master/iiif) within the repository accessible to a IIIF Image Server
* Browse the subfolders within the project to see how the images have been arranged.  
  * This project contains 17 photos organized by location and the year that the photo was taken.
  * Dublin core metadata exists in each folder describing the images
  * An EAD file exists at the root directory providing more context about each subfolder with the project


## Step 3: Make a local copy of [Manifest Generator Property File](https://github.com/Georgetown-University-Libraries/File-Analyzer/blob/master/demo/src/main/edu/georgetown/library/fileAnalyzer/filetest/iiif/README.md) within the **iiif/dog-photos** directory

    cd iiif/dog-photos
	cp manifestGenerate.template.prop manifestGenerate.prop
	
## Step 4: Configure the manifestGenerate.prop file for your server

### Set the root URL for the dog-photos directory within your IIIF Image Server

    # URL Prefix to prepend to IIIF resource URL's for this proejct
    IIIFRoot: https://your.image.server.edu/project

### Set the output file name where your manifest file will be written (this must be web accessible)

    # Manifest Output Directory
    # If blank, the current dir will be used
    # Enter the path as a linux style path even for windows
    #   \\server\share\path --> //server/share/path
    ManifestOuputDir: 
	
### If desired, you can embed your own logo into the generated manifest file

    # Manifest Logo URL
    # URL to a logo image to embed within the manifest
    ManifestLogoURL: https://your.image.server.edu/logo.jpg
	
## Step 5: Launch File Analyzer (DemoFileAnalyzer-2.0.jar)

**Main Menu** | [Next](demo1.md) 
------------------------- | ------------------------- 
