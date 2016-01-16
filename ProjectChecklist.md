# Introduction

This page lists how to learn enough about Git to move an open font project available in this Mercurial repository to a Git repository, and how to manage a open font project with it.

## Tools

### Mobile

Testing your type on mobile devices is essential, and more important than on desktops.
You'll need both iOS and Android devices to do this testing.

- [ ] iPhone 4S+ with iOS 8+ ([reference](https://david-smith.org/iosversionstats/)) Safari
- [ ] Android 4.x or higher (ideally latest) with a "normal" size screen ([reference](https://developer.android.com/about/dashboards/index.html)) Chrome

The support of OpenType features in iOS is buggy, but improving.  

### Windows

You will need a Windows 7 computer, real or virtual machine, for testing your fonts as web fonts.
Windows 7 is the most commonly used desktop operating system ([reference](https://en.wikipedia.org/wiki/Usage_share_of_operating_systems)), and also the most challenging font rendering system compared to alternatives.

Microsoft offers zero-price virtual machine images at https://dev.modern.ie/tools/vms/mac/

- [ ] MSIE
- [ ] Firefox
- [ ] Chrome
- [ ] Safari
- [ ] Opera

### Mac

- [ ] Homebrew is a package manager for installing unix tools, such as FontForge. http://brew.sh

    brew install fontforge;

- [ ] pip is a package manager for installing python tools. https://pip.pypa.io

    pip install pyfontaine;
    pip install fontbakery;

- [ ] FontForge http://fontforge.github.io
- [ ] Glyphs https://glyphsapp.com
- [ ] FontLab https://fontlab.com
- [ ] OTMaster http://dtl.nl

#### Note on Adobe CS

The support of OpenType features in Adobe applications is buggy, but improving. 
Since Google Fonts are primarily for use on the web, how web browsers render the font is primarily important (and fortunately
browsers tend to have much better and up to date OpenType support in general.) 
If your font works on Windows MSIE and Android Chrome, but not in CS, then it is likely to be a CS bug. 

## Project Repository

### Set up a Github Repo

I expect all development to be done publicly, to invite the public to review work in progress, and to discuss all technical/design issues. 

Github is a online project collaboration platform, somewhat similar to Dropbox but more fine-grained as it uses the Git version control system.
New to Github and Git? Play the http://try.github.io 15 minute interactive game, and read http://nvie.com/posts/a-successful-git-branching-model, an essay about using Git for ongoing project management.

David Lemon said at ATypI 2014 how the Adobe Type team has benefited from libre fonts culture, and that Git and Github was one of the most positive things ([reference video](https://www.youtube.com/watch?v=DBz0rVUYNPA).)
Adobe have recently used this kind of "publish early and often, gathering feedback" approach with the Vortice design ([reference](http://blog.typekit.com/2015/03/04/introducing-vortice-and-the-adobe-type-concepts-program/).) A designer recently commented on his experience with all this:

> But really, I used to hate Git because I don’t understand why I have to use it…. until I started working with agile method. Since then I keep using Git even on projects I work alone because commit messages help me remember thing I did or why I did it on each project.

Glyphs has a plugin for working with Git, [github.com/simoncozens/GlyphsGit](https://github.com/simoncozens/GlyphsGit)

### Repo Contents

- [ ] README.md

Each Github repo must have a README.md that summarises the project, and inlines a sample.png file near the top.

- [ ] `documentation/sample.png`

A sample.png banner image showing the project, so people get an instant and visual overview. 
Create a `doc` subdirectory for keeping this and other such files.

- [ ] `documentation/DESCRIPTION.en_us.html`

Description paragraph in HTML to be used directly in font directories. 
This may be omitted, but if so requires Google to create one based on the contents of the README.md.

- [ ] `documentation/BRIEF.md`

A design brief that describes the intentions and goals of the project. 
Ideally this will be be added at the start of a project, defining the milestones that will be completed.
Typically it will be based on a proposal document made by the designer for financial support.

- [ ] Actual source files (`sources/`)

Project must include actual source files, the ones that we type designers use ourselves when drawing the design. 
These are typically files with extensions like `.glyphs .ufo .vfb .sfd .sfdir`.
These are often quite 'messy'. 
Common indications of actual source files are:

- guidelines
- overlapping shapes
- multiple layers with alternative drawings
- unencoded glyphs with alternative drawings
- 'smart components'

- [ ] Build source files (`sources/builds/`)

Some type projects maintain a set of 'build sources', which are used as input to a build script. 
They are updated less frequently than the actual source files, and updated with care. 
These are typically UFO files, compiled with the [afdko](https://github.com/adobe-type-tools/afdko)
Common indications of build source files are:

- no or minimal guidelines
- no overlapping shapes (the result of a Remove Overlaps operation)
- a single layer per Master
- no unusual or additional unencoded glyphs with alternative drawings
- no 'smart components'

- [ ] Build process documentation
- [ ] Build process script

You may maintain a build script that runs the build steps, or you may make a tutorial for taking those steps manually (or a mix.)

- [ ] Clean repo

There should not be 'stray' files in the repo, such as `.empty` or `.DS_Store`. 
Create a `.gitignore` file to prevent these being casually commited to the repo.

- [ ] Binary files **as ttx**
 
After the build process you will have OTF and TTF files, which must be included in the repo but only as TTX files. 
This enables the differences in binaries to be reviewed, and disincentivises development binaries from wider use.

## Pre-Production

Here are production steps you can take at the start of a project.

- [ ] The font family naming should follow the naming scheme described in the Family Naming section of [designwithfontforge.com/en-US/Font_Info_&_Metadata.html](http://designwithfontforge.com/en-US/Font_Info_&_Metadata.html)

Here is the default value in FontLab 5:

![Regular PSName Setting in FontLab - default](ProjectChecklist-FL-regular-default.png)

Here is the corrected value:

![Regular PSName Setting in FontLab - fixed](ProjectChecklist-FL-regular-fixed.png)

- [ ] The `fsType` embedding bits must be set to 0

![Set fsType to 0 in FontLab 5](ProjectChecklist-FL-fstype.png)

- [ ] If using FontForge, the Generate options should be set to not include an `FFTM` table
- [ ] The `DSIG` table should be included
- [ ] The `gasp` table should be set to 15
- [ ] License is set to 

    This Font Software is licensed under the SIL Open Font License, Version 1.1. This license is available with a FAQ at: http://scripts.sil.org/OFL

- [ ] License URL is set to http://scripts.sil.org/OFL
- [ ] Maintain a build script that applies ttfautohint with specific command line options and control file, that does not create a 'ttfautohint table' in production builds
- [ ] Name files according to the [DWFF Family Naming](http://designwithfontforge.com/en-US/Font_Info_&_Metadata.html) scheme ([spreadsheet](https://docs.google.com/spreadsheets/d/1ckHigO7kRxbm9ZGVQwJ6QJG_HjV_l_IRWJ_xeWnTSBg/edit#gid=0))
- [ ] Use a UPM of 1000 (even for TrueType fonts)
- [ ] Keep all points below `1056` and above `-270`, which is 132% of a 1000 UPM font; Android TextView widgets will clip fonts beyond that if there's no explicit padding (and designers tend to work just in Latin, so are unlikely to set it) says [Raph](https://groups.google.com/d/msg/googlefonts-discuss/qIPdk9Y7YUY/Eu21xtm0YrsJ)

## Post-Production

Here are production steps you can take during or near the end of a period of development.

- [ ] The Vertical Metrics must be set correctly, to the __family's__ y-axis bbox values, with linegaps of 0. 

This is where to find these values for each font in FontLab 5:

![BBox values in FontLab 5](ProjectChecklist-FL-vertical-metrics-id.png)

This is where to set the vertical metrics in FontLab 5:

![Vertical Metrics set correctly in FontLab 5](ProjectChecklist-FL-vertical-metrics-set.png)

- [ ] Production masters have PostScript manual hinting https://www.glyphsapp.com/tutorials/hinting-manual-postscript-hinting
- [ ] Develop a ttfautohint controls file to correct any problems in hinting. 

## Latin Design

- [ ] Support the 219 "base Latin" glyphs https://github.com/google/fonts/blob/master/tools/encodings/latin_unique-glyphs.nam
- [ ] Support all four figure sets https://www.glyphsapp.com/tutorials/figure-sets/
- [ ] Support mark based diacritics https://www.glyphsapp.com/tutorials/diacritics https://www.glyphsapp.com/tutorials/advanced-diacritics-narrow-marks
- [ ] Support the tallest glyph (perhaps Ǻ, per http://typedrawers.com/discussion/65/r-i-p) 
- [ ] Lining numerals with tabular spacing should be default; old style figures, and proportional variants, should be included with appropriate OpenType features. The general public calls old style the "jumping numbers" and like their tables to line up.
- [ ] Support Adobe Latin 3 http://adobe-type-tools.github.io/adobe-latin-charsets/adobe-latin-3.html
- [ ] Support Adobe Latin 4 (mainly Vietnamese) http://adobe-type-tools.github.io/adobe-latin-charsets/adobe-latin-4.html https://www.glyphsapp.com/tutorials/advanced-diacritics-multiple-anchors
- [ ] The `.notdef` glyph should be the recommended design https://www.microsoft.com/typography/otspec/recom.htm
- [ ] Anchors for all letter and diacritics https://github.com/weiweihuanghuang/Work-Sans/pull/17#issuecomment-139910842
- [ ] Prime design distinct from apostrophe https://github.com/googlei18n/noto-fonts/issues/510#issue-105444463

## OpenType

- [ ] Support fractions, superscript and subscript numerals https://www.glyphsapp.com/tutorials/fractions https://www.glyphsapp.com/tutorials/superscript-and-subscript-figures 
- [ ] Support Slashed Zero https://www.glyphsapp.com/tutorials/slashed-zero
- [ ] Support Catalan https://www.glyphsapp.com/tutorials/localize-your-font-catalan-punt-volat
- [ ] Support Dutch https://www.glyphsapp.com/tutorials/localize-your-font-accented-dutch-ij
- [ ] Support German https://www.glyphsapp.com/tutorials/localize-your-font-german-capital-sharp-s
- [ ] Support Polish https://www.glyphsapp.com/tutorials/localize-your-font-polish-kreska http://www.twardoch.com/download/polishhowto/ogonek.html 
- [ ] Support Romanian and Moldovian https://www.glyphsapp.com/tutorials/localize-your-font-romanian-and-moldovan
- [ ] Support Turkish https://www.glyphsapp.com/tutorials/localize-your-font-turkish
- [ ] Support Turkish with OpenType http://typedrawers.com/discussion/1101/izmir-turkey
- [ ] Support tabular numbers with a consistent glyph width across the Regular, Italic, Bold and Bold Italic styles of a family http://typedrawers.com/discussion/1103/tabular-figures-width-consistency

## Test Documents

Your project should include comprehensive testing documents, both for yourself to confirm your design works well, and so that others can evaluate their modifications.

These testing document projects may also be helpful:

- [ ] http://understandingfonts.com/2011/fonttest
- [ ] http://impallari.com/testing
- [ ] http://testmyfont.com

### Tests

- [ ] Test for all letter/diacritic combinations (see https://github.com/weiweihuanghuang/Work-Sans/pull/17#issuecomment-139910842)

## Release

- [ ] Version your binaries appropriately

Abstractly, we can distinguish between work that is public and publicised. 
Proprietary software/fonts are developed privately, and then tightly couple their releases' publication and publicity, marking clear versions in each release. 
Publicly developed libre software/fonts necessarily make more of a difference between the two concepts, since publication is constant. 

Practically speaking, the availability of fonts in the Google Fonts API is the primary point of publicity. 
A secondary point is the Github releases system - https://help.github.com/articles/creating-releases/ - which is a good way of marking new versions when you wish to queue them up for release in the Google Fonts API.
Its important that the version fields inside the source and binary font files in a release (eg in the NAME table, or Font Info inputs) match the version labelled on the release. 

That github help article links to <http://semver.org>. 
While this is a good version numbering scheme for software it does not work for fonts, because the binary font metadata field can only have one period separator. 

So a `MAJOR.MINOR-or-PATCH` scheme is better for fonts, starting with 1.000 and incrementing from there (1.001, 1.002, etc.) 

It would be good to have some note in the version string where possible like 'development version' that is removed when making a release build. 

- [ ] Use the Github Releases system to tag a release of your git repository, and then upload a ZIP with the actual release OTF/TTF files.

* https://github.com/blog/1547-release-your-software
* https://help.github.com/articles/about-releases/
* https://help.github.com/articles/creating-releases/

## Post Release

- Promote your project on social media
- Submit the work to awards competitions (TDC, TDC2, Granshan, Morisawa...)
- Reach out to users and find out how the font can be improved, and ask them to co-pay for improvements with Kickstarter or similar.

# Further Reading

**UFO:** The UFO format is documented at http://unifiedfontobject.org and developed on Github (https://github.com/unified-font-object/ufo-spec) and the ufo-spec mailing list (https://groups.google.com/forum/#!forum/ufo-spec)