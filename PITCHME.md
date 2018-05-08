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

+++?code=iiif/dog-photos/manifestGenerate.template.prop&lang=ini
@[1-2](URL Prefix for image resources)
@[4-5](Component manifest file prefix)
@[7-11](Manifest output directory)
@[13-15](Manifest output file name)
@[20-24](Directory Separator for subfolders of image assets)
@[26-33](Collection manifest configuration)
@[35-38](2Page view)
@[40-42](Manifest Logo)
@[44-51](Global metadata file - applies to all items)
@[53-60](Global metadata fields)
@[62-70](Item Identifier Calculation)
@[72-83](Item Metadata Location)
@[85-89](Conversion class name - references a java enum class name)
#### Manifest Prop File Overview

---

## Tutorial Demo

@ul

- Basic Manifest
- Item Metadata
- Date Ranges
- Folder Ranges
- EAD+Folder Ranges
- EAD Ranges
- EAD Ranges + DAO's
- CSV Metadata
- Collection Manifests

@ulend

---
### Basic Manifest

![Basic Use Case](iiif/tutorial-screenshots/IIIFScenarios/Slide2.JPG)


+++

### Select "Create IIIF Manifest" from the dropdown on the "Criteria" panel

![Screenshot](iiif/tutorial-screenshots/fa1.png)

+++

### Set "Root Directory" to the dog-photos directory

![Screenshot](iiif/tutorial-screenshots/fa2.png)

+++

### On the "File Test Properties Tab", note the options that exist. 
The "Manifest Generate Property Filename" should match the name of the file that you modified.

![Screenshot](iiif/tutorial-screenshots/fa3.png)

+++

### Click "Analyze"

![Screenshot](iiif/tutorial-screenshots/fa4.png)

+++

### The results will display in a table describing the items found

![Screenshot](iiif/tutorial-screenshots/fa5.png)

+++

## Step 6: Preview the Manifest in the Universal Viewer

![Screenshot](iiif/tutorial-screenshots/uv1.png)

+++

Note that the image filenames are used as canvas labels.

![Screenshot](iiif/tutorial-screenshots/uv1a.png)

---

## Demo 2