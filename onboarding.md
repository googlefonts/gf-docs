<div>

# Adding & upgrading fonts to Google Fonts

</div>

> <span class="icon">🐸</span>  Any contribution to Google Fonts should be first submitted through the [google/fonts issue tracker](https://github.com/google/fonts/issues).

Don't forget to search in the issue tracker (using keywords) if your issue has already been raised before opening a new one :) The following links can be used to create different kinds of issues:

-   [Submitting a new OFL Font](https://github.com/google/fonts/issues/new?assignees=&labels=II+New+Font%2C+%3E+Submission&template=1_add-font.md&title=Add+%5BFont+Name%5D)
-   [Submitting an upgrade to an existing font](https://github.com/google/fonts/issues/new?assignees=&labels=II+Font+Upgrade&template=2_update-font.md&title=Update+%5BFont+Name%5D)
-   [Reporting a problem with a font](https://github.com/google/fonts/issues/new?assignees=&labels=II+Font+Bug&template=3_font-bug.md&title=)
-   [Anything else](https://github.com/google/fonts/issues/new?assignees=&labels=II+API+%2F+Website+%2F+Platform%2C+II+Tools+%2F+workflow+%2F+repo&template=4_anything-else.md&title=)

From time to time, Google Fonts provides financial and design assistance for projects. If you would like to discuss this, please mention that you would like someone to contact you privately when filing an issue (and have contact details on your Github profile page.)

</div>

**Table of content**

## New fonts

If you would like to include a new font family into the GF collection, we'll be happy to include it if it meets the following criteria:

-   **The typeface design must be original, or a legitimate revival of a design in the public domain, and of good quality.**

    The Google Design team curates the overall Google Fonts collection and decides if fonts are of good quality. GF may reject families if they fail to meet their criteria. You can get general reviews of your project from the wider international type community during development by posting review requests in the [googlefonts-discuss](https://groups.google.com/forum/#!forum/googlefonts-discuss) group, and the [typedrawers](http://typedrawers.com/categories/critiques%E2%80%94type-design) review forum.
-   **The project must be wholly licensed under the** **[SIL Open Font License v1.1](http://scripts.sil.org/OFL).**

    There must also be no proprietary/restricted-license versions of the project available elsewhere (such as additional weights/styles.)
-   **The Open Font License should not have any Reserved Font Names ([why](https://github.com/simoncozens/silson/issues/1)).**
-   **The copyright holders must all have filled in the** **[Google Contributor's License Agreement](https://cla.developers.google.com/)** **forms.**
-   **The font family name should not include any copyright holder's full names.**

    First names are accepted, though. No registered trademarks, no initials or abbreviations, no references to languages or writing systems, and no cultural reference that may be offensive in any way. Use only ASCII alphanumeric characters in the family name and begin with an alphabet character, no dashes nor diacritics. Aim for a simple and unique name, ideally short and easy to remember. Long names can be harder for people to remember and type correctly and problematic for software with name length limitations.

    CamelCase names are not allowed except in some cases discussed and approved by a Google Fonts team member.

    If you are making a libre version of your prior proprietary font or designing something in an established genre, add "Libre" or a local equivalent to that well-known name E.g., *Vesper Libre* or *Libre Baskerville.*

    A limited but easy way to test for uniqueness is [namecheck.fontdata.com](https://namecheck.fontdata.com/) along with a general web search for *name* + font.
-   **The project must be developed on GitHub or similar platform.**

    A VCS open to public participation and actively maintained. Please read our [Github guide](hosting.md).
-   **The source files are available** in your preferred font editor format.

    The file formats most used are `UFO`, `.glyphs`, `fontforge` or `fontlab 7`. `Fontlab V` files must be converted to another format because the software runs only on older OS versions. GF builds fonts using [Fontmake](https://github.com/googlefonts/fontmake), which can generate binaries from `UFO`. Fontmake can also convert `.glyphs` files to UFO, but if your are using any other font format, your build process should contain a step that converts the sources to UFO. Read the chapter about [building fonts](build.md) to know more about the build process.python
-   **The build should follow the** [**Scalable Font Production**](production.md) **principle.**
-   **All binary font files must be available in TTF format.**
-   **All font files should support, at least, the** [**"GF Latin Core"**](https://github.com/googlefonts/glyphsets/tree/main/GF_glyphsets/Latin) **glyph set.**
-   **All font files should follow the** **[Overall font files requirements](requirements.md).**
-   **All font files should pass the** **[Font Bakery](https://github.com/googlefonts/fontbakery)** **checks for the** **[googlefonts profile](https://font-bakery.readthedocs.io/en/stable/fontbakery/profiles/googlefonts.html).**

    Under special circumstances, you can request an exception to these requirements.

## Font upgrades

Remember that, following the informations given in the [production requirements](production.md), the fonts used on websites via HTTP request to Google Fonts are served from the actual fonts contained in the API. In fact, GF contains more than a thousand fonts, and serves them to billions of websites. A very important detail to remember is that GF *does not* serve more than one version of the same font. This means that once a font is upgraded and in production, the *upgrade is served everywhere*.

To make sure users are correctly served the upgraded font:

-   **The family name and style names should be the same.**
-   **The version number should be incremented from the previous version** following the [specified criteria](requirements.md) for it.
-   **We must avoid visual regression between the new version and the previous version**:
    -   No previously encoded glyphs should be removed.

    

    -   No previously served styles/instances should be removed.

    

    -   **The visual thickness and width of the glyphs must be the same.**

        Visual weight and width of a font influence the overall “grey” of a paragraph and change the line length. Users get very angry when the weight/width of a style has changed.
-   **The line length must be** ***kind of*** **the same.**

    The font spacing can be improved whenever needed, but upgrades must not create an obvious change in line length or significant reflow of text for end users.
-   **The interline space must be the same.**

    The vertical metrics must be the same so that the line spacing has the same visual appearance to end-users.
-   **The rendering should be of the same quality.**

    This means that the hinting should match as closely as possible. Manual hinting programs from previous versions should be re-applied to the new binaries. More information about that matter is given in the [Static font requirements](statics.md), and in the [Variable font requirements](variable.md).
-   **Contributions from forks are not accepted.**

    We need to make sure that the original author of the font has agreed with the upgrade, therefore:

    -   The modification must be merged with updated contributors and authors in the upstream project's repository.

    

    -   The modification must be made to the existing sources.

All of these requirements are to be navigated with the [statistics](https://fonts.google.com/fonts/stats?key=WebFonts2010) of use in mind; exceptions to compatibility requirements can be made for fonts that are not heavily served.

If an upgrade is too much of a change, we can consider onboarding it as *a new font with a different family name.* We then decide if the old versions remain visible on the catalogue, and/or whether to make the old version unavailable for new users. This allows websites to be served with the old version that they already use, while new requests would get the upgraded versions.

Since all the fonts available are licensed with permission to redistribute subject to the license terms, if you want to have more control over the version of the font you use you can self-host the font using a variety of third-party projects.

## Designer Profile

Each credited entity on Google Fonts should have a registered profile in [google/fonts/catalog/designers](https://github.com/google/fonts/tree/main/catalog/designers). This profile appears in the [about](https://fonts.google.com/specimen/Praise?sort=date#about) section of the specimen page.

You can request the addition or modification of your name, bio, and image using **[this form](https://docs.google.com/forms/d/e/1FAIpQLSeMwHN8J213ZaxHrr5lHCrX56HY_NjGrWB8o604g98YxuMrdA/viewform)**.

You can find more about the technical aspect of adding a profile to google/fonts repo by reading the [Designer Profile chapter](profile.md).

</div>
