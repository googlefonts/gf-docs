# A quick guide to mastering new families for Google Fonts.

## Useful resources

### Tools

- [Font Bakery](http://github.com/googlefonts/fontbakery)
- [GF-Glyphs-Scripts](https://github.com/googlefonts/gf-glyphs-scripts)

### Docs

- [Project Checklist](https://github.com/googlefonts/gf-docs/blob/master/ProjectChecklist.md)
- [Glyphs Quick Start](https://github.com/googlefonts/gf-docs/blob/master/QuickStartGlyphs.md)

## Mastering process

### Repo layout

Arrange your repo into the following folder structure - the following are **mandatory**:

```
.
├── AUTHORS.txt
├── CONTRIBUTORS.txt
├── OFL.txt
├── README.md
├── fonts
│   └── Notable-Regular.ttf
└── sources
    └── Notable.glyphs
```

A good project to study is [https://github.com/googlefonts/mavenproFont](https://github.com/googlefonts/mavenproFont)

This has additional **optional** parts, like the /docs folder, which is a good place to put automatically generated content, or image files used in the README. Eg,

```
├── docs
│   └── sample.png
```

Note that the /docs folder is special, because its contents is directly available to web browsers.

### Design Inspection

Check each glyph is good. A simple way to do this is copy all glyphs in Glyphsapp into a tab.

![All glyphs of a font open in a tab of Glyphs app](assets/MasteringNewFamiliesForGF/Mastering0.png 'All glyphs of a font open in a tab of Glyphs app')

### Update Metadata so it's correct

Inside Glyphsapp with all open .glyphs sources execute the following:

Run Script > Google Fonts > QA. Fix everything until it clears

![Google Fonts QA Script](assets/MasteringNewFamiliesForGF/Mastering1.png 'Google Fonts QA Script')

### Double Check designer/meta info

Ensure copyright, author names etc are correct.

![Glyphs app font info window](assets/MasteringNewFamiliesForGF/Mastering2.png 'Glyphs app font info window')

### Generate ttfs and check with Fontbakery

![Checking TTF font files with FontBakery in the command line](assets/MasteringNewFamiliesForGF/Mastering2.png 'Checking TTF font files with FontBakery in the command line')

Fix all FAILS/ERRORs until capcake appears. If error cannot be cleared, post issue to [https://github.com/googlefonts/fontbakery](https://github.com/googlefonts/fontbakery)

### Push changes to git!

Push your latest revision to github, and file a request for a family update or publication on [https://github.com/google/fonts/issues](https://github.com/google/fonts/issues)
