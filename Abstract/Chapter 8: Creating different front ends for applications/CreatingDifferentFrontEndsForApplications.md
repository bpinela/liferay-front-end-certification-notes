# Creating different front ends for applications

## Customizing applications
Theme Templates control the basic HTML and page styling for every page
in Liferay
Layout Templates control application layout on pages
Web Content Templates control the look and feel and functionality of Web
Content
Workflow Notification Templates apply our styles to Workflow notifications
Just like Web Content Display, applications can also support Templates.
Application Display Templates take the same templating framework, and
apply it to applications.

## Application display templates
- Application Display Template (ADT) framework allows administrators
to override the default display of supported applications, removing
limitations to the way your applications display content.
With ADTs, you can define custom templates used to render
asset-centric applications.
Any application can support ADTs, including custom-built applications.
Liferay provides lots of content applications with full ADT support.
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
- Web Content Templates and ADTs use the same basic type of template.
The main job of ADTs is to display dynamic data in markup.
This ADT is for the Asset Publisher, whose main content is assets.
## Asset Urls
We’re using a URL for the article called View in Context.
View in Context needs the article to be displayed on a page in order to
work.