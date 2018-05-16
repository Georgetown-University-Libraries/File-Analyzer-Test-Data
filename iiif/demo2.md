# Generate Manifest with Item Metadata

{% include nav.html %}

The Create Manifest Builder is able to merge item metadata into the manifest file as it is being generated.  

![Basic Use Case With Metadata](tutorial-screenshots/IIIFScenarios/Slide3.JPG)

Since this application was built to support content described in DSpace, the following metadata formats are supported.

* DSpace metadata input file: dublin_core.xml
* DSpace AIP export file: mets.xml
* DSpace REST API 

The application is also designed to support the following non-DSpace specific metadata types
* CSV File 
* Embedded metadata within images (future support)

## Step 1: In manifestGenerate.prop, set GetItemMetadata to "ItemMetadataFile"

    # Get Item Metadata
    GetItemMetadata: ItemMetadataFile

## Step 2: Re-run the Create IIIF Manifest task in File Analyzer (click Analyze)

![Screenshot](tutorial-screenshots/fa4.png)

## Step 3: Review the results. Note that title information is extracted for each item

![Screenshot](tutorial-screenshots/fad2.png)

## Step 4: Preview the results in Universal Viewer

Note the descriptive metadata in the right-hand panel.

![Screenshot](tutorial-screenshots/uv2.png)

Note the descriptive canvas names.

![Screenshot](tutorial-screenshots/uv2a.png)

{% include nav.html %}
