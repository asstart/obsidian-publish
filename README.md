---
tags:
- main 
---

# OBSIDIAN-PUBLISH-ACTION

## What is it for?

It's a GitHub Actions, that can help to publish publish notes from [Obsidian](https://obsidian.md/) to [GitHub Pages](https://pages.github.com/).

This project uses [slightly modyfied version](https://github.com/asstart/just-the-docs) of theme [just-the-docs](https://github.com/just-the-docs/just-the-docs). Read about modifications [here](https://github.com/asstart/just-the-docs/blob/main/docs/fork-features/fork-features.md).

## Features

- Publish notes that marked with specific tag or publish all notes
- Transforming and resolving obsidian style links to a common markdown link: `[[Link to note|Alias]]` => `[Alias](Link to note)`
- Transforming, resolving and copying images `![[Link to img|Alias]]` => `![Alias](Link to img)`. Other media types will be transformed and copied as well, but will be displayed just as link for now.
- Publish under [GitHub Pages](https://pages.github.com/) domain or under a custom domain
- Publish to the same repositrory that holds obsidian or to a separate
- Publish from either public or private repository

### Features provided by Just-The-Docs theme

- Search across all published notes
- Auto-generated ToC for folders
- Heading anchor links
- Dark/light theme

## Quick Start

1. Configure Obsidian backup to a GitHub repository(E.g. [Obsidian Git Plugin](https://github.com/denolehov/obsidian-git) can be used)

> For this quick start guide, repository must be public. To get know how to publish from private repository look "All settings reference"

2. Configure GitHub action for deploying Obsidian notes as GitHub Actions site

    2.1 Create following folders in the root of the obsidian directory: `.github/workflows`

    2.2 Create file `publish.yml` in the `.github/workflows`

    2.3 Configure `publish.yml`

    ```yaml
    name: Publish

    on: [workflow_dispatch]

    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          - name: "publish obsidian"
            uses: asstart/obsidian-publish@main
            with:
              publishAll: true
    ```

3. Go to "Actions" tab and run "Publish Action"

## All Settings Reference

|Option|Required|Default value|Description|
|---|---|---|---|
|targetRepo|false|Same repository that holds Obsidian backup|Repository where notes will be published|
|targetBranch|false|gh-pages|Branch where notes will be published<br><br>**Be carefull with this settings. During publish process branch with name from this property will be created as orphan branch and force pushed, so you may lose your changes in a particular branch. Action does check that branch neither default branch nor branch that used to start action, but other branches can be corrupted**|
|sourceFolder|false|Root folder in the Obsidian backup|Folder in the Obsidian backup that will be used as root for searching files|
|targetFolder|false|Root folder in the the target repository|Can be '.' or 'docs' because GitHub Pages allows only this values|
|tags|false|no tags by default|List of tags in format `tag1,tag2` that will be published|
|publishAll|false|false|If specified `true`, `tags` option will be ignored and all pages will be published|
|token|true|No default value|Personal Access Token to get access to push to a target repository<br><br> This property required if `targetRepo` doesn't match with repo that contains Obsidian backup<br><br>[How to create personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)|
|colorSchema|false|light|Color schema of the site. Available values: dark, light|
|domain|false|No default value|If domain specified, site will be published under a custom domain insted of *.github.io|
|jekyllTitle|fasle|Name of your repository with Obsidian backup|Here can be specified site label (string in the left top corner above the side bar)|

#### Example

```yaml
name: Publish Same Repo Full Conf

on: [workflow_dispatch]

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: "publish"
        uses: asstart/obsidian-publish@main
        with:
          token: ${{ secrets.OBISDIAN_PUBLISH_TOKEN }}
          targetRepo: asstart/obsidian-publish-action-test
          targetBranch: gh-pages-fullconf
          sourceFolder: .
          targetFolder: .
          tags: example
          publishAll: false
          jekyllTitle: Full Conf Example
          colorSchema: dark
```