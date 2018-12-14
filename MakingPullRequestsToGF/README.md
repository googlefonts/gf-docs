# Making a Pull Request to Google Fonts

## Get google/fonts repo locally to make a branch with updates

First, you’ll need to get the `/fonts` repo on your computer in order to make updates for a pull request.


1. Fork the repo [google/fonts](https://github.com/google/fonts) to make a copy under your username.
2. `git clone` your fork to a logical place on your computer.

## Add google/fonts as an upstream repo

You’ll need to link your local remote git repo with the main google/fonts repo, usually called the “upstream.” 

First, check which remotes are connected to your local repo with:

```
git remote -v
```

If you haven’t yet connected it with the main google/fonts repo, the above command will probably return something like this:

```
origin        git@github.com:username/fonts.git (fetch)
origin        git@github.com:username/fonts.git (push)
```

If you don’t see the upstream repo in that list, add it with the following format:

```
git remote add <name> <upstream-url>
```

Specifically, the command you’ll probably want is this:

```
git remote add upstream https://github.com/google/fonts.git
```


## Get latest version of google/fonts master, then make a PR branch

When you are ready to make a new pull request, you’ll want to make sure you have the latest updates to the main google/fonts repo, so you only submit the changes you’ve made.

Checkout the `master`  branch from the github.com/google/fonts.git remote (this could be named anything, but would usually be called `upstream`)

```
git checkout upstream/master
```

Then, fetch the latest commits from the remote, and then rebase, to avoid unneeded merge commits: 

```
git fetch upstream
git rebase upstream/master

# git pull -r upstream/master # equivalent, but less safe because not step-by-step
```

Then, check out a new ‘fresh’ branch (replace `family-name-pr` with the appropriate family name):

```
git checkout -b family-name-pr
```

Next, copy your files to the directory, add them to git, commit, and push (you could also manually drag files between file windows, if `cp` isn’t your style):

```
mkdir ofl/familyname
cp -rp /path/to/git/project/*.ttf ofl/familyname/
cp -rp /path/to/git/project/METADATA.pb ofl/familyname/
cp -rp /path/to/git/project/OFL.txt ofl/familyname/
cp -rp /path/to/git/project/DESC* ofl/familyname/
git add ofl/familyname
git commit ofl/familyname -m "ofl/familyname Add files, metadata"
git push origin family-name-pr
```

Finally, go to *github.com/username/fonts* and open the PR from family-name-pr to master. You’ll see a banner at the top of your repo, so click the button and make that PR!


---


## A useful pull request message structure

**Upstream repo**
Point to your project repo.

```
From upstream repo https://github.com/username/family-name
```

**Remaining to-do items**
Optionally, you can add remaining to-do items to the PR. If you use the markdown “checkbox” syntax, GitHub will give a handy progress bar on the list of PRs. As an example:

```
- [ ] close out remaining fontbakery WARNs
- [ ] finish diffing against hosted versions
- [ ] QA glyph outlines with Red Arrows
```

**FontBakery checks**
Copy and paste your latest FontBakery checks, using the `--ghmarkdown` argument to save them in a format that is convenient on GitHub.

```
<details>
<summary><b>[25] Family checks</b></summary>
<details>
<summary>:fire: <b>FAIL:</b> Check METADATA.pb parse correctly. </summary>
<!-- etc etc -->
```

You can even wrap each set of FontBakery checks in a `<details>` HTML element, in order to show several font files in a condensed manner.

```
<details>
<summary><b>Family Name Variable</b></summary>
<!-- Copy and paster FontBakery markdown here -->
</details>

<details>
<summary><b>Family Name Regular (Static)</b></summary>
<!-- Copy and paster FontBakery markdown here -->
</details>

<summary><b>Family Name Italic (Static)</b></summary>
<!-- Copy and paster FontBakery markdown here -->
</details>
```

