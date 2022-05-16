# Hosting projects on Github
{:.no_toc}

> <span class="icon">🐰</span>  **Git**
Git is an open-source Version Control System (VCS) that runs on your local machine. It is a powerful tool that allows you to save discrete versions of a project as you work on it and makes it possible for collaborators to work together on code-based projects (including fonts) in a controlled manner.
Using Git is essential to track the history of a project.
**GitHub**
Is one of the various web providers of Git services (Bitbucket, GitLab, to name a few). Google Fonts requires to use GitHub since it includes various other features to help administer the workflow of a project that further simplify working and collaborating via Git.

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## GitHub Culture

Using GitHub means embracing GitHub culture. One of the main goals of using a VCS like GitHub is to facilitate open contribution, one of the four freedoms (the Freedom to Contribute) of the [Libre Fonts movement](culture.md).

When working on an open platform like GitHub, development should happen publicly, ideally from day one, allowing others to view work in progress, and enabling the public to point out issues during development instead of after the typical 1.0 release.

Early feedback and contributions are some of the most valuable assets of open-source culture, as having multiple eyes on the project’s development leads to better tested and, therefore more robust projects.

At [ATypI 2014](https://www.youtube.com/watch?v=DBz0rVUYNPA) David Lemon, the senior manager of the Adobe Type group, discussed how the Adobe Type team has benefited from libre fonts culture and said that Git and Github were some of the most positive aspects. Adobe used the “*publish early and often, gathering feedback”* approach of Libre projects in its [Vortice typeface project](https://blog.typekit.com/2015/03/04/introducing-vortice-and-the-adobe-type-concepts-program/).

## Github Account

The first step is to [create a GitHub account](https://github.com/join). This is done similarly to any other cloud service by providing basic information: name, user name, and password.

Be sure to use a valid email as it is used to sign every commit (interaction) that you have with the platform. You also receive GitHub notifications from your repositories to that email account.

Once you have an account, you need to create authentication keys to be able to interact with the platform.

## GitHub authentication

When you work with GitHub, you will work in a local clone of a repository (a Git project folder on your computer), which you will frequently sync with the connected remote repository on GitHub.

There are two protocols used to connect to and interact with GitHub repositories: [HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https) and [SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh), and each of them requires a different form of authentication to GitHub.

### GitHub Token

When performing Git operations over the HTTPS protocol, Git prompts you for a username and password every time you try to interact with GitHub. In those cases, a **Personal Access Token (PAT)** is used in place of a password for authentication to GitHub (e.g. when cloning repositories using HTTPS), so you would need to [create a PAT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

You can avoid being prompted for your token and enter it manually each time you interact with GitHub by configuring Git to [cache your credentials](https://docs.github.com/en/github/getting-started-with-github/caching-your-github-credentials-in-git) for you.

Once you have created the PAT, you must configure it as part of your [environment variables](https://medium.com/chingu/an-introduction-to-environment-variables-and-how-to-use-them-f602f66d15fa) to work properly with GitHub, by saving it in your `.bash_profile` like this:

``` code
GH_TOKEN=YOUR_CREATED_PERSONAL_TOKEN
```

Where the value after the `=` corresponds to your created personal token. *Please keep in mind that your token is private. Keep it safe, and never share it publicly.*

### SSH keys

When working with GitHub using the Secure Shell Protocol (SSH), you need to first [check for existing SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys) or, if you don’t have one, you would need to [generate a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key) and add it to your GitHub account before it can be used to authenticate. With an SSH key, you can connect to GitHub without supplying a username and PAT at each interaction.

To avoid reentering your passphrase each time you use the SSH Key, you must [add your key to the SSH agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent).

## Software for working with GitHub

-   The [**GitHub CLI**](https://cli.github.com/) [(Command Line Interface)](https://cli.github.com/) is a tool for using GitHub from the command line. It makes it possible to use all Github features using git commands from a Terminal prompt.
-   [**GitHub Desktop**](https://desktop.github.com/) and **[Sourcetree](https://www.sourcetreeapp.com)** are open-source GUI applications for interacting with GitHub.
-   There are also plugins for Glyphs and RoboFont which allow you to commit to GitHub on save.

Don’t hesitate to search the Internet for how to install the SSH key properly according to your chosen environment, as it is different depending on your OS and software.

## Github workflow

### Repositories: administer files, manage the work and collaborate with others

**A repository** (or “repo”) is a place to save the project’s files and work history, allowing you to share, review and track the project's development.

-   If you are working on a new project, you will need to [create a new repository](https://docs.github.com/en/get-started/quickstart/create-a-repo) using our template outlined below.
-   If you contribute to an existing project, [fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) it into your GitHub account and later return your changes using a [PR](https://docs.github.com/en/get-started/quickstart/github-flow#create-a-pull-request) (Pull Request).

Both new repos and forked ones will be located in your GitHub account, and they are called the `remote` repositories because the “source” of the repository is hosted remotely on GitHub.

The forked repo will be the `origin` remote location, while the source repo will be `upstream` remote location.

After you have created or forked a repo, you will need to [clone](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) the repository to have a local copy on your computer so that you can access, edit, and later sync the files between locations.

Having the repository hosted remotely allows you to keep different copies of the same files that could be at different stages of development, and this also allows for multiple collaborators to be working on the same project in a planned and synchronized way.

When working with source projects on GitHub, it's common to have multiple forks of the same project, each owned by different users. Each contributor works on their own fork, periodically contributing their changes to the upstream repository. Therefore, it is crucial to work organized and coordinated, but GitHub helps you to achieve that.

→ **Create and name your repository**

-   GF requires a [particular structure for the repository](upstream.md) however, we have provided a [repository template](upstream.md) that you can use to get started.
-   Ideally, the repository name matches the [Font Project name](onboarding.md).

If you are a foundry or collaborative project:

1.  Set up a [Github organization](https://help.github.com/articles/creating-a-new-organization-account/)
    -   [Github Blog: Introducing Organizations](https://github.com/blog/674-introducing-organizations)

    

    -   [Github Help: Setting up and managing organizations and teams](https://help.github.com/categories/setting-up-and-managing-organizations-and-teams/)

    

    -   [Github Help: What's the difference between user and organization accounts?](https://help.github.com/articles/what-s-the-difference-between-user-and-organization-accounts/)
2.  Create usernames for each person involved in the project.
3.  Create each repo inside that organization. Github Organization examples:

-   [github.com/rosettatype](https://github.com/rosettatype)
-   [github.com/cadsondemak](https://github.com/cadsondemak)
-   [github.com/cyrealtype](https://github.com/cyrealtype)

→ **Repositories vs. cloud syncing**

If you are used to keeping design work synced to Dropbox, Google Drive, or iCloud, it is strongly advised you *exclude* your Git repos folder from this type of cloud syncing. If you start a project inside a cloud-synced area, then move that work into your git-repos area, make sure the syncing doesn't follow your content. General-purpose cloud syncing and Git have different purposes and can interfere with one another in strange ways.

### Commits: manage progress and track changes

Git detects which files have been changed. It allows you to be aware of those changes and register them in an organized way using *commits*.

**Commits** are often referred to as a *snapshot* of the current changes and are a mechanism to make a labeled record of each step of the development. Registering these snapshots also makes it possible to roll back changes and return to a previous state of development if needed; this is the key concept of working with Git.

-   We strongly suggest you learn to “Commit early, commit often” to keep small chunks of easy to define and understand changes. Make commits at meaningful points, e.g. one commit for updating the metadata, another for setting the metrics of your font, and a separate commit for changing a set of anchor positions.
-   It is important to provide a clear and meaningful message with each commit to make it easy for other users to track the process and know what each change was for. If in doubt, study [Montserrat’s commit history](https://github.com/JulietaUla/Montserrat/commits/master). The commit titles should be short, clear and specific, and not repeated. For example, a series of commits that are all titled “VF Update” is not helpful. This is important because GF tools will use the commit messages to generate release notes. (See eg <https://github.com/googlefonts/gftools/issues/544> for a discussion of this.)
-   Tracking the changes in a list of commits also makes it easier to go back in the repository’s history and reverse or recover any step performed. One Thai type designer and web developer said this about his experience with Git:

> *I used to hate Git because I didn’t understand why I had to use it… until I started working with agile methods. Since then, I’ve kept using Git even on projects that I work on alone because the commit messages help me remember things I did and why I did them on each project.*

### Pulling and pushing: keep everything in sync

As well as making frequent commits, it is also suggested that you frequently *push* and *pull* the job done. *Pushing* means publishing the commits you have made locally to GitHub; making them visible to other contributors and visitors to the repository site. Conversely, *pulling* means integrating the changes made by others into your local work. Pushing and pulling is how you synchronize the copy of the repository on your computer with the remote origin hosted on GitHub.

What happens if you work on your project, but others have also worked on it in the meantime and pushed their changes? If multiple people have worked on exactly the same part of a file, then it is possible for the changes to *conflict*. Git is very good at working out the best way to resolve conflicts and integrate multiple sets of changes together, but the structure of font source files tends to make conflicts more likely.

Because of the above, it’s a good practice to

-   Creating your changes under a new specific branch for it
-   Beginning every editing session by pulling the latest state of the remote into your local repository branch
-   Frequently push your changes to make them available to others who may also be working on the project. It would be best to certainly push your changes when you have finished working for a time. Ideally, you push your changes to your forked repo first and then create a Pull Request to the main repository for others to be able to review your work before including it. Frequent pushes and pulls can help to avoid conflicts.

### Pull Requests: collaborate with others safely

**Pull Requests (PRs)** allow changes to a project to be merged into another project location (whether it is the remote upstream location or the fork origin). Typically, someone who wishes to contribute a change to a project will make a new [branch](https://docs.github.com/en/github-ae@latest/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches) in the <span class="mark highlight-red">origin</span> repo, where they make the change, and then request that this branch be “pulled” into the <span class="mark highlight-red">upstream</span> repo.

If a contributor has writing access to a repository, it is possible to skip the forking step and commit to a branch (often called `dev`) on the original project that can be later merged to the `main` branch. However, different projects have different workflows, so check what other contributors are doing to follow it, avoiding creating conflicts.

-   When posting a Pull Request, do not merge your own PR, but ask someone to review it.
-   Open PRs are linked to your fork; updating your fork by adding new commits will also add those commits to the PR.
-   [GitHub PR pages](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests) offer line-by-line commenting to allow highly specific discussions when necessary.

### Issues: manage bugs and tasks

If you run into a bug, question, or have a feature request for a project on GitHub, you can file an [**Issue**](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues) on that repo to alert the owners and get help.

-   You should practice good etiquette by first searching for existing issues. You may find that your question is already answered or that there is already an issue open that you can contribute to. Don’t forget to include *closed* issues in your search which aren’t immediately visible. Your problem may have been already discussed a while back.
-   If you report an unknown issue, project owners will value your input.
-   When addressing an issue on your own project, please do not close it when you think it is done; ask the person who reported it whether it is resolved, and close the issue once they have verified that it is fixed.

Check out the complete [Github’s documentation about issues](https://docs.github.com/en/issues) to know more about them.

### Github Actions: Continuous Integration testing of your work

**Continuous Integration** was originally defined as the process of merging the work of all developers of a project into the main source code repository regularly, up to several times per day. However, the term is mainly used for automated code testing and analyses, which are activated whenever a code merge occurs.

**GitHub Actions** allow automated actions to be run when specified things happen in the repository. For example, a repository containing a software project might define an Action that is run each time a new PR is made, which runs the project’s test suite.

Our [Google Fonts project template](upstream.md), recommended as a starting point for font repositories, defines some GitHub Actions that runs every time you push your changes to GitHub.

Using GitHub Actions means that you can always get an up-to-date view of your fonts and their readiness for production, relying on Google Font’s latest versions of build tools.

If you are not using our template, it is strongly suggested that you include at least a `Build & Test` action to check the building process is running ok to produce the fonts and test the resulting fonts with Fontbakery each time you push a change into a source file. Here is an [example of that action](https://github.com/Omnibus-Type/Texturina/blob/master/.github/workflows/build_and_check.yml).

### Using git with a code editor

You can also set git to use your preferred code editor for all git commit messages and similar.

If you are a *Visual Studio Code* user, run:

``` code
git config --global core.editor "code --wait" 
```

If you are an *Atom* user, run:

``` code
git config --global core.editor "atom --wait"
```

**Git on Mac**

On Mac OS X, the filesystem is "case insensitive," which means these two file names access the same file data:

`Montserrat-SemiBold.ttf`

`montserrat-semibold.ttf`

This often causes problems when renaming files. To configure git to be case-sensitive, run:

``` code
git config core.ignorecase false
```

------------------------------------------------------------------------

## Useful links

-   [Github Docs](https://docs.github.com/en)
-   [Learn the workings of Git, not just the commands](https://developer.ibm.com/technologies/web-development/tutorials/d-learn-workings-git/)
-   [Git for type designers by Dave Crossland](https://github.com/davelab6/git-for-type-designers)
-   [A short and friendly introduction book to git](https://abookapart.com/products/git-for-humans)
-   [Best practices for managing issues](https://blog.zenhub.com/best-practices-for-github-issues/)
