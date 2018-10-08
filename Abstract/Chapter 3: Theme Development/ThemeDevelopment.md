#Theme development

##Themes definition and use
- Controls every part of UI and UX (Html, css, images)
- Is a collection of: Css, Js, images and templates. These files are packaged 
in a module that gets deployed in your instance
- Developers can create modules to override: Product and control menu, control
panel, site administration panel, simulation menu and application displays
- Tools and libraries to develop themes:
    - Liferay theme generator, themelets, bourbon, theme contributors, 
    importing resources
- A custom theme can be based on one or two base themes
- A theme can be created with Liferay theme generator
- Themelets used to modify small areas in a theme (looks like a component)
- Bourbon is a mixin library for Sass
- Theme contributors package UI resources independent of a theme and include 
them on a page
- Resource importer allow to deploy a theme with predfined content helping out
to provides a reusable site template

##Liferay theme generator
- Create a theme with theme generator and theme tasks
- Generator is used to create a theme boilerplate
- Tasks is a set of gulp tasks used for building and deploying a theme

##Yeoman generator
- There are four generators in generator-liferay-theme package
    - `liferay-theme` --> Create the base theme files and install the 
    dependencies for deployment
    - `liferay-theme:import` --> Imports an existing theme
    - `liferay-theme:layout`
    - `liferay-theme:themelet`
- After run `liferay-theme` it's create this structure
    - gulpfile.js: register tasks from liferay-theme-tasks to your theme
    - liferay-theme.json: Created by `gulp init` that stores configuration
    - node_modules: Dir where npm are installed
    - package.json: Where metadata and npm dependencies are declared
    - src: contais source files of theme
        - /WEB-INF: metada files such as plugin-package.properties and 
        liferay-look-and-feel.xml
##Gulp tasks
- All these tasks are executed from root's theme directory
- `gulp build`: compiles all source files into the build directory and creates
a war file in dist directory of your theme
- `gulp deploy`: run all build tasks and then deploys the generated war file
to specified appserver
- `gulp watch`: watch for changes to theme sources files, make a quick deploy 
and on refresh the page take the effect
- `gulp init`: specify your appserver for use with the deploy task
- `gulp extend`: Set what base theme you will extend your theme from, also
add themelets to your themes
- `gulp status`: Reports what base theme and themelets are implemented
##Key files for theme customization
- portal_normal.ftl: the main HTML source file
- _custom.scss: global styling
- main.js: global scripts
- liferay-look-and-feel.xml: theme settings, color schemes and packaged layout
templates
##Page structure
- 3 major customizable sections in portal_normal.ftl
    - Banner: top page
    - Content: breadcrumbs, layouts and applications
    - Footer: Bottom of the page
- Themes use freeMarker (.ftl) as the main templating language
- Basic features: 
    - Interpolations: `${default_url}`, expressions that will be evaluated and 
    then results on the page
    - Directives: Special tags that doesn't always result on a visual difference
    `<#assign default_url = "http://spaceprogram.liferay.com/" />`
- A theme contains:
    - Fonts: custom fonts 
    - Images: images used
    - Js: js referenced in templates
    - Layouttpl: custom liferay layout templates
    - Templates: freemarker templates for html structure
- When a html file is generated a few templates are to create the source HTML
    - portal_normal.ftl: main document of every page (like a master page)
    - portlet.ftl: contains the html surrounds each application on the page
- Include external templates using: `<#include />`
- Macros allow you to assign template fragments to a variable 
`<@liferay.language_format />`
- Assign a value to a variable `<#assign />`
- For instance, including a new font can be this easy: `@include font-face(` +
    `"open_sansregular", "../fonts/opensans-bolditalic-webfont", bold, italic);`
##Custom JS
- liferay-theme-es2015-hook allows es2015 transpilation
- after build with transpiled files they will be packaged as amd modules
- it needed to be add on package.json 
`hookModules: ["liferay-theme-es2015-hook"]`
- import dependencies like `import State from 'metal-state/src/State'`
- With ES2015 you can also uses class, constructors and inheritance
##Theme configuration
- liferay-look-and-feel.xml configs for custom layout templates, theme settings,
and application decorators
- liferay-plugin-package.properties contains info and properties for our theme
##Application decorators
- In liferay-look-and-feel when this decorators is applied --> happens:
    - Barebone: Neither the wrapping box nor custom application title is shown
    - Borderless: The application is no longer wrapped by a white box, but the
    custom title is displayed at the top
    - Decorate: The application is wrapped in a white box with a border and the
    custom title is displayed at the top
- Every decorator added to .xml require css class:
`<portlet-decorator-css-class>[Class name]</portlet-decorator-css-class>`
- And add css styling on _portlet_decorator.scss
- A default decorator need to be set, so just add on liferay-loon-and-feel.xml: 
`<default-portlet-decorator>true</default-portlet-decorator>`
- Import it on _custom.scss `@import "portlet_decorator";`
##Theme Settings
- Set configurable values into a theme that can be accessed into ftl 
(like this: `<#assign new_variable = getterUtil.getBoolean(`
`themeDisplay.getThemeSetting("new-theme-setting")) />`) and once deployed 
is editable on control panel
- Each them setting have default properties:
    - configurable: bool var to set hidden or displayed to a field
    - key: retrieve user value (like id)
    - type: typ of form field
    - options: a comma separated list of options
    - value: default setting value
- liferay-plugin-package.properties contains default information of our theme
- A color scheme can be personalized on liferay-look-and-feel.xml
##Themelets
- Reusable pieces of code that are implemented by a theme (like a component)
- Consists of css, templates, images and js like a theme
- Can be saved like a npm package and published
- `yo liferay-theme:themelet` import a new themelet to yout theme
- it's structed like themes with src folders, a package json containing metadata
and a custom scss file
- Themelet css and js can be injected via Sass imports and script tags between
its respectives comment tags:
    - Css: `/* inject:imports */ /* endinject */`
    - JS: `<!-- inject:js --> <!-- endinject -->`
##Theme contributors
- Is a module that contains UI resource independent of theme (global content)
- Control menu, Product menu and simulation panel are packaged in theme 
contributors
- To create a theme contributor you have to: Create an Osgi module an identify
the module as a theme contributor by adding `Liferay-Theme-Contributor-Type` 
and `Web-ContextPath` properties on bnd.bnd file
    - Liferay-Theme-Contributor-Type: To identify your module as a theme 
    contributor
    - Web-ContextPath: sets the context for which theme contributors resources
    are hosted
- Set Priority to your bnd file setting `Liferay-Theme-Contributor-Weight: 100`
- All SCSS resources are imported in blade.theme.contributor.scss file
##Resources importer
- Defined in sitemap.json, describing the contents and hierarchy of a site that
liferay can import as a site template
- Sitemap.json defines: Pages, layout templates, applications, preferences and
content
- Assets can be also imported with or without metadata
- Documents and media, web content can be imported as well
##Portlet Preferences
- Are properties that stores basic application configuration data
- groupId -> selects a site
## Embedding applications
- embed your application into portal_normal.ftl that will render them on each
page
- There are 3 taglibs to use: 
    - `<@liferay_portlet["runtime"]>`: Expect 2 parameters: 
    portletProviderAction and portletProviderClassName
    - `<@liferay_journal["journal-article"]>`
    - `<@liferay_ui["asset-display"]>`
- PortletName is the application id as string reference of the application 
class path
- Is possible to set preferences in an application using 
${freeMarkerPortletPreferences}, allows to change application preferences and
have it immediately displays on theme
- Portlet Runtime attributes:
    - defaultPreferences: include look 'n feel configs
    - instanceId: instance id
    - persistSettings: if the settings persists across layouts
    - settingsScope: which settings the application is to use