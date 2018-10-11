# Delivering Consistent Content Experiences

## Styling content with web content templates
- Provide style to web content using WYSIWYG editor or embedding int web 
content template
- Alloy editor
## Adding templates
- In Site Administration > Content > Web Content you can add structures 
and templates
- They are managed in options menu
## Developing templates
- Web content is unique in that structure
- all Html tags by default inherit global theme style
## Generic Templates
- Are web content templates that are not associated to any structure
- It could be imported into another template 
`<#include "${templatePath}/TEMPLATE-ID />"`
## Embed application in templates
- Custom or core can be embedded into templates
    - in Ftl: `<@liferay_portlet_ext["runtime"]portletName=`
    `"com_liferay_currency_converter_web_portlet_CurrencyConverterPortlet" />`
    - In Velocity: `$theme.runtime("`
    `com_liferay_currency_converter_web_portlet_CurrencyConverterPortlet");`
## Simulation options
- Simulation menu has options for:
    - Desktop: show content from desktop view
    - Tablet: show vertical and horizontal preview of a tablet
    - Mobile: show vertical and horizontal preview of a mobile device
    - Auto-size: Resize as needed
    - Custom: Set custom breakpoints