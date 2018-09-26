# Liferay front-end certification notes
    - Personal notes for the Liferay Front-end Certification

## Table of contents
* [Liferay introduction and first steps](#liferay-introduction-and-first-steps)
* [UI Techs](#ui-techs)


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
#### Install JDK8 (necessary to run and develop liferay)

#### Default paths to install liferay
- Mac: /Users/[your-user]/liferay
- Linux: /home/[your-user]/liferay
- Windows: C:\liferay

#### Install node.js

#### After install node you can install your project dependencies (npm i -g yo gulp)

#### Install liferay theme generator (npm install -g generator-liferay-theme)

#### Liferay Tomcat bundle
- It contains all you need to run liferay;

#### Creating bundle structure
- Windows: C:\liferay\bundles
- Mac/Linux: [user-home]/liferay/bundles

#### Tomcat bundle
- Windows: C:\liferay\bundles\liferay-dxp-digital-enterprise-[version]\tomcat-[version]\bin
- Mac/Linux: [user-home]/liferay/bundles/liferay-dxp-digital-enterprise-[version]/tomcat-[version]/bin
- To start tomcat just :
    - Windows: startup.bat
    - Mac/Linux: ` .catalina.sh `

#### Activate liferay
- After deploy your project you will need to activate it with your activation dev key

#### Liferay Home
- Is the primary location for any custom liferay properties or config files
- In prod env this is will almost always be configured to specific location for being used for config files
- portal-setup-wizard.properties is created in LIFERAY_HOME to store basic config properties
- There are 2 ways to override properties:
    - Liferay's control panel or creating a file called portal-ext.properties in LIFERAY_HOME
    - This file overrides properties from portal.properties
- Liferay reads: portal.properties #### portal-ext.properties #### portal-setup-wizard.properties

## UI Techs