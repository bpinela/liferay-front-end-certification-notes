# Customizing the front end

## Templates
- Liferay provides ADTs (Application display templates) for styling different
aspets of applications
- There are many resources where you can use templates for styling:
    - Assets: Web content and data lists have their own templates
    - Applications: Asset Publisher or navigation can be styled through ADTs
    - Custom applications: Can also have ADTs to style them
    - Notifications: You can provide branding for workflow email notifications
- Additionally you can use Soy and Jsx templates
- An ADT can be displayed as full content displays full article in list form
and rich summary provides the option `read more...` and the share action
- A template can be built with .xls, .ftl or .vm(velocity)
- Use taglibs with ftl like:
    - liferay-portlet-ext.tld is specified as `@liferay_portlet_ext`
- you CANNOT access db with ftl files, just using `serviceLocator`but you
have to leave your db unrestricted...
- Context Contributors offers a middle ground to access your data safely in
your template
    - There are 2 types of them:
        - TYPE_GLOBAL: Global variables
        - TYPE_THEME: theme scope variables