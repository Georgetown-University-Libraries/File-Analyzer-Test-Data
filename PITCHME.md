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
  - [Digitized AIDS Papers - Test Server](https://repository-test.library.georgetown.edu/handle/10822.2/4410)
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
  
+++?image=iiif/overview.png&size=auto 90%

---

## Manifest Generation Property File

- Address of IIIF Server
- Manifest Output Directory
- Where to find metadata
- How to assemble manifest contents

+++?image=iiif/dog-photos/manifestGenerate.template.prop
@[1-2](URL Prefix for image resources)
@[4-5](Component manifest file prefix)
@[7-11](Manifest output directory)
@[13-15](Manifest output file name)
@[17-18](DSpace REST API Integration - experimental)
@[20-24](Directory Separator for subfolders of image assets)
@[26-33](Collection manifest configuration)
@[35-38](2Page view)
@[40-42](Manifest Logo)
@[44-51](Global metadata file - applies to all items)
@[53-60](Global metadata fields)
@[62-70](Item Identifier Calculation)
@[72-83](Item Metadata Location)
@[85-89](Conversion class name - references a java enum class name)




