# Google Fonts Docs (WIP)

## Contents

**[Getting started](#getting-started)**
- [Prerequisite knowledge](#prerequisite-knowledge)
- [Tooling](#tooling)
- [Scalable font production](#scalable-font-production)

**[Contributing](#Contributing)**
- [Creating a new family](#creating-a-new-family)
- [Updating an existing family](#updating-an-existing-family)

**[Universal](#universal)**
- [Font copyright](#font-copyright)
- [Font versioning](#font-versioning)
- [Font embedding (fsType)](#font-embedding-fstype)
- [Font vertical metrics](#font-vertical-metrics)
- [Monospace fonts](#monospace-fonts)
- [CJK fonts](#cjk-fonts)

**[Static Fonts](#static-fonts)**
- [Static font filenames](#static-font-filenames)
- [Supported styles](#supported-styles)
- [Single weight families](#single-weight-families)
- [Hinting](#hinting)

**[Variable Fonts](#variable-fonts)**
- [Font Origin](#font-origin)
- [Variable font requirements](#variable-font-requirements)
- [VF Font filenames](#vf-font-filenames)
- [Axes](#axes)
- [Instances](#instances)
- [STAT table](#stat-table)
- [VF Hinting](#vf-hinting)

**[The google/fonts repo](#the-googlefonts-repo)**
- [Repository structure](#repository-structure)

**[QA](#qa)**
 - [Our process](#our-process)

[**FAQ**](#todo)

TODO

## Getting started

### Prerequisite knowledge

We expect font developers to understand the following:

- Basic understanding of how OpenType fonts work.
- A commercial font editor such as Fontlab VI, Glyphsapp, Robofont or Fontforge
- Version control, specifically git. Use of desktop clients such as Github desktop is acceptable
- Shell scripting
- Managing python packages/tools using pip

The following resources should bring you up to speed.

- [Microsoft OpenType Specification](https://docs.microsoft.com/en-us/typography/opentype/spec/) (skim read! focus on what each table does)
- [Glyphsapp Tutorials](https://glyphsapp.com/tutorials)
- [Learn the workings of Git, not just the commands](https://developer.ibm.com/technologies/web-development/tutorials/d-learn-workings-git/)
- [Shell scripting basics](https://supportweb.cs.bham.ac.uk/docs/tutorials/docsystem/build/tutorials/unixscripting/unixscripting.html)
- [What is pip](https://realpython.com/what-is-pip/)


### Tooling

Google Fonts has its own tooling which will help you master and check your families. All our tools are written in Python.

Our tools can be installed using the following terminal commands:

```
pip install gftools
pip install fontbakery
pip install fontmake
```

We recommend installing our tools inside a Python virtualenv.


### Scalable font production

Google Fonts is used in approximately a third of all websites (citation needed, it may be more). We treat fonts with the same level of care as we do with software. We must ensure updated fonts do not break existing documents or websites. This requires treating fonts as software. We abide by the following principles:

- Font builds are repeatable
- Fonts can be built in one step
- Fonts can be built on any platform since we use opensource tools
- Projects are kept in version control
- We fix issues before upgrading
- We use CI for build and testing purposes
- We have testers with font domain knowledge

#### How we achieve this

- All our font production tools can be run from the commandline. This allows us to write [shell scripts](https://github.com/googlefonts/mavenproFont/blob/master/sources/build.sh) to generate font families.
- We use [fontmake](https://github.com/googlefonts/fontmake) to build our fonts.
- If we need to post process generated fonts, we use our `gftools` fix scripts.
- All of our tools are written in Python. We distribute these tools using [pypi/pip](https://pypi.org/). This allows us to use specific versions of each package. This ensures we're able to get the same results for each build.
- Since we only release Open Source fonts, we expect every family we release to have its own upstream github repository.
- Our main repository [github.com/google/fonts](https://github.com/google/fonts) uses CI. When new fonts are pushed, the CI will run our test suite and the results will be reviewed.

Font developers may find the above requirements overkill but our scale requires them. Joel Spolsky's classic article *[The 12 steps to better code](https://www.joelonsoftware.com/2000/08/09/the-joel-test-12-steps-to-better-code/)* illustrates why these requirements are beneficial.

## Contributing

### Creating a new family

- Font Design is original and of high quality
- Fonts and sources are available on Github
- There should only be one set of sources
- Fonts are built using fontmake and can be built in one step


### Updating an existing family

- Your modifications must be merged into the upstream project's github repository
- Your modifications must be made to the existing sources.
- No glyphs should be missing
- No styles should be missing
- Visual regressions must be avoided as much as possible.

*TODO MF: expand this section*


## Universal

The following applies to all fonts.

### Font copyright

Copright strings should be based on the following schema:

`Copyright { year } The { family } Project Authors ({ git_url })`

e.g

`Copyright 2019 The Oswald Project Authors (https://www.github.com/googlefonts/Oswald)`

If the project is OFL licensed, the first line of the OFL.txt file should be identical to the font copyright string.

Project authors can be specified in an [AUTHORS.txt](https://github.com/JulietaUla/Montserrat/blob/master/AUTHORS.txt) file. Project contributors can be specified in a [CONTRIBUTERS.txt](https://github.com/JulietaUla/Montserrat/blob/master/CONTRIBUTORS.txt) file. Please duplicate and modify these files instead of reinventing the wheel.


### Font versioning

Versioning is based on [semver](https://semver.org/), apart from we use `MAJOR.SIGNIFICANTMINORPATCH`, instead of `MAJOR.MINOR.PATCH`.

**Examples:**

If a breaking change is made e.g converting a static font family to a variable font family, the MAJOR must be incremented by 1 and the others reset e.g


Current `1.230`, new `2.000`

If a new character set is inserted, SIGNIFICANT should be incremented e.g:

Current `1.230`, new `1.330`


If a few new glyphs are added, MINOR should be incremented e.g:

Current `1.230`, new `1.240`


If a name table record is updated such as the copyright string, PATCH should be incremented e.g:

Current `1.230`, new `1.231`


## Font Embedding (fsType)

Set to `0` (Installable embedding)


## Font Vertical Metrics

TODO

### CJK Vertical Metrics

CJK vertical metrics are based on Source Han Sans and Noto CJK fonts.


The following metrics must be applied to all CJK fonts

- OS/2.sTypoAscender = `0.88 * font upm` e.g `0.88 * 1000 = 880`
- OS/2.sTypoDescender = `-0.12 * font upm` e.g `-0.12 * 1000 = -120`
- OS/2.sTypoLineGap = `0`

- hhea.ascent = `Set to look comfortable. Source Han Sans uses 1160`
- hhhea.descent = `Set to look comfortable. Source Han Sans uses -288`
- hhea.lineGap = `0`

- OS/2.winAscent =  `Same value as hhea.ascent` e.g `hhea.ascent = 1000, OS/2.winAscent = 1000`
- OS/2.winDescent = `abs value of hhea.descent` e.g `hhea.descent = -150, OS/2.winDescent = 150`

Our decision to follow the Adobe schema was based on dr Ken Lunde's comments and his release notes on Source Han Sans 

- https://github.com/source-foundry/font-line/issues/2
- [SourceHanSansReadMe.pdf](https://github.com/adobe-fonts/source-han-sans/raw/release/SourceHanSansReadMe.pdf)



## Monospace fonts

We require the OS/2 `panose` and post table `isFixedPitch` to be set. If neither of these are set, users may get fallback glyphs which are not monospaced, if they type a character which doesn't exist in the font.

Set `OS/2.panose.bProportion` to 9 and `post.isFixedPitch` to 1.

Developers can set these automatically by using the following gftools command:

`gftools fix-isfixedpitch`


## CJK Fonts

CJK fonts have the following additional requirements:

- Font format should be `.otf` not `.ttf`
- Vertical metrics should follow the [CJK vertical metrics](#cjk-vertical-metrics) guide
- Developers should check their fonts using the `googlefonts-cjk` fontbakery profile. This can be done using the following cli command`fontbakery check-googlefonts-cjk`.


## Static Fonts

### Static font filenames

Font filenames must be based on the following schema:

`FamilyName-Style.ttf` e.g `Montserrat-Regular.ttf`

The filename must not contain anything else.


### Supported Styles

The static fonts api supports 18 styles which consist of 9 weights, Thin-Black + Italics. The table below lists each style its font specific settings. *TODO MF convert integers to bits*

| Filename                        | Family Name (nameID 1) | Subfamily Name (nameID 2) | Typographic Family Name (nameID 16) | Typo Subfamily Name (nameID 17) | OS/2.usWeightClass | OS/2.fsSelection | hhea.macStyle |
|---------------------------------|------------------------|---------------------------|-------------------------------------|---------------------------------|--------------------|------------------|---------------|
| FamilyName-Thin.ttf             | Family Name Thin       | Regular                   | Family Name                         | Thin                            | 100                | 64               | 0             |
| FamilyName-ExtraLight.ttf       | Family Name ExtraLight | Regular                   | Family Name                         | ExtraLight                      | 200                | 64               | 0             |
| FamilyName-Light.ttf            | Family Name Light      | Light                     | Family Name                         | Light                           | 300                | 64               | 0             |
| FamilyName-Regular.ttf          | Family Name            | Regular                   |                                     |                                 | 400                | 64               | 0             |
| FamilyName-Medium.ttf           | Family Name Medium     | Regular                   | Family Name                         | Medium                          | 500                | 64               | 0             |
| FamilyName-SemiBold.ttf         | Family Name SemiBold   | Regular                   | Family Name                         | SemiBold                        | 600                | 64               | 0             |
| FamilyName-Bold.ttf             | Family Name            | Bold                      |                                     |                                 | 700                | 32               | 1             |
| FamilyName-ExtraBold.ttf        | Family Name            | ExtraBold                 | Family Name                         | ExtraBold                       | 800                | 64               | 0             |
| FamilyName-Black.ttf            | Family Name            | Black                     | Family Name                         | Black                           | 900                | 64               | 0             |
|                                 |                        |                           |                                     |                                 |                    |                  |               |
| FamilyName-ThinItalic.ttf       | Family Name Thin       | Italic                    | Family Name                         | Thin Italic                     | 100                | 1                | 2             |
| FamilyName-ExtraLightItalic.ttf | Family Name ExtraLight | Italic                    | Family Name                         | ExtraLight Italic               | 200                | 1                | 2             |
| FamilyName-LightItalic.ttf      | Family Name Light      | Italic                    | Family Name                         | Light Italic                    | 300                | 1                | 2             |
| FamilyName-Italic.ttf           | Family Name            | Italic                    |                                     |                                 | 400                | 2                | 2             |
| FamilyName-MediumItalic.ttf     | Family Name Medium     | Italic                    | Family Name                         | Medium Italic                   | 500                | 1                | 2             |
| FamilyName-SemiBoldItalic.ttf   | Family Name SemiBold   | Italic                    | Family Name                         | SemiBold Italic                 | 600                | 1                | 2             |
| FamilyName-Bold.ttf             | Family Name            | Bold Italic               |                                     |                                 | 700                | 33               | 3             |
| FamilyName-ExtraBold.ttf        | Family Name ExtraBold  | Italic                    | Family Name                         | ExtraBold Italic                | 800                | 1                | 2             |
| FamilyName-Black.ttf            | Family Name Black      | Italic                    | Family Name                         | Black Italic                    | 900                | 1                | 2             |


If a family has styles which are not in the above table, they should be released as a new family. To do this is, append the Unsupported style e.g Condensed to the family name. We frequently use this approach for [Condensed](https://fonts.google.com/?query=condensed) and [smallcap](https://fonts.google.com/?query=sc) sibling families.

For projects which use glyphsapp, we have an example [repository](https://github.com/davelab6/glyphs-export) which contains glyphs files that are set correctly.


### Single Weight families

If a family is a single weight and it visually doesn't have the appearance of a Regular weight, "One" must be appended to the family name. This approach allows us to keep the desired font name available if we decide to add more styles in the future. We have released many of these [families](https://fonts.google.com/?query=one) in the past.

The single weight families must have the following font specific settings:

| Filename                        | Family Name (nameID 1) | Subfamily Name (nameID 2) | Typographic Family Name (nameID 16) | Typo Subfamily Name (nameID 17) | OS/2.usWeightClass | OS/2.fsSelection | hhea.macStyle |
|---------------------------------|------------------------|---------------------------|-------------------------------------|---------------------------------|--------------------|------------------|---------------|
| FamilyNameOne-Regular.ttf          | Family Name One            | Regular                   |                                     |                                 | 400                | 64               | 0             |


### Hinting

Static fonts should be hinted using the latest version of [ttfautohint](https://www.freetype.org/ttfautohint/). If the results look poor on Windows browsers, it's better to release the fonts unhinted. Ttfautohint often struggles to hint display or handwritten typefaces.

Once the fonts have been hinted, run the fonts through `gftools fix-hinting`. If the fonts are unhinted, run the fonts through `gftools fix-nonhinting`.


## Variable Fonts


### Font origin

A variable font is simply a static font which has some additional tables FVAR, GVAR etc These new tables allow text clients to visually alter the font so it has a different appearance to end users.  Often font developers are unaware what the font origin is within their fonts. They'll then complain that fontbakery is failing many checks. It is recommended that font developers read the [Microsoft OpenType Font Variations Overview](https://docs.microsoft.com/en-us/typography/opentype/spec/otvaroverview) to understand how a variable works.


### Variable font requirements

#### Family is new and isn't on Google Fonts

- `VF` must not be appended to the family name.
- Fonts should be unhinted and have `gftools fix-nonhinting` applied to them
- The `wght` axis range must include `400` e.g 100-900, 400-900, 100-400 etc
- Fonts must conform to the sections listed below

#### Family already exists on Google Fonts

- Family name must be the same
- Hinting should match as closely as possible. If ttfautohint-vf produces bad results, we can release the family unhinted
- Every style that is available on Google Fonts must be included as an fvar instance
- There should be no missing glyphs
- Visual regressions should be as minimal as possible
- Fonts must conform to the sections listed below

A good rule to consider is that users should be able to swap the old family with the new VFs and not notice any differences.


### VF Font filenames

Font filenames must be based on the following schema:

`FamilyName[axis1,axis2].ttf` e.g `Montserrat[wdth,wght].ttf`

Axes should be listed in alphabetical order.

If your font contains unregistered axes, they should be capitalised and be listed first.

`Montserrat[GOOF,VEST,wdth,wght].ttf`

If the family consists of two VFs, one for Italic, the other for Roman. The fonts should named:

    Montserrat[axis1,axis2...].ttf
    Montserrat-Italic[axis1,axis2...].ttf


### Axes

Google Fonts supports all [Microsoft registered axes](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg).

We only support the following axes ranges:

**wght**: 100-900

**wdth**: 50-200

**opsz**: 0-∞


Developers can include their own axes but FontBakery will warn users that we cannot determine if the values are correct.


### Instances

Instance names and fvar coordinates must relate to the following tables.


**wght**

| name       | wght coordinate value |
|------------|-----------------------|
| Thin       | 100                   |
| ExtraLight | 200                   |
| Light      | 300                   |
| Regular    | 400                   |
| Medium     | 500                   |
| SemiBold   | 600                   |
| Bold       | 700                   |
| ExtraBold  | 800                   |
| Black      | 900                   |
| ExtraBlack | 1000                  |


**wdth**

| name           | wdth coordinate value |
|----------------|-----------------------|
| UltraCondensed | 50                    |
| ExtraCondensed | 62.5                  |
| Condensed      | 75                    |
| SemiCondensed  | 87.5                  |
|                | 100                   |
| SemiExpanded   | 112.5                 |
| Expanded       | 125.0                 |
| ExtraExpanded  | 150.0                 |
| UltraExpanded  | 200.0                 |


**opsz**

| name  | opsz coordinate value |
|-------|-----------------------|
| XXpt  | XX                    |

*XX can be any value*



#### Instance names

Instance names must mention the axes in the following order:

opsz wdth wght 

e.g `10pt Expanded Regular`

The order of the axes cannot be changed e.g `Regular Expanded 10pt` is not valid.

If a font doesn't include an axis which is listed above, it is simply skipped but the order kept e.g `10pt Regular`.


### STAT Table

All variable fonts should contain a STAT table (style attributes table). This table makes sure that instances are selectable in DTP apps. We recommend reading the [MS Spec](https://docs.microsoft.com/en-us/typography/opentype/spec/stat).

We use DaMa [statmake](https://github.com/daltonmaag/statmake) to generate this table. Marc Foley has written a python helper [script](https://github.com/googlefonts/Inconsolata/pull/44/files#diff-6cfd30d43aea19fb31ba7be6c7fb9b7c) that will generate the STAT table for Inconsolata. *TODO (M Foley) may be worth making a more general STAT table generator or include templates that can be altered. The prerequisite knowledge section is fairly advanced due to these types of requirements.*


## VF Hinting

Variable Font hinting still doesn't have a clear policy. Marc Foley has been applying the following pattern:

**Family already exists on Google Fonts**

If the family has over a billion weekly views, use [VTT](https://docs.microsoft.com/en-us/typography/tools/vtt/). *TODO Marc Foley. Write more about this. Also include example to Inconsolata once it is finished.*

If the family has under a billion weekly views, try [ttfautohint-vf](https://groups.google.com/d/msg/googlefonts-discuss/WJX1lrzcwVs/SIzaEvntAgAJ). If the results are bad, release unhinted.

If the font has been hinted using VTT or ttfautohint-vf, run the fonts through `gftools fix-hinting` e.g

`gftools fix-hinting Montserrat[wght].ttf`

**Family does not exist on Google Fonts**

Release unhinted. Run fonts through `gftools fix-nonhinting` e.g

`gftools fix-nonhinting Savant[wght].ttf`


## The google/fonts repo

The [google/fonts](https://github.com/google/fonts) repository is used as a staging area which allows font developers to upload their families to our website, [Google Fonts](https://fonts.google.com). When font developers push families, they are reviewed by a member of the team. If the family meets our quality criteria, the family will be pushed into production. We aim to push families into production every fortnight.

### Repository structure

The repository has the following structure:

```
.
├── AUTHORS
├── CONTRIBUTING.md
├── CONTRIBUTORS
├── README.md
├── TRIVIA.md
├── apache
├── catalog
├── ofl
├── to_production.txt
├── to_sandbox.txt
├── tools
└── ufl
```

The `ofl`, `ufl` and `apache` directories contain font families which we refer to as family dirs. Each family dir has the following structure:

```
.
├── DESCRIPTION.en_us.html
├── FONTLOG.txt
├── METADATA.pb
├── License (OFL.txt, UFL.txt, License.txt)
├── FontFamily-Regular.ttf
```

If the family is a variable font family, another directory called "static must be included. This directory contains static fonts for the family.


Each file has the following purpose:

- DESCRIPTION.en_us.html: describes the font family
- FONTLOG.txt: (optional) lists all the changes which have happened to the family
- METADATA.pb: contains metadata related to the family
- License: License for the font family. Valid choices are OFL.txt, UFL.txt, License.txt. If you're unsure what license to use, we recommend OFL.txt
- \*.ttfs: Family font files.


## QA

The quality assurance process if fairly strict in comparison most foundries and for good reasons. The Google Fonts font apis are non-versioned. This means that all users will recieve the same fonts. If we make an update to an existing family and radically alter it, it will affect existing users. The following general rules apply:

**Family is already on Google Fonts**

- Family name must be the same
- No missing encoded glyphs
- No missing styles/instances
- Vertical metrics must have the same visual appearance to end users


**Family is not on Google Fonts**

- Family name must be original. Use https://namecheck.fontdata.com/
- Family must contain the following [glyphs](https://github.com/googlefonts/gftools/blob/master/Lib/gftools/encodings/latin_unique-glyphs.nam)
- Vertcal metrics should comply to our guide

*TODO M Foley, include these requirements as individual sections.*

### Our process

*TODO*


### FAQ

*Fontbakery keeps reporting that my masters are not named correctly?*

If the source file is .glyphs, ...

If the source file is .designspace. Inspect the designspace and see if the Axis map elements are set correctly

*Fontbakery keeps reporting that the usWeightClass is incorrect?*

...
