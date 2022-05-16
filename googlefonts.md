# google/fonts repository explained
{:.no_toc}

> <span class="icon">🦉</span>  [google/fonts](https://github.com/google/fonts) is the GitHub repository that is used as a staging area to upload font families to [Google Fonts](https://fonts.google.com/). 
> The first step to contributing your font to Google Fonts is to submit your contribution as a Pull Request to google/fonts.
> This section will help users understand which are the directories, files, and python modules included in the Google/Fonts repository and how they are related.

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## google/fonts repository explained

### Repository structure

``` code
.
├── AUTHORS
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── CONTRIBUTORS
├── README.md
├── TRIVIA.md
├── apache
├── axisregistry
├── catalog
├── knowledge
├── lang
├── ofl
├── ufl
├── to_production.txt
└── to_sandbox.txt
```

### Family directories

The `ofl`, `ufl` and `apache` directories contain font families. There is a directory per family published by GF and each directory has the following structure:

``` code
.
├── DESCRIPTION.en_us.html
├── METADATA.pb
├── License (OFL.txt, UFL.txt, License.txt)
├── FontFamily-Regular.ttf
└── upstream.yaml
```

Each file has the following purpose:

-   [DESCRIPTION.en_us.html](description.md): describes the font family
-   [METADATA.pb](metadata.md): contains metadata related to the family
-   [License](license.md): License for the font family. Valid choices are OFL.txt, UFL.txt, License.txt. If you're unsure what license to use, we recommend OFL.txt
-   [.ttf](requirements.md): Family font files.
-   [upstream.yaml](package.md): file linking the font files with the upstream. It is used by the [Packager](package.md) (our onbaording tool) to facilitate the font upgrading process.

If the family is a variable font family, another directory called `static` can be included to contain the static (non-variable) fonts for the family:

``` code
.
├── DESCRIPTION.en_us.html
├── METADATA.pb
├── License (OFL.txt, UFL.txt, License.txt)
├── FontFamily[axis].ttf
├── static
│   ├── FontFamily-Regular.ttf
│       └── FontFamily-Bold.ttf
└── upstream.yaml
```

This static directory is mandatory *if the static fonts are manually hinted;* otherwise, it should not be added at all.

### Designers catalog

``` code
.
├── info.pb
├── bio.html
└── image.png
```

Each credited entity on Google Fonts should have a registered profile in [google/fonts/catalog/designers](https://github.com/google/fonts/tree/main/catalog/designers). This profile appears in the [about](https://fonts.google.com/specimen/Praise?sort=date#about) section of the specimen page.

You can request the addition or modification of your name, bio, and image using [this form](https://docs.google.com/forms/d/e/1FAIpQLSeMwHN8J213ZaxHrr5lHCrX56HY_NjGrWB8o604g98YxuMrdA/viewform).

Find more information about the requirements for these files in [the designer profile chapter](profile.md).

### Axis registry

Google Fonts supports all the [Microsoft registered axes](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg) for variable fonts, but it has its own [Axis Registry](https://github.com/googlefonts/axisregistry), which defines the names and ranges of additional axes supported by the API. This registry is used to generate the static instances of each variable family (which you can find in the downloadable zip file); the API will generate only those locations registered in the registry.

### Lang directory

This python module provides the API with data about [languages](https://github.com/felipesanches/gflanguages/tree/main/Lib/gflanguages/data/languages)/[regions](https://github.com/felipesanches/gflanguages/tree/main/Lib/gflanguages/data/regions)/[scripts](https://github.com/felipesanches/gflanguages/tree/main/Lib/gflanguages/data/scripts) for use in the language-support categorization of the font families in the Google Fonts collection.

As with the axis registry, [the Lang directory](https://github.com/googlefonts/lang) also has its own repository, and all issues related to language data should be opened there.

### Push lists

-   `to_sandbox.txt` is a list of font directories or designer directories to be pushed to sandbox.
-   `to_production.txt` is a list of fonts directories or designer directories to be pushed to production. Once the elements (fonts, bio, etc) have been checked and validated in sandbox, they can be sent to the API so users can have access to them. We can only push to production something that was first pushed to sandbox.
