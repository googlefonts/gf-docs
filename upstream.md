<div>

# Upstream repository structure

</div>

> <span class="icon">🐰</span>  Font projects must be hosted on GitHub (or another VCS), and the repositories must be public. Google Fonts accepts private repositories whilst the project is still in progress projects are private, but they must be public once completed.

This guide will help users understand what and why directories, files, and documents are needed in a Google Fonts project.

Before starting this reading, make sure that:

-   [You have become familiar with Libre Font culture](culture.md)
-   [You already know how to use Github](hosting.md)
-   [You have installed all the required tools](tools.md)

</div>

**Table of content**

## The Google Fonts Project Template repo

If you read this before you have created your project Github repo, you would like to use the [Google Fonts project template](https://github.com/googlefonts/googlefontsproject-template) repo to start with everything set up for you.

The template is based on [Raphael Bastide’s UFR](https://github.com/unified-font-repository/Unified-Font-Repository), and was adapted to meet Google Fonts' needs. Its only purpose is to help type designers set up their repo of open-source fonts — especially if they want to publish them on Google Fonts. A unified structure throughout all the repositories helps GF to automate the fonts' quality assurance and onboarding processes into the catalog.

But there is more: the project template incorporates [GitHub Actions](https://docs.github.com/en/actions) to provide users with many automation.

-   The actions will build the font files from the source, use Fontbakery for the Quality Analysis test of the fonts, generate HTML proof sheets, publish them with the test results to HTML files, and generate an *artifact* containing all the files that it has built.
-   You can download the latest artifact (produced fonts) by visiting the Actions tab of your repository.

This is particularly practical if you don’t want to run [gftools](https://github.com/googlefonts/gftools) by yourself: your GitHub repo is doing it for you! The downside is that it is harder to customize for GitHub beginners or people who don’t want to get their hands dirty in some code, and so maybe harder to use for a project that doesn’t follow this exact template.

But give it a try :) Simon Cozens has made a [1 minute video](https://twitter.com/simoncozens/status/1405267459028905984) to show how quick this way to start is.

## The essentials explained

Be aware that the scripts and automated actions provided by the Google Fonts project template are not mandatory, although your font repo still must follow certain requirements.

[Texturina](https://github.com/Omnibus-Type/Texturina) is a good example of a simple repo that only contains the essentials.

``` code
├── AUTHORS.txt
├── CONTRIBUTORS.txt
├── OFL.txt
├── README.md
├── documentation
│   ├── readme-images.jpg
│   └── promo.zip
├── fonts
│   ├── otf
│   │   └── FontFamily-Regular.otf
│   ├── ttf
│   │   └── FontFamily-Regular.ttf
│   ├── webfonts
│   │   └── FontFamily-Regular.woff2
│   └── variable
│       └── FontFamily-[wdth,wght].ttf
├── sources
│   ├── FontFamily.ext
│   ├── FontFamily-Italic.ext
│   └── config.yaml and/or build.sh
├── requirements.txt
└── .gitignore
```

Each file or dir has the following purpose:

*An example is provided for each file (from this Guide or other repositories). Please use these templates and modify what you need.*

-   [AUTHORS.txt](authors.md)

    Includes contact information for the project's authors. Contributors must not be included in this file.
-   [CONTRIBUTORS.txt](authors.md)

    Includes contact information for the project's contributors.
-   [OFL.txt](https://www.notion.so/0a589f36247844b98dd11b8f2635ed0c)

    The OFL license file. The first line of the license file must contain the font family's copyright string.
-   [README.md](readme.md)

    Contains information about the font family and instructions on how to build the family. You should take particular care over this file, and you also must add at least one image and a short description of your font project.
-   **[documentation](https://github.com/googlefonts/Unified-Font-Repository/tree/main/documentation)**

    A directory that contains expanded information about the Family. You can eventually store in it your PDF specimen, screenshots or process definition, the pictures you use for the README.md, and [**promo**](marketing.md)[**tional assets**](marketing.md) for twitter.
-   **[sources](https://github.com/Omnibus-Type/Texturina/tree/master/sources)**

    A directory containing the design source files and scripts used to build the fonts. Sources must not be kept in another directory.

    There must be either a `config.yaml` or `build.sh` file that allows building the fonts in one command.

    -   **[config.yaml](https://github.com/googlefonts/Unified-Font-Repository/blob/main/sources/config.yaml)**

        A configuration file that includes all the relevant information of a project for the Builder to build the font files.

    

    -   **[build.sh](https://github.com/googlefonts/lexend/blob/main/sources/build.sh)**

        A Bash script to build the fonts in one command if the build process requires more than the single config.yaml file to build the font families of this repo.
-   [**fonts**](requirements.md)

    A directory containing font binaries or subdirectories for each font format. If your project provides multiple formats, do not include them all in one folder. Create a folder for each format e.g `fonts/otf`, `fonts/ttf`, `fonts/webfonts`. The [Builder](build.md) told does that by default.
-   **[requirements.txt](https://github.com/googlefonts/Unified-Font-Repository/blob/main/requirements.txt)**

    File listing the python packages (and their version if necessary) used for a project, so that any user can install easily the necessary packages and replicate the production process.
-   **[.gitignore](https://github.com/googlefonts/Unified-Font-Repository/blob/main/.gitignore)**

    File specifying untracked files that Git should ignore. Since [the tools](tools.md) should be installed under a virtual environment dedicated to this repository, the `.gitignore` should include the env (or the name of your virtual environment you are using, for example, `venv` or `env`). Indeed it is better not to push your virtual environment to Github and keep it local. To keep collaboration between Mac and Windows users, you can add `.DS_Store` to the list of untracked files. If you use `.glyphs` sources, `*(Autosave)*` and is also a relevant addition.
-   Releases should be tagged; [Montserrat does this well](https://github.com/JulietaUla/Montserrat/releases).

The files and directories listed above are mandatory. However, we don't mind if you include further doc and dirs, but they should have a clear purpose (such as a `scripts` directory for example).

------------------------------------------------------------------------

## Useful links

-   [Github release explained](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)
-   [How to use requirements.txt files](https://pip.pypa.io/en/stable/user_guide/#requirements-files)

</div>
