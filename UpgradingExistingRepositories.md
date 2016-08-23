# Preparing old Font repositories
Getting repositories to the same standard has to be done on a case by case basis. Here are some examples of good repositories. It is worth studying these first before you begin:
[Neuton](https://github.com/m4rc1e/Neuton)
[Mirza](https://github.com/Tarobish/Mirza)
[Nunito](https://github.com/m4rc1e/NunitoFont)

Each project differs greatly in quality so it is very difficult to script a workflow which does everything automatically. Fortunately, we have written some scripts to check the most important parts. 


## Finding sources.
Locating sources is the most crucial step. Without decent sources, more effort will be required. The following approaches below are listed in priority. The last option should be used as a last resort only

1. Find repository on Github
2. Browse old [repository](https://bitbucket.org/lassefister/old-googlefontdirectory/src/21142f3bf7ad39d89c1c682d30830494ef1c905c/tools/nonhinting/setnonhinting-fonttools.py?at=default&fileviewer=file-view-default)
3. Contact Author and ask for sources
4. Rebuild sources from binary ttfs

### Other considerations to keep in mind:
- Do the version numbers match the family on [Google Fonts?](https://fonts.google.com)?
    - An [md5 checksum](https://www.youtube.com/watch?v=dzdom0Objq4) comparison between the Google Font binary ttfs and your discovered repos ttfs will check if the files are identical.
- Are the newest sources unreleased?
    - This means they may be a work in progress. You must decide whether it is best to work on these or rollback to a previous version.


## High level overview of workflow

- Reorganise repo into the following folder heirachy (example [Maven Pro](https://github.com/m4rc1e/Maven-Pro)):

```
    ├── AUTHORS.txt *
    ├── CONTRIBUTORS.txt *
    ├── OFL.txt *
    ├── README.md *
    ├── fonts
    │   ├── MavenPro-Black.ttf
    │   ├── MavenPro-Bold.ttf
    │   ├── MavenPro-Medium.ttf
    │   └── MavenPro-Regular.ttf
    ├── old *
    │   └── version-1.000 *
    │       ├── DESCRIPTION.en_us.html
    │       ├── METADATA.json
    │       ├── MavenPro-Black.ttf
    │       ├── MavenPro-Bold.ttf
    │       ├── MavenPro-Medium.ttf
    │       ├── MavenPro-Regular.ttf
    │       ├── OFL.txt
    │       └── src
    │           ├── METADATA_comments.txt
    │           ├── MavenPro-Black-VTT.ttf
    │           ├── MavenPro-Black.glyphs
    │           ├── MavenPro-Black.otf
    │           ├── MavenPro-Black.vfb
    │           ├── MavenPro-Bold-VTT.ttf
    │           ├── MavenPro-Bold.glyphs
    │           ├── MavenPro-Bold.otf
    │           ├── MavenPro-Bold.vfb
    │           ├── MavenPro-Medium-VTT.ttf
    │           ├── MavenPro-Medium.glyphs
    │           ├── MavenPro-Medium.otf
    │           ├── MavenPro-Medium.vfb
    │           ├── MavenPro-Regular-VTT.ttf
    │           ├── MavenPro-Regular.glyphs
    │           ├── MavenPro-Regular.otf
    │           ├── MavenPro-Regular.vfb
    │           ├── VERSIONS.txt
    │           └── fontsquirrel_generator_config.txt
    └── sources *
        ├── MavenPro.glyphs *
        └── build
            └── instances.yml
```

- The old folder should contain the original files from the repo you are working on. They should be subfoldered with the sources version number.
- Every file/folder with an asterisk is essential.
- Source folder should have 1 .glyphs file for Roman weights and 1 for Italics
- Upgrade the .glyphs file version number by += 1.000. eg v2.1000 -> v3.1000
- Implement everything from this [checklist](https://github.com/googlefonts/gf-docs/blob/master/ProjectChecklist.md)
- A glyphs script exists to [test the above checklist steps](MY SCRIPT)
- Implement everything which is not design intensive from the [Cleanup Checklist](https://docs.google.com/spreadsheets/d/1vFNVR1lf14S1cthPQ59Mav5uZCnWw8_nS3ehKwueUz0/edit#gid=1988585029)
    - MM compatiblity, anchors, kerning can take several days to implement. These should be fixed by the designer if there is enough time.
- Check [github for issues](https://github.com/google/fonts/issues) on font family and fix them. Again, some issues involving design or extensions will take too long to implement.
- Check and fix vertical metrics. Khaled proposed a [schema](https://groups.google.com/d/msg/googlefonts-discuss/W4PHxnLk3JY/MpyLLY4jAwAJ), we use this for these repos. A [GlyphsApp script](My script) exists to check if it fulfils his spec.
- Push repo to your github account
- Send repo link to designer to work on. Link should be included in your daily work log on the [Google Fonts Group Discussion board](https://groups.google.com/forum/#!forum/googlefonts-discuss).
- Designer should send you back a pull request when finished. You should merge it back into your repo.
- If you originally forked the project from a repo. It may be nice to send them a PR of the upgraded project, with a note explaining the project and changes made. By doing this, we have consolidated all forks back into the original repo.


## Case Study: Step by step log of Upgrading Cabin
by Marc Foley

Below is typically how I approach upgrading a repository so it is ready for designers to work on. The final repo can be found [here](https://github.com/m4rc1e/Cabin)

### Retrieve sources
- Project has [github repo](https://github.com/impallari/Cabin)
- Project gets forked to my [github account](https://github.com/m4rc1e/Cabin)
- I clone my fork to my local system

### Tidyup
The following section is each commit I made to my forked repo.

commit 609126c3a11cf5cddc243c86349b63db8a799b0c
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 11:26:05 2016 +0200

    gitignore: Added, ignore glyphsapp autosaved files

commit 74e49f5b9674ec94d67d277262a355afe75d0a1b
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 11:26:48 2016 +0200

    old: Moved old v1.005 sources into old folder. Version number was discovered by opening ttf binary in fontlab. Ttf binaries can also be opened in Glyphsapp.

commit e7047e0fed51a3efc92cd0c90efacab7aa99f49e
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 11:28:22 2016 +0200

    txt files: Readded mandatory txt files to top level of directory. These will need further updating to reflect the new state of the project

commit d025ffb4aee5f390b3a35b5ef90107d035c449f5
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 11:35:34 2016 +0200

    Generated .glyphs files from the extremes of MM .vfb file, using this script in [FL](https://github.com/schriftgestalt/Glyphs-Scripts/blob/master/Glyphs%20Export.py). '_' in file name to denote it is a temporary file. We will delete these later, once we have them combined into 1 glyphs file'

commit 1129934409ff4deec6798c1c6eadf7aec9b85b8c
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 11:38:11 2016 +0200

    Cabin: Both temporary glyphs files have been combined into 1 master .glyphs file. Temp files also deleted

commit 3c51ee43104cd77a89077dbce28d8e2142e0be9a
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 11:53:58 2016 +0200

    Cabin.glyphs: The script 'Test repo matches gf-checklist structure' was run. The script returned there were errors in the font file, fsType, copyright... These errors have been fixed in this commit. I still need to fix errors in the txt files'

commit c1ec7cfd2d4ccd0b6307e42178bcc1628c252cbc
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 11:57:12 2016 +0200

    CONTRIBUTORS: added, Test repo matches gf-checklist reported this file was missing. The contributors were found by looking in the fonts meta data

commit 5b304ebfe7452c176b521ac846a0323549c2ff7c
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:01:21 2016 +0200

    OFL.txt | Cabin.glyphs: Updated first line of OFL.txt and .glyphs file copyright field. These need to match according to the checklist spec. This error was reported in the 'Test repo match gf-checklist spec' script

commit 761f256a126b1ec17034bc4fe55e95f8de25138e
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:07:13 2016 +0200

    Cabin.glyphs: Added vendorID. I had to find this by looking at a [Libre Franklin](https://github.com/impallari/Libre-Franklin) which was also made by the same author. This error was reported from previous script. Everytime we fix an error which was reported by the script we should rerun it and continue fixing errors until everything passes

commit 29924c852849544afa442363b08f601dfa302bc1
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:19:49 2016 +0200

    TRADEMARKS.md: added, Script reported this file was missing. Text for this file came from the trademarks field in the font metadata. I am skeptical if this is correct so I will include an issue for it on the repo. I have now successfully made all the checks pass for the script 'Test repo structure matches gf-checklist structure'. We still need to check the vertical metrics, MM compatibility and see if we need to complete some steps from the other cleanup checklist

commit 6a8c37d788aa1aaa60a515bb4cad86e061008d25
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:21:20 2016 +0200

    Cabin.glyphs: removed panose and glyph order family values. I removed te panose because the panose should be unique for each weight. This field will be included in each instance later. The glyph order was removed because Glyphsapp has its own order function

commit ff16905147edf22d7326b17670229b9bebc3216e
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:28:13 2016 +0200

    Cabin.glyphs: Both masters now have weight values. The weight values come from the vertical stem width of the 'H'. We need these values so we can generate instances. In the next step, we'll add the instances

commit b673471802ef13c92ec6e34f72c9e0f622c478bc
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:34:53 2016 +0200

    Cabin.glyphs: instances added. To get the correct weight for each instance. We need to measure the 'H' for each weight from the old fonts. The names of each instance have to match this [document](https://docs.google.com/spreadsheets/d/1ckHigO7kRxbm9ZGVQwJ6QJG_HjV_l_IRWJ_xeWnTSBg/edit#gid=0).

commit 852064c9e3d259c541137ee54dcb2311d7122c0e
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:40:00 2016 +0200

    Cabin.glyphs: Added vertical metrics to each instance. The script 'Test vertical metrics match Khaled's approach' was used in order to check they are correct. For this font it was very easy. Unfortunately most people do not understand how the three sets of vertical metrics work very well. Refer to [Kalapi's work log on the Google Fonts Group](https://groups.google.com/d/msg/googlefonts-discuss/W4PHxnLk3JY/Uvxm1qj6AgAJ) for an indepth discussion on how it works. It is worth reading all posts on this.

commit 1dca9fef83430dcdab23bebf2f121414b8e0414a
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:41:18 2016 +0200

    Cabin.glyphs: ran update glyph info. This should rename glyphs according to Glyphsapp internal naming scheme. We can now use Glyphsapp's auto OT features etc

commit 973d1c108f8bc8f0cecffef23c718cffd5c99c61
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:46:26 2016 +0200

    Cabin.glyphs: Added auto OT features and reintroduced smcp feature. Glyphsapp allows us to use auto OT features. The original sources only included smcp and kern. We now have ordn, subs, sups, frac etc

commit cc5111be221a989b11427ff21fc1e943289c541a
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:49:42 2016 +0200

    Cabin.glyphs: added 'http://' to meta data fields which need urls. This was reported with the Preflight Fonts script

commit de2e655e90353f9bf46aae2777e2d06eebfb4328
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:56:19 2016 +0200

    Cabin.glyphs: Fixed all errors reported in Preflight font script.
    
    We now have a clean repo, 1 master .glyphs file with all masters and instances, correct vertical metrics, Better OT features. Luckily the original font was to a very very high standard. Most fonts are not this easy to work on.
    
    I will need to repeat all the steps we did on the fonts for the Italics and Condensed files which existed in the old repo. I will also need to generate some tests fonts and run them through font bakery. I leave the font bakery step till the designers have finished working on the repo.

commit ccc9bc75cd87f879120911ddb7afcf4609d4f739
Author: Marc Foley <m.foley.88@gmail.com>
Date:   Tue Aug 23 12:57:11 2016 +0200

    Cabin.glyphs: increased version number from 1.005 to 2.005

