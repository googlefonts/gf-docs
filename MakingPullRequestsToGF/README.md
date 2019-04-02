# Making a Pull Request to Google Fonts

In order to submit a new family or upgrade an existing family on [fonts.google.com](https://fonts.google.com), we must add or update the fonts held in the [fonts/google](https://www.github.com/google/fonts) repository. This guide will help users submit pull requests which can then be reviewed by a team member.

## Prerequistes
- Users should know git. If they don't, they should go through [http://try.github.io/](http://try.github.io/) the handbook is especially useful.
- Users should have a basic understanding of the commandline. They should be able to traverse directories and understand the commands cd, ls, mv, cp.
- Users should have [gftools](https://github.com/googlefonts/gftools) installed (TODO M Foley make pip installable)

## Initial setup

- [Fork](https://help.github.com/en/articles/fork-a-repo) the [google/fonts](https://github.com/google/fonts) repo so you have your own copy.
- `git clone` your fork to a logical place on your computer. If you want to clone it to your Documents directory do:
```
cd ~/Documents
git clone https://www.github.com/your-username/fonts
cd fonts
```

You’ll now need to link your local remote git repo with the main google/fonts repo, usually called the “upstream”.

First, check which remotes are connected to your local repo with:

```
git remote -v
```

If you haven’t yet connected it with the main google/fonts repo, the above command will probably return something like this:

```
origin        git@github.com:your-username/fonts.git (fetch)
origin        git@github.com:your-username/fonts.git (push)
```

If you don’t see the upstream repo in that list, add it with the following format:

```
git remote add <name> <upstream-url>
```

Specifically, the command you’ll probably want is this:

```
git remote add upstream https://github.com/google/fonts.git
```


## Submitting a pull request

### Syncing our repo

When you are ready to make a new pull request, you’ll want to make sure your master branch is in sync with the upstream.

```
git checkout master
git pull upstream master
```

With our repository now synced, we can create a new branch. For simplicity, it's recommended to name branches the same as the family name.

```
git checkout -b family-name
```

### Adding/updating family files
If we are submitting a new family, we have to create a new family directory.
```
mkdir ofl/familyname
```

Copy the ttfs, license and DESCRIPTION.en_us.html from the upstream repository to the family dir.
```
cp /path/to/upstream/fonts/*.ttf ofl/familyname/
cp /path/to/upstream/OFL.txt ofl/familyname/
cp /path/to/upstream/DESCRIPTION.en_us.html ofl/familyname/
```

Run gftools add-font on the family dir.
```
gftools add-font ofl/familyname
```

If the family is new, you'll need to hand edit the generated METADATA.pb file and change the CATEGORY and DESIGNER fields. Our add-font script will only insert placeholders for these fields if the family is new.


We can now git add the files we've made/changed.
```
git add ofl/familyname
```

Once the files have been added, we need to commit them. The commit message is constructed in the following manner:

```
git commit -m "<familyname>: <font-version> added

Taken from the upstream repo <repo-url> at commit <commit-url>"
```

e.g if the family was called Montserrat and had the version number v3.002 and its commit was https://github.com/JulietaUla/Montserrat/commit/49e9a093314a504e85cd80ecfd7a4bc4b5aa50b5. We'd get:

```
git commit -m "montserrat: v3.002 added

Taken from the upstream repo https://github.com/JulietaUla/Montserrat at commit https://github.com/JulietaUla/Montserrat/commit/49e9a093314a504e85cd80ecfd7a4bc4b5aa50b5"
```

And finally push your branch to google/fonts
```
git push upstream family-name:family-name
```

Finally, go to *github.com/google/fonts* and open the PR from family-name-pr to master. You’ll see a banner at the top of your repo, so click the button and make that PR!


---


## Niceties

**Remaining to-do items**
Optionally, you can add remaining to-do items to the PR. If you use the markdown “checkbox” syntax, GitHub will give a handy progress bar on the list of PRs. As an example:

```
- [ ] close out remaining fontbakery WARNs
- [ ] finish diffing against hosted versions
- [ ] QA glyph outlines with Red Arrows
```

See https://github.com/google/fonts/pull/1911 for an example

