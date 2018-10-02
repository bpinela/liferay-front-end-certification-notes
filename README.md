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
- portal_normal.ftl: The main HTML source file There are a number of HTML files we can modify, but the portal_normal 
file contains the main structure of the page.
- _custom.scss: The file used for custom, global styling Developers can style a number of elements in different files 
as seen in the build folder. These files are combined into one file called main.css, which is then linked
into the theme’s <head>, on every page.
- main.js: Developers should place their custom JavaScript in this file, which is loaded on every page.
- liferay-look-and-feel.xml: Developers can add different settings, such as Theme Settings, Color Schemes,
and packaged Layout Templates in this file

### Controlling page structure
- Themes have control over every aspect of the page.
- Every site page in Liferay breaks down to three major customizable sections as we see in the portal_normal.ftl:
    - The Banner Section: Includes the top part of a page with its sections
    - The Content Section: Includes breadcrumbs and code to render layouts and applications
    - The Footer Section: Includes the bottom of the page that can be customized

### FTL (Freearker templating language)
- Interpolations: these are basic variable expressions that will be
evaluated, and the result put on the page:
${default_url}
- Directives: special tags that tell FreeMarker to do something that doesn’t
always result in a visual difference:
<#assign default_url = "http://spaceprogram.liferay.com/" />

### What makes up a theme
- Let’s take a look at what’s in the theme and find our place:
    - fonts will contain any necessary custom fonts for the theme.
    - images will contain images that will be used in the theme.
    - js will contain JavaScript referenced in the themes templates.
    - layouttpl will contain any custom Liferay Layout Templates for the theme.
    - templates will contain the FreeMarker templates that provide the HTML structure of the theme.

TEMPLATES AT OUR DISPOSAL
When an HTML page in Liferay is generated and sent to the browser, a
few templates are used to create the source HTML:
portal_normal.ftl: This is the main HTML document for every page,
containing the <html>, <head>, and <body> tags.
portlet.ftl: This contains the HTML that surrounds each application
on the page.

We can include templates in other templates to modularize our page
structure.
For instance, we can separate our page navigation, body, and footer into
different files.

PAGE COMPOSITION
We’ll build the main page using two additional templates.
This will make the structure easier to maintain and modify.
Our main page will be laid out with portal_normal.ftl:
HTML Head
JavaScript
Stylesheets
Body
Header
Navigation - we’ll include navigation.ftl
Page layout - controlled by a Layout Template
Footer - we’ll include footer.ftl

MAKING A STATEMENT
You’ll see all of our basic FreeMarker syntax in this template.
Text and URLs that Liferay gives us are in variables:
${site_name}
We check to see if navigation is enabled using the <#if /> directive:
<#if has_navigation>
...
</#if>
We also check if we’re supposed to show the Site name:
<#if show_site_name>
...
</#if>

NCLUDING EXTERNAL TEMPLATES
A useful directive for us is <#include />.
This takes a template file name, and includes it in your template.
It’s the same as copying and pasting the contents:
FreeMarker looks in the same location as the current template.
If it finds the file, it adds the content of the template where the
<#include /> directive is.
The whole template file is processed, with this new template code in
place.
This makes separating our navigation into another file easy:
<#include "${full_templates_path}/navigation.ftl" />
This also uses the full_templates_path variable Liferay gives to us.

USEFUL VARIABLES
We’re already seeing some helpful tools available in our theme
templates.
Some of the useful default variables include:
site_name: Returns the name of the Site, usually set by the Site
Administrator
site_default_url: Returns the URL to the current Site
site_logo: Returns the URL to the Site logo image, usually set by the
Site Administrator
the_title: The title of the application being displayed
full_templates_path: An absolute path on the file system to the
folder containing the templates in the theme, useful for including external
files.

ADDING TEMPLATE FUNCTIONALITY WITH MACROS
Macros allow you to assign template fragments to a variable, which
makes them helpful for creating reusable pieces of template code.
They will look very similar to normal tags:
<@liferay.language_format />
Instead of starting with a #, they begin with a @.
Like directives, they’re used to perform different functions.
When the page is rendered, the macro is replaced with the template
fragment.

DEFAULT LIFERAY MACROS
Liferay provides a few default macros for integrating the most commonly
used applications in your theme (e.g., search, breadcrumbs, user
personal bar).
There is also a set of default macros for users seeking to make their site
more friendly to foreign languages.
You’ll find default Liferay macros used all around our templates.

- Defaul Macros:
    - breadcrumbs: Adds the Breadcrumbs portlet with optional preferences
    - control_menu: Adds the Control Menu portlet
    - css: Adds an external stylesheet with the specified file name location
    - date: Prints the date in the current locale with the given format
    - js: Adds an external JavaScript file with the specified file name source
    - language: Prints the specified language key in the current locale
    - language_format: Formats the given language key with the specified arguments
    - languages: Adds the Languages portlet with optional preferences
    - navigation_menu: Adds the Navigation Menu portlet with optional preferences and instance ID
    - search: Adds the Search portlet with optional preferences
    - user_personal_bar: Adds the User Personal Bar portlet

FOOTER DETAILS
A few new directives show up in the footer:
<#assign /> lets us assign a value to a variable.
Here, we’re using it to call methods on objects, and store the result:
<#assign VOID = freeMarkerPortletPreferences.setValue(...) />
When the setValue() method returns, that value is stored in VOID.
We don’t use VOID anywhere on the page, so that value never gets
displayed.
This is a nifty way to keep return values from being added to the page.
<@liferay.navigation_menu /> is a macro that adds the Navigation
application to the page.

FILLING IN THE FRAMING
With our basic templates in place, we’ve now provided the basic
structure for styling.
After modifying the core portal_normal.ftl:
We have a custom navigation that complements our branding
We have a custom footer section in place that we can easily modify later
We can add or remove some of the basic features using macros
We can now start applying our custom styles to make the new page
structure fit our vision.

Adding fonts
Our font SCSS file uses mixins to simplify adding fonts:
@include font-face(...);

Taking advantage of atlas styles
To include additional styles that are used in the classic theme, we can
modify our aui.scss file to include the Atlas theme.

CUSTOMIZING ALL THE SCSS
The main file for adding any custom style changes is the
_custom.scss file.
This is where we can add our global styling for things like:
Background color
Accent colors
Applications Styling
Etc.

MODULARITY WITH STYLE
We’ve added the partials folder to organize each CSS component we
want to customize.
Each aspect of the platform we want to change will be it’s own file.
For example, we want to change the button styles in our theme, so we
have a _buttons.scss file in the partials folder.
All we need to do from there is import the files into our _custom.scss
file.
This will make maintanence and organization much better for any theme
scss in the future.

INHERITANCE
Our _custom.scss is a good place to some other useful SASS features.
Sometimes we need to apply styles to areas of the DOM that are
logically related.
For instance, a span inside a div, all wrapped in another div.
It’d be nice to show this hierarchy.
Sass lets you do this:
.portlet-layout {
&.row {
margin: 0;
.col-md-12 {
padding: 0;
}
}
}
Instead of .portlet-layout.row, we can use & to show the
relationship.

MODIFYING DEFAULT STYLES
The base build folder includes a number of default styles that can be
modified.
These sections include things like application, navigation, layout styles,
and more.
This folder also includes the portlet folder with all the default styles.
To modify application styles in a theme, you can simply copy that folder
and the relevant .scss files into your theme’s src folder.
We already have the folder, so we can add some variable modifications
for our applications.

## Adding custom js
ALLOYUI, YUI, AND JQUERY
If you’re familiar with YUI or jQuery, main.js looks pretty familiar.
AlloyUI is avaliable through AUI(), much like YUI() or $().
Just like a jQuery page might have:
$(document).ready(function () {
// Do stuff...
});
AlloyUI (much like its parent YUI) uses:
AUI().ready(function (A) {
// Do stuff...
});
You can see syntax comparison at the AlloyUI Rosetta Stone:
http://alloyui.com/rosetta-stone/
While AlloyUI and jQuery are available if you want to use them, you can
also include any other JavaScript framework in your theme.

METAL.JS AND ECMASCRIPT 2015
Along with AlloyUI, the S.P.A.C.E. theme is also built with another of
Liferay’s default libraries: Metal.js.
As mentioned in a previous module, Metal.js is a JavaScript library that
uses the ECMAScript 2015 language specification.
By taking advantage of ECMAScript 2015 features like classes, modules
and arrow functions, we can build modern, flexible UI components.
The top_search.es.js uses Metal.js and ECMAScript 2015 syntax and
will need to be transpiled to ensure that different browsers can read our
theme.
Earlier, we discussed ECMAScript 2015 and transpilation - compiling source
to be output in a different language from the input language.
Liferay provides an ECMAScript 2015 hook that has exactly what we need.

IMPORTING IN METAL.JS
Let’s take a look at some of the Metal.js code that features ECMAScript
2015 syntax.
In the top_search.es.js file, we are creating the TopSearch class.
This class will create a basic component that enhances the default
behavior of the search application form.
We can take advantage of modules in ECMAScript 2015 that give us the
ability to create, load, and manage dependencies via the new import
and export keywords.
import
import
import
import
async from 'metal/src/async/async';
core from 'metal/src/core';
dom from 'metal-dom/src/dom';
State from 'metal-state/src/State';

CLASSES IN METAL.JS
Using ECMAScript 2015 features, we can also create classes with
constructors and inheritance

WRITING FUNCTIONS WITH METAL.JS
Arrow functions make creation of anonymous functions easier.
With let, we can create variables with scope limited to the block in
which they are declared.
With Metal.js, we can use let and other modern features to create
powerful UI components.


ADDING LAYOUTS
As we’ll see later, you can create custom layout templates.
Layout templates can be bundled into our theme just like our fonts.
Let’s start by including the layout template files, and then finish our
theme’s configuration.

FINISHING UP WITH THE THEME CONFIGURATION
The last thing we need to do is provide special settings for our theme as
well as some package properties.
These configuration settings are found in the WEB-INF folder of the
theme.
The liferay-look-and-feel.xml file includes the configuration for
things like custom layout templates, theme settings, and application
decorators.
The liferay-plugin-package.properties will contain the
information and properties for our theme.

OUT OF THE BOX APPLICATION DECORATORS
There are three out of the box application decorators that are added to
your themes liferay-look-and-feel.xml:
Barebone: when this decorator is applied, neither the wrapping box nor
the custom application title is shown. This option is recommended when
you only want to display the bare application content.
Borderless: when this decorator is applied, the application is no longer
wrapped in a white box, but the application custom title is displayed at
the top.
Decorate: this is the default Application Decorator when using the Classic
theme. When this decorator is applied, the application is wrapped in a
white box with a border and the application custom title is displayed at
the top.

ADDING CUSTOM DECORATORS
All the decorators added to the liferay-look-and-feel.xml require
that a css class is set using the following line:
<portlet-decorator-css-class>[Class Name]</portlet-decorator-css-class>
You can then add styling to these classes in the
_portlet_decorator.scss.
.portlet-trending .portlet-content {
background-color: $brand-bg-color-2;
font-size: 12px;
margin-top: 40px;
padding: 50px 20px 20px;
...
We added the styles for our Application Decorators earlier.

SETTING THE DEFAULT APPLICATION DECORATOR
A default application decorator also needs to be set in the
liferay-look-and-feel.xml.
In order to do this, we can simply use the line we see here:
<default-portlet-decorator>true</default-portlet-decorator>
Once this is set, we’ll be able to style the standard application decorator
while being able to choose others when the need arises.

ADDING APPLICATION DECORATOR CSS
The styling in the _portlet_decorator.scss is imported into the
_custom.scss.
@import "portlet_decorator";
Once your theme is deployed you can select your new application
decorator.
The new Trending option, for example, will be selectable from the
Application Decorators drop-down list in the Look-and-Feel Configuration
section of our applications.

THEME SETTINGS
We can also add Theme Settings into our theme.
Theme Settings are used to set either hard-coded or configurable values
into the theme.
These setting keys can be accessed inside FreeMarker theme files and,
once deployed, are editable through the Control Panel.
You can provide special settings in your theme that allow administrators
to make stylistic changes from the platform.
These settings provide stylistic flexibility within a theme.

THEME SETTING PROPERTIES
Each Theme Setting can have the following properties:
configurable: a value of true or false determines whether this field should
be displayed or hidden from the Control Panel.
key: a name used to retrieve user value in the theme (no spaces)
type: defines the type of form field to show. Possible values are text,
textarea, select, or checkbox
options: a comma separated list of options the user can choose for the
select type.
value: default setting value


DEFAULT AVAILABLE SETTINGS
There are some default Theme Settings that can used in your theme
without further configuration:
Bullet Style: Adds Bullet Point options for different applications
Show Header Search: Displays Header Search if set to true
Show Maximize Minimize Application Links: Gives a link to navigate
between maximized and minimized view of an application
Show Site Name Default: Lets you control the Site name display
Show Site Name Supported: Lets you control the Site name support

USING CUSTOM THEME SETTINGS
Custom Theme Settings that are added to the
liferay-look-and-feel.xml can also be turned into variables.
These variables are added in the init_custom.ftl file like so:
<#assign new_variable = getterUtil.getBoolean(themeDisplay.getThemeSetting
("new-theme-setting")) />
With the variable created, developers can add logic to their Theme
Freemarker templates.
Our theme has a new variable for the show-header-search Theme
Setting in order to control how the search is displayed with this setting
turned on inside the navigation.ftl.


CUSTOM SHOW HEADER SEARCH EXAMPLE
The show_header_search variable was created in the
init_custom.ftl using:
<#assign show_header_search = getterUtil.getBoolean(themeDisplay.
getThemeSetting("show-header-search")) />
In the navigation.ftl, this custom variable is used to control what
displays:
<#if show_header_search>
<div class="navbar-form navbar-right" role="search">
<div id="search">
...
</div>
<button aria-controls="navigation" class="btn-link btn-search hidden-xs"
type="button">
...
</button>
</div>
</#if>

THE THEME PLUGIN PACKAGE PROPERTIES
The liferay-plugin-package.properties file contains the default
information for our theme.
We’ll revisit this file after we look at some other features of Liferay
themes.
name=Space Program
module-group-id=liferay
module-incremental-version=1
module-version=1.0.0
tags=
short-description=
long-description=
change-log=
page-url=http://www.liferay.com
Provide-Capability=osgi.webresource;osgi.webresource=space-program-theme
author=Liferay, Inc.
licenses=LGPL
liferay-versions=7.0.0+
resources-importer-developer-mode-enabled=true

ADDING COLOR SCHEMES
Developers can also include Color Schemes into the
liferay-look-and-feel.xml.
Color Schemes are variations of CSS and Images with a theme.
Using this option, developers can effectively provide themes within
themes for their administrators to configure based on the business
needs.
Let’s look at how we would add these using the example of fire and ice
Color Schemes.

Color Schemes can be added to the liferay-look-and-feel.xml by
using the following:
<color-scheme id="01" name="Default">
<default-cs>true</default-cs>
<css-class>default</css-class>
<color-scheme-images-path>${images-path}/color_schemes/${css-class}
</color-scheme-images-path>
</color-scheme>
<color-scheme id="02" name="Fire">
<css-class>fire</css-class>
</color-scheme>
We need to set the default as well as any new Color Scheme we’re
adding.
The default-cs makes sure to auto-select this color scheme.
Each Color Scheme needs to include a css-class while the images are
set using different variables in the default.

Once the XML is set, You can add the CSS changes using the following
steps:
1. Create a new directory in src/css called color_schemes.
2. Add a new scss file for each Color Scheme in this folder.
Example: _fire.scss or _ice.scss
3. Add styling to these files using the class selector identified in the XML.
body.fire {
color: #F00 !important;
}
4. Last, import the new scss files into the _custom.scss:
@import "color_schemes/fire";
@import "color_schemes/ice";

Next, images can be added using the following:
1. Create a new directory in src/images called color_schemes.
2. Add a new folders for each Color Scheme such as color_schemes/fire or
color_schemes/ice.
3. Place any images or thumbnails for the color schemes in their
appropriate folder.
The thumbnail that will display in the page configuration menu needs to
go here.

Once Color Schemes and Theme Settings are added to the Theme, they
can be accessed on each Site where the Theme is in use.

THEMELETS

WHAT IS A THEMELET?
Themelets are small, extendable, and reusable pieces of code that are
implemented by a theme.
They can consist of CSS, templates, images, and JavaScript just like a
theme.
They exist as npm packages and can be published to the npm registry
for easy sharing and reuse.
Themelets allow you to share pieces of code between themes, cutting
down on boilerplate and repetition.
You can either create new themelets or take advantage of existing
themelets.

The themelet generator is packaged within the
generator-liferay-theme npm package.
1. Run yo liferay-theme:themelet in the command line or Terminal
from your liferay folder.
2. Name the themelet Application Drag Indicator.
3. Press Enter to accept the default Id.
4. Choose 7.0 for the version.
! Now we have a Themelet with an src folder and a package.json.

THEMELET STRUCTURE
The src directory is where all themelet files exist that will eventually be
used by a theme.
Note: A themelet can have multiple JS files. Any file with the extension
.js, in src/js will automatically be injected into a theme during build.
For files not CSS or JS, they will be made available in the built theme’s
files.

THEMELET CSS
Themelet CSS and JS files will automatically be injected into your theme
during the build task.
Themelet CSS will be injected via Sass imports into the theme’s
_custom.scss file wherever the following CSS comment exists:
/* inject:imports */
/* endinject */

THEMELET JAVASCRIPT
Themelet JS will be injected via <script> tags into the theme’s
portal_normal template wherever the following HTML comment exists:
<!-- inject:js -->
<!-- endinject -->
These comments can be moved anywhere in the files they reside in. If
you remove these comments, the themelet resources in question will
not be added during the build.
Note: the build task is also run during the deploy and deploy:gogo
tasks, so themelet files will also be injected during deploy.

SUCCESSFULLY ADDED
Once deployed, we will see both the clear outline when moving
applications around as well as the animation when we click on the
Menu.

THEME CONTRIBUTORS
WHAT IS A THEME CONTRIBUTOR?
A Theme Contributor is a module that contains UI resources
independent of a theme.
On deployment, the module is scanned for all valid CSS and JS files.
These resources are then included on all pages, regardless of the current
theme.
If you’d like to package UI resources independent of a specific theme
and include them on all pages, Theme Contributors are the right tool.

IDENTIFYING EXISTING THEME CONTRIBUTOR MODULES
In previous Liferay versions, the standard UI for user menus and
navigation, such as the Dockbar, was included in the theme template.
Starting in Liferay DXP, these standard UI components are packaged as
Theme Contributors.
Specifically: the Control Menu, the Product Menu, and the Simulation
Panel are now packaged as Theme Contributor modules.
Styles for these UI components are handled outside of the theme.
In order to edit the standard UI components, you’ll need to create your
own Theme Contributor to add your modifications on top of the existing
components.
You can also add new UI components to Liferay by creating new Theme
Contributor modules.

CREATING YOUR OWN THEME CONTRIBUTOR
To create a new Theme Contributor, you must first create an OSGi
module.
You can use the Liferay Blade CLI tool to create the module.
Next, you must identify your module as a Theme Contributor by adding
the Liferay-Theme-Contributor-Type and Web-ContextPath
properties to your bnd.bnd file.
Liferay-Theme-Contributor-Type helps Liferay identify your module
as a Theme Contributor.
Web-ContextPath sets the context from which the Theme Contributors
resources are hosted.

EXAMPLE BND.BND FILE
Let’s take a look at the Control Menu’s bnd.bnd file.
Notice the Liferay-Theme-Contributor-Type and
Web-ContextPath headers in the file.
Bundle-Name: Liferay Product Navigation Control Menu Theme Contributor
Bundle-SymbolicName: com.liferay.product.navigation.control.menu.theme.contributor
Bundle-Version: 1.0.0
Liferay-Releng-Module-Group-Description:
Liferay-Releng-Module-Group-Title: Product Navigation
Liferay-Theme-Contributor-Type: product-navigation-control-menu
Web-ContextPath: /product-navigation-control-menu-theme-contributor
-include: ../../../../../marketplace/web-content-management/bnd.bnd

MODIFYING STANDARD THEME CONTRIBUTORS
If you want to edit or style standard Theme Contributors, you’ll need to
create a new, overriding Theme Contributor.
In order to control Theme Contributor priority, you can set a weight for
your Theme Contributor in your bnd.bnd file.
You set the weight by adding the
Liferay-Theme-Contributor-Weight: property to the bnd.bnd file.
Liferay-Theme-Contributor-Weight: 100
Theme Contributors with higher weight will see their resources included
later, thus overriding Theme Contributors with lower weight.

THEME CONTRIBUTOR RESOURCES
Once the weight has been set, you can create a
src/main/resources/META-INF/resources folder in your module
and place your resources (CSS and JS files) in that folder.
For example, in order to change the background color of the Control
Menu, you could add _control_menu.scss to the
src/main/resources/META-INF/resources/css
/blade.theme.contributor/ folder.
In the _control_menu.scss file, you would add CSS to style the menu:
body {
.control-menu {
background-color: darkkhaki;
}
}

IMPORTING RESOURCES
All of the SCSS files are imported into the main
blade.theme.contributor.scss file:
@import "bourbon";
@import "mixins";
@import
@import
@import
@import
"blade.theme.contributor/body";
"blade.theme.contributor/control_menu";
"blade.theme.contributor/product_menu";
"blade.theme.contributor/simulation_panel";
If you add your own SCSS files, remember to add them to the list of
imports in the blade.theme.contributor.scss file.

WRAP-UP
Once you have everything styled to your liking, build and deploy your
new Theme Contributor module to see your modifications applied to
pages and themes.
Make sure to use Theme Contributors wisely.
The UI contributions will affect every page and will remain, regardless of
the theme.

IMPORTING PREDEFINED CONTENT
The Resources Importer allows you to deploy your themes with
predefined content.
This can be useful for creating content and themes together to provide a
wholesale style change.
When deployed, the Resources Importer creates a site template, which
can be used for creating new sites with a predefined look and feel.

RESOURCES IMPORTER’S FILE STRUCTURE
Theme resources reside in the source of your theme.
You can create files and folders in a new
[theme-folder]/docroot/WEB-INF/src/resources-importer directory.
Example file structure:
resources-importer/
document_library/
documents/
journal/
articles/
structures/
templates/
assets.json
sitemap.json

RESOURCES IMPORTER CREATES A SITE TEMPLATE
The site template that will be generated is defined in the
sitemap.json file.
This file describes the contents and hierarchy of a site that Liferay can
import as a site template.
The sitemap.json file defines the following:
Pages of a to-be-generated site template
Layout templates
Applications
Application preferences (Portlet preferences)
Content to display

RESOURCES IMPORTER EXAMPLE
Here is a sitemap.json example that will create one page named
Welcome that has two columns, a Login application in one and a Hello
World application in the other.
{
"layoutTemplateId": "2_columns_ii",
"publicPages": [
{
"columns": [
[ { "portletId": "com_liferay_login_web_portlet_LoginPortlet" } ],
[ { "portletId": "com_liferay_hello_world_web_portlet_
HelloWorldPortlet" } ]
],
"friendlyURL": "/home",
"name": "Welcome",
"title": "Welcome"
}
]
}

IMPORTING ASSETS WITH METADATA
The assets.json file specifies details about the assets to be imported.
Tags can be applied to any asset.
Abstract summaries and small images can be applied to web content
articles. As an example:
{
"assets": [
{
"name": "company_logo.png",
"tags": [ "logo", "company" ]
},
{
"abstractSummary": "This is an abstract summary.",
"name": "My Example.xml",
"smallImage": "company_logo.png",
"tags": [ "web content" ]
}
]
}

IMPORTING DOCUMENTS AND MEDIA
By default, all assets under the directory
document_library/documents/ get imported into the platform’s
global Documents and Media.
Example file structure:
document_library/
documents/
image.png
Custom Folder/
image 2.png
With this example file structure, image.png will be placed in the root
folder of the Documents and Media application.
image 2.png will be placed in a folder named Custom Folder.

IMPORTING WEB CONTENT
The journal directory is used for importing various assets related to
web content such as structures (JSON), templates (Velocity/FreeMarker),
and web content articles (XML).
journal/
articles/
My Example Template A/ (matches Template name)
My Example Article X.xml
My Example Article Y.xml
structures/
My Example Structure H.json
templates/
My Example Structure H/ (matches Structure name)
My Example Template A.flt
My Example Template B.flt

EXAMPLE STRUCTURE
Here is an example of a Structure. We’ll call it My Example Structure
H.json:
{
"availableLanguageIds": [ "en_US" ],
"defaultLanguageId": "en_US",
"fields": [
{ "name": "Header", "type": "text", ... },
{ "name": "Body", "type": "textarea", ... }
]
}
The source JSON of Web Content Structures can be found by clicking the
Source tab while editing the Structure.

EXAMPLE TEMPLATE
Here’s an example of a Template. We’ll call it My Example Template
A.ftl:
<h1>${Header.getData()}</h1>
<p>${Body.getData()}</p>
Both Structures and Templates can be created/edited by navigating to
Web Content in Site Administration via the Product Menu.

EXAMPLE ARTICLE X.XML
To access the source XML of an article, go to the edit page of the article
and click the View Source option.
Let’s take a look at an example article. We’ll call it Example Article
X.xml:
<?xml version="1.0"?>
<root available-locales="en_US" default-locale="en_US">
<dynamic-element name="Header" type="text" index-type="keyword"
instance-id="mdyl">
<dynamic-content language-id="en_US"><![CDATA[My Header]]>
</dynamic-content>
</dynamic-element>
<dynamic-element name="Body" type="text_box" index-type="keyword"
instance-id="opiq">
<dynamic-content language-id="en_US"><![CDATA[My body <em>with</em>
HTML.]]>
</dynamic-content>
</dynamic-element>
</root>

ADDING WEB CONTENT TO THE SITEMAP
To add a Web Content Display and choose a content article to display,
we could do something like this example in the sitemap.json:
"columns": [
[
{ "portletId": "com_liferay_hello_world_web_portlet_HelloWorldPortlet" },
{
"portletId":
"com_liferay_journal_content_web_portlet_JournalContentPortlet",
"portletPreferences": {
"articleId": "My Example Article X.xml",
"groupId": "${groupId}",
...
}
},
...
Here, we’ll add the web content application right below the Hello World
application.

PORTLET PREFERENCES
You’ll notice we use a portletPreferences property to select the
article we will display in the Web Content Display application.
portletPreferences are properties that store basic application
configuration data.
Just as you can apply some configurations for applications through the
UI, portletPreferences properties allow you to set configurations for
applications in the sitemap.json file.

COMMON PORTLET PREFERENCES
Here are a few commonly used portletPreferences properties:
articleId
groupId
portletSetupTitle_en_US
portletSetupUseCustomTitle
portletSetupPortletDecoratorId
Selects an article
Selects a site
Sets custom title
Allows use of custom title
Sets Application Decorator
Some portletPreferences properties are general, while others are
application-specific.

EXAMPLE PORTLET PREFERENCES
In the previous example, we are taking advantage of
portletPreferences to configure the Web Content Display
application.
"portletPreferences": {
"articleId": "My Example Article X.xml",
"groupId": "${groupId}",
...
}
With the articleId property, we choose which article to display in the
Web Content Display application.
The Example Article X.xml will be located in the
journal/articles folder of our example Resource Importer module.
The groupId property determines the site where the content will be
displayed.

SETTING APPLICATION DECORATORS
It is also possible to set the application decorator from a
sitemap.json where portletSetupPortletDecoratorId is the id
of the decorator to be used:
{
"portletId": "com_liferay_journal_content_web_portlet_
JournalContentPortlet",
"portletPreferences": {
"articleId": "My Content.xml",
"groupId": "${groupId}",
"portletSetupPortletDecoratorId": "barebone"
}
}
In this example, the application decorator is set to the barebone setting.
The portletSetupPortletDecoratorId property can be set to any
of the application decorators available (i.e., barebone, borderless,
decorate).

SETTING CUSTOM DECORATORS
The portletSetupPortletDecoratorId preference could be set to
our custom decorator id as well. The preference can be set when
embedding applications in a theme:
<#assign VOID = freeMarkerPortletPreferences.setValue
("portletSetupPortletDecoratorId", "barebone") />
<div aria-expanded="false" class="collapse navbar-collapse"
id="navigationCollapse">
<#if has_navigation && is_setup_complete>
<nav class="${nav_css_class} site-navigation" id="navigation"
role="navigation">
...
</nav>
</#if>
</div>
<#assign VOID = freeMarkerPortletPreferences.reset() />
Application decorators can also be updated from the application’s Look
and Feel menu.

DEPLOYING RESOURCES
With the necessary sitemap.json and resources, you can deploy the
theme.
With the default configuration, the Resources Importer will create a Site
Template that shares the name of the theme.
We can also create a new site that includes the resources on the page.

IMPORTING RESOURCES TO EXISTING SITES
To configure the Resources Importer to import resources into a site,
rather than a site template, add the following properties to:
{theme-name}/src/WEB-INF/
liferay-plugin-package.properties.
...
resources-importer-target-class-name=com.liferay.portal.kernel.model.Group
resources-importer-target-value=[site-name]
...
If the site-name is an existing site, the Resources Importer will import
into that site.
When the site doesn’t exist, the Importer will create it for you.
Note: This can be a great way to show off your theme’s feaures, or
demonstrate how to arrange content nicely.

DEVELOPER MODE
The Resources Importer has a developer mode, which deletes and
re-creates the target site or site template on each deploy.
To enable developer mode, add the following to:
liferay-plugin-package.properties
...
resources-importer-developer-mode-enabled=true
...
Themes created via the Liferay Theme Generator have developer mode
enabled by default.
Although this is useful for development, it should never be used in a
production environment.

EMBEDDING APPLICATIONS INTO THEMES

EMBEDDING APPLICATIONS
It’s often necessary for developers to embed applications into their
themes.
Embedding applications into the portal_normal.ftl will render them
on each site page.
Let’s look at a couple of ways we can embed applications.

TAGLIBS USED IN EMBEDDING APPLICATIONS
There are three taglibs that we can use in our theme to embed
applications or content:
<@liferay_portlet["runtime"]
<@liferay_journal["journal-article"]
<@liferay_ui["asset-display"]
Each of these taglibs takes different parameters.

USING PORTLET PROVIDER CLASS NAME
The <@liferay_portlet["runtime"] expects two parameters:
1. portletProviderAction requests the portlet provider to perform an
action for display.
Using portletProviderAction.VIEW for the first parameter most commonly
used displays the default application view.
2. The portletProviderClassName requires the fully qualified class
name of the entity on which we want to perform the action.
The portletProviderClassName is always coupled with the
portletProviderAction.
<@liferay_portlet["runtime"]
portletProviderAction=portletProviderAction.VIEW
portletProviderClassName="CLASS.NAME"
/>

APPLICATIONS IN THE TAGLIB
Using the above method will work for a set of applications that can be
found in the source code.
To find which applications work, follow these steps:
1. You can go to https://github.com/liferay/liferay-portal
2. Search the code for extends BasePortletProvider
From there, you will be able to find the list of applications and what
actions you can use with them.

EMBEDDING WEB CONTENT USING LIFERAY PORTLET TAGLIB
For other applications, such as Web Content, you would need to pass in
the portletName.
Here is an example of adding Web Content using
<@liferay_portlet["runtime"].
<#assign VOID = freeMarkerPortletPreferences.setValue
("portletSetupPortletDecoratorId", "barebone") />
<#assign VOID = freeMarkerPortletPreferences.setValue
("groupId", "${group_id}") />
<#assign VOID = freeMarkerPortletPreferences.setValue
("articleId", "ARTICLE_ID") />
<@liferay_portlet["runtime"]
defaultPreferences="${freeMarkerPortletPreferences}"
portletProviderAction=portletProviderAction.VIEW
instanceId="INSTANCE_ID"
portletName="com_liferay_journal_content_web_portlet_JournalContentPortlet"
/>
<#assign VOID = freeMarkerPortletPreferences.reset() />

THE PORTLET NAME ATTRIBUTE
The portletName is the application id, written as the string reference
of the application class path.
<@liferay_portlet["runtime"]
portletName="CLASS_NAME"
/>
For example, the Web Content application would be
com_liferay_journal_content_web_portlet
_JournalContentPortlet.

PORTLET PREFERENCES FOR EMBEDDED APPLICATIONS
It is also possible to set preferences in an application using
${freeMarkerPortletPreferences}, as we can see in the Web
Content example.
This allows you to change the application preferences and have it
immediately display in the theme.
<#assign VOID = freeMarkerPortletPreferences.setValue(
"portletSetupPortletDecoratorId", "barebone") />
<@liferay_portlet["runtime"]
defaultPreferences="${freeMarkerPortletPreferences}"
portletName="com_liferay_login_web_portlet_LoginPortlet"
/>
<#assign VOID = freeMarkerPortletPreferences.reset() />

PORTLET RUNTIME ATTRIBUTES
Let’s look at some of the additional attributes that can be used:
defaultPreferences: This is a string of Portlet Preferences for the
application that will be rendered. It could include look and feel
configurations.
instanceId: If the application is instanceable, this allows for the instance
id to be set.
persistSettings: This attribute will have an application use its default
settings, which will persist across layouts. By default the attribute is set
to true.
settingsScope: This attribute specifies which settings the application is to
use. The default setting is portletInstance but can be set to group or
company.

USING THE JOURNAL ARTICLE TAGLIB
You can also embed Web Content using the
<@liferay_journal["journal-article"] taglib.
<@liferay_journal["journal-article"]
articleId="ARTICLE_ID"
ddmTemplateKey="TEMPLATE_KEY"
groupId=${group_id}
/>
The <@liferay_journal["journal-article"] taglib requires the
following:
Article ID: The id of the Web Content Article you wish to display
Template Key: The id of any Web Content Template you want to identify
groupId: The Site id where the content is available

USING THE ASSET DISPLAY TAGLIB
Finally, you can also embed other specific assets, such as wiki articles or
blogs, using the <@liferay_ui["asset-display"] taglib.
<@liferay_ui["asset-display"]
className="JAVA_CLASS_NAME"
classPK="CLASS PK (RESOURCE PK) OF ASSET"
template="full_content"
/>
The <@liferay_ui["asset-display"] taglib requires the following:
Class Name: The Java Class Name of the asset
This would be the content type, such as blogs or documents
Class PK: The Primary Key id of the specific asset to display
This would be the specific blog or document you want to display
Template: This identifies the template used to display the asset

EMBEDDING WITH THE RIGHT TAGLIB
In the past, the only option was to embed applications themselves.
With these taglibs, you can choose to embed applications, specific web
content, or any other asset you’d like on display.
This gives you the flexibility to choose the option that best fits your
requirements.

## Layout Templates

EXAMINING THE LIFERAY PAGE
A Site page has three
main sections.
1. The Header
2. The Content Section
3. The Footer
As we know, the Theme is
responsible for providing
the global styling, as well
as header and footer
styling.
Layout Templates control
the positioning of the
content between the
header and the footer.

CONTROLLING DISPLAY
Multiple applications can be added to the page that align with the
Layout Template.
Applications stack vertically and fill the available width of its parent
column.

PREDEFINED LAYOUT TEMPLATES
Liferay comes bundled with a number of predefined layout templates
you can choose from.
If none of the provided layout templates suit your needs, custom layout
templates can be created and deployed to accomplish any combination
of rows/columns.

ROWS AND COLUMNS
Each layout can have any number of rows with columns.
Columns in a layout use Bootstrap’s Grid system (see:
http://getbootstrap.com/css/#grid) to determine screen and column
size.
There are 12 sections total in the fluid grid system, and you can divide
them up any way you like.
Because it’s part of Bootstrap’s grid system, we never have to specify
percentages or pixel widths, and the layouts are also responsive.

USING THE LIFERAY THEME GENERATOR FOR LAYOUTS
We have seen how the Liferay Theme Generator can be used to create
themes and themelets.
We can also use the generator to create layout templates by using:
yo liferay-theme:layout
This will create a new folder for your layout template in your current
working directory.
Let’s walk through creating one of the layout templates from our theme.

PACKAGING LAYOUTS IN THEMES
As we saw with our Space Program Theme, we can bundle content and
layouts with themes.
This layout has already been included in the theme using the following
steps:
In [your-theme]/src, create a layouttpl folder.
Copy and paste the tpl and png file from [your-layout]/docroot to
[your-theme]/src/layouttpl.
Last, you can copy the <layout-template> structure from the
liferay-layout-templates.xml found in WEB-INF.
Paste it into the theme’s liferay-look-and-feel.xml.
But we can use gulp commands to deploy layouts separately as well.

LAYING IT OUT
The Themes Generator makes new layouts quick and easy!
After creating a new layout using the generator, you will see
docroot/{layout-name}.tpl in your layout template directory that
reflects the layout you created.
The generator will also install the npm dependencies used for
deployment.
After running gulp deploy, you will also see a dist folder containing
the application file itself.
This file can then be deployed on any server you’re working with.

COLUMN ELEMENTS AND CLASSES
Let’s take a closer look at the first column of the previous example and
the various elements it consists of.
<div class="col-md-2 portlet-column portlet-column-first" id="column-1">
$processor.processColumn("column-1", "portlet-column-content
portlet-column-content-first")
</div>
You’ll notice three things that we’ll work through:
1. The id
2. The classes
3. the $processor.processColumn

COLUMN CONTAINER
The id: column-1
Unique identifier for the column that matches ID passed to
$processor.processColumn.
Classes: col-md-2
This class comes from Bootstrap’s grid system and determines two things:
the percentage-based width of the element, and the media query
breakpoint for when this element expands to 100% width.
12 is the maximum amount, so col-md-2 indicates 2/12 width, or
16.66%.
Classes portlet-column portlet-column-first
All column containers should have the portlet-column class.
For rows with more than one column, the first column will have
portlet-column-first and the last will have portlet-column-last.
For rows with only one column, the column will have the
portlet-column-only class.

INSIDE $PROCESSOR.PROCESSCOLUMN
$processor.processColumn is necessary to render our layouts.
The $processor.processColumn function takes the CSS column ID
and the list of CSS classes as its two arguments.
$processor.processColumn: column-1
Unique identifier; should match ID of the parent div
$processor.processColumn: portlet-column-content
portlet-column-content-first
Additional classes added to the content element; classes match the parent
div’s classes with -content appended
MODIFYING TEMPLATE BREAKPOINTS
When looking at the example template, you’ll notice this Bootstrap grid
class used on every column.
col-md-{size}
The different sizes available are xs, sm, md, and lg.
The medium size is used by default, but the others can be used in layout
templates as well.
For example, setting the column classes to col-lg-{size} means the
columns would expand to 100% width at a larger screen width than
col-md-{size}.
These classes can also be mixed to achieve more advanced layouts.

BREAKPOINT EXAMPLE
In this example row, on medium-sized view ports (such as a tablet),
column-1 will be 33.33% width.
column-2 will be 66.66% width.
On small-sized view ports, both column-1 and column-2 will be 50%
width.
<div class="portlet-layout row">
<div class="col-md-4 col-sm-6 portlet-column portlet-column-first"
id="column-1">
$processor.processColumn("column-1", "portlet-column-content
portlet-column-content-first")
</div>
<div class="col-md-8 col-sm-6 portlet-column portlet-column-last"
id="column-2">
$processor.processColumn("column-2", "portlet-column-content
portlet-column-content-last")
</div>
</div>

EMBEDDING APPLICATIONS
It is possible to embed an application in your layout template.
This is very similar to embedding an application into the theme.
The major difference is that administrators can be more flexible with
where to apply a layout.
If the application does not have a Java class that extends
BasePortletProvider, developers can use $theme.runtime().
If it does, this is done using
$processor.processPortlet("CLASS_NAME", ACTION).

USING $THEME.RUNTIME()
In Liferay 6.2, you would pass the application id as a parameter into
runtime().
In DXP, the application id is no longer a number but a snake case string
of the application class path.
For example, in 6.2, you could write $theme.runtime('58') to embed
the login application into their layout.
In DXP, you can accomplish the same thing by passing
$theme.runtime('com_liferay_login_web_portlet_
LoginPortlet').
$THEME.RUNTIME() EXAMPLE
Here is an example where the Login application is embedded into a
layout:
<div class="columns-1-2" id="main-content" role="main">
<div class="portlet-layout">
<div class="portlet-column portlet-column-only" id="column-1">
$theme.runtime("com_liferay_login_web_portlet_LoginPortlet")
$processor.processColumn("column-1", "portlet-column-content
portlet-column-content-only")
</div>
</div>
...
</div>

PROCESSOR.PROCESSPORTLET(”CLASS_NAME”, ACTION)
The $processor.processPortlet declaration, just as the theme
declaration, expects two parameters:
The class name of the entity type you want the application to handle
The type of action
For example, if you wanted to embed the Breadcrumb application into
the layout, you could use the following:
$processor.processPortlet("com.liferay.portal.kernel.
servlet.taglib.ui.BreadcrumbEntry", $portletProviderAction.VIEW)

WHERE SHOULD MY APPLICATION GO?
If you want an application, such as the search or language application,
to be embedded on every site page, you should embed the application
in the theme.
In the case where you want to embed an application with a particular
layout not to be displayed on every page, you can embed it in the
layout template.
This gives developers as much flexibility as they need when embedding
applications.

## Customizing the Front-end

TEMPLATES IN LIFERAY

USING TEMPLATES
As previously noted, you can provide styling for every aspect of the
platform.
Global Styling and page design can be modified using theme and layout
templates.
Liferay also provides Application Display Templates (ADTs) for styling
different aspects of applications, which have integrated the ADT
framework.

TEMPLATE EXAMPLES
Templates in Liferay consist of FreeMarker templates you can use with
different resources.
There are a number of resources on the platform where you can use
templates for styling.
Assets: Web Content and Dynamic Data Lists are special content types;
they have their own templates.
Applications: A number of applications such as the Asset Publisher, or
Navigation, can be styled through ADTs.
Custom Applications: Custom-developed applications can also have ADTs
attached, giving you stylistic control.
Notifications: You can provide branding for Workflow email notifications.
Additionally, you can use Soy Templates and JSX templates when
developing applications.

USING TEMPLATES
There are many other templates that can be used on the platform.
Next, we’ll take a look at using templates along with our theme to style
our content.

TEMPLATE LANGUAGE OPTIONS
Templates can use the following templating languages:
Velocity: Velocity is a scripting language that lets you mix logic with
HTML. Velocity is deprecated as of 7.0.
Extensible Style Sheet Language: Widely used for transforming XML into
other formats.
FreeMarker: FreeMarker is a templating language that could be
considered a successor to Velocity and is recommended.

FREEMARKER: THE WAY FORWARD
FreeMarker templates in Liferay act as the intermediary between the
back-end code in Java and the front-end.
They enhance HTML by adding constructs such as variables, conditional
statements, and loops.
Once it’s processed, the result is HTML, which is then styled by your CSS
and displayed by the browser.
FreeMarker provides a straightforward, clean, and simple method for
incorporating dynamic content in a webpage.
It permits the user to use a simple yet powerful template language to
reference objects defined in the Java code.

FREEMARKER OPTIONS
Here are some examples of what you can use in Freemarker:
Variable: accessed by its name ${var_name}
Arithmetics: +, -, /
Logical Operators: &&, ||, <=
Sequence slice: ${profile.assets[1..]}
Include files: [#include “header.html”]
Comments: [#– this is a comment –]
You can also use if else statements or loops, using the directive symbol
#.
Macros can also be created and reused using @.
Let’s walk through some examples.

FREEMARKER EXAMPLES IN THE THEME
Let’s look at some examples from the theme we created.
We defined a variable in the init_custom.ftl file.
<#assign show_header_search = getterUtil.getBoolean(themeDisplay.
getThemeSetting("show-header-search")) />
The variable can then be used in the following way:
${show_header_search}
Our theme also has an if statement that includes a file if a theme
setting is turned on.
<#if has_navigation>
<#include "$full_templates_path}/navigation.ftl" />
<#/if>
We also have macros being used for things like the menu.
<@liferay.control_menu />

USING TAGLIBS WITH FREEMARKER
Developers using FreeMarker have access to Liferay’s taglibs in
templates.
There is no need to instantiate taglibs as they’re already available.
Taglibs are accessed by indicating the TLD file name with underscores.
For example, liferay-portlet-ext.tld is specified as
@liferay_portlet_ext.
Note: The utilLocator, objectUtil, and staticUtil variables for
FreeMarker and the utilLocator variable for Velocity are disabled by
default.
These variables are vulnerable to remote code execution and privilege
escalation and should be used with caution, if enabled.

FREEMARKER EXAMPLES IN THE CONTENT TEMPLATES
We can see an example of the Carousel Content Template.
This section includes the <#list> as well in order to iterate through
content for display in the Carousel format.
<#list contents.getSiblings() as cur_contents>
<div class="${(cur_contents?counter == 1)?then('active', '')} item">
<#assign article = cur_contents.getData()?eval />
<#-- Here is our taglib call -->
<@liferay_ui["asset-display"]
className=article.className
classPK=getterUtil.getLong(article.classPK, 0)
template="full_content"
/>
</div>
</#list>
The <@liferay_ui["asset-display"] is a taglib that allows us to
grab information and display content articles.

ACCESSING DATABASE INFORMATION
Although Freemarker gives us a helpful way to interact with back-end
code, it doesn’t natively provide access to contextual information we
may need (e.g., current user, page information).
In some cases, the need may arise to create custom variables that can
access the database and inject contextual information into our
templates.
We can use the serviceLocator property to access the database, but
would have to leave it unrestricted, which can become a security risk.
Context Contributors offer a middle ground where we can safely access
contextual information in our template.

195CONTEXT CONTRIBUTORS
Context Contributors give users the ability to inject contextual variables
and functionality into Freemarker templates.
There are two types of Context Contributors in Liferay DXP:
TYPE_GLOBAL: Variables that are available globally
TYPE_THEME: Variables available only within themes
For more information on creating and using Context Contributors,
documentation is available at https://dev.liferay.com/develop/tutorials/
-/knowledge_base/7-0/context-contributors

CHANGES IN FREEMARKER FOR DXP
There are some changes to Freemarker Templates in DXP that are worth
noting for those who created templates on previous version.
One major change is that the theme variable is no longer injected into
the FreeMarker context.
For more information about why the theme variable was removed for
Liferay DXP and suggestions for updating your code, go here:
https://dev.liferay.com/develop/reference/-/knowledge_base/7-0/
breaking-changes#
taglibs-are-no-longer-accessible-via-the-theme-variable-in-freemarker

USING LEXICON CSS COMPONENTS IN TEMPLATES

LEXICON CSS COMPONENTS AND ELEMENTS
As we discussed earlier, Lexicon CSS provides a large number of styles
and components we can take advantage of in development.
We’ve seen that we can use these styles and components in Themes.
You can also use Lexicon CSS components in various Templates to
include consistent and modern design for your applications and content.

SIMPLIFYING TEMPLATE DEVELOPMENT
Using the Lexicon CSS framework can simplify development across the
board.
In many cases, you can simply copy code snippets from the component
you are interested in using, and it’ll work in your Templates.
Lexicon CSS components are also built with modularity in mind, further
simplifying the development of consistent, modern content
presentations.
The list of Lexicon CSS components and elements can be found here:
http://liferay.github.io/clay/
Let’s take a look at some examples.

DISPLAYING USER INFORMATION WITH CARDS
One example of a component we can use is a Card component.
This component is versatile, as it can be combined with other
components to provide the design developers need.
All we need is a <div> element with the class card, and we can build
from there.
Let’s take a look at the code behind this example.

CARD-CODED
In our example, we’re actually using a couple Lexicon CSS components
and elements to provide information about our User.
Inside the card component, we are using the user-icon component.
We’re also using the crop-img component to fit the image to the Card.
<div class="card" style="max-width: 300px;">
<div class="crop-img crop-img-bottom crop-img-center" style="height: 150px;">
<img alt="thumbnail" src="../../images/thumbnail_hot_air_ballon.jpg">
</div>
<div class="user-icon user-icon-danger user-icon-xxl" style="border: 4px
solid #FFF; line-height:120px; margin: -64px auto 0; position: relative;">
<span>SN</span></div>
<div class="card-block" style="text-align: center;">
<h3 style="margin:0;">Space Nova</h3>
<h5 class="text-default" style="margin-top:0;">
Out-Of-This-World Trainer</h5>
<p>The Most Interesting Man In Space.</p>
</div>
</div>

BADGES, LABELS, AND STICKERS, OH MY
Badges, Labels, and Stickers are other
examples of smaller components.
These components can be placed on
larger components to maintain a
consistent look-and-feel.
For example, we could place a Sticker on
an image using something like this:
<div class="aspect-ratio">
<img alt="thumbnail" src="thumbnail.jpg">
<span class="sticker sticker-danger">PDF</span>
</div>

INSPECTING ELEMENTS
One simple way to speed
up the usage of these
components is to take
advantage of your
browser’s developer tools.
In many cases, you can
use Inspect Element to
copy/paste the code into
your Template and modify
it as needed.

THEMING COMPONENTS
As we mentioned earlier, you can completely control the styling of each
component.
Each component can be customized to suit your needs with the Lexicon
CSS Customizer or through the component CSS in the Theme.
With this in mind, you can easily use the Lexicon CSS components and
inherit the presentation from the theme itself.
This means you can control styles and still maintain the simplicity and
flexibility of Template development.

BEST PRACTICES FOR COMPONENTS AND ELEMENTS
As you can see, there are many components and elements in Lexicon
CSS.
Some components overlap, some look the same at first glance, and
several are combined to form a whole new component.
It’s always good to take the time to choose the right component for the
job.
As we look forward to Template development, keep these in mind

## Delivering Consistent Content Experiences

STYLING CONTENT ARTICLES
You can provide styles to Web Content using either the WYSIWYG editor
directly, or by embedding the styles into a Web Content Template
(Template).
The Alloy Editor can be used to add HTML/CSS/JavaScript changes into
basic Web Content.
We’re going to focus on the more advanced Template option.
A Template is responsible for displaying content from a Web Content
Structure (Structure) and ultimately determines how the content is
displayed.

ADDING TEMPLATES
In Site Administration→Content→Web Content, you can add Structures
and Templates.
Templates are managed in the Options menu.
You have two methods of adding templates:
Attaching an ftl file
Using the editor
The editor gives you quick access to some default variables.

DEVELOPING TEMPLATES
Web Content is unique in that Structures can be provided by Content
Managers.
When developing Templates, you can simply reference the Structure
fields and determine how to display them.
All HTML tags, by default, will inherit the global styling from the Theme.
You can use the <style> and <script> tags to provide custom CSS
and JavaScript for the Template.

LEXICON CSS IN TEMPLATES
As discussed previously, Lexicon CSS styles can easily be applied to both
Themes and Templates.
Developers can take advantage of Lexicon CSS components and
elements to anything from Cards to Modals.
If the Theme has customized any of the base Lexicon CSS styling, these
changes will also apply to Templates.

GENERIC TEMPLATES
You can also create what are called Generic Templates.
Generic Templates are Web Content Templates that are not associated
with a Structure.
This allows you to create stand-alone Templates that include certain
taglibs, and/or embedded applications, that can be applied to any
content.
Generic Templates can also be imported into other Templates using:
<#include "${templatesPath}/TEMPLATE-ID" />

EMBEDDING APPLICATIONS IN TEMPLATES
Applications, custom or core, can be embedded into Templates.
This means you can ensure application functionality is displayed with
Web Content.
For example, if we wanted to embed the Currency Converter application,
we could do the following:
In FreeMarker:
<@liferay_portlet_ext["runtime"] portletName="com_liferay_currency
_converter_web_portlet_CurrencyConverterPortlet" />
In Velocity:
$theme.runtime("com_liferay_currency_converter_
web_portlet_CurrencyConverterPortlet");

THE POWER OF TEMPLATES
You can provide consistent look and feel on the platform with Web
Content Templates.
These Templates have access to many of the same tools used in
front-end development such as:
Bootstrap
CSS
HTML
Lexicon CSS
Freemarker

EXAMINING WEB CONTENT TEMPLATES
Content creators are typically responsible for Structures, while front-end
developers are responsible for Templates.
Let’s first examine the Template included in our Theme.
Afterwards, we will create some new Templates together.

STYLING THE PORYGON STRUCTURE
Embedded in our theme is the Porygon Structure and Template.
The Template is styling the following fields as defined by the Structure:
Cover Image: A documents and media field to select an image
Title: A text field for the image title
Sub Title: A textarea field adding subtitle information
Content: A ddm-text-html, otherwise known as the Alloy Editor, for
providing additional content


THE PORYGON TEMPLATE
Let’s look at a couple key points in the Template.
The variables are assigned at the top of the file:
<#assign
author = request.attributes.author!""
displayMode = getterUtil.getInteger(request.attributes.displayMode!0,0)
viewURL = request.attributes.viewURL!""
/>
We also see the Template controlling different display modes:
<#if displayMode == 1 >
...
<#elseif displayMode == 2 >
...
<#elseif displayMode == 3 >
...
<#else>
...
</#if>

STYLING STRUCTURE FIELDS
The Structure fields can be added to the template with the following
syntax:
${[field-name].getData()}
The Structure fields being styled in the Porygon Template are as follows:
coverImage.getData()
title.getData()
subTitle.getData()
content.getData()

DEFAULT STRUCTURE AND TEMPLATE
Each article is displaying the default template that simply includes the
structured content.
To accomplish the business requirements, we’ll need more control over
how the Structure is presented.
Let’s start with modifying the banner Template.
THE BANNER FTL IMAGE
Our banner is a simple FreeMarker template.
We are simply providing a <div> with the figure class that includes our
image and text overlay.
Our image is using the default editor option for an image field, but we
have added crop-img-top class with a specified height.
By default, the editor adds the img-responsive class to our images to
ensure responsive design.
For more on Lexicon CSS figure design, you can go here:
https://liferay.github.io/clay/content/figures/
<div class="crop-img-top" style="height: 500px">
<img alt="${Image6kp8.getAttribute("alt")}" src="${Image6kp8.getData()}"
class="img-responsive"/>
</div>

THE BANNER FTL IMAGE
Our banner is a simple FreeMarker template.
We are simply providing a <div> with the figure class that includes our
image and text overlay.
Our image is using the default editor option for an image field, but we
have added crop-img-top class with a specified height.
By default, the editor adds the img-responsive class to our images to
ensure responsive design.
For more on Lexicon CSS figure design, you can go here:
https://liferay.github.io/clay/content/figures/
<div class="crop-img-top" style="height: 500px">
<img alt="${Image6kp8.getAttribute("alt")}" src="${Image6kp8.getData()}"
class="img-responsive"/>
</div>

THE BANNER FTL TEXT
Our text has been centered at the top of the image using the
figcaption and center classes.
By including the flex classes, we’ve also ensured our text is responsive.
Inside the <div> structure, we have our title and heading using our
getData() methods.
<div class="figcaption-top figcaption-info">
<div class="flex-container" style="height: 100%">
<div class="flex-item-center text-center" style="width: 100%">
<h1>${title.getData()}</h1>
<p class="lead">${heading1.getData()}</p>
</div>
</div>
</div>

THE 3 COLUMN WITH IMAGES FTL STRUCTURE
The 3 Column with Images Template is relatively similar to the Banner
Template.
We include the class row so we can take advantage of Bootstrap
columns for responsive design.
Each item in the row contains the following classes for mobile, tablet,
and desktop breakpoints:
<li class="col-lg-4 col-md-4 col-xs-6">

THE 3 COLUMN WITH IMAGES COLUMNS
Each column in this Template is the same, referencing different fields
from the Web Content Structure.
We’re using the figure classes for our rounded styling.
The text overlay is being accomplished using the figcaption class.
<div class="figure figure-rounded aspect-ratio aspect-ratio-3-to-2">
<#if image1.getData()?? && image1.getData() != "">
<img alt="${image1.getAttribute("alt")}" src="${image1.getData()}" />
<div class="figcaption-full text-center">
<div class="flex-container" style="height: 100%">
<div clas="flex-item-center">
<h2>${heading1.getData()}</h2>
<p>${content1.getData()}</p>
</div>
</div>
</div>
</#if>
</div>

THE FOOTER FTL
In the course of development, you’ll likely come across the need to
work with legacy code.
In our footer example, we’ve worked with legacy HTML code to create
the template.
We’re using a style tag to place the bgimage field from our Structure
as the background.
This example actually uses the same image as the banner, but only uses
the image clouds as the background padding class.
Then, using a <table>, we can provide our columns to reference our
logo, text, and action button.
With that, we have accomplished the business requirements for web
content on the front page of S.P.A.C.E.


SIMULATION OPTIONS
The Simulation Menu has options for following:
Desktop: This allows you to see content from the Desktop view
Tablet: This allows you to see the Vertical and Horizontal preview of a
Tablet.
Mobile: This allows you to see the Vertical and Horizontal preview of a
Mobile device.
Auto-size: This allows you to resize as needed.
Custom: This allows you to set custom breakpoints.
Let’s look at our Templates in the three main breakpoints.

STYLE ALL THE CONTENT
Content Templates can be extremely powerful.
Our current templates take content from a Structure and style it in a
consistent way.
We’ve used Lexicon CSS to create beautiful content displays like a
banner and thumbnails.
As we style more content throughout the site, we may need more
advanced tools:
Taglibs
Repeatable fields from Structures
Passing settings between templates

CREATING AN EVENTS PAGE
They’ve decided to create a new Events page on the site.
Events will be created through Web Content and displayed in a number
of different styles.
Our Content Team has already created a Structure for events, but needs
to style it.
Some events will be featured, or highlighted, on the Events page.
Instead of creating multiple Structures for events (whether they’re
featured or not), the Content Team has come up with something a little
different.

THE COMPOSITE SOLUTION
The Content Team has created an additional Structure, Content List.
The Content List Structure contains:
A ddm-journal-article field called contents
This field is different from what we saw before because it:
Allows the writer to choose a Web Content Article for the field
Can be repeated many times

DEVELOPING A NEW TYPE OF TEMPLATE
Using the structured content from the Content Team, we’ll need to:
Develop a Template for the Event Structure
Develop a Template for Content List that embeds other Web Content
Articles
Develop Templates to display the Content List in different ways

STYLING EVENTS
Our first task is to provide basic styling for the Events.
We’ll build a nice display with Lexicon CSS components, like Card, with
the Structure fields.
Events contain:
Cover Image: A beautiful image to display when listing or displaying the
event
Headline: The name of the event
Date: When the event is happening
Lead Text: Brief information to display about the event
We can style these into a nice card, displaying all the event details.

THE EVENT DISPLAY TEMPLATE
Events will now be styled using the basic styling outlined in the Event
Display template.
230FEATURING EVENTS
Now that we have our basic events styled, any time we want to show an
event, it will look clean and consistent.
The Content Team would also like to feature some events.
A Content List Structure allows for selecting Web Content Articles to
feature.
We’ll need to write a Template that can:
Embed content from another Web Content Article
Style multiple fields from a list
To embed Web Content Articles, we’ll need to use some other Liferay
features.

EMBEDDING WEB CONTENT
If you tried to use getData() on each Web Content Article, you’d only
get:
The Java class that article uses
The primary key of the article
If you’re a Java developer, or have access to the serviceLocator, this
might be useful.
You could call the service for the Web Content Article
(JournalArticleServce) and ask for its content.
But what if we can display articles without needing to call more
back-end services?

USING TAGLIBS IN TEMPLATES
Taglibs provide reusable components that simplify complex displays in
Liferay.
Normally, Java developers can use these in JSPs to make building
application views easy.
Templates have access to Taglibs using a simple syntax in FreeMarker:
<@taglib_name["tag-name"] attribute=value />
There are a lot of taglibs available for displaying data and building
complex UIs:
liferay_ui: some general components for displaying data
liferay_frontend: contains some Lexicon CSS components
aui: components for AlloyUI

DISPLAYING CONTENT WITH A TAG
Taglibs are so useful that applications like the Asset Publisher use them
for displaying Web Content and other assets.
Can we use the same tags as the Asset Publisher for displaying Web
Content?
The taglib liferay_ui contains the tag asset-display that takes
three attributes:
className: the Java class of the asset
classPK: the primary key of the asset
template: how to display the asset
We already have most of this information from our Structure field,
contents.

DISPLAYING OUR ASSET LIST
Using this tag, we can easily display the Web Content Article in
FreeMarker:
<@liferay_ui["asset-display"]
className=article.className
classPK=getterUtil.getLong(article.classPK, 0)
template="full_content"
/>
The template called full_content just needs to render our Web
Content Article as if it were being displayed on its own.
This way, the Content Template for the article gets used.
We can use the tag <@liferay_ui["asset-display"] \> to display
each article in our list.

USING REPEATABLE FIELDS
Our list of Web Content Articles is implemented as a repeatable field in
the Structure.
When content creators are building an article, they can click a button to
add as many copies of the field as they want.
We could have 1, 2, or 10 articles, depending on how many fields there
are.
To use a list of fields, we need to be able to:
Get the list
Iterate over the list
This is actually pretty easy to do.

GETTING THE LIST OF FIELDS
When we want data from a field, we usually call its getData() method.
Repeatable fields have siblings.
Each sibling is a copy of the field.
Each field would have a getData() method.
In our case, each sibling would have the className and classPK for
the article.
Getting our list of content is pretty easy:
$contents.getSiblings()
So how do we iterate over the list?

LIST BY LIST
We see list iteration in a number of our templates, using the directive
<#list>.
Listing items means we need to know the name of the list and each
individual item:
<#list items as item>
$item.getData()
</#list>
items is the list of variables, and item represents each item in the list.
We can apply this to our articles:
<#list contents.getSiblings() as cur_contents>
$cur_contents.getData()
</#list>
We now have enough information to create a template that can iterate
over a list of Web Content Articles and display each article.

CONTENT LIST DISPLAY TEMPLATE
With the Content List strucure, we can feature multiple Web Content
Articles.
We’ve set the basic styling in the Content List Display template.

BUILDING DIFFERENT DISPLAYS
It’s really useful to be able to reuse the same Web Content Articles and
just display them differently.
We’d like to be able to provide multiple displays for featured events:
Basic display
Thumbnail display
Carousel display
We’ve just completed the basic display, and could create new templates
to build out a thumbnail and carousel display.

A CAROUSEL AND A THUMBNAIL
What would it look like if we built carousel and thumbnail templates
and displayed the Web Content Articles inside them?
Not pretty.
We need to change how the article displays in each component.

SETTING VARIABLES ACROSS TEMPLATES
The Events Display template is responsible for how the article is
displayed.
But it doesn’t know anything about how the carousel or thumbnail
display or what changes they need.
We need a way to tell the events template how to change its display for
each template.

USING PREFERENCES TO SHARE SETTINGS
All of our Web Content Articles are being displayed in the Web Content
Display application.
Each application has a way to store preferences, or settings, as variables.
Setting preferences allows those settings to be used by any other
template in the application.
These preferences are available through an object in FreeMarker called
$freeMarkerPortletPreferences.
We can set and get different values using this object:
<#assign VOID = freeMarkerPortletPreferences.setValue("mySetting", "stuff") />
...
<#assign mySetting = freeMarkerPortletPreferences.getValue("mySetting") />
Note: we use an empty variable called $VOID to run the method
silently. We wouldn’t want return values displayed on the page.

A CAROUSEL, A LIST, AND THUMBNAILS...
We can now design each of the Web Content Templates to set a setting
we’ll call view:
thumbnailListView: We’ll set view to this when we’re displaying
thumbnails.
carouselListView: We’ll set view to this when we’re displaying a
carousel.
When we’re displaying the content in full, we won’t set the view setting.
Now, let’s build each template to tell the Event Display template which
style we need.

THUMBNAIL DISPLAY TEMPLATE
We’ve set the thumbnailListView setting in the Thumbnail Display
template.
This setting will be referenced in logic we’ll add to the Event Display
template.

CAROUSEL DISPLAY TEMPLATE
We’ve set the carouselListView setting in the Carousel Display
template.
This will be referenced in logic we’ll add to the Event Display template.

MAKING OUR EVENT DISPLAY SMART
We’re going to smarten up our Event Display template so that it
responds to the value of the view setting.
Using <#if> directives, we can build our event display using the right
Lexicon CSS components for the containing template.
If there is no view setting, then we’ll just display the event the way we
originally did.

ADVANCED EVENT DISPLAY TEMPLATE
In our updated Event Display template, we’ve added logic to allow the
template to respond to the view preference set in the Content List
templates.

TEMPLATES IN ACTION
With the logic we’ve added, the Event Display template will respond to
whichever template the Content List structure is using.

DISPLAYING LOTS OF CONTENT
Now that our displays are smart, respond to different environments, and
use the same type of Web Content (Event), let’s import some events.
Our Content Team has provided us with events that are featured on the
new Events page.
Let’s update our site to display these events using our new templates.

## Customizing Workflow Email Notifications

WORKFLOW OVERVIEW
Liferay’s Kaleo Workflow engine makes it easy to build and use review
processes with notifications to different parties.
While front-end developers aren’t responsible for setting up workflow,
they can provide FreeMarker notification templates.
These templates are useful for both branding and functionality.

WORKFLOW NOTIFICATIONS
Notifications can be sent to different parties on the following channels:
Email: Email notifications sent out to those assigned to a workflow task.
User Notification: Notifications sent to users logged into the platform
Instant Messenger & Private Message: Placeholders for Social Office

NOTIFICATIONS IN A WORKFLOW DEFINITION
Workflow Definitions are written in XML and include the notifications
within.
Here is an example of a review notification:
<notification>
<name>Review Notification</name>
<template>
${userName} sent you a ${entryType} for review in the workflow.
</template>
<template-language>freemarker</template-language>
<notification-type>email</notification-type>
<notification-type>user-notification</notification-type>
<execution-type>onAssignment</execution-type>
</notification>
In this simple example, we are using the ${userName} and ${entryType}
variables to pull in information for the name of the submitter and the
type of asset.

CREATING ADVANCED NOTIFICATION TEMPLATES
Because Workflow notifications are just FreeMarker templates, front-end
developers can provide the same kind of customization here that they
would elsewhere.
There are a number of context variables available that allow developers
to add functionality.
Lexicon CSS styling and JavaScript can also be added into the templates
using the <style> and <script> tags.
With these features at the ready, notifications can be as simple or
advanced as the business requirement needs.

GETTING INFORMATION INTO THE WORKFLOW TEMPLATE
Pulling information into our workflow definition is not much different
from the same process for an Application Display Template.
In this example, we’ll start off simple and pull information from the
workflow.
Recall that as something goes through the workflow, workflow approvers
are able to leave comments along the way.
We’ll pull information from the comments that are left from the
workflow approvers.

WHAT’S GOING ON HERE?
Our email notification template is simple.
We first assign taskComments to the comments variable, allowing us to
display comments from the workflow process.
Then we create a simple HTML structure that shows the graded
assignment, using the entryType variable, and the included comments if
they exist.
<![CDATA[
<#assign comments = taskComments!"">
<!-- email body -->
<p>
Your assignment, ${entryType}, has been graded by the instructor.
<#if comments != "" >
<br />Here are the comments included: <strong>${comments}</strong>
</#if>
</p>
<!-- signature -->
<p>Sincerely,<br /><strong>S.P.A.C.E. Instructor</strong></p>
]]>

STYLING AND BRANDING OUR EMAIL NOTIFICATIONS
We can provide additional company branding or styling to our
notification templates.
Adding styling to the template is simple, but more complex notifications
could potentially be a bit unwieldy.
Instead of adding all the styling in the template, we can do things like
reference web content in our notifications.
Injecting web content helps keep things much cleaner and more
modular in the workflow xml file.

THE SERVICELOCATOR
Our snippet is referencing web content by using the following:
<#assign journalArticleLocalService = serviceLocator.findService("com.
liferay.journal.service.JournalArticleLocalService") />
Because the serviceLocator can get access to the database, it is
restricted by default.
This variable can be unlocked by removing it from the Freemarker
Engine Restricted Variables found in Menu→Control
Panel→Configuration→System Settings→Foundation.
This is typically done by a System Administrator.

MAKING THE WORKFLOW DEFINITION AVAILABLE
Once the notification templates have been added, the xml can be
handed off to an administrator.
Administrators can make the workflow definition xml available for use
by doing the following:
Going to Menu→Control Panel→Configuration→Workflow Definition
Uploading the xml definition
Once the definition is available, workflow can be configured on
document folders where Students upload their assignments.
When an assignment is uploaded, Instructors can grade and provide
comments.
Our notification template will take those comments and provide the
feedback directly to the students via email.

## Creating Different Front Ends for Applications

CUSTOMIZING APPLICATION DISPLAYS

KEEPING THE LOOK
We want to keep applying our look and feel throughout Liferay.
Templates give us the tools to create consistent styling in most places:
Theme Templates control the basic HTML and page styling for every page
in Liferay
Layout Templates control application layout on pages
Web Content Templates control the look and feel and functionality of Web
Content
Workflow Notification Templates apply our styles to Workflow notifications
That takes care of most of the areas of Liferay we can directly control,
aside from additional features.
Many features are implemented in applications.
Ideally, we want to make sure applications in Liferay look, feel, and
behave consistent with our branding.

CUSTOMIZING APPLICATIONS
Usually applications are built by developers using Java and complex
back-end tooling.
Customizing the display usually means becoming familiar with:
Java Web App structure
JSPs
Taglibs in JSPs
JSF
In addition, you’d also need to have an environment set up to modify,
build, and deploy applications in Liferay.
Fortunately, Liferay lets us override the default display of lots of
applications.
Just like Web Content Display, applications can also support Templates.
Application Display Templates take the same templating framework, and
apply it to applications.

WHAT ARE APPLICATION DISPLAY TEMPLATES?
The Application Display Template (ADT) framework allows administrators
to override the default display of supported applications, removing
limitations to the way your applications display content.
With ADTs, you can define custom templates used to render
asset-centric applications.

APPLICATIONS INCLUDED IN THE ADT FRAMEWORK?
Any application can support ADTs, including custom-built applications.
Liferay provides lots of content applications with full ADT support.
The following applications support ADTs:
Asset Categories Navigation
Asset Publisher
Asset Tags Navigation
Blogs
Breadcrumb
Language
Media Gallery
Navigation Menu
RSS
SiteMap
Wiki

WHY USE ADTS?
ADTs can create different displays for applications without back-end
development.
Use the same knowledge for building Web Content Templates, Workflow
Notification Templates, and ADTs.
ADTs provide the ability to:
1. Create multiple views for a single application that can be selected by a
Site Administrator
2. Develop with advanced back-end functionality like serviceLocator and tag
libraries through the GUI without having to deploy your changes to the
server
3. Use advanced styling options like Lexicon CSS

STYLING APPLICATIONS

WHAT YOU NEED
This module uses:
Installed theme:
space-program-theme.war
You can find the theme in exercises/front-end-developer-exercises/05-
front-end-developer/03-theme-development/solutions.
Our Theme includes some content and Application Display Templates
(ADTs) for us to take a look at.

ASSET PUBLISHER ADT EXAMPLE
Let’s look at an example of an ADT bundled in our theme.
The theme let us create some useful assets in a sample site
We have a number of Asset Publisher ADTs in use on the sample Space
Program site generated by the Resources Importer.
We’ll look at the Entry List 3 Item ADT.

ADTS AND WEB CONTENT TEMPLATES
Web Content Templates and ADTs use the same basic type of template.
Since they both use FreeMarker, it’s easy to write for both.
The difficulty can be in remembering what makes them different.
ADTs reinforce styling, but have the main purpose of displaying
(rendering) different types of assets.
Let’s look at our example ADT in detail so you can see what that looks
like.
This ADT displays content articles as image tiles with information below
with 3 columns.

ADTS HAVE ONLY ONE JOB
The main job of ADTs is to display dynamic data in markup.
This ADT is for the Asset Publisher, whose main content is assets.
You’ll notice the ADT gets a list of assets to display.
Let’s look more closely at how the assets are displayed and styled
consistently.

MAKING ADT DESIGN EASIER
The built-in editor makes it easier to reference variables.
You can see an example of that in the Entry List 3 Item ADT.
The ADT takes the default Asset Entries * field and expands upon it.
Here is what is generated when you select Asset Entries * in the
editor:
<#if entries?has_content>
<#list entries as curEntry>
${curEntry.getTitle(locale)}
</#list>
</#if>

ADDING CUSTOM ADT CODE
Within the <#if> Structure, there are attributes set on the displayed
content:
<#if entries?has_content>
${request.setAttribute("displayMode", 2)}
${request.setAttribute("colMd", "col-md-4")}
...
${request.setAttribute("author", "" )}
${request.setAttribute("displayMode", 0)}
${request.setAttribute("viewURL", "" )}
</#if>
We also have this markup added:
<div class="blog-list container-fluid-1280">
<div class="row">
<#list entries as curEntry>
...
</#list>
</div>
</div>

CARD LIST - FEED: EXPLANATION
1. In the Card List - Feed ADT, we check to see if there are any
entries, and then iterate through the list.
You can hover over Asset Entries * for more information on entries.
2. Next, we use Lexicon CSS Cards to create the card layout.
http://liferay.github.io/clay/content/cards/
3. Finally, we’ll display the article title, URL, and summary from our Asset
Renderer.
As we’re displaying Web Content Articles, see JournalArticleAssetRenderer
for more information.
4. As front-end developers, we can collaborate with our back-end team to
display dynamic content.

ASSET URLS
We’re using a URL for the article called View in Context.
View in Context needs the article to be displayed on a page in order to
work.
If you’d like to test the URL, you’ll want to add the Web Content Article
to a page somewhere before using the link.

CARD LIST - EVENTS: EXPLANATION
1. In the Card List - Events ADT, the code is almost identical except for a
few CSS changes.
Instead of an rss icon, we displayed a calendar icon and changed the font.
2. The main difference is that we configured Asset Publisher to pull Web
Content Articles that use the Events Web Content Structure.
3. We’ll see the results of these changes in a few slides.
4. Asset Publisher, Application Display Templates, and Web Content
Templates gives us precise control to create consistent branding and
work better with our content marketing team in a way that allows both
teams to focus on our areas of our expertise.

BRINGING IT ALL TOGETHER
Let’s import some content created by our content team in order to see
everything in action.
The content team has already configured the Asset Publishers to pull in
the content they want to display.
For the Asset Publisher at the top, they’ve configured it to pull in Web
Content Articles that use the News Structure.
For the second Asset Publisher, they’ve configured it to pull in Web
Content Articles that use the Events Structure.
The front-end team provided consistent styling for the Web Content
using Web Content Templates.
The front-end team will be responsible for applying the design, which
we’ve completed above with ADTs.