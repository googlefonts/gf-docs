# Designer Profile
{:.no_toc}

> <span class="icon">🦥</span>  This guide is a technical review of the different requirements related to the [catalog/designers](https://github.com/google/fonts/tree/main/catalog/designers) directory in the [google/fonts](https://github.com/google/fonts) repo.
> Each credited entity on Google Fonts should have a registered profile in [google/fonts/catalog/designers](https://github.com/google/fonts/tree/main/catalog/designers). This profile appears in the [about](https://fonts.google.com/specimen/Praise?sort=date#about) section of the specimen page.
> You can request the addition or modification of your name, bio, and image using [this form](https://docs.google.com/forms/d/e/1FAIpQLSeMwHN8J213ZaxHrr5lHCrX56HY_NjGrWB8o604g98YxuMrdA/viewform).


## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## How to write the biography

-   **Fill up the** **[AUTHORS.txt](authors.md)** **file carefully.**

    All the names present in [AUTHORS.txt](authors.md) will be credited in the font’s specimen page on Google Fonts. The names should be written with all necessary signs and marks to be considered correct.
-   **There is one bio per designer and per foundry mentioned.**
-   **The text should be around 100 words.**
-   **The text must be written in the 3rd person.**
-   **We recommend one or two links directing to a webpage or social media.**
-   **Bio must be written in English and names translated in Latin script.**

### About section - Foundry information

**What to include:**

-   Foundry name and location
-   Short description
-   Notable projects
-   Link to website or social media

**Example:**

> *Based in New York and London, Commercial Type is a joint venture between Paul Barnes and Christian Schwartz, who have collaborated since 2004 on various typeface projects, beginning with the award-winning Guardian Egyptian, through to typefaces for clients worldwide including Vanity Fair; Helsingin Sanomat; T, The New York Times Style Magazine; MoMA; Visa; and Chobani. Commercial Type has also published typefaces that have helped to define the look of the last 10 years, including Graphik, Druk, and Dala Floda.* [*commercialtype.com*](https://commercialtype.com)

### About section - Designer information

**What to include:**

-   Designer’s name and location
-   Short bio
-   Notable projects
-   Link to website or social media

**Example:**

> *Greg Gazdowicz (b. 1988) hails from the suburbs of Gaithersburg, Maryland. He studied graphic design at the Maryland Institute College of Art, then completed the Type@Cooper Extended program in 2014, months after joining the design staff of Commercial Type. Greg has designed custom typefaces for Mailchimp, La Republica, Google, and New York magazine, and has released several families through Commercial Type, including Robinson and the ambitious Terza family.* [*Twitter*](http://www.twitter.com/)

## Registering a designer profile

You wrote a biography and you are happy with it. Now you want it to be added to Google Fonts so it appears in the `#About` section of the font family linked to that bio. As a designer or a foundry, you would just have [to submit it through this form](https://docs.google.com/forms/d/1HinKkdCPbHTaiXxakeaUpDo1qsW3P9ZFemK65yWkru0/edit), and a team member will register the profile for you.

As a developer or a team member, you may want to know the process for registering or updating a new profile. You will find below all the necessary information to that effect.

### Technical requirements

-   **There is a directory per (moral/physical) person added.**
-   **There are all the necessary elements.**

    Each designer directories should have these 3 elements:

    ``` code
    .
    ├── info.pb
    ├── bio.html
    └── image.png
    ```
-   **The directory is named correctly.**

    The directory should use the designer or the company’s name using ascii characters only and no hyphen.

    E.g `José María Ribagorda` → `josemariaribagorda`
-   `info.pb` **has proper name and file path.**

    The info.pb is a file made to link a designer’s name to an image, and to a font.

    <div class="indented">

    -   The name should be spelled exactly the same as in a related [METADATA.pb](metadata.md) of a font (with all the necessary characters event accented letters). If not, the platform won’t be able to display the right profile on the right specimen page.

    

    -   The image file path should be the same as the one within the same directory.

    Example:

    ``` code
    designer: "José María Ribagorda"
    link: ""
    avatar {
      file_name: "josemariaribagorda.png"
    }
    ```

    </div>
-   **The image is formatted ready to use.**
    -   Should be a `PNG` or `JPEG` image between 100px and 300px. It will be cropped as a circle, so the image must be submitted as a square (1:1).

    

    -   The filename should be the same as the directory name (ascii characters only).
-   `bio.html` **contains all necessary informations.**

    The bio.html file is an HTML snippet (similar to the description file) that contains a short bio of the designer.

    -   Should contain a link to a webpage and/or social media profile: social media links are referenced as “Twitter”, “Instagram” etc, not as a name tag. Other web pages are displayed truncated from the protocol prefix.

    

    -   We recommend a bio length of around 100 words. So it should be more than 200 characters and less than 1000 characters.

    Example:

    ``` code
    <p>
    José María Ribagorda is coordinator of the Graphic Design Degree at the Escuela Superior de Diseño de Madrid. 
    He has a PhD in Image, Technology and Design from the Complutense University of Madrid.
    </p>
    <p>
    <a href="https://www.joseribagorda.com" target="_blank">joseribagorda.com</a> |
    <a href="https://twitter.com/Jm_ribagorda" target="_blank">Twitter</a>
    </p>
    ```

### Process for adding a designer

1.  Before adding the profile, make sure you have [cloned the google/fonts repo](making-pr.md) into your machine and [installed gftools in a virtual environment](tools.md).
2.  To simplify adding a new profile, we use `gftools add-designer` script that is part of `gftools`. It takes the different pieces of information and create a new directory in your local clone

    Team members have access to a spreadsheet linked to [this form](https://docs.google.com/forms/d/e/1FAIpQLSeMwHN8J213ZaxHrr5lHCrX56HY_NjGrWB8o604g98YxuMrdA/viewform). They can download the spreadsheet to add it as an argument; it will take the description and the link and format it correctly in `bio.html`.

    This is a common usage:

    ``` code
    gftools add-designer path/to/local/designer/dir "José María Ribagorda" --img_path path/to/josemariaribagorda.png --spreadsheet path/to/speadsheet.xls
    ```

    1.  If you don’t use the `--spreadsheet` argument, then the script will insert a blank `bio.html` that you will have to update manually.

    

    2.  If there are several links, make sure there are separated with a bar sign ` | `.
3.  You will need to make a manual Pull Request to GF to add the profile to the main repo. Follow [the guideline to make PR to google/fonts](making-pr.md).
    -   Please create one PR per profile.

    

    -   In your PR you should mention a font (one is sufficient) the profile is linked to.

    

    -   Don’t forget to add the labels `Designer profile` and `Ready for review`, and add the PR to Traffic Jam (cf [The onboarder workflow guide](onboarder-workflow.md)). A team member will review the PR and merge it. Once done, it should appear on the platform in 2-4 weeks.
