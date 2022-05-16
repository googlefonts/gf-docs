<div>

# Static fonts specifics

</div>

> <span class="icon">🐓</span>  “Static” fonts is a way of saying traditional, *non-variable* fonts.

Before going further, make sure you read carefully [the documentation common to any font format](requirements.md). And please refer to the [requirements about Variable Fonts](variable.md) if you are developping a VF.

Note that GF only onboards OTF-TTF files: `.ttf` — so TrueType fonts only! The upstream repo can of course contain OTF-CFF `.otf` fonts, as well as webfonts `.woff2`. GF redirects users to the upstream repo to find these files if they are not satisfied with the one served by the API.

Even if the statics are available in the upstream repository, GF may not onboard them:

-   If a VF exists and the statics are autohinted, then only the variable font is onboarded. The API will generate statics fonts by instanciating the VF: they will be served to browsers which doesn’t support the variable font technology, and they will be available in a downloadable zip file (`download family` button in any specimen pages).
-   If a VF exists and the statics are manually hinted, then both formats are onboarded.
-   If there is no VF, then the statics available upstream will be onboarded.

</div>

**Table of content**

## Supported Styles

Google’s static fonts API supports up to 18 styles in one family: up to 9 weights (Thin–Black), + their matching Italics. The table below lists each style’s specific name table and bit settings.

`fontmake` doesn’t produce Mac names entries any more. If you must add the name for platform 1 (Mac), make sure they are the same as the one in Platform 3 (Windows).

| Filename                        | Family Name (ID 1, Win) | Subfamily Name (ID 2, Win) | Typographic Family Name (ID 16) | Typo Subfamily Name (ID 17) | OS/2 usWeightClass | OS/2 fsSelection | head macStyle |
|---------------------------------|-------------------------|----------------------------|---------------------------------|-----------------------------|--------------------|------------------|---------------|
| FamilyName-Thin.ttf             | Family Name Thin        | Regular                    | Family Name                     | Thin                        | 100                | bit 6            |               |
| FamilyName-ExtraLight.ttf       | Family Name ExtraLight  | Regular                    | Family Name                     | ExtraLight                  | 200                | bit 6            |               |
| FamilyName-Light.ttf            | Family Name Light       | Regular                    | Family Name                     | Light                       | 300                | bit 6            |               |
| FamilyName-Regular.ttf          | Family Name             | Regular                    |                                 |                             | 400                | bit 6            |               |
| FamilyName-Medium.ttf           | Family Name Medium      | Regular                    | Family Name                     | Medium                      | 500                | bit 6            |               |
| FamilyName-SemiBold.ttf         | Family Name SemiBold    | Regular                    | Family Name                     | SemiBold                    | 600                | bit 6            |               |
| FamilyName-Bold.ttf             | Family Name             | Bold                       |                                 |                             | 700                | bit 5            | bit 0         |
| FamilyName-ExtraBold.ttf        | Family Name ExtraBold   | Regular                    | Family Name                     | ExtraBold                   | 800                | bit 6            |               |
| FamilyName-Black.ttf            | Family Name Black       | Regular                    | Family Name                     | Black                       | 900                | bit 6            |               |
| FamilyName-ThinItalic.ttf       | Family Name Thin        | Italic                     | Family Name                     | Thin Italic                 | 100                | bit 0            | bit 1         |
| FamilyName-ExtraLightItalic.ttf | Family Name ExtraLight  | Italic                     | Family Name                     | ExtraLight Italic           | 200                | bit 0            | bit 1         |
| FamilyName-LightItalic.ttf      | Family Name Light       | Italic                     | Family Name                     | Light Italic                | 300                | bit 0            | bit 1         |
| FamilyName-Italic.ttf           | Family Name             | Italic                     |                                 |                             | 400                | bit 0            | bit 1         |
| FamilyName-MediumItalic.ttf     | Family Name Medium      | Italic                     | Family Name                     | Medium Italic               | 500                | bit 0            | bit 1         |
| FamilyName-SemiBoldItalic.ttf   | Family Name SemiBold    | Italic                     | Family Name                     | SemiBold Italic             | 600                | bit 0            | bit 1         |
| FamilyName-BoldItalic.ttf       | Family Name             | Bold Italic                |                                 |                             | 700                | bit 5 + bit 0    | bit 0 + bit 1 |
| FamilyName-ExtraBoldItalic.ttf  | Family Name ExtraBold   | Italic                     | Family Name                     | ExtraBold Italic            | 800                | bit 0            | bit 1         |
| FamilyName-BlackItalic.ttf      | Family Name Black       | Italic                     | Family Name                     | Black Italic                | 900                | bit 0            | bit 1         |

If the style name matches the RIBBI convention (ie. `ID 2 = ID 17`), then `name IDs 16/17` are not exported.

In Glyphs.app, the `Family Name` in font info (or the `Localised Family Name` in the instance), and the `Style Name` fields are meant to generate the `name ID 16/17`, or `name ID 1/2` if the naming matches RIBBI convention. Although, the export tool can guess it right only if you set the style linking bits correctly as explained below.

Note for OTF-CFF fonts:

Some fonts with a CSS `font-weight` property of 100 or 200 then the `usWeightClass` value may be 250, as values of 249 or less in CFF fonts suffered from blurry rendering on older versions of Windows — but in 2020 this is no longer necessary.

## Style linking

As mentioned above, we strictly follow the RIBBI convention for nameID2 (such as required in the OpenType spec), to allow functional style linking in most environments (button Bold and Italic in desktop apps for example). This means that you can’t have another style name than Regular, Italic, Bold, Bold Italic in `name ID 2` (for any platform). Other style name should be appended to `name ID 1`. The “real” font family name that is impacting how a family is grouped in font menu is handles by the `name ID 16` and the “real” style names are in `name ID 17`.

In Glyphs.app, the `Style Name` field in the set instances will be the one used for the `name ID 17`. The `name ID 2` will be set according to the style linking bits and if the style name matches RIBBI. So don’t forget to tick the proper cases: `This instance is the [ ] Bold, [ ] Italic of: ___________`. You can leave the last field blank which suggests “Regular”.

**Regular**

In Glyphs.app: `This instance is the [ ] Bold, [ ] Italic of: ___________`

OS/2 table: `<fsSelection value="00000000 01000000"/>`

head table: `<macStyle value="00000000 00000000"/>`

**Italic**

In Glyphs.app: `This instance is the [ ] Bold, [X] Italic of: ___________`

OS/2 table: `<fsSelection value="00000000 00000001"/>`

head table: `<macStyle value="00000000 00000010"/>`

**Bold**

In Glyphs.app: `This instance is the [X] Bold, [ ] Italic of: ___________`

OS/2 table: `<fsSelection value="00000000 00100000"/>`

head table: `<macStyle value="00000000 00000001"/>`

**Bold Italic**

In Glyphs.app: `This instance is the [X] Bold, [X] Italic of: ___________`

OS/2 table: `<fsSelection value="00000000 00100001"/>`

head table: `<macStyle value="00000000 00000011"/>`

## Unsupported styles

If a family has styles which are not in the above table, they should be released as a separate/new family. To do this, append any unsupported style (e.g Condensed) to the family name, so it becomes part of the family name, rather than part of the style name. We frequently use this approach for [Condensed](https://fonts.google.com/?query=condensed) and [smallcap](https://fonts.google.com/?query=sc) sibling families. This way, we never have to use `name IDs 21/22` for the WWS convention.

For projects which use Glyphs.app, you can follow the example of [Archivo](https://github.com/Omnibus-Type/Archivo) which contains glyphs files that are set correctly. An additional field `Localised Family Name` should be added in all concerned instances in order to append the non supported style to the family name and override the one in font info.

Example:

`Localized Family Name: Archivo Condensed`

`Style Name: Light Italic`

## Static font filenames

Font filenames must be based on the following schema:

`FamilyName-Style.ttf` e.g `Montserrat-Regular.ttf`

The filename must not contain anything else.

Remember Google Fonts only allows weight styles, and doesn’t even follow the WWS scheme in the sense that width styles are forbidden and must be part of the family name of the font family:

`FamilyNameWidth-Style.ttf` e.g `ArchivoExpanded-Regular.ttf`

Same for optical size or any other attribute.

## Single Weight families

If a family is a single weight and it visually doesn't have the appearance of a Regular weight, "One" must be appended to the family name and “Regular” used for the style name, since any family must contain a Regular.

This approach allows us to keep the desired font name available if we decide to add more styles in the future: if a future extension of a previously single-weight font includes a Regular, the family name without “One” is used and the “Regular” style name can be given to the new actual Regular weight.

We have released many of these [families](https://fonts.google.com/?query=one) in the past.

The single weight families must have the following font specific settings:

| Filename                  | Family Name (nameID 1) | Subfamily Name (nameID 2) | Typographic Family Name (nameID 16) | Typo Subfamily Name (nameID 17) | OS/2.usWeightClass | OS/2.fsSelection | hhea.macStyle |
|---------------------------|------------------------|---------------------------|-------------------------------------|---------------------------------|--------------------|------------------|---------------|
| FamilyNameOne-Regular.ttf | Family Name One        | Regular                   |                                     |                                 | 400                | bit 6            |               |

## Hinting

Static fonts should be hinted using the latest version of [ttfautohint](https://www.freetype.org/ttfautohint/). If the results look poor on Windows browsers, it's better to release the fonts unhinted with GASP table set to "grayscale / symmetric smoothing" (0x000A) across the full PPEM range. `ttfautohint` often struggles to hint display or handwritten typefaces.

If you don’t use [gftools builder](build.md) (which autohint static fonts by default but you can turn off that option), you should run the fonts through `gftools fix-hinting` once the fonts have been hinted. If the fonts are unhinted, run the fonts through `gftools fix-nonhinting`.

Fontmake does not support manual hinting from Glyphs. You can use use [VTT](https://docs.microsoft.com/en-us/typography/tools/vtt/) instead and you can patch a VTT program with [gftools builder](package.md) — see [Montserrat](https://github.com/googlefonts/Montserrat/tree/master/sources) as an example.

------------------------------------------------------------------------

## Useful links

-   [OpenType Spec about the name table](https://docs.microsoft.com/en-us/typography/opentype/spec/name)
-   [Glyphs.app naming tutorial](https://glyphsapp.com/learn/naming)

<div>

**You can view the name tables using these tools:**

-   [Font Table Viewer](https://glyphsapp.com/tools/fonttableviewer)
-   [DTL OT Master](https://www.fontmaster.nl/otmaster.html)
-   [ttx](https://fonttools.readthedocs.io/en/latest/ttx.html), a practical command line tool of [fonttools](https://github.com/fonttools/fonttools).

**Some font testing web pages allow you to view a selection of tables:**

-   <https://fontdrop.info/#/> → in the “data” tab
-   [https://fontgauntlet.com](https://fontgauntlet.com/) → if you click on the small search icon next to the font name

</div>

</div>
