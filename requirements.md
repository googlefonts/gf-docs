# Overall font files requirements

> <span class="icon">🦥</span>  The following guidelines apply to all fonts, regardless of their format.
Then, depending on the format, we have different specifications for static and variable fonts. Please [read the guidelines for static fonts](statics.md) and the [guidelines for variable fonts](variable.md).
It is recommended to read [the guidelines to add or upgrade font in Google Fonts](onboarding.md) before continuing.

## Font copyright and license

These font info parameters are not optional and should follow the same scheme within the entire GF library.

-   **The font must contain a copyright string within the name table** with the following format:

    ``` code
       Copyright { year } The { family } Project Authors ({ git_url })
    ```

    E.g. Copyright 2011 The Montserrat Project Authors (<https://github.com/JulietaUla/Montserrat>)

    If you are using the Glyphs font editor, add a “Copyright” entry under the “Font” tab of the Font Info panel.
-   **The first line of the** **[OFL.txt](license.md)** **file should be identical to the font copyright string** **detailed above**.
-   **The license string must be the same for all GF font projects:**

    ``` code
    This Font Software is licensed under the SIL Open Font License, Version 1.1. This license is available with a FAQ at: https://scripts.sil.org/OFL
    ```

    If you are using the Glyphs font editor, add this string to a “License” entry in the “Font” tab of the Font Info panel.
-   **The license URL must be the same for all GF fonts projects:**

    ``` code
    https://scripts.sil.org/OFL
    ```

    If you are using the Glyphs font editor, add this string to a “License URL” entry in the “Font” tab of the Font Info panel.

## Trademarks

Typically libre fonts are not subject to any trademarks.

**If you do not trademark your project name:**

-   Do not declare trademarks in font info metadata.

**If you do trademark your project name:**

-   Declare trademarks in font info metadata.
-   License your trademarks for redistribution in a `TRADEMARKS.md` file.

    Example:

    ``` code
    Font Name is a trademark of Company Name.
    ```
-   Explicitly permit Google to use the trademarks. Email <fonts@google.com> with an email like this:

    > *Dear Google Fonts*
    >
    > *We would like our font project "Font Family Name" to be included in Google Fonts and other Google products.*
    >
    > *I hereby grant permission in perpetuity to Google LLC and affiliates to use the following trademarks, and Reserved Font Names declared in the SIL Open Font License notices, for the following font family names:*
    >
    > *Font Family Name Font Family Name Mono Font Family Name Sans*
    >
    > *Best regards,*
    >
    > *Firstname Othername*
    >
    > *Job Title, Organization*

## Font versioning

Every new version onboarded to GF should have an increased version number compared to the precedent. This is explained in the [Main contribution cases](onboarding.md).

Versioning is based on [semver](https://semver.org/), apart from we use `MAJOR.SIGNIFICANTMINORPATCH`, instead of `MAJOR.MINOR.PATCH`.

**Examples:**

If a breaking change is made e.g. converting a static font family to a variable font family, the MAJOR must be incremented by 1, and the others reset, e.g.:

Current `1.230`, new `2.000`

If a new character set is inserted, SIGNIFICANT should be incremented, e.g.:

Current `1.230`, new `1.330`

If a few new glyphs are added, MINOR should be incremented, e.g.:

Current `1.230`, new `1.240`

If a name table record is updated such as the copyright string, PATCH should be incremented, e.g.:

Current `1.230`, new `1.231`

## Font Embedding (fsType)

[fsType](https://docs.microsoft.com/en-us/typography/opentype/spec/os2#fstype) parameter should be set to `0` (Installable embedding).

This is how it should look like in the OS/2 table: `<fsType value="00000000 00000000"/>`

If you are using the Glyphs font editor, create a new custom parameter called “fsType” in the “Font” tab of the Font Info pane. Change the Embedding drop-down to “Installable” and leave the “Subsetting Forbidden” checkbox unchecked.

## Font Vertical Metrics

Please read the [following pages about vertical metrics](metrics.md) for setting vertical metrics.

## Monospace fonts

We require the post table `isFixedPitch` to be set and the OS/2 `panose` table to have `OS/2.panose.bProportion` (bit 4) set correctly. If either of these is set incorrectly, users may get fallback glyphs that are not monospaced if they type a character that doesn't exist in the font.

-   Set `post.isFixedPitch` to 1
-   If `OS/2.panose.bFamilyType` is 2 (Latin Text), set `OS/2.panose.bProportion` to 9.
-   If `OS/2.panose.bFamilyType` is 3 (Latin Script), set `OS/2.panose.bProportion` to 3.
-   If `OS/2.panose.bFamilyType` is 5 (Latin Picture), set `OS/2.panose.bProportion` to 3.
-   If you are unsure what to set `OS/2.panose.bFamilyType` to, use 2 for "normal" fonts.
-   If `OS/2.panose.bFamilyType` is 4, you do not need to worry about `OS/2.panose.bProportion`.

Developers can set these automatically by using the following gftools command: `gftools fix-isfixedpitch`

## Glyphsets

[GF Glyphsets](https://github.com/googlefonts/glyphsets/tree/main/GF_glyphsets) provides the glyph set definition standards that Google Fonts fonts must adhere to.

The structure of these sets is based on a modular scheme that allows the use of different blocks of information to be combined to build sets of glyphs with different levels of complexity according to the needs of each project.

This system aims to give enough flexibility to define the intended scope of each project as well as a way to better assess the font development status and quality analysis.

Currently, the most used ones are:

-   [**GF Latin Kernel**](https://github.com/googlefonts/glyphsets/tree/main/GF_glyphsets/Latin/latin-kernel) is the minimum Latin set required to be included within fonts targeting non-latin scripts users. Since it matches the ASCII set, it only includes full support for the English language.
-   [**GF Latin Core**](https://github.com/googlefonts/glyphsets/tree/main/GF_glyphsets/Latin/latin-core) is the minimum set required to be included within any font family that addresses Latin based languages (*be it an open contribution or a commissioned font*). It includes the Latin Kernel plus additional glyphs to support the most widely used languages, including those encompassing Central and Western Latin based languages, among \~200 others.
-   [**GF Latin Plus**](https://github.com/googlefonts/glyphsets/tree/main/GF_glyphsets/Latin/latin-plus) includes additional numerals sets (like numerators, denominators, inferior and superior), expanded math and currency symbols, as well as arrows and bullets in use in Google Docs.
-   [**Latin Vietnamese**](https://github.com/googlefonts/glyphsets/tree/main/GF_glyphsets/Latin/latin-vietnamese) includes the extended marks and combined letters required to support the Vietnamese language. It requires to be combined with Latin Core for complete Latin + Vietnamese support.

Find all the glyphsets definition and filter lists in the [Glyphsets repository](https://github.com/googlefonts/glyphsets/tree/main/GF_glyphsets). Be aware that these glyphsets are still a work in progress and any advise or recommendation can be submitted using the [Glyphsets’ issue tracker](https://github.com/googlefonts/glyphsets/issues).

## Stylistic Sets

The Google Fonts API currently does not support the inclusion of OpenType *Stylistic Set* features. Fonts that absolutely need them need to be published as a separate family with the stylistic feature added to the family name.
