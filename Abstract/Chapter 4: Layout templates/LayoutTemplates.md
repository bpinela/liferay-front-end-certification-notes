# Layout templates

## Layouts definition
- Layuout templates control the positioning of the content between header and
footer
- Liferay comes bundled with some predefined layout templates like: 1 column,
2 columns(50/50), 2 columns(30/70), etc...
- 12 sections following bootstrap model `col-md-12`
- A layout can be created `yo liferay-theme:layout`
- `$processor.processColumn` is necessary to render our layouts.
- It's possible to embeed an application into your layout an it's more flexible
in comparison of a theme `$theme.runtime('portlet_name')`


