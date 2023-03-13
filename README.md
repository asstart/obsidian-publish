# OBSIDIAN-PUBLISH-ACTION

> Project is under development

## What is it?

It's a GitHub Actions, that can help to publish publish notes from [Obsidian](https://obsidian.md/) to [GitHub Pages](https://pages.github.com/)

## Features

- Publish notes that marked with specific tag or publish all notes
- Transforming and resolving obsidian style links to a common markdown link: `[[Link to note|Alias]]` => `[Alias](Link to note)`
- Transforming, resolving and copying images `![[Link to img|Alias]]` => `![Alias](Link to img)`. Other media types will be transformed and copied as well, but will be displayed just as link for now.
- Publish under [GitHub Pages](https://pages.github.com/) domain or under a custom domain
- Publish to the same repositrory that holds obsidian or to a separate

## Quick Start

> This section isn't finished yet

1. Configure Obsidian backup to a GitHub repository(E.g. [Obsidian Git Plugin](https://github.com/denolehov/obsidian-git) can be used)
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
            uses: asstart/obsidian-publish-jsaction/actions/compose@main
            with:
              token: ${{ secrets.OBISDIAN_PUBLISH_TOKEN }}
              publishAll: true
              targetFolder: '/docs'
    ```
3. Go to "Actions" tab and run "Publish Action"

## All Settings Reference

|Option|Required|Default value|Description|
|---|---|---|---|
|targetRepo|false|Same repository that holds Obsidian backup|Repository where notes will be published|
|targetBranch|false|gh-pages|Branch where notes will be published<br>Make warning about history cleanup and force push|
|sourceFolder|false|Root folder in the Obsidian backup|Folder in the Obsidian backup that will be used as root for searching files|
|targetFolder|false|Root folder in the the target repository|Can be '.' or 'docs' because GitHub Pages allows only this values. If targetRepo is the same as source, can be only 'docs'|
|tags|false|no tags by default|List of tags in format `[tag1,tag2]` that will be published|
|publishAll|false|false|If specified `true`, `tags` option will be ignored and all pages will be published|
|token|true|No default value|Token to get access to push to a repository<br>Add instruction how to create|
|colorSchema|false|light|Color schema of the site. Available values: dark, light|
|domain|false|No default value|If domain specified, site will be published under a custom domain insted of *.github.io|