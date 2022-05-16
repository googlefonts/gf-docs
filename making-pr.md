# Making a PR to Google Fonts
{:.no_toc}

> <span class="icon">🐸</span>  In order to submit a new family or an upgrade of an existing family on [fonts.google.com](https://fonts.google.com/), we must add or update the files held in the [google/fonts](https://github.com/google/fonts) repository. This guide will help users submit Pull Requests (PR) which can then be reviewed and merged by a team member.
>
> Before submitting your pull request, make sure you have read the following documentations:
>
> -   [Contributing to GF](production.md)
> -   [Main contribution cases](onboarding.md)
> -   [Font files requirements](requirements.md)
>
> The PR process requires a good understanding of GitHub and command line tools. If this isn’t you, we suggest simply opening an issue using the `Add Font` or the `Update Font` template in the [issue tracker](https://github.com/google/fonts/issues), and waiting for a team member to ship the font for you.
>
> As a general rule, **GF requires users to open an issue before submitting anything through a PR**. The PR is the formality that achieve a project, not its starting point. GF uses the issue tracker to define an agenda, generate statistics to estimate the work done, but also to archive decisions. Anything that is going out of GF standards, needs to be documented somewhere, and the issue tracker is here for that purpose. If your font isn’t submitted through an issue first, your PR may never be merged.

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Prerequisites

-   Users should have [gftools](https://github.com/googlefonts/gftools) installed in a virtual environment (see [Google Fonts Tools](tools.md)).
-   Users should have their [Git client configured](hosting.md) with an SSH key or HTTPS protocol. HTTPS is easier, but if you want to use our [Packaging tool](package.md) to make a pull request, you will need an SSH key.
-   Users should have read the [Contributor License Agreement](https://cla.developers.google.com/about) and should have signed it by clicking the “Manage your agreements” button at the bottom of the CLA page.
-   Users should make sure to set git to record commits with their name, and the email they signed the [Google CLA](https://opensource.google/documentation/reference/cla) with, otherwise, your pull requests will trigger a CLA-checker warning.

    These metadata can be set with your git GUI tool, otherwise manually with a CLI:

    ``` code
    git config --global user.name "Your Name";
    git config --global user.email user@host;
    git config --global push.default simple;
    ```

## Initial setup

Before making a pull request to [google/fonts](https://github.com/google/fonts) (aka the source repo), you will need to have your own copies of the google/fonts repository: one hosted *remotely* on git server (the fork), one *locally* on your own machine (the clone of your fork). The forked repo will then be the “origin” remote of your local repo and therefore will be linked to each other.

<figure style="float:left">
<img src="https://lh3.googleusercontent.com/0igaOH8GUJH7ktvFPOALF7wsI_UFD98SWnVlMUXutzbg2wEyS_KKGK7AzoGrCoT1lQj5-hDOnp4JO7J9Oyv_NM6O30QFLL35GjIC0vp_w6SdNVqIOAEuyvd2Qa7pr3cwwMz3-khp" style="width:192px" />
</figure>

1.  **Fork** the [google/fonts](https://github.com/google/fonts) repo so you have your own copy.
2.  **Clone your fork** to a sensible place on your computer.
3.  At this stage, your `local clone` is only tracking its **origin remote** (aka your `fork` of [google/fonts](https://github.com/google/fonts)). It means that if you **fetch** changes from all remotes, you will only be able to **pull** the changes that happened on your `fork`. To be sure you receive the latest updates from google/fonts (aka the **“upstream” remote**), you need your `local clone` to be linked to it. Add [google/fonts](https://github.com/google/fonts) as a remote and call it “upstream”.
4.  **Fetch** from the `main branch` of the `upstream repo`.

If the upstream has changes, you need to **pull** them locally, and then have your `origin remote` also in sync:

5.  **Pull** from the **upstream repo** (into the `main branch` of your `local clone`).
6.  **Push** into the `main branch` of the `origin repo`.

Now all remotes are connected with your local repo and they are all in sync.

## Making a pull request to GF

You’ve completed the initial set-up to make a pull request to the `google/fonts` repo, and the font you want to submit follows all the requirements in terms of both its hosting (in a public git repository) and engineering (passes fontbakery checks). Now you want to submit it to Google Fonts.

The `google/fonts` repository is a **big** repository. It contains more than a thousand fonts. A lot of people have forked it, and a lot of people are contributing to it. So we don’t commit and push directly into the main branch — and this is also mandatory for your own fork and clone. Instead, we create a new branch, and make a pull request from this branch. The rule is that one Pull Request will relate to one changed directory changed. (eg. one PR will deal with updates to `ofl/castoro`, but a separate PR must be made for updates to `ofl/lexend`.)

They are several workflows possible, but we recommend this one when it comes to making manual pull requests to `google/fonts`:

1.  Create a local branch, make changes, and commit the changes.
2.  Push the commits to a branch of the same name to the origin remote (your fork).
>    Note that if you have contributing permission (you are a GF team member), you can directly create a branch on `google/fonts` and make a PR from this branch instead of from your fork’s branch.
3.  Make a pull request to `google/fonts` either from the branch on your fork, or, if you are a team member, from the branch you made on the upstream.
4.  Then we will review it, and eventually merge it.

When the PR is merged, then you can sync up your local clone and your fork. Finally, you can delete the local and the origin remote branch to save space everywhere.

### Making a manual PR

Now that you have the general scheme in mind, let’s dive into more details. You have completed the initial set-up to make a pull request to the `google/fonts` repo, and the font you want to submit meets all the requirements, in terms of its hosting and engineering.

1.  Create a branch that has the name of the font family (all lowercase, no spaces).
2.  If you are adding a new family, you will have to create a new directory in the `ofl/` folder. Name it after the font family name (all lowercase, no spaces, no hyphens).
> **Note:**
>  -   If you have, for example, MyFont and MyFontCondensed, this is 2 families: remember that GF only accepts weight styles. So this is also 2 font directories, and **2** separate PRs. Read more about the [Font Files requirements](requirements.md) to know more about the [supported styles for static](https://www.notion.so/Static-font-files-requirements-71d00ce1fbd44d72bf4e24b430abf2a2) and [variable fonts](variable.md).
> -   If you upgrade a font, then simply go to the existing directory of said font.
3.  Add (or replace) the font files inside the font directory.
4.  Add (or replace) the [license OFL.txt](license.md).
5.  Run `gftools add-font`. You can do that from the root directory of your local clone of the Google Fonts repository. The argument expected is the path of the font family directory:
    ``` code
    gftools add-font ofl/fontname
    ```
>    **Note:**
>     -   If you add a font, this will create 2 files: a dummy description for the font in HTML format, and a `METADATA.pb` file which gives instructions to the API.
>    -   If you upgrade the font, it will simply update `METADATA.pb`.
6.  Open [DESCRIPTION.en_us.html](description.md) and update it.
7.  Open and check if [METADATA.pb](metadata.md) is not saying anything absurd.
8.  When you are happy with everything, commit and push to the origin’s branch (same branch name you already created) with this message: `<FontName> : <font-version> added`.

    E.g: <https://github.com/google/fonts/pull/4146>
>   **Note:** If you have permissions to contribute to `google/fonts` repo (such as team members), we recommend you to push directly on a new `google/fonts` branch. This will allow the CI to work properly.
9.  Then go to <https://github.com/google/fonts/pulls>, and create a “new pull request.”
10. Unless your branch is part of the `google/fonts` repository (i.e. you are a team member), you will have to compare across forks; choose the branch of your fork containing the font you want to submit, then click on `Create a pull request`.
11. The title of the PR will be the message above, if not, please re-enter: `<FontName> : <font-version> added`. Don’t forget to add a body text following this schema: `Taken from the upstream repo <repo-url> at commit <commit-url>`.
> **Note:**
>    -   Add a short description of the PR, especially if the font is an upgrade, we want to know what we shall be reviewing.
>    -   If you are an official onboarder, please add the PR into the Traffic Jam project and don’t forget the labels. Refer to the [Onboarder Workflow Guide](onboarder-workflow.md) for more details.
12. Press the green button and there you go – you have made a PR!

### Make a PR with the Packager

Good news! Google Fonts also has a tool that packages the font and makes the pull request to google/fonts repo for users with *contributor access* (team members). It uses the SSH protocol, which is why you would need to set up Git with an SSH key if you are a team member. For more info about `gftools packager` and its usage, read [this documentation](package.md).
