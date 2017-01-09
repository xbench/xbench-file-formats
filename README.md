# ApSIC Xbench 3.0 file formats

There are three file formats relevant for ApSIC Xbench 3.0:

* [**ApSIC Xbench Project file**](#heading-xbp) (.xbp extension).  This file defines the
  bilingual files added to the Xbench project, their types, their attributes.
  It also defines the inline entries of the project checklist and the paths
  for any additional checklist files attached to the project.

* [**Xbench QA settings at load time**](#heading-xml) (.xml extension).  This file defines the QA
  settings (including the spell-checking dictionary) that must be selected in the
  Xbench **QA** tab.  It also refers to the Xbench project file (.xbp) that must be
  loaded with these settings.

* [**Xbench checklist file**](#heading-xbckl) (.xbckl extension).  This file defines the checklist 
  entries and the included or inherited checklists.

## ApSIC Xbench Project File (.xbp extension)<a name="heading-xbp"></a>

The ApSIC Xbench project file is used to store the settings for the files or
directories that must be loaded by Xbench.

The file format is a UTF-8 XML file and you can cone simply by choosing 
**File**->**Save** in ApSIC Xbench.

Please remember that XML element and attribute names are case-sensitive.

The .xbp file has this structure:

```xml
<?xml version="1.0" ?>
<xbench version="2.9.438" savedwith="3.0.1374">
    <project>
        <filename xml:space="preserve">C:\Users\me\EXAMPLE.xbp</filename>
        <maxcols>5</maxcols>
        <showfilename>1</showfilename>
        <showkeytermsattop>1</showkeytermsattop>
        <removedupes>0</removedupes>
        <autorefreshinterval>0</autorefreshinterval>
        <instructions xml:space="preserve"></instructions>
        <memoryfile></memoryfile>
        <checklistgroup>
            <checklist name="$project"></checklist>
        </checklistgroup>
        <glossarylist>
            <glossary type="13">
                <ident>0</ident>
                <filename xml:space="preserve">TheDocs.xliff</filename>
                <level>1</level>
                <process>0</process>
                <static>0</static>
                <srclang>0</srclang>
                <trglang>0</trglang>
                <flag>0</flag>
                <comments></comments>
                <removedupes>0</removedupes>
                <newtranslations>1</newtranslations>
                <swapsourcetarget>0</swapsourcetarget>
                <keyterms>0</keyterms>
                <autorefresh>0</autorefresh>
            </glossary>
        </glossarylist>
    </project>
</xbench>
```

This is the meaning of the attributes and element values in the sample above:

```xml
<xbench version="2.9.438" savedwith="3.0.1374">
```    

* **version**: The first Xbench version in which the file can be loaded.
* **savedwith**: The Xbench version in which the file was saved.

```xml
<filename xml:space="preserve">C:\Users\me\EXAMPLE.xbp</filename>
```
* **filename**: The file name for the xbp file. This file name is just
  informative, the path name here does not have any functional effect.

```xml
<maxcols>5</maxcols>
```

* **maxcols**: The maximum number of columns that must be shown in the **Search**
  tab in Xbench.  If the value is 0, Xbench sets the number of columns in the
  **Search** tab per the values retrieved from files loaded.

```xml
<showfilename>1</showfilename>
```

* **showfilename**: If its value is 1, the last column of the **Search** tab will
  contain the file name.  If its value is 0, the file name will not be shown as a
  column.

```xml
<showkeytermsattop>1</showkeytermsattop>
```

* **showkeytermsattop**: If its value is 1, any files defined as key
  terms in the project file, will be shown at the top of the search results
  above any other priorities with a black font.  If its value is 0, the key terms
  files will be shown with their assigned priority (either high, medium, or low)
  and the font color of the priority.

```xml
<removedupes>0</removedupes>
```

* **removedupes**: If its value is 1, duplicated entries with the same source and
  target text in the same file will be consolidated as one single entry in the 
  **Search** (the number of instances consolidated will be indicated in the **#** column).

```xml
<autorefreshinterval>0</autorefreshinterval>
```

* **autorefreshinterval**: The value indicated the number of minutes between reloads
  of files defined as *autorefresh*.  If the value is 0, there will not be
  autorefresh.

```xml
<instructions xml:space="preserve"></instructions>
```

* **intructions**: The instructions for the project.  If there are instructions
  defined, the **Project Instructions** tab will be shown when the Xbench project
  loads.  The instructions can have rich formatting if its value is in RTF (Rich
  Text Format).

```xml
<memoryfile></memoryfile>
```

* **memoryfile**: This value is not currently used by Xbench.

```xml
<checklistgroup>
    <checklist name="$project"></checklist>
    <checklist name="My favorite typos" path="C:\Users\me\My favorite typos.xbckl" active="true"></checklist>
</checklistgroup>
```

* **checklistgroup**: The container for all checklists attached to the project.
* **checklist**: The individual checklist attached to the Xbench project.  It has 
  these attributes:
  * **name**: The display name of the checklist.  If the value is `$project`, it is
  the Project checklist, which was its checklist items inlined in the .xbp file.
  * **path**: The file path to the .xbp file.
  * **active**: If `true` the checklist is active in the **QA** tab. If `false`, the 
  checklist is listed but not active in the **QA** tab.

```xml
<glossarylist>
    <glossary type="13">
```

* **glossarylist**: The container of **glossary** elements.
* **glossary**: Indicates a glossary (bilingual file) block.  Please note that
  anything that can be loaded in Xbench (for example an .sdlxliff file) may be called
  a glossary. They are called glossaries for historical reasons (at the beginning 
  of time, Xbench only had a search function, which was used to search glossaries).
  * **type**: The type number of the glossary.  Possible type numbers are:
    * **-1**: Auto-detect
    * **1**: Tab-delimited text file (.txt, .tsv, .utx extensions)
    * **2**: Trados exported TM (.txt extension)
    * **3**: Multiterm 5 exported file (.txt extension)
    * **4**: IBM TM/OpenTM2 glossary (.sgm extension)
    * **5**: Microsoft glossary (.csv extension)
    * **6**: TMX (.tmx extension)
    * **7**: Wordfast TM (.txt extension)
    * **8**: Trados uncleaned file (.doc or .rtf extensions)
    * **9**: Trados TagEditor file (.ttx extension)
    * **10**: SDLX file (.itd extension)
    * **11**: Wordfast glossary (.txt extension)
    * **12**: Exported TM/2 folder (.fxp extension)
    * **13**: XLIFF-based file (.xlf, .xlif, .xliff, .mxliff, .xlz, .mqxlz, .mqout, .mqback, .xlf.zip extensions)
    * **14**: TBX/Martif file (.tbx, .mtf, .xml)
    * **15**: Multiterm glossary (.xml, .sdltb, .mdb extensions)
    * **16**: MacOSXGLossary (.ad or .lg extensions)
    * **17**: Deja Vu X/Idiom file (.wsprj, .dvpng, .dvprj, .dvsat extensions)
    * **18**: Deja Vu X/Idiom TM (.wstm, .dvmdb, .dvapr)
    * **19**: SDLX TM file (.mdb extension)
    * **20**: Logoport file (.rtf extension)
    * **21**: IBM TM/OpenTM2 exported TM (.exp extension)
    * **22**: PO file (.po extension)
    * **23**: Wordfast Pro file (.txml, .txlf extensions)
    * **24**: SDL Studio file (.sdlxliff, .sdlproj extensions)
    * **25**: QtLinguist file (.ts extension)
    * **26**: MemoQ file (.mqxliff, .mqxlz, .mqback, .mqout extensions)
    * **27**: SDL Studio TM (.sdltm extension)
    * **28**: TIPP file (.tpp extension)
    * **29**: Passolo glossary (.glo extension)
    * **30**: Transifex
    * **31**: Deja Vu X/Idiom termbase (.wstd, .dvtdb)
    * **32**: Matecat job
    * **33**: Google Translator Toolkit (GTT) file (.xbgtt extension)
    * **50**: Transit XV/NXT directory
    * **51**: Directory of Tag Editor ttx files
    * **52**: Directory of SDLX itd files
    * **53**: Directory of Trados uncleaned Word files
    * **54**: Remote Xbench Server
    * **55**: Directory of Logoport RTF files
    * **56**: Directory of Tab-delimited text files
    * **57**: Directory of Trados exported TMs
    * **58**: Directory of IBM TM/OpenTM2 glossary files
    * **59**: Directory of Microsoft glossary files
    * **60**: Directory of TMX files
    * **61**: Directory of Wordfast TMs
    * **62**: Directory of Wordfast files
    * **63**: Directory of exported TM/2 folders
    * **64**: Directory of XLIFF-based files
    * **65**: Directory of Mac OSX glossaries
    * **66**: Directory of exported IBM TM/OpenTM2 TMs
    * **67**: Directory of PO files
    * **68**: Directory of Wordfast Pro tmxl files
    * **69**: Directory of SDL Studio sdlxliff files
    * **70**: Directory of Qt Linguist files
    * **71**: Directory of Trados glossaries
    * **72**: Directory of TBX files
    * **73**: Directory of Multiterm files
    * **74**: Directory of Deja Vu X/Idiom files
    * **75**: Directory of Deja Vu X/Idiom TMs
    * **76**: Directory of SDLX TMs
    * **77**: Directory of memoQ files
    * **78**: Directory of SDL TMs
    * **79**: Directory of TIPP files
    * **80**: Directory of Passolo glossaries
    * **81**: Directory of Deja Vu X/Idiom termbases
    * **82**: Directory of GTT files
    * **99**: IBM TM/OpenTM2 installed folder

```xml
<ident>0</ident>
```        

* **ident**: The internal identifier of the glossary. It must be a number greater
  or equal to 0, and **it must be unique** for each `glossary` element in the 
  `glossarylist` container.

```xml
<filename xml:space="preserve">TheDocs.xliff</filename>
```
* **filename**: The path to the file. If can be an absolute path or a relative path
to the location of the .xbp file.

```xml
<level>1</level>
```

* **level**: The priority level of the file for search. Possible values are:
  * 1: Low priority
  * 2: Medium priority
  * 3: High priority

```xml  
<process>0</process>
```
* **process**: Determines the mnemonic processing that must be applied to segments. Possible values are:
  * 0: None
  * 1: Remove Shortcuts (&)
  * 2: Remove Shortcuts (~)
  * 3: Remove Shortcuts (_)
  * 4: Remove Shortcuts (_&)
  * 5: Remove Shortcuts (~&)
  * 6: Remove Shortcuts (_~)
  * 7: Remove Shortcuts (^)
  * 8: Remove Shortcuts (&amp;)

```xml
<static>0</static>
```

* **static**: A value of 1 means that the glossary will not be reloaded with Refresh (F5)
```xml
<srclang>0</srclang>
```

* **srclang**: This value is not currently used by Xbench.

```xml        
<trglang>0</trglang>
```

* **tgtlang**: This value is not currently used by Xbench.

```xml        
<flag>0</flag>
```

* **flag**: This value indicates if the entry should appear with a colored square 
  (a.k.a. flag) in the **Search** tab.  Possible values can be:
  * 0: No flag
  * 1: White
  * 2: Gray
  * 3: Light blue 
  * 4: Dark blue
  * 5: Red
  * 6: Magenta

```xml        
<comments></comments>
```

* **comments**: These are the comments for the glossary biligual file.

```xml
<removedupes>0</removedupes>
```

* **removedupes**: If the value is 1, entries with the same source and target will
  be consolidated in a single entry.  

```xml
<newtranslations>1</newtranslations>
```

* **newtranslations**: If the value is 1, the file is ongoing translation. If you need
  to QA this file, you need to set this element to 1.

```xml        
<swapsourcetarget>0</swapsourcetarget>
```        

* **swapsourcetarget**: If the value is 1, Xbench will swap the source and target texts.

```xml
<keyterms>0</keyterms>
```

* **keyterms**: If the value is 1, the file is considered to be a key terms file.  The
  key terms files have two main purposes:
  * In the search results, they appear with a star.
  * In QA, they are used as the source of terms from QA check 'Key Terms Check'.

```xml
<autorefresh>0</autorefresh>
```

* **autorefresh**: If the value is 1, the file will be reloaded at the interval defined
  by autorefreshinterval.  The file will be reloaded only if it has changed.

Certain file types also have *special settings*.  These special settings are stored
in the xxxx element.  The file types with special settings are:

* TBD
* TBD
            
## Xbench QA settings at load time<a name="heading-xml"></a>

You can launch Xbench with project file and a preselected set of QA settings using 
the `-o` switch.

```
c:\> xbench.exe -o=qa-settings-file.xml
```

The XML file has the following structure:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xbenchqa>
    <input>
        <project xml:space="preserve" addtorecent="yes">E:\XBench\prova3.xbp</project>
        <qaoptions defaults="saved">
            <speller>fr-FR</speller>
            <option group="Basic" function="Untranslated Segments" status="enabled" />
            <option group="Basic" function="Target same as Source" status="disabled" />
            <option ... />
        </qaoptions>
    </input>
</xbenchqa>
```

This is the meaning of the attributes and element values in the sample above:

```xml
<project xml:space="preserve" addtorecent="yes">C:\Xbench\test.xbp</project>
```

* **project**: This value contains the path of the .xbp file that should be launched
  with these QA settings.
* **addtorecent**: If `yes`, the .xbp project will be added to the recent projects list,
  so that it can be reloaded later with **Project**->**Reopen**.

```xml
<qaoptions defaults="saved">
```

* **defaults**: This value indicates the source for default values of any QA options
  not specified expressly in this file.  The possible values are:  
  * **saved**: The QA values that are in the registry, typically saved when you shut
    down Xbench.
  * **current**: The QA values that are in the Xbench session currently opened by the
    user.
  * **preset**: The QA values of a newly installed Xbench on a new machine.

  The default value is **saved**.

```xml  
<speller>fr-FR</speller>
```

* **speller**: This value indicates the target language for spell-checking in ISO format.  The
  spell-checking dictionary must have been previously installed with **Tools**->
  **Spell-checking dictionaries**.

```xml
<option group="Basic" function="Untranslated Segments" status="enabled" />
```

* **group**: The name of the group in the **Check Group** list box of the **QA** tab.
  The name is case-sensitive and must match exactly the text shown in the Xbench user interface.
  The values available are `Basic` and `Content`.
* **function**: The name of the check in the **List of Checks** list box of the **QA** tab.
  The name is case-sensitive and must match exactly the text shown in the Xbench user interface.
  The values available for the `Basic` group are:
  * `Untranslated Segments`
  * `Inconsistency in Source`
  * `Inconsistency in Target`
  * `Target same as Source`
  
  The values available for the `Content` group are:
  * `Tag Mismatch`
  * `Numeric Mismatch`
  * `URL Mismatch`
  * `Alphanumeric Mismatch`
  * `Unpaired Symbol`
  * `Unpaired Quotes`
  * `Double Blank`
  * `Repeated Word`
  * `Key Term Mismatch`
  * `CamelCase Mismatch`
  * `ALLUPPERCASE Mismatch`
* **status**: If the value is `enabled` the QA check will be selected in the **QA** tab,
  if the value is `disabled` the QA check will not be selected in the **QA** tab.
 
## Xbench checklist file<a name="heading-xbckl"></a>

The checklist file has the *.xbckl* file extension and contains the checklist items.
The checklist file may include other checklist files or inherit checklist items from
other checklist files.

The checklist file is an XML file with the following structure:

```xml
<?xml version="1.0" ?>
<xbench-checklist version="1.0">
  <checklist name="my favorite typos">
    <inherit name="Common typos">C:\Users\me\Common typos.xbckl</inherit>
    <check name="ApSIC: Missing or mistyped company name?" categories="Proper Names">
      <term type="source" xml:space="preserve" casecheck="yes" wholeword="yes" 
            notrim="no" normalizewhitespace="no" normalizeaccents="no"
            powersearch="yes" searchmode="simple">ApSIC</term>
      <term type="target" xml:space="preserve" casecheck="yes" wholeword="yes" 
            notrim="no" normalizewhitespace="no" normalizeaccents="no"
            powersearch="yes" searchmode="simple">-ApSIC</term>
      <description xml:space="preserve">Check proper ApSIC&apos;s spelling</description>
      <timestamp>2017-01-05 12:30</timestamp>
    </check>
  </checklist>
</xbench-checklist>
```

This is the meaning of the attributes and element values in the sample above:

```xml
<xbench-checklist version="1.0">
  <checklist name="my favorite typos">
```

* **version**: The version of the checklist file format.
* **name**: The display name of the checklist.  This is the name that will appear in
Xbench Checklist Manager navigation's tree.

```xml
<inherit name="Common typos">C:\Users\me\Common typos.xbckl</inherit>
```

* **inherit**: The path to a checklist whose items are inherited into 
  this one.  You can inherit more than one checklist into a checklist.
* **name**: The display name of the inherited checklist.

```xml
<check name="ApSIC: Missing or mistyped company name?" categories="Proper Names">
```

* **name**: The name of the checklist item. 
* **categories**: The category that is assigned to checklist item.  This is an arbitrary
  text.

```xml
<term type="source" xml:space="preserve" casecheck="yes" wholeword="yes" 
      notrim="no" normalizewhitespace="no" normalizeaccents="no"
      powersearch="yes" searchmode="simple">ApSIC</term>
<term type="target" xml:space="preserve" casecheck="yes" wholeword="yes" 
      notrim="no" normalizewhitespace="no" normalizeaccents="no"
      powersearch="yes" searchmode="simple">-ApSIC</term>
```
* **term**: The text that is matched (or not matched) in the checklist item.  There can
  be one `term` element for the source text and one `term` element for the target text.
* **type**: Indicates if the text refers to `source` or to `target`.
* **casecheck**: If the value is `yes`, the text is case-sensitive. The default value 
  is `no`.
* **wholeword**: If the value is `yes`, the text must match a whole word. The default 
  value is `no`.
* **notrim**: If the value is `yes`, leading or trailing whitespace is significant. The default value is `no`.
* **normalizewhitespace**: If the value is `yes`, whitespace is converted to regular 
  blanks prior to search. The default value is `no`.
* **normalizeaccents**: If the value is `yes`, any native characters are normalized to
  ASCII 7 prior to search. The default value is `no`.
* **powersearch**: If the value is `yes`, it means that the search uses the PowerSearch
  grammar.  This value must be the same in both `source` and `target` elements. The default value is `no`.
* **searchmode**: Indicates the search mode.  Possible values are `simple`, `regexp` 
  (regular expression), and `msword` (Microsoft Word wildcard).

```xml
<description xml:space="preserve">Check proper ApSIC&apos;s spelling</description>
<timestamp>2017-01-05 12:30</timestamp>
```

* **description**: A detailed description of the checklist item.
* **timestamp**: The date and time the checklist item was last updated.
