# Liferay front-end certification notes
Personal notes for the Liferay Front-end Certification

## Table of contents
* [Liferay introduction and first steps](#liferay-introduction-and-first-steps)
* [UI Techs](#ui-techs)
* [Theme development](#theme-development)

<br/>

## Liferay introduction and first steps

### Introduction to Front end development
- Fully customizable platform
- Front and back have wide variety of options for functional and stylistic customizations

#### Styling options
- Modules: include themes and layouts templates for global look and feel changes
- Templates: include specific customizations options for content, applications and email notifications

#### Developing with style
- You can work with a lot of tools to help the development and beautify your application

### Front end Development tools
#### Developing in liferay
- Is tool-agnostic
- Customizations and new features are deployed in modules
- Themes and layout templates are installed as modules
- needed to use plugins SDK
- Node.js, gulp and yeoman are used as default to create a liferay project

#### Tools for creating
- Node provides a platfrom for building and testing themes
- Yeoman easily create new projects
- Gulp helps to build and deploy projects also runs tasks with ` gulp build `

#### Development tools for modules
- JDK8: used to run liferay. Also need to set JAVA_HOME env variable
- Node.js: used to install liferay theme generator and dependencies
- Yeoman and gulp: global dependencies used to run liferay theme generator and gulp liferay theme tasks
- Liferay theme generator: used to generate themes and themelets
- Liferay tomcat bundle: used to view development changes on local env

#### Theme builder gradle plugin
- As an alternative for liferay theme generate it offers gradle plugin for theme development

### Setting up development env
- Install JDK8 (necessary to run and develop liferay)
- Default paths to install liferay
    - Mac: /Users/[your-user]/liferay
    - Linux: /home/[your-user]/liferay
    - Windows: C:\liferay
- Install node.js
- After install node you can install your project dependencies (npm i -g yo gulp)
- Install liferay theme generator (npm install -g generator-liferay-theme)
- Liferay Tomcat bundle
    - It contains all you need to run liferay;
- Creating bundle structure
    - Windows: C:\liferay\bundles
    - Mac/Linux: [user-home]/liferay/bundles
- Tomcat bundle
    - Windows: C:\liferay\bundles\liferay-dxp-digital-enterprise-[version]\tomcat-[version]\bin
    - Mac/Linux: [user-home]/liferay/bundles/liferay-dxp-digital-enterprise-[version]/tomcat-[version]/bin
    - To start tomcat just :
        - Windows: startup.bat
        - Mac/Linux: ` .catalina.sh `
- Activate liferay
    - After deploy your project you will need to activate it with your activation dev key
- Liferay Home
    - Is the primary location for any custom liferay properties or config files
    - In prod env this is will almost always be configured to specific location for being used for config files
    - portal-setup-wizard.properties is created in LIFERAY_HOME to store basic config properties
    - There are 2 ways to override properties:
        > Liferay's control panel or creating a file called portal-ext.properties in LIFERAY_HOME 
        also this file overrides properties from portal.properties
    - Liferay reads: portal.properties > portal-ext.properties > portal-setup-wizard.properties

<br/>

## UI Techs
### Introduction
- Liferay is based on an experience language called lexicon
- Lexicon describes how a user interacts with liferay (define liferay's look and feel)
- The goal of this experience language is to provide a unified experience through all aspects of a 
site or a application, this means offers a visual design where everything flows and fits together

### Lexicon CSS
#### What is it ?
- Is a web implementation of liferay's lexicon design language
- Provides style guidelines and best practices for designing web apps
- Have components and features to cover most use cases, also use reusable patterns
- Uses bourbon to handle with cross browser compatibility

#### Building a theme
- Look and feel come from a theme
- Lexicon base theme is used as default (contains bootstrap API extension and includes all of the default Lexicon CSS styles)
- Atlas is liferay's custom bootstrap theme

### Javascript in DXP
- Uses metal.js and jquery as default frameworks

### Alloy UI
- Is a front end library
- Is deprecated in current dxp version but can be maintaned and customized for legacy purposes

### Metal.js
- Js library to build UI components
- Uses ES2015 specification

### Custom displays with templates
- Using liferay to build UX means:
    - Lexicon CSS: provides Html, css and js for consistent design
    - Metal.js and Alloy UI: provides js components
    - Themes: using tehcs like lexicon css to provide a base look and feel across liferay
- Web content templates provides a direct way to define the UX
- Application display templates allow the freedom to control app UX

## Theme development
- Liferay uses themes to control UX
- A theme is a collection of CSS, JS, Images and templates
- This files are packaged up in a module that gets deployed on your liferay's instance
- Themes can be built using liferay Theme Generator in Yeoman
- You can export and import resources (To import: ` yo liferay-theme:import `)
- This import command do almost `liferay-theme`, except it pull in source files from an existing theme created using plugins sdk
- 

### What is NOT in a theme
- Themes just cant layout of applicatios on the page
- Menus and panels, styling for web content, customizing application displays
- This items above can be customized through templates or custom modules
- You can create modules to override:
    - The Product Menu
    - The Control Menu
    - Control Panel
    - Site Administration Panel
    - Simulation Menu
    - Some application displays

### Themelets
- Used to modify fwe areas of the theme like colors or fonts for example
- Have the same structure as a theme
- Can be created as npm packages and can be published to npm registry for easy sharing and reuse

### Theme contributors
- Provides a ay to package UI resources independent of a theme and include it on the page
- These have Ui resources to style Product Menu, control menu and simulation menu

### Tools to generathe themes
- Liferay theme generator is a yeoman generator that is used to create a theme boilerplate
    - There are four generators in generator-liferay-theme package
        - liferay-theme
        - liferay-theme:import
        - liferay-theme:layout
        - liferay-theme:themelet

- Liferay theme tasks is a set of gulp tasks for building and deploy your theme
    - This tasks are automatically installed when create a theme with the generator

- After the generation you will see this files and folders:
    - gulpfile.js, liferay-theme.json, node_modules, package.json, src, src/WEB-INF

### Build and deploy
- `gulp build`: compiles all source files into build directory and creates WAR file in the dist dir of your theme
- `gulp deploy`: runs all build tasks then deploys the generated war file to specified appserver
- `gulp watch`: watch for changes to theme source files
- `gulp init`: allows to specify your appserver path for use with the deploy task
- `gulp extend`: allows to set what base theme you like to extend your theme from, also let you add themelets to your theme
- `gulp status`: reports what base theme and themelets are implemented

### Key files for theme customization
- portal_normal.ftl: 

