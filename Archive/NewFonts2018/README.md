# Uploading fonts to google/fonts

This guide from May 2018 explains how to upload new font families to Google Fonts, by contributing via Pull Request to the [google/fonts](https://github.com/google/fonts) repository.

## Uploading

1. Make sure your font family has its own Github repo and complies with the [checklist](https://github.com/googlefonts/gf-docs/blob/main/ProjectChecklist.md)
2. Create your own fork of https://github.com/google/fonts and clone your fork locally
3. Get a [BrowserStack "open source" account](https://www.browserstack.com/opensource)
4. Download and install [gfdispatcher]().
5. Run `gfdispatcher GITHUB-REPO-URL /path-containing-ttfs`. Eg, for <https://github.com/googlefonts/anaheimFont> the command will be:

    gfdispatcher https://github.com/googlefonts/anaheimFont /fonts/ttf

Note that (1) could be made more simple with a set of Font Bakery checks for repos; and this whole uploading process could be more simple with a web service that runs the dispatcher remotely. 


## How GF Dispatcher works

1. Download fonts and license file from upstream font repo
2. Package downloaded files into a [family dir]() located in the user's local google/fonts repo
3. Generate the family dir's METADATA.pb file using googlefonts/tools
4. QA the fonts using fontbakery and diffbrowsers
5. Send a PR to the user's google/fonts fork.
6. If the user is happy with the pr, he can resend the pr to google/fonts
7. google/fonts PR gets reviewed by GF team
8. PR is merged by GF team
9. google/fonts `main` branch is pushed to GF sandbox API and Directory servers and checked
10. google/fonts `main` branch is pushed to GF production API and Directory servers


## What makes for a successful pull request?

The biggest factor today to determine whether a pull request is accepted or not is these QA tools.
The GF Reviewers team has discretion to accept PRs even if some checks are failing.
