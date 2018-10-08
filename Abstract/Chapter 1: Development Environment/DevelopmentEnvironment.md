#Development Environment

##Introduction to front end development
- 2 general options for stylistc changes
    - Modules: Themes and laoyut templates for global look'n feel changes
    - Templates: specific customizations for content, applications and 
    email notifications
- Developing
    - Customizations and new features are deployed in modules
    - Themes and layout templates are installed as modules
- Standard Tools
    - Node.js: provides the platform
    - gulp: create new projects
    - Yeoman: build and deploy
- Dev tools for modules
    - JDK8: run liferay and the installer. also set JAVA_HOME env var
    - Node.js: install theme generator and its dependencies
    - Yeoman and gulp: run theme generator and theme tasks
    - Liferay theme generator: generate themes and themelets
    - Brackets: Text editor
    - Liferay tomcat bundle: view dev changes locally
##Setting up the dev env
- Install Java (Jdk8), also set JAVA_HOME env variable
- Install node.js
- Install gulp and yeoman globally `npm install -g yo gulp`
- Install liferay theme generator `npm install -g generator-liferay-theme`
- Install liferay tomcat bundle (provided with basic material in liferay
website)
## Config files
- portal-setup-wizard.properties for basic config properties
- portal-ext.properties to override basic properties (portal.properties)
- Read order: 
    - portal.properties > portal-ext.properties > portal-setup-wizard.properties

    


