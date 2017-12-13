# Coding Manifest Project Translations

[Main Menu](README.md) |
------------------------- | 

## Project Translation Modules implement the [ManifestProjectTranslate](https://github.com/Georgetown-University-Libraries/File-Analyzer/blob/master/demo/src/main/edu/georgetown/library/fileAnalyzer/filetest/iiif/ManifestProjectTranslate.java) interface

## Code Your Own Translator

    package edu.georgetown.library.fileAnalyzer.filetest.iiif;
    
    import java.util.regex.Matcher;
    import java.util.regex.Pattern;
    
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.IIIFEnums.IIIFProp;
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.IIIFEnums.IIIFType;
    
    public class AIDSPapersProjectTranslate extends EADFolderTranslate {
    
        @Override
        protected Pattern getBoxFolderPattern() {
                return Pattern.compile(".*[\\\\/]+b(.*)_f(.*)$");
        }
    
        @Override
        public String translate(IIIFType type, IIIFProp key, String val) {
                //Pattern p = Pattern.compile("b(\\d+)_f(\\d+)_item_(\\d+)_(\\d+)");
                if (type == IIIFType.typeCanvas && key == IIIFProp.label) {
                        return val.replaceFirst("mss_aids_.*_item_", "Item ").replaceFirst("_", " Page ").replaceFirst("\\.jpg", "");
                }
                return super.translate(type, key, val);
        }
        
        @Override
        public String rangeTranslate(String val) {
                Matcher m = Pattern.compile("^b(.*)_f(.*)$").matcher(val);
                if (m.matches()) {
                        return String.format("Box %s: Folder %s", m.group(1), m.group(2));
                }
                
                return super.rangeTranslate(val);
        }
    
    }

## Register Your Translator Class within a [ManifestProjectTranslateEnum](https://github.com/Georgetown-University-Libraries/File-Analyzer/blob/master/demo/src/main/edu/georgetown/library/fileAnalyzer/filetest/iiif/ManifestProjectTranslateEnum.java)

    package edu.georgetown.library.fileAnalyzer.filetest.iiif;
    
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.DefaultManifestProjectTranslate;
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.IIIFEnums.IIIFLookup;
    
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.ManifestProjectTranslate;
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.ManifestProjectTranslateEnum;
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.MetadataInputFile;
    
    public enum GeorgetownManifestProjectTranslate implements ManifestProjectTranslateEnum {
        EAD_AIDS_Papers{
                public ManifestProjectTranslate getTranslator() {
                        return new AIDSPapersProjectTranslate();
                }
        }
        ;
        
        @Override
        public ManifestProjectTranslate getTranslator() {
                return new DefaultManifestProjectTranslate();
        }
    }	
	
## Create a local CreateIIIFManifest class

    package edu.georgetown.library.fileAnalyzer.filetest.iiif;
    
    import gov.nara.nwts.ftapp.FTDriver;
    
    import java.util.ArrayList;
    
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.CreateIIIFManifest;
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.DefaultManifestProjectTranslateEnum;
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.ManifestProjectTranslateEnum;    public class GeorgetownIIIFManifest extends CreateIIIFManifest {
        @Override
        public ManifestProjectTranslateEnum[] getProjectTranslatorValues() {
                ArrayList<ManifestProjectTranslateEnum> opts = new ArrayList<>();
                for(ManifestProjectTranslateEnum tranlateEnum: DefaultManifestProjectTranslateEnum.values()) {
                        opts.add(tranlateEnum);
                }
                for(ManifestProjectTranslateEnum tranlateEnum: GeorgetownManifestProjectTranslate.values()) {
                        opts.add(tranlateEnum);
                }
                
                return opts.toArray(new ManifestProjectTranslateEnum[0]);                
        }
        public GeorgetownIIIFManifest(FTDriver dt) {
                super(dt);
        }
        @Override
        public String toString() {
                return "GU Create IIIF Manifest";
        }
        @Override
        public String getDescription() {
                return "GU Create IIIF Manifest for files";
        }
    
    }
	
## Register Your Task as a File Analyzer FileTest

    package edu.georgetown.library.fileAnalyzer.filetest;
    
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.CreateIIIFManifest;
    import edu.georgetown.library.fileAnalyzer.filetest.iiif.GeorgetownIIIFManifest;
    import gov.nara.nwts.ftapp.FTDriver;
    
    public class GUActionRegistry extends DemoActionRegistry {
        
        private static final long serialVersionUID = 1L;
    
        public GUActionRegistry(FTDriver dt, boolean modifyAllowed) {
                super(dt, modifyAllowed);
                
                removeFT(CreateIIIFManifest.class);
                add(new GeorgetownIIIFManifest(dt));
        }
    }

	
[Main Menu](README.md) | 
------------------------- | 
