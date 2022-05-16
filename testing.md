<div>

# Local testing

</div>

> <span class="icon">🐸</span>  This guide will help user to test their font locally to confirm quality-assurance. We recommend to test your font on the latest stable version of your OS and apps.

Bear in mind:

-   You can use virtual machines to test your fonts into different environments (practical for testing on older machine and therefore ensure backward compatibility).
-   Installing consecutively different versions of a font family will lead to cache issues. So don’t forget to remove any remaining version of the font, restart the app, open the font menu and quit the app before installing any other version of the font. You may even need to clean the caches and then restart your computer. Another trick would be to append some kind of version number suffix to the family name until final version.
-   If you plan on having both `.otf` and `.ttf` fonts on the same machine, we recommend you use a different name (specifically name ID 1, 4 and 6) to avoid any potential conflict.

</div>

**Table of content**

## Apple macOS

### Installation

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">No conflict during installation (in user fonts folder: `user/Library/Fonts`).</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Fonts appear in Font Book.</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Fonts looks good in Font Book.</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Family names and style manes are displayed correctly.</span>

### Usage in external office apps

*MS Word, Powerpoint, LibreOffice Writer, LibreOffice Impress…*

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Fonts are grouped in menu by family name and all instances appear in weight order.</span>

    → If VF, at least 1 instance appears in dropdown menu (font origin), but since late 2021 version of MS Office (Mac OS 11.\*) all of them should appear.
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Style linking works properly (bold and italic button or regular, italic button for all other cuts)</span>

    → In MS Word, when style linking is absent or not working properly, you will see a fake bold or fake italic, watch carefully for that
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Fonts are displayed correctly</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Kerning works (just display a few kerning pairs to see if it works)</span>

    → In MS Word, kerning is applied to the text *as an option*, it is not a parameter that you activate for all your documents. Find it in the advanced parameters of Fonts settings: you have to check the box and specify a minimum text size to apply kerning (5pt for Mac, and 8pt for Windows)
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Glyphs having special interpolation (rvrn or special layers) are displaying as expected</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Letters with components work</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Combining characters (ligatures, conjuncts) work</span>

### Usage in external layout apps

InDesign, Illustrator, Photoshop (Sketch, Figma, Affinity, CorelDRAW…)

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">All styles appear in weight order in dropdown menu</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Instances are accessible through dropdown menu</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Instances are displayed correctly</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Sliders work properly (try from an upright instance and then with an italic instance)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">No unexpected behavior during variation</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Spacing and kerning work properly when using the sliders</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">All OpenType Features work properly (activation from menu or style)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Stylistic sets have names</span>

**Variable Fonts**

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Composites and glyphs using brace/bracket layers have the same kerning and spacing as base-glyph</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Style linking is working in Adobe Mac apps (shift+cmd+b / shift+cmd+i)</span>

### Usage in native apps

*TextEdit / Pages…*

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Font appear in font dropdown menu, all styles appear in style dropdown menu; default style is first on the list and then in weight order.</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Style linking works properly (cmd+b, cmd+i)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Fonts are displayed correctly</span>

Remember to remove fonts from the user fonts folder at the end of testing.

## Microsoft Windows

### Installation

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">No conflict during installation</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Fonts appear in `C:/Windows/Fonts` folder</span>

Double-click on each style and check if:

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Outline type is correct (PS for .otf, TT for .ttf)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Font is displayed correctly (small size in waterfall)</span>

    → This is actually a good way to quickly check out your hinting.

### Usage in Office apps

*MS Word, Powerpoint, LibreOffice Writer, LibreOffice Impress…*

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Upright fonts appear in alphabetical order in dropdown menu (except for Bold and Italic instances that are activated only the B and I buttons)</span>

    → If VF, at least 1 instance appears in dropdown menu (font origin), but since 2022 version of MS Office (Windows 11) all of them should appear.
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Style linking works properly (bold and italic button or regular, italic button for all other cuts)</span>

    → In MS Word, when style linking is absent or not working properly, you will see a fake bold or fake italic, watch carefully for that
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Fonts are displayed correctly</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Kerning works (just display few kerning pairs to see if it works)</span>

    → In MS Word, kerning is applied to the text *as an option*, it is not a parameter that you activate for all your documents. Find it in the advanced parameters of Fonts settings: you have to check the box and specify a minimum text size to apply kerning (5pt for Mac, and 8pt for Windows)
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Glyphs having special interpolation (rvrn or special layers) are displaying as expected</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Letters with components work</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Combining characters (ligatures, conjuncts) work</span>

## Web Browsers

*Chrome, Firefox, Safari, Edge…*

### All web formats

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Fonts are display correctly</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Fonts have kerning</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Linespacing looks okay (not too lose, not too tight)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">No clipping</span>

### Variable Fonts

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">[Samsa](https://lorp.github.io/samsa/src/samsa-gui.html) displays all instances with propers names in the STAT sidebar section. Regular and other default names are Elided (in parenthesis), and there is style linking between Regular and Bold (400 → 700), and between Roman and Italic (0 → 1)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">AVAR table display the expected result (linear or not)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">FVAR table has the instances you want with proper name and proper coordinates (only weight instances with coordinates every 100 for GF)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Variation works properly (also glyphs with special layers)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Kerning too</span>

## Compatibility

If your fonts of different formats have the same naming, you will have to test formats one by one, restarting the computer between each to avoid cache issues and conflicts. If they have a different naming system, eg. `NameCFF.otf`, `NameTT.ttf`, `NameVF.ttf`, test their compatibility when installed on the same machine.

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">No conflicts during installation</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">All fonts are displayed in the fonts folder with their respective naming</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">They can all be used in the same document, in whatever software, with no trouble</span>

## TrueType Hinting

Manual hinting is often applied from 8ppm to 21ppm. Overshoot suppression until 48-51ppm.

How to prepare hinted rendering to review:

-   Install [gftools-qa](https://github.com/googlefonts/gftools#readme) and look at the image-waterfall output of diffbrowser.
-   Use `gftools gen-html` and upload 2 versions of generated fonts (hinted and unhinted) to look at if the font is better with or without hinting.

What to check:

-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">All glyphs are well aligned: if you see your /r higher than other letter, it is probably because top point is out of the blue zone. So checks where your guidelines normally are (baseline, x-height, caps-height, ascenders, descenders)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Superior and inferiors figures are well aligned too with each other.</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">No overshoot until 48ppm</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Glyphs are aligned also between styles (bold is not higher than Regular at the same ppm size)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">All glyphs of the same set look consistent (there is no glyph better or worse than the other)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Letters are readable</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Weight is equally distributed (horizontally and vertically) in symmetrical letters (`o`, `e`, `g`, `c`)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Spacing is not messed up</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Accents don't clash with letters</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Counter-shapes are not collapsed (`e`, `g`, `ring`)</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Upright and italic of the same weight have a consistent weight</span>
-   <div class="checkbox checkbox-off">

    </div>

    <span class="to-do-children-unchecked">Dots on `i` and `j` are aligned</span>

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
