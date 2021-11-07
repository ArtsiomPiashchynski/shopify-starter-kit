# shopify-starter-kit

Starter theme and environment for the largest Shopify stores.
Repository makes it easier to work with the distribution of files in the project and automates some tasks.
Starter-kit based on Shopify Theme Kit and inspired by Shopify Slate and popular front-end frameworks (React, Vue).


Dev technologies and tools:
- Node.js
- Webpack
- Scss
- Eslint, Stylelint
- Prettier
- Git hooks with husky
- Shopify Theme Kit

---

## Table of contents
* [General info](#General-Info)
  - Shopify-starter-kit in [Basic mode](#basic-mode)
  - Shopify-starter-kit in [Advanced mode](#advanced-mode)
* [Getting Started](#Getting-Started)
* [Shopify Theme Kit](#Shopify-Theme-Kit)
    - [Configuration for themekit](#configuration-for-themekit)
* [File Structure Contract](#File-Structure-Contract)
  - [Folders descriptions](#folders-descriptions)
* [Commands](#Commands)



### General info

Shopify-starter-kit - it is a tool for comfortable team development of Shopify stores. 
The main goal of our team was to facilitate the start of new projects. 
For us, this means a quick start, the use of latest js standards and the use of  teamwork tools. 
We tried to collect the most important things  in one place -  this is how the shopify-starter-kit tool turned out.

Shopify-starter-kit is supported to 2 ways to use: [**basic**](#basic-mode) and [**advanced**]((#advanced-mode)) modes.

### Basic mode

Basic Mode provides a shopify starter kit to expand current functionality in current Shopify stores. 
For using this mode, you need to follow a few simple steps:
- Clone this repo to own project folder
- Install dependencies
- Clean src folder to keep only “scripts” folder
- Set actual data to the config.yml file
- Download current shopify store with command `npm run download:theme`
- Then all your store files will be placed into the `./theme` folder and everything is ready to go.

All new functionality (logic or styles) you can add directly to `./src/folder`. 
After the build they must be processed and placed in `./dist/assets` as build artifacts. 
We are using webpack: ‘mini-css-extract-plugin’ for build style files, and it should work at this point.

❗**NOTE**: after removing src folder you must get build error. It happens because webpack look at srctipts in the `./src/scripts` folder.
For fix this problem please open `webpcak.config.js` and remove the line with code: `...mkJsEntryPoints('src/scripts')`.


### Advanced mode

Advanced Mode provides a powerful suite for building Shopify stores.
This mode makes it easier to work with store pages. 
An advanced file structure allows you to separate the code between pages and load only the necessary functionality on the page, which increases the speed of the site. 
The structure also makes it easier to find and fix problems in the code, which speeds up the work of developers.

The advanced mode allows you to use all the features of the shopify-starter-kit:
1. separation of scripts and styles by pages.
2. Rigid component structure support
3. CLI for generating components of this structure
4. Separation of styles between pages, which allows to optimize loading of styles and scripts, code splitting
5. Using inside styles to speed up page loading
6. Using linting and code styling tools
7. Customized auto-corrections style code at the time of commit creation

All templates in src folder based on shopify starter theme and provide BEM naming methodology.
Advanced mode supported partial moving to new structure and all files in `./theme` folder will work totally fine.

❗**NOTE**: this mod is only suitable for those stores where no code changes are expected in the admin panel.
In advanced mode, at the moment there is no way to do full syncing with the existing store. 
All files downloaded from the existing store will be placed in the theme folder and there will be no replacement in the structure

---

## Getting Started

For starting core of project you need to do few simple steps:
1. Install frontend dependencies using npm or yarn. `npm install`
2. Then you need to create `config.yml` with correct settings and run command `npm run start`, or `npm run start:prod`.
3. Start you project using npm or yarn `npm run start` or `npm run start:prod`.

After build all changes will be applied into you selected Shopify theme.
Additional info you can find in the [Shopify Theme Kit](https://shopify.dev/tools/theme-kit) block.


## [Shopify Theme Kit](https://shopify.dev/tools/theme-kit)

Do not forget to check theme ids before launching theme kit watcher!
Watch starts a process that will watch the directory for changes and upload them to Shopify.

#### Configuration for themekit

After cloning the repo, copy `config.example.yml` and rename the copy to `config.yml`.
`config.yml` should contain production credentials (the current live theme) and development credentials (the current feature theme).

The current feature theme is the developers's own theme. Starting to work on a new feature the developer must change the **development** theme_id to the corresponding one every time.

For example:

```
development:
  store: [your-store].myshopify.com
  password: [your-api-password]
  theme_id: "[your-theme-id]"
  proxy: http://localhost:3000
```

The **production (live)** `theme_id` must be changed only after the release.
For example:

```
production:
  store: [your-store].myshopify.com
  password: [your-api-password]
  theme_id: "[your-theme-id]"
```

---

## Commands

The Shopify starter kit contains many commands for working on a project. 
Most of the commands for working with the theme are shortnames for the Shopify-themekit. 
However, most of it allows you to work with the project itself. Just a few basic commands are described below. 
A complete list of commands can be found in the `package.json` file.

#### Download
The commands for download existing shopify stores.
We have 2 command to download theme:

```bash
npm run theme:download
```

or 

```bash
npm run theme:download:prod
```

`theme:download` related to development environment part of your config.yml file, 
`theme:download:prod` related to production part.

#### Start
Start command will run webpack watcher, themekit deploy watcher and open development store in new browser window.
By default, this command runs only for development environment. You can modify it own remo after doing clone.

```bash
npm run start
```

---

#### Build
Build command prepare all files for deploy. 
All files will be processed and placed into `./dist` folder.
Supported development and production modes

```bash
npm run build
```
or
```bash
npm run build:prod
```
Build command it is shorthand for webpack. 
By default it starts with a progress flag.

---

#### Deploy
Command for upload all files from `./dist` folder to shopify store. 
Based on themekit functionality.

```bash
npm run deploy
```
or
```bash
npm run deploy:prod
```

Deploy command it is shorthand of few base commands: lint, build, and themekit deploy.


#### Create component
The Shopify-starter-kit provides the CLI to creating new entities in own structures.
CLI based on `yeoman` generator and can be started with the `yo` command. 
CLI supported to create style, script and liquid files for templates, section, snippets.
All templates already contain import scripts and styles inside liquid file.
You can change it in generator folder after clone shopify-starter-kit.

```bash
npm run gen
```

Customer templates temporally unsupported.

## File Structure Contract
This file structure contract is main feature of Shopify-starter-kit. 
It is used in advanced mode and doesn't support syncing with shopify store.   

```
/src
 ├── assets
 |    └── index.js
 ├── customers
 |    └── customer-template
 |         ├── section-name
 |         |    ├── section-name.js
 |         |    ├── section-name.liquid
 |         |    └── section-name.scss
 |         ├── customer-template.js
 |         ├── customer-template.liquid
 |         └── customer-template.scss
 ├── templates
 |    ├── common
 |    |    └── common-section-name
 |    |         ├── common-section-name.js
 |    |         ├── common-section-name.liquid
 |    |         └── common-section-name.scss
 |    └── template-name
 |         ├── section-name
 |         |    ├── section-name.js
 |         |    ├── section-name.liquid
 |         |    └── section-name.scss
 |         ├── template-name.js
 |         ├── template-name.liquid
 |         └── template-name.scss
 ├── scripts
 └── snippets
      └── snippet-name
           ├── snippet-name.js
           ├── snippet-name.luqiid
           └── snippet-name.scss
/theme
```

### Folders descriptions:

`./src/assets` - folder for assets. It might be images, fonts, any necessary files for shopify store. 
By default, files from this folder will be copied to dist without changes.
In production mode images will be compressed.

`./src/customers` - folders for customer templates. Can be empty.

`./src/templates` - include all store pages with necessary styles and scripts. All page should include own sections. 

`./src/snippets` - are regular snippets with own styles. Style of each snippet can be included in section, template or theme. By default snippets styles or scripts are unwatched.

`./src/scripts` - the main folder functionality. All js files in this folder will be processed with wabpack and placed in `dist/assets`. Can't be empty.

`./theme` - folder for all shopify files, used in base mode. 
All files from this folder will be copied to dist without changes. 
It is recommended to use the `npm run gen` command to add new components
.

---

# Contributing
For help on setting up the repo locally, building, testing, and contributing please see [CONTRIBUTING.md](https://github.com/spiral/shopify-starter-kit/blob/master/CONTRIBUTING.md).

# Code of Conduct
All developers who wish to contribute through code or issues, take a look at the [CODE_OF_CONDUCT.md](https://github.com/spiral/shopify-starter-kit/blob/master/CODE_OF_CONDUCT.md).

# License
Copyright (c) 2021 SpiralScout. See [LICENSE](https://github.com/spiral/shopify-starter-kit/blob/master/LICENSE) for further details.
