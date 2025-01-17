# Geek Blog

> Geek blog built with [Gridsome](https://gridsome.org) that uses Markdown for writing content

## Built with
- [Gridsome 0.7](https://gridsome.org/)
- [Windi CSS 3](https://windicss.org/) (top of Tailwind CSS v2)

## Features
- [x] Markdown Parser (for creating post and pages)
- [x] [Blog Post](blog)
- [x] [Pages](docs)
- [x] Taxonomies: Categories and Tags
- [x] Featured Image (recommended size 16:9 ratio)
- [x] Code Syntax Highlighter ([shikijs](https://github.com/shikijs/shiki))
- [x] Global Search for Posts and Pages ([fuse.js](https://fusejs.io/))
- [x] Post Excerpt
- [x] Recent Post
- [x] Related Post
- [x] Approximate read time for posts
- [x] Pagination for Blog, Tags, Categories
- [x] Github Comments (issue based) ([VSSUE](https://github.com/meteorlxy/vssue))
- [x] SEO Friendly
- [x] Sitemap
- [x] RSS Feed
- [x] TOC
- [x] Google Analytics
- and more in future maybe 🥳

## Todo
- VSSUE update css for dark theme support (pull-request is appreciated 😝 )
- Update README.md with Installation

## Demo URL
https://gridsome-geek-blog.netlify.app
or check my blog
https://codedine.com

# Installation

There are several ways to to install this theme.

## Using the Gridsome CLI

The easiest way to install this theme or a Gridsome theme in general is by using their CLI tool.

If you don't already have it installed, simply run:

```bash
npm i -g @gridsome/cli
```

After that run `gridsome -v` to verify that the tool is working.

If everything is working as expected, run the following command:

```bash
gridsome create your-project-name https://github.com/xqsit94/gridsome-geek-blog
```

This command creates a folder named `your-project-name` in your current working directory, clones the repository and automatically installs the dependencies.

If everything is downloaded and installed you can now run `npm run develop` which starts the development server and bundles all assets. After bootstrapping has finished, head to `http://localhost:8080` to view your freshly created site!

## Installing manually

To install this theme manually you need to:

1. Clone the repository
2. Install the dependencies

To clone the repository simply run:

```bash
git clone https://github.com/xqsit94/gridsome-geek-blog.git
```

After cloning the project, change to the project you just created.

```bash
cd gridsome-geek-blog
```

Now you only need to install the dependencies.

Using npm:
```bash
npm install
```

Or by using yarn:
```bash
yarn
```

After all dependencies are installed you can now run `npm run develop` to start the development server!

## Configuring Environmental Variables
This boilerplate helps to configure important data using `.env`. All you need to do is just copy `.env.example` to `.env`
and fill the data for following variables

```dotenv
SITE_NAME=
SITE_TITLE=
SITE_DESCRIPTION=
SITE_AUTHOR=
SITE_AUTHOR_URL=
SITE_FAVICON_PATH="./static/images/favicon.png"

GRIDSOME_BASE_URL=http://localhost:8080
GRIDSOME_VSSUE_OWNER=
GRIDSOME_VSSUE_REPO=
GRIDSOME_VSSUE_CLIENT_ID=
GRIDSOME_VSSUE_CLIENT_SECRET=
GRIDSOME_VSSUE_PERPAGE=
GRIDSOME_VSSUE_CREATE_ISSUE=

GOOGLE_ANALYTICS_ID=
```

## More Configuration
You can edit other configuration values inside `gridsome.config.js`