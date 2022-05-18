# Local testing
{:.no_toc}

> <span class="icon">🐸</span>  This guide will help user to test their font locally to confirm quality-assurance. We recommend to test your font on the latest stable version of your OS and apps.
> Bear in mind:
> -   You can use virtual machines to test your fonts into different environments (practical for testing on older machine and therefore ensure backward compatibility).
> -   Installing consecutively different versions of a font family will lead to cache issues. So don’t forget to remove any remaining version of the font, restart the app, open the font menu and quit the app before installing any other version of the font. You may even need to clean the caches and then restart your computer. Another trick would be to append some kind of version number suffix to the family name until final version.
> -   If you plan on having both `.otf` and `.ttf` fonts on the same machine, we recommend you use a different name (specifically name ID 1, 4 and 6) to avoid any potential conflict.

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Apple macOS

### Installation

- [ ] No conflict during installation (in user fonts folder: `user/Library/Fonts`).
- [ ] Fonts appear in Font Book.
- [ ] Fonts looks good in Font Book.
- [ ] Family names and style manes are displayed correctly.

### Usage in external office apps

*MS Word, Powerpoint, LibreOffice Writer, LibreOffice Impress…*

- [ ] Fonts are grouped in menu by family name and all instances appear in weight order.
    - If VF, at least 1 instance appears in dropdown menu (font origin), but since late 2021 version of MS Office (Mac OS 11.\*) all of them should appear.
- [ ] Style linking works properly (bold and italic button or regular, italic button for all other cuts)
    - In MS Word, when style linking is absent or not working properly, you will see a fake bold or fake italic, watch carefully for that
- [ ] Fonts are displayed correctly
- [ ] Kerning works (just display a few kerning pairs to see if it works)
  -  In MS Word, kerning is applied to the text *as an option*, it is not a parameter that you activate for all your documents. Find it in the advanced parameters of Fonts settings: you have to check the box and specify a minimum text size to apply kerning (5pt for Mac, and 8pt for Windows)
- [ ] Glyphs having special interpolation (rvrn or special layers) are displaying as expected
- [ ] Letters with components work
- [ ] Combining characters (ligatures, conjuncts) work

### Usage in external layout apps

InDesign, Illustrator, Photoshop (Sketch, Figma, Affinity, CorelDRAW…)

- [ ] All styles appear in weight order in dropdown menu
- [ ] Instances are accessible through dropdown menu
- [ ] Instances are displayed correctly
- [ ] Sliders work properly (try from an upright instance and then with an italic instance)
- [ ] No unexpected behavior during variation
- [ ] Spacing and kerning work properly when using the sliders
- [ ] All OpenType Features work properly (activation from menu or style)
- [ ] Stylistic sets have names

**Variable Fonts**

- [ ] Composites and glyphs using brace/bracket layers have the same kerning and spacing as base-glyph
- [ ] Style linking is working in Adobe Mac apps (shift+cmd+b / shift+cmd+i)

### Usage in native apps

*TextEdit / Pages…*

- [ ] Font appear in font dropdown menu, all styles appear in style dropdown menu; default style is first on the list and then in weight order.
- [ ] Style linking works properly (cmd+b, cmd+i)
- [ ] Fonts are displayed correctly

Remember to remove fonts from the user fonts folder at the end of testing.

## Microsoft Windows

### Installation

- [ ] No conflict during installation
- [ ] Fonts appear in `C:/Windows/Fonts` folder

Double-click on each style and check if:

- [ ] Outline type is correct (PS for .otf, TT for .ttf)
- [ ] Font is displayed correctly (small size in waterfall)
  -  This is actually a good way to quickly check out your hinting.

### Usage in Office apps

*MS Word, Powerpoint, LibreOffice Writer, LibreOffice Impress…*

- [ ] Upright fonts appear in alphabetical order in dropdown menu (except for Bold and Italic instances that are activated only the B and I buttons)
  -  If VF, at least 1 instance appears in dropdown menu (font origin), but since 2022 version of MS Office (Windows 11) all of them should appear.
- [ ] Style linking works properly (bold and italic button or regular, italic button for all other cuts)
  -  In MS Word, when style linking is absent or not working properly, you will see a fake bold or fake italic, watch carefully for that
- [ ] Fonts are displayed correctly
- [ ] Kerning works (just display few kerning pairs to see if it works)
  -  In MS Word, kerning is applied to the text *as an option*, it is not a parameter that you activate for all your documents. Find it in the advanced parameters of Fonts settings: you have to check the box and specify a minimum text size to apply kerning (5pt for Mac, and 8pt for Windows)
- [ ] Glyphs having special interpolation (rvrn or special layers) are displaying as expected
- [ ] Letters with components work
- [ ] Combining characters (ligatures, conjuncts) work

## Web Browsers

*Chrome, Firefox, Safari, Edge…*

### All web formats

- [ ] Fonts are display correctly
- [ ] Fonts have kerning
- [ ] Linespacing looks okay (not too lose, not too tight)
- [ ] No clipping

### Variable Fonts

- [ ] [Samsa](https://lorp.github.io/samsa/src/samsa-gui.html) displays all instances with propers names in the STAT sidebar section. Regular and other default names are Elided (in parenthesis), and there is style linking between Regular and Bold (400 → 700), and between Roman and Italic (0 → 1)
- [ ] AVAR table display the expected result (linear or not)
- [ ] FVAR table has the instances you want with proper name and proper coordinates (only weight instances with coordinates every 100 for GF)
- [ ] Variation works properly (also glyphs with special layers)
- [ ] Kerning too

## Compatibility

If your fonts of different formats have the same naming, you will have to test formats one by one, restarting the computer between each to avoid cache issues and conflicts. If they have a different naming system, eg. `NameCFF.otf`, `NameTT.ttf`, `NameVF.ttf`, test their compatibility when installed on the same machine.

- [ ] No conflicts during installation
- [ ] All fonts are displayed in the fonts folder with their respective naming
- [ ] They can all be used in the same document, in whatever software, with no trouble

## TrueType Hinting

Manual hinting is often applied from 8ppm to 21ppm. Overshoot suppression until 48-51ppm.

How to prepare hinted rendering to review:

-   Install [gftools-qa](https://github.com/googlefonts/gftools#readme) and look at the image-waterfall output of diffbrowser.
-   Use `gftools gen-html` and upload 2 versions of generated fonts (hinted and unhinted) to look at if the font is better with or without hinting.

What to check:

- [ ] All glyphs are well aligned: if you see your /r higher than other letter, it is probably because top point is out of the blue zone. So checks where your guidelines normally are (baseline, x-height, caps-height, ascenders, descenders)
- [ ] Superior and inferiors figures are well aligned too with each other.
- [ ] No overshoot until 48ppm
- [ ] Glyphs are aligned also between styles (bold is not higher than Regular at the same ppm size)
- [ ] All glyphs of the same set look consistent (there is no glyph better or worse than the other)
- [ ] Letters are readable
- [ ] Weight is equally distributed (horizontally and vertically) in symmetrical letters (`o`, `e`, `g`, `c`)
- [ ] Spacing is not messed up
- [ ] Accents don't clash with letters
- [ ] Counter-shapes are not collapsed (`e`, `g`, `ring`)
- [ ] Upright and italic of the same weight have a consistent weight
- [ ] Dots on `i` and `j` are aligned

------------------------------------------------------------------------

## Useful Links

<div id="7dc7c317-aea1-431b-bbd2-1c444c0f7b68" class="column-list">

<div id="f3825586-3bd5-4763-8618-28818f95f083" class="column" style="width:50%">

**Testing web pages:**

-   [Wakamai Fondue](https://wakamaifondue.com/)
-   [FontDrop](https://fontdrop.info/)
-   [Impallari Testing Pages](http://www.rosaliewagner.com/font-testing/index.php)
-   [Axis-Praxis](https://www.axis-praxis.org/specimens/__DEFAULT__) and [Samsa](https://www.axis-praxis.org/samsa/)
-   [Dinamo Font Gautlet](https://dinamodarkroom.com/gauntlet/)
-   [Type Network’s Tools](https://typetools.typenetwork.com)
-   [Idiot Proof](https://idiotproofed.com/)
-   [Monotype’s interactive font specimen](https://www.fontspecimen.com/)
-   [FontGoggles](https://fontgoggles.org/)

</div>

<div id="b394bcd5-dd88-4c98-838b-335883397a54" class="column" style="width:50%">

**Testing apps:**

-   [DTL OT Master](https://www.fontmaster.nl/index.php/otmaster/)
-   [Font table viewer](https://glyphsapp.com/tools/fonttableviewer)
-   [Fontproof](https://github.com/silnrsi/fontproof) (still in development)

</div>

</div>

</div>
