# Heroku submodules buildpack
Adds support for GIT submodules to pipelines triggered through integrations (such as GitHub sync).

## Why another buildpack?
The [only buildpack](https://github.com/SectorLabs/heroku-buildpack-git-submodule) that
doesn't attempt to parse `.gitsubmodules` file manually and uses
Git instead unfortunately supports only SSH transfer. While this is the go-to way
of working with repositories locally, for CI a simple generated GitHub token passed in
an HTTPS request is usually simpler and preferable.

# How does it work
This buildpack takes a minimalistic approach and simply replaces SSH urls in the `
gitsubmodules` with HTTPS urls including the Git token stored as provided through `GIT_TOKEN`
environment variable.

# Installation
Add the buildpack to your app in Heroku pipeline and ensure it gets executed prior
any stack specific buildpack (such as Node.js buildpack).
