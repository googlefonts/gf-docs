# Local Testing and proofing
To do : 
- add a table of content
- update with the latest Mac Word VF support stuff.
- update with dome proffing tips using gftools
- Make a table to avoid repeating stuff between Mac and Windows
- add images

## Apple macOS

### Installation

- [ ] No conflict during installation (in user fonts folder: `user/Library/Fonts`)
- [ ] Fonts appear in Fontbook
- [ ] Fonts looks good in Fontbook


### Usage

#### External office apps

MS Word, Powerpoint, LibreOffice Writer, LibreOffice Impress

- [ ] Upright fonts appear in alphabetical order in dropdown menu
  - [ ] If VF, at least 1 instance appears in dropdown menu (font-origin), ideally all of them should appear.
- [ ] Style linking works properly (bold and italic button or regular, italic button for all other cuts)
  * In MS Word, when style linking is absent or not working properly, you will see a fake bold or fake italic, watch carefully for that
- [ ] Fonts are displayed correctly (basic alphabet)
- [ ] Kerning works (just display few kerning pairs to see if it works)
  * In MS Word, kerning is applied to the text _as an option_, it is not a parameter that you activate for all your documents. Find it in the advanced parameters of Fonts settings: you have to check the box and specify a minimum text size to apply kerning (5pt for Mac, and 8pt for Windows)
- [ ] Glyphs with components work
- [ ] Glyphs with special layers work
- [ ] Combining characters (ligures, conjucnts) work

#### External layout apps

InDesign, Illustrator, Photoshop, Sketch, Figma, Affity, CorelDRAW

- [ ] All styles appear in weight order in dropdown menu
- [ ] Fonts are displayed correctly
- [ ] All OpenType Features work properly (activation from menu or style)

Variable Fonts

- [ ] Cursors work properly
- [ ] No weirdness during variation
- [ ] Instances are accessible through dropdown menu
- [ ] Instances are displayed correctly
- [ ] Spacing and kerning work properly when using the cursor
- [ ] Composites and glyphs using brace/bracket layers have the same kerning and spacing as base-glyph

#### Standard app

TextEdit

- [ ] Font appear in font dropdown menu, all styles appear in style dropdown menu (its OK if order looks random)
- [ ] Style linking works properly
- [ ] Fonts are displayed correctly

Remember to remove fonts from the user fonts folder at the end of testing.

## Microsoft Windows

### Installation

- [ ] No conflict during installation
- [ ] Fonts appear in `C://Fonts` folder

Double-click on each style and check if:

- [ ] Outline type is correct (PS for .otf, TT for .ttf)
- [ ] Font is digitally signed
- [ ] Font is displayed correctly (small size in waterfall)

### Usage

#### Office apps

MS Word, Powerpoint, LibreOffice Writer, LibreOffice Impress

- [ ] Upright fonts appear in alphabetical order in dropdown menu
  - [ ] If VF, at least 1 instance appears in dropdown menu (font-origin), ideally all of them appear
- [ ] Style linking works properly (bold and italic button or regular, italic button for all other cuts)
- [ ] Fonts are displayed correctly (basic alphabet)
- [ ] Kerning works (just display few kerning pairs to see if it works)
  * In MS Word, kerning is applied to the text _as an option_, it is not a parameter that you activate for all your documents. Find it in the advanced parameters of Fonts settings: you have to check the box and specify a minimum text size to apply kerning (5pt for Mac, and 8pt for Windows)
- [ ] Glyphs with components work
- [ ] Glyphs with special layers work
- [ ] Combining characters (ligures, conjucnts) work

Remember to remove fonts from the user fonts folder at the end of testing.

## Web Browsers

Chrome, Firefox, Safari, Edge

### All web formats

- [ ] Fonts are display correctly
- [ ] Fonts have kerning
- [ ] Linespacing looks okay (not too lose, not too tight)
- [ ] No clipping

Variable Fonts

- [ ] [Samsa](https://lorp.github.io/samsa/src/samsa-gui.html) displays all instances with propers name in the STAT sidebar section
- [ ] Variation works properly
- [ ] Kerning too

## Compatibility

If your fonts of different formats have the same naming, you will have to test formats one by one, restarting the computer between each to avoid cache issues and conflicts.
If they have a different naming system, eg. `NameCFF.otf`, `NameTT.ttf`, `NameVF.ttf`, test their compatibility when installed on the same machine.

- [ ] No conflicts during installation
- [ ] All fonts are displayed in the fonts folder with their respective naming
- [ ] They can all be used in the same document, in whatever software, with no trouble

## TrueType Hinting (from 9ppm to 50ppm)

How to prepare hinted rendering to review:

* Install [gftools-qa] and look at the image-waterfall output of diffbrowser. 
* Use [GF Regression](http://35.238.63.0) and upload 2 versions of generated font (hinted and unhinted) to look at if the font is better with or without hinting.

What to check:

- [ ] All glyphs are well aligned: if you see your /r higher than other letter, it is probably because top point is out of the blue zone. So checks where your guidelines normally are (baseline, x-height, caps-height, ascenders, descenders)
- [ ] Superior and inferiors figures are well aligned too with each other.
- [ ] No overshoot until 48ppm
- [ ] Glyphs are aligned also between styles (bold is not higher than Regular at the same ppm size)
- [ ] All glyphs of the same set look consistent (there is no glyph better or worse than the other)
- [ ] Letters are readable
- [ ] Weight is equally distributed (horizontally and vertically) in symmetrical letters (o, e g, c)
- [ ] Spacing is not messed up
- [ ] Accents don't clash with letters
- [ ] Counter-shaped are not closed (e, g, ring)
- [ ] Upright and italic of the same weight have a consistent weight
- [ ] Dots on /i and /j are aligned

## Testing Tools

#### Web

- [FontDrop](https://fontdrop.info)
- [Wakamai Fondue](https://wakamaifondue.com)
- [Impallari Testing Pages](http://www.rosaliewagner.com/font-testing/index.php)
- [Axis-Praxis](https://www.axis-praxis.org/specimens/__DEFAULT__) and [Samsa](https://www.axis-praxis.org/samsa/)
- [Dinamo Font Gautlet](https://dinamodarkroom.com/gauntlet/)

#### Desktop

- [FontGoggles](https://fontgoggles.org)
- [DTL OT Master](https://www.fontmaster.nl/index.php/otmaster/)
- [Font table viewer](https://glyphsapp.com/tools/fonttableviewer) (for static fonts)
- [Fontproof](https://github.com/silnrsi/fontproof) (still in development)
