# Generate Manifest Metadata from a CSV

[Main Menu](README.md) | [Next](demo9.md) 
------------------------- | ------------------------- 

In this example, we will use a CSV file to populate manifest metdata.

![Use CSV Metadata](tutorial-screenshots/IIIFScenarios/Slide9.JPG)

## Step 1: In manifestGenerate.prop, set ManifestMetadataInputFile to "[metdata.csv](dog-photos/metadata.csv)"

    # Manifest Metadata Input File
    # - EAD File containing metadata
    # - CSV File for each input directory of resources
    # If blank, this property file will be utilized
    #ManifestMetadataInputFile: dogPhotosEAD.xml
    #ManifestMetadataInputFile: dogPhotosEADWithLinkedDAO.xml
    ManifestMetadataInputFile: metadata.csv

## Step 2: In manifestGenerate.prop, set GetItemMetadata to "ManifestMetadataFile"

    # Get Item Metadata
    # - ItemMetadataFile - extract metadata from a file
    #   - mets.xml from DSpace AIP export
    #   - dublin_core.xml from DSpace Simple Archive Format metadata file
    # - ManfiestMetadataFile - manifest level file containing metadata for all items
    #   - CSV files
    # - RESTAPI - extract metadata using the DSpace REST API
    # - None - no metadata file exists
    #GetItemMetadata: RESTAPI
    #GetItemMetadata: None
    #GetItemMetadata: ItemMetadataFile
    GetItemMetadata: ManifestMetadataFile

## Step 3: On the "File Test Properties" tab of "Criteria" tab, keep the Project Value Translator to "Default"

Then click "Analyze"...

## Step 4: Preview the results in Universal Viewer

Note that the metadata was pulled from the CSV file (using the filename as a matching key)

![Screenshot](tutorial-screenshots/uv8.png)

[Main Menu](README.md) | [Next](demo9.md) 
------------------------- | ------------------------- 
