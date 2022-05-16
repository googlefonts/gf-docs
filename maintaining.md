# Maintaining your font repo
{:.no_toc}

> <span class="icon">🐰</span>  A font is not finished just because it has been released. From time to time, you may want to update your design; users may find and report issues with the font that need to be addressed, or Google may commission you to update your own or someone else’s font.
> This guide will help designers to adopt good habits while maintaining their work within a GitHub repository.
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Recommendations

Here are a few principles regarding font maintenance and upgrades:

-   **Follow the rules regarding font upgrades.**

    This ensures that your upgrade does not cause “visual regressions.” See the [font upgrades](onboarding.md) section.
-   **Engage with any issue reported via the GitHub issue tracker.**

    When you begin working on an issue, ask questions of the issue reporter if you need clarification; if you do not need clarification, at least comment on the issue to let the reporter know that you have received the issue, verified it, and are working on it.
-   **Create issues in your own repo to track your tasks and progress.**

    The purpose of engaging with issue tracking is to provide greater public visibility into what the upgrade addresses and how it is progressing. Because of this, you may also wish to create issues yourself, even if the repository is your own, to track the changes that you plan to make. This will also help people planning to report an issue that they have found; they may be about to report an issue that you are already aware of.
-   **Make Pull Requests to your own repository.**

    Ideally, when starting work on a font upgrade, create a new branch of the repository, and deliver the upgrade as a Pull Request. You can do this even if you are making and merging a Pull Request in your own repository. This helps to group together all of the commits which form part of the same upgrade.
-   **Tackle one issue at a time.**

    In Git, commits are used to identify discrete changes to a project. As much as possible, a single commit should address a single issue. Try to develop the habit of making frequent small commits instead of infrequent large ones!

    Starting from a “clean” checkout of the repository, make a change to the source files which addresses a single issue, and then commit this change before working on the next part of your upgrade.
-   **Link commits to issues.**

    When you commit a change that addresses an issue, mention the issue ID in the commit message:

    -   If the commit partially addresses issue \#1234, mention “#1234” somewhere in the first (title) line of the commit message. This will link the commit to the issue, and will provide further visibility to the issue reporter into the fact that you are working on it.

    

    -   If the commit fixes issue \#1234, use the words “fixes \#1234” or “closes \#1234”. This will link the commit to the issue, and will also automatically close the issue when the commit is merged.

    

    -   Sometimes a change that you make will affect multiple issues. If you need to address multiple issues in a single commit, mention all issue IDs in the same commit message.
-   **Clearly identify your releases**.

    When you have finished all the changes you plan to make for a particular upgrade, update the version number in the font and commit that as a separate commit. This will be the commit that is “tagged” as the new font release. If you opened a pull request for this upgrade, now merge it into the main branch. Finally, create a new release using the GitHub “Release” facility on the right of the main repository page.

------------------------------------------------------------------------

## Useful links

-   [Managing release with GitHub](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)
-   [Using key words in GitHub](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue)
