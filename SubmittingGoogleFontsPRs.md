# Uploading fonts to google/fonts

This guide will assist users in uploading fonts to the [google/fonts](https://github.com/google/fonts) repository.


## Uploading

1. Make sure your font family has its own Github repo and complies with the [checklist](https://github.com/googlefonts/gf-docs/blob/master/ProjectChecklist.md).
2. Create your own fork of https://github.com/google/fonts and clone your fork locally.
3. Get a [BrowserStack account](https://www.browserstack.com).
4. Download and install [gfdispatcher]().
5. run `gfdispatcher https://www.github.com/user/yourfontfamily /ttf-fonts-dir-in repo`

For https://github.com/googlefonts/anaheimFont the gfdispatcher command will be

```
gfdispatcher https://github.com/googlefonts/anaheimFont /fonts/ttf
```


In 2018, we plan to make the uploading process simpler by building a webapp for users to upload their fonts.


## How GF Dispatcher works

1. Download fonts and license file from upstream font repo
2. Package downloaded files into a [family dir]() located in the user's local google/fonts repo
3. Generate the family dir's METADATA.pb file using googlefonts/tools
4. QA the fonts using fontbakery and diffbrowsers
5. Send a PR to the user's google/fonts fork.
6. If the user is happy with the pr, he can resend the pr to google/fonts
7. google/fonts PR gets reviewed


## What makes for a successful pull request?

Our QA tools determine whether a pull request is accepted or not. Reviewers also have the power to accept PRs even if some tests are failing.