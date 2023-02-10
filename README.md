Build Status:
[![Actively Maintained](https://img.shields.io/badge/Pantheon-Actively_Maintained-yellow?logo=pantheon&color=FFDC28)](https://pantheon.io/docs/oss-support-levels#actively-maintained-support)

## Status Update: 2023 - January/February

Pantheon's Docs team has suspended publishing all updates to [pantheon.io/docs](https://pantheon.io/docs) following the [4 January CircleCI incident](https://circleci.com/blog/january-4-2023-security-alert/).

We took the incident as an opportunity to revoke and rotate tokens and auths in a variety of places. Doing so showed us that the way that we were publishing changes to the site wasn't ideal and that the docs site is a perfect candidate for Pantheon's [Front-End Sites offering](https://pantheon.io/docs/guides/decoupled-sites/), currently in Early Access.

We're looking forward to re-deploying on the Front-End architecture sometime in mid-February. Until then, changes that have been merged to `main` [since 4 January](https://github.com/pantheon-systems/documentation/pulls?q=is%3Apull+is%3Amerged+updated%3A%3E2023-01-04+sort%3Aupdated-desc+) are available in the [GitHub repository code](https://github.com/pantheon-systems/documentation) and can be built locally using the [steps below](#local-installation).

We'll remove this notice and update the [Changelog below](#changelog) after we've migrated the site.

Pantheon Documentation
======================

https://pantheon.io/docs/

This repository contains the [Pantheon](https://pantheon.io) documentation as well as the tools to build local test environments.

## Changelog

 - 2019/08/05: We've relaunched the project using [Gatsby](https://www.gatsbyjs.org) for faster development, and _much_ faster page speed.

### Contributing
Our docs are written in [Markdown](https://daringfireball.net/projects/markdown/), extended with [MDX](https://github.com/mdx-js/mdx) components. The pages live in `source/content`. Read [CONTRIBUTING](<CONTRIBUTING.md>) for more details on contributing documentation improvements.

### Style Guide
Read [our Style Guide](https://pantheon.io/docs/style-guide) for our guidelines on how to write documentation.

## Local Installation

### Prerequisites
  - MacOS or Linux system (untested with Bash on Windows)
  - [Node.js](https://nodejs.org/en/)
  - [NVM](https://github.com/nvm-sh/nvm#installing-and-updating)
  - Gatsby CLI:

    ```bash
    npm install -g gatsby-cli
    ```

  - Alternatively, you can use [Lando](https://docs.lando.dev). Use Lando to bypass installing Node.js and the Gatsby CLI on your local machine. Lando requires a Docker version in the `2.1.0.0` - `3.1.99` range.

#### Mac Steps

This list of steps should work on a Mac with [Homebrew](https://brew.sh/):

```bash
brew install node
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
nvm install 14
npm install -g gatsby-cli
```

### Get the Code

Fork and clone this repository:

```bash
git clone git@github.com:pantheon-systems/documentation.git
cd documentation
```

### Create a GitHub API Token

We use the [gatsby-remark-embed-snippet](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-remark-embed-snippet) to use files from GitHub in our docs. Before you can build a local development site, you need to provide a GitHub token to the environment:

1. Log in to GitHub and go to <https://github.com/settings/tokens>
1. Click **Generate new token**.
1. Give the token a name, expiration, and description.
1. Select your GitHub user as the resource owner.
1. For repository access, select **Only select repositories** and select your fork of this repository.
1. Under Repository permissions, choose **Access: Read-only** from the **Access** dropdown button.
1. Click **Generate token**.

#### GitHub Tokens (classic)

Alternatively, if you'd rather create a classic-style token:

1. Log in to GitHub and go to <https://github.com/settings/tokens>
1. Click **Generate new token (classic)**
1. Give the token a name and click the **public_repo** checkbox, then the **Generate Token** button at the bottom
1. Copy the token to your clipboard
1. In the root `documentation` directory, create a new file called `.env.development` and add (replacing `$TOKENHASH` ):

    ```bash
    GITHUB_API=$TOKENHASH
    ```

## Install With The Gatsby Cli

From the `documentation` directory:

```bash
npm ci
```

### Run

Still in the `documentation` directory:

```bash
npm start
```

Use your local browser to navigate to `localhost:8000/`.

Locally saved updates to docs are automatically refreshed in the browser.

## Install With Lando

Alternatively, you can use [Lando](https://gist.github.com/tormi/a8b8fc39f9481373b24dc94cb8d2ee31). The `lando start` command initiates the app, installs node dependencies, and starts the `gatsby develop` server for you:

```bash
lando start
```

You can view the local environment at `localhost:8000/`. Updates to docs are automatically refreshed in the browser.

## Testing

We include several tools to test that new content doesn't break the documentation. Most of these tests are performed automatically by our continuous integration service, but pull requests created from external contributors aren't included in CI tests. If you want to manually test your branch, you can execute the following tests within the Docker container.

### Merge Conflicts

To check for merge conflict messages accidentally committed into the docs, run `merge_conflicts.sh` from `scripts`.
