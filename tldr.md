# Google Fonts Guide TL;DR

> <span class="icon">🦉</span>  This document aims to specify all the requirements to contribute to Google Fonts. It ranges from the general knowledge required to contextualize the what and why of some of the requirements and the specifics regarding technical aspects with some suggestions on how to comply with them. Therefore, it covers different levels of information for both newcomers and more experienced contributors. If you are already familiar with some of the concepts, please feel free to jump to the other bits that you may be looking for.

## Introduction

-   **Libre Fonts Culture**

    You are contributing to an open-source based platform. It’s important for you to get familiar at least with the basics about [Libre Fonts Culture](culture.md)
-   **Typography & Fonts**

    Google Fonts expect font developers to understand the following:

    1.  Overall type design knowledge.
    2.  Basic understanding of how [fonts](https://simoncozens.github.io/fonts-and-layout/) and [OpenType Specification](https://docs.microsoft.com/en-us/typography/opentype/spec/) works (skim read! focus on what each table does).
    3.  Proficiency in a fully featured font editor such as [Fontlab 7](https://www.fontlab.com/font-editor/fontlab/), [Glyphsapp](https://glyphsapp.com/), [Robofont](https://robofont.com/), or [Fontforge](https://fontforge.org/en-US/); not a toy editor like a "handwriting page scan to font" tool fix.
-   **Tools & Dependencies needed**
    -   [Setting up a working environment](tools.md)
        Includes:

        1.  Shell and Command-line
        2.  Homebrew
        3.  Python 3
        4.  Virtual environments

    -   [Installing the required tools](tools.md)
        Includes:

        1.  Fontbakery
        2.  Google Fonts Tools (known as gftools)
        3.  gftools qa
        4.  The `bash_profile` file

-   **GitHub the required Version Control System (VCS)**

    Since we only release Open Source fonts, we expect projects to be kept in a VSC like [GitHub](hosting.md). Every family we release must have its own upstream GitHub repository (or similar).

    -   [Hosting projects on Github](hosting.md)
        1.  GitHub Culture
        2.  Account
        3.  Authentication
        4.  Software to interact with GH
        5.  Workflow
            1.  Repositories
            2.  Commits
            3.  Pulling and pushing
            4.  Pull Request
            5.  Issues
            6.  Actions
    -   [Upstream Repo Structure required](upstream.md)
        1.  Google Fonts Template Repository
            Files & actions included
        2.  Essential files required explanation
            1.  Authors
            2.  Contributors
            3.  OFL
            4.  Readme
            5.  Documentation
                1.  Promotional assets
            6.  Sources
                1.  design sources
                2.  `config.yaml`
                3.  build.sh
            7.  Fonts
            8.  Requirements.txt
            9.  .gitignore
            10. Tagged releases
    -   [Google Fonts repo structure explained](production.md)

        (currently under Contributing to Google Fonts)

        1.  Repo structure
        2.  Families directories
        3.  Designers Catalog
        4.  Axis Registry
        5.  Lang directory
        6.  Push Lists

## Production Requirements

-   [Context: fonts are massively available](production.md)

    Includes

    1.  Analytics (usage numbers scale)
    2.  API (to improve)
-   [Scalable font production](production.md)
    1.  Source files must be available (currently on new fonts)
    2.  Must Open-source tools
    3.  One step
    4.  Repeatable builds
    5.  VCS - Lint to Github content
    6.  CI
-   **QA assurance** (TO DO)
    1.  Early inclusion of Fontbakery tests
    2.  Issues/Fails must be fixed
-   **Tools usage** (details TO DO)
    1.  Builder
        1.  Fontmake
        2.  gftools (bin)
    2.  Fontbakery
    3.  Packager

## Fonts Requirements

-   [New fonts](onboarding.md)

    Includes:

    1.  Originality
    2.  OFL license
    3.  No RFN
    4.  CLA
    5.  Font family name conditions
    6.  Minimum Glyphsets required
    7.  New fonts VM
    8.  Following the Overall font files requirements
    9.  Following the Production Requirements
-   [Fonts Upgrades](onboarding.md)
    1.  matching family + stylename
    2.  Version number increased
    3.  No visual regressions
        1.  matching encoded glyphs
        2.  same instances included
        3.  same glyphs visual thickness + width
    4.  Line length equivalence
    5.  Line height (interline) equivalence - Link to upgrading fonts VM
    6.  Same render quality (manual hinting re-applied)
    7.  No contributions from forks
-   [Overall fonts files requirements](requirements.md)
    1.  binaries must be in TTF format
    2.  Copyright & license strings
    3.  Font versioning
    4.  fsType
    5.  Vertical Metrics
        1.  General VM schema
            1.  VM consistency across family + sibling families
            2.  New Fonts VM
            3.  Upgrading fonts VM
            4.  fsSelection / Use of Typo Metris
        2.  CJK VM
    6.  Monospaced Fonts
    7.  Glyphsets
-   [Static fonts specifics](statics.md)
    1.  Supported Styles
    2.  Style Linking
    3.  Unsupported styles
    4.  Static font filenames
    5.  Single weight families
    6.  Hinting
-   [Variable Fonts specifics](metrics.md)
    1.  New Vs. Upgrading static to a VF
    2.  VF filenames
    3.  VF (zero) origin
    4.  Supported Axes
    5.  Unsupported axes
        1.  Axis registry mention
    6.  Designspace
    7.  Axis Mapping
    8.  Avar table
    9.  fvar instances
    10. Stat table
    11. Name-table specific entries required
    12. Instantiated Static Fonts
    13. VF Hinting
-   Font Mastering (\~to do)
    -   [Refining your typeface](refining.md)
        1.  Spacing
        2.  Kerning
        3.  Outlines compatibility + interpolation
        4.  Open Type features
        5.  Script specific guidance

    1.  [Outline Quality](outlines.md)
    2.  “Rubric” (to do)

## Onboarding process

-   [Making a PR to GF](making-pr.md)
    1.  Manual process
    2.  Packager asisted process
    3.  Peer review and approval before merge
-   [METADATA.pb file](metadata.md)
    1.  History
    2.  Generation
    3.  Keys’ description
-   [Description file](description.md)
    1.  Requirements
    2.  Examples
-   [Designer Profile](profile.md)
    1.  Writing bio guidelines
    2.  Foundry information for the About section
    3.  Designer information for the About section
    4.  Registering a designer profile
    5.  Adding the designer profile
-   [Promo / Marketing](marketing.md)

    Requirements and guidelines for creating the promotional asstes.
-   [Onboarder workflow guide](onboarder-workflow.md)
    1.  Specific content for the Google Fonts onboarding team. Includes:
    2.  Issue tracker
    3.  Milestones
    4.  Pull Request policies
    5.  Project boards
    6.  Labels
    7.  Categories
    8.  Status
    9.  The servers validation process
    10. Workflow example
