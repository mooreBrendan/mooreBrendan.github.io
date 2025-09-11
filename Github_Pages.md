# GitHub Pages

## Purpose
GitHub Pages is a service offered by GitHub where they will give you a web-accessible webpage hosted by GitHub.  This allows you to have a webserver connected to the internet without exposing any of your devices to the internet.  This Website is running on GitHub pages.

This guide will be using [[Obsidian]] to create markdown files with the website's info and then GitHub actions will run mkdocs to convert the markdown files into static html files.

## Setup
In order to use GitHub Pages, you first need to create a repository named "{x}.github.io" where "{x}" is your GitHub username.  You then will need to setup GitHub Actions to add the files in the repository to the website.

### Sub-repositories
You can set up your new GitHub pages repository to be a sub repository of another repository, in this case, the repository that is running the obsidian docker container. 

### MKDOCS File
To use mkdocs, you will need to create a ".yml" file in the same folder as all of the markdown files. 
```
site_name: Be Moore Homelab

theme:
    name: 'material'
    palette:

    # Dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      primary: black
      accent: light blue
      # toggle:
      #   icon: material/toggle-switch
      #   name: Switch to light mode


# Extensions
markdown_extensions:
  - pymdownx.highlight
  - footnotes
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - pymdownx.superfences
  # - attr_list
  # - pymdownx.arithmatex
  # - pymdownx.superfences
  # - pymdownx.details
  # - pymdownx.magiclink
  # - pymdownx.tasklist:
  #     custom_checkbox: true
#  - pymdownx.emoji:
#      emoji_generator: !!python/name:pymdownx.emoji.to_svg
  # - admonition
  - toc:
      permalink: true

nav:
  - Introduction: 'README.md'
  - 'VMWare ESXi.md'
  - 'Docker.md'
  - 'Dashy.md'
  - 'Github_Pages.md'
  - 'HomeAssistant.md'
  - 'NGinx_Server.md'
  - 'NTFY.md'
  - 'PeaNUT.md'
  - 'PiHole.md'
  - 'Portainer.md'
  - 'Traefik.md'
  - 'Uptime Kuma.md'
  - 'Rick': 'https://www.youtube.com/watch?v=dQw4w9WgXcQ&list=RDdQw4w9WgXcQ&start_radio=1'
exclude_docs: |
  .gitignore
  mkdocks.yml

plugins:
  - search
  - roamlinks 
```

### GitHub Actions File
To setup the actions create a ".yml" file in the path of your repository "/.github/workflows/".
Here is the github actions file I use.  You will need to replace the "{username}"'s with your GitHub username:
```
name: mkdocs convert

#detect when a commit is pushed and then run the action
on:
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: write
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  #the command to convert from markdown files to html files
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: 3.x
      #install mkdocs into the action container a nd run it
      - name: Build static files
        id: build
        run: |
          pip install mkdocs-material
          pip install mkdocs-roamlinks-plugin
          mkdir docs
          cp *.md ./docs/
          mkdocs gh-deploy --force
      #uploads the static html to the github actions so that other actions can use them
      - name: Upload static files as artifact
        id: deployment
        uses: actions/upload-pages-artifact@v3 # or specific "vX.X.X" version tag for this action
        with:
          path: /home/runner/work/{username}.github.io/{username}.github.io/site

  #actually deploys the html files to the GitHub pages site
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

## Verification

## DNS Name