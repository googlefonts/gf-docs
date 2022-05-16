<div>

# Package the fonts

</div>

> <span class="icon">🦦</span>  [gftools packager](https://github.com/googlefonts/gftools/tree/main/docs/gftools-packager) is the tool team members use to package fonts from the upstream repo to ship then to [google/fonts](https://github.com/google/fonts) repo. It basically replaces [Making a PR to GF](making-pr.md) process. It saves a lot of time, and prevent lots of human mistakes.

Note that Packager will create a branch on `google/fonts` directly. However, this is possible only if the user has a special contribution permission to the repo. This is why this chapter is specifically for Google Fonts’ Team Members.

</div>

**Table of content**

## What the Packager does

### When used on a font family for the first time

This is the process tha Packager allows to automate:

1.  Takes elements from the upstream repo: fonts, OFL.txt, eventually Description file if available. It can also package fonts from a `tag release`, which is quite practical.
2.  Creates a local branch of your local clone of google/fonts It should follow this scheme: `gftools_packager_ofl_fontname`.
3.  If the font is new, it creates a new font family directory in the `ofl` directory. If the font is an upgrade, it updates the existing directory with the new elements.
4.  Adds an `upstream.yaml` file with the location of the linked elements upstream.
5.  Runs [gftools add-fonts](making-pr.md) on the fonts. That script creates or update [METADATA.pb](metadata.md). Packager also create a link to the source repo and commits at which the elements where taken to facilitates any updates. It also adds an empty [Description file](description.md) if not part of the upstream linked elements.
6.  Commits and pushes that package (step 1-4) onto the branch made at step 2.
7.  Makes a Pull Request to `google/fonts` on a branch of the same name, and write the required description in comment:

    ``` code
    Taken from the upstream repo <repo-url> at commit <commit-url>.
    ```

### When already used before on that font family (upstream.yaml)

Once the font family has been packaged once with the packager (and that PR has been merged), packager will be able to update the font in `google/fonts` repo very easily and fast thanks to the `upstream.yaml` file. In few words, it will use it to speed up the entire process because the font has a source URL, and an endpoint location in google/fonts repo.

Note that the font has to be in the same location as before, otherwise you would have to correct `upstream.yaml` first.

This file should look like this:

``` code
branch: main
files:
  fonts/variable/FontName.ttf: FontName.ttf
  OFL.txt: OFL.txt
```

## Main usages explains

`-u` creates a yaml file which will help packager to set up the links and the informations inside METADATA.pb

`-b` calls the branch on which you want to push commits or add the fonts

`-g` packages the fonts on a new branch of googe/fonts without creating a PR

`-a` pushes commits (needs to indicate a branch then)

`-p` makes a pull request to google fonts.

## Adding a new fonts with Packager

### Short method (advanced users)

The shortest usage of the packager require to know how to use `vim`:

``` code
gftools packager "Font Name" path/to/local/google/fonts -p
```

You will have to fill up all needed informations directly from the Terminal using vim, it then will package the font, run some script, create a branch and PR all of that to google/fonts.

### Method which doesn’t need vim

1.  The Packager needs informations to know where to find the necessary files (fonts, OFL etc), so we need to create a `.yaml` file that will provide such info. Open your terminal and run:

    ``` code
    gftools packager -u ~/Desktop/fontname.yaml 
    ```

    This will create a `.yaml` file on your desktop. You can chose whatever path is relevant to you. Open it and fill up the gaps. At the end, you should have this kind of information in your yaml file:

    ``` code
    name: Font Name

    repository_url: https://github.com/owner/Font-Name

    branch: main

    category:
      - SANS_SERIF
      - MONOSPACE

    designer: Foundry Name, Designer Name 1, Designer Name 2

    files:
      OFL.txt: OFL.txt
      fonts/variable/FontName[axis].ttf: FontName[axis].ttf
      fonts/variable/FontName-Italic[axis].ttf: FontName-Italic[axis].ttf
    ```

    → This example above works if the upstream repository in having a `fonts` directory where the binaries are stored. In `files` field you have the file path in the upstream repo on the left side of the `:`, and the target files in `ofl/fontname` directory of `google/fonts` repository.

    → If fonts are in a zip file of a **tagged release**, and not in a font directory, you should use the `archive` field this way:

    ``` code
    repository_url: https://github.com/owner/Font-Name

    archive: https://github.com/{owner}/{repo}/releases/download/{version}/project.zip

    branch: main
    ```

    → You obtain the link of the zip by right-clicking on it from the upstream repo.
2.  The Packager will package all the files from the font upstream repository, commit and push them onto a new branch in the google/fonts repo. It will also create/update a `METADATA.pb`, and add a dummy `DESCRIPTION.en_us.html` if not already there.
    1.  If you add a new font, run:

        ``` code
        gftools packager path/to/yaml path/to/local/google-fonts-repo -p
        ```

        Then follow the guidelines and choose the correct options.

    

    2.  If you upgrade an existing font, first check in the font directory in the `ofl` folder (of the main branch) if there is already an upstream.yaml with the correct information. If not, proceed as if it was a new font. If yes, run `gftools packager "Font Name" path/to/local/google-fonts-repo -p`. Then choose the correct options. If the upstream.yaml didn’t have correct information, you can do as if you were adding a new font.
3.  Update [DESCRIPTION.en_us.html](https://www.notion.so/886ed42e143247b1b22c1ddd0bd4d19b) , check and eventually correct [METADATA.pb](https://www.notion.so/f218d09a5c1145aeb79592d568cf79cc) if needed. Commit and push to the branch that the Packager created. Everytime you commit and push something into the [google/fonts](https://github.com/google/fonts/pulls) repo, please specify `<Font Name> : <file> updated/added` in your commit message.

### Method that allows editing before PR

If you use the previous method, and if you want to modify your PR, every time you run `-p` argument in conjunction with a “font name” or a `yaml` file, you will actually re-package and override the PR (because it will ask you to do a force-push). This means that all your manual commits you may have done in between will be lost.

To avoid that, you can first use `-g` to package and commit on a new branch (but no PR), and in a second step, use `-p` in conjunction with `-b` to push a branch. So instead of specifying a `yaml` file as source (or a font name) you will specify a branch — this way the packager won’t force-push the fonts, it will only PR the branch as-is (because it is the source and not the target).

Also, keep in mind that every push you make on a google/fonts PR, will trigger the continuous integration which generate QA reports. If the CI is triggerred multiple times at once, it can happens that it breaks. It is therefore wise to make all modifications to [metadata.pb](metadata.md) and [Description_en.html](description.md) beforehand, and push all the changes at once.

To do so, follow this process:

1.  Follow step 1 from previous method.
2.  Now you can use the `-g` argument to package the elements, create a branch, generate or update `METADATA.pb` and commit on that branch without making a PR :

    ``` code
    gftools packager path/to/fontname.yaml path/to/local/google/fonts -g
    ```
3.  Check out the branch the packager created.
4.  Modify description, the metadata file, or else, and commit the changes onto the new branch — the usual way with the CLI, or SourceTree etc.
5.  Make a PR to GF using packager using the `-b` argument to push a branch—and so `-p` doesn’t override the last modification by repackaging the font.

    ``` code
    gftools packager -b gftools_packager_ofl_fontname path/to/google/fonts -p
    ```

## Upgrading an existing font with Packager

The power of packager resides in its efficiency for upgrading families which were onboarded with the tool at the first place.

Before doing so, check if:

-   There is an upstream.yaml in the font family directory: if not you will have to do as if you were packaging the font for the first time.
-   The informations are correct: make sure the branch and file paths are still up to date.
-   The source URL (or the archive URL) located in [METADATA.pb](metadata.md) is still correct.

If all is in good place, team members would only have to run:

``` code
gftools packager "Family Name" path/to/google/fonts -p
```

</div>
