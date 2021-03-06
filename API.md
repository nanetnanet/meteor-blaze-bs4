# API

The following file documents the high level usage of the available components.

### Conventions

* The template are named like the respective components in the [Bootstrap documentation](https://getbootstrap.com/docs/4.1/components/alerts/) in lowercase.
Some Templates allow to insert dynamic content, while others don't. Therefore you should check the documentation for each component's example code.

* Many templates are parameterized and offer optional functionality. The component's documentation should also show you, which parameter formats are required.

* The github repository comes also with an example project that includes all components for demonstration purposes.
Consider to check it's code in order to get a better understanding of all the possible parameters.

* There will be sometimes a reference to the "theme color names". These include the following values:

  * `primary`
  * `secondary`
  * `success`
  * `warning`
  * `danger`
  * `info`
  * `light`
  * `dark`

Wherever referenced as parameters (and not stated otherwise) these values are required as listed above and without any prefix.

**Note:** Components which strictly require a given color of the theme colors will default to `secondary` if none is given. 

### Components / Templates

The following properties are documented:

* name - the **name of the template** as it will be included
* dynamic - whether a template is dynamic (`{{#example}}<p>custom markup</p>{{/example}}`) or not (`{{> example}}`). Sometimes both are possible.
* param - description of a parameter; follows the pattern `name` - `type` - `description`
* event - description of an event callback that can be passed from another template; follows the pattern `name` - `eventName` - `description` 

#### Alert

**name:** `alert`

**dynamic:** yes (optional)

**param** type (String) - One of the theme color names.

**param** heading (String) - Text to be rendered as head (`h4`)

**param** dismissible (Boolean) - Add dismiss button to the component

**param** onClose ('close.bs.alert') - This event fires immediately when the close instance method is called.

**param** onClosed ('closed.bs.alert') - This event is fired when the alert has been closed (will wait for CSS transitions to complete).

**example**

```html
<template name="myTemplate">
{{#alert type="success" heading="Well done!" onClose=onClose onClosed=onClosed}}
    <p>Aww yeah, you successfully read this important alert message. This example text is going to run a bit longer
        so
        that you can see how spacing within an alert works with this kind of content.</p>
    <hr>
    <p class="mb-0">Whenever you need to, be sure to use margin utilities to keep things nice and tidy.</p>
{{/alert}}
</template>
```

```javascript
const logEvent = event => console.log(event)

Template.myTemplate.helpers({
  onClose () {
    return logEvent
  },
  onClosed () {
    return logEvent
  }
})
```

**example**

```html
<template name="myTemplate">
{{> alert type="success" heading="Yeah, one-liners!" dismiss=true onClose=onClose onClosed=onClosed}}
</template>
```

#### Badge

name: `badge`

**dynamic:** no

**param** type (String) - One of the theme color names.


**example**

```html
<template name="myTemplate">
  <h1>Example heading {{> badge type="secondary" content="New"}}</h1>
</template>
``` 

#### Breadcrumb

**name** `breadcrumb`

**dynamic** no

**param** entries (Array) - List of all entries for being rendered as links.

entries.entry (Object) - Representing all required data to create a link.

entry.title (String) - The title / label to be displayed
entry.href (String) - The route / url
entry.classes (String) - Optional. Add optional classnames to each link
entry.<html a attributes> - any html <a> related attributes

example

```javascript
Template.myTemplate.helpers({
  bredcrumbEntries () {
    return [
      {
        title: 'home',
        active: false,
        href: '/'
      },
      {
        title: 'examples',
        active: false,
        href: '/examples'
      },
      {
        title: 'breadcrumbs',
        active: true,
        href: '/examples/breadcrumbs'
      }
    ]
  }
})
```

```html
<template name="myTemplate">
  {{> breadcrumb entries=bredcrumbEntries}}
</template>
```

#### Button


**name** `button`

**dynamic** yes / no

**param** type (String) - One of "button", "submit", "reset"

**param** colortype (String) - One of the theme color names. Additional possible: "link"

**param** id (String) - id of the button

**param** class (String) - additional classes

**param** atts (Object) - Dynamic attributes, overrides attributes, that are manually set.

**param** label (String) - Set this to a string to display a label in non-dynamic buttons. Leave out if you want dynamic content blocks.

**param** size (String) - one of "lg", "sm", "block", leave for default

**param** outline (Boolean) - convert to outline button style

**param** disabed (Boolean) - disable component (no events fired if true)

**example non-dynamic**

```html
{{> button colortype="primary" label="Large Button" size="lg"}}
```

**example dynamic**

```html
{{# button colortype="primary" size="lg"}}
    <i class="fa fa-fw fa-pencil"></i>
    <span>Custom Label</span>
{{/button}}
```

### Jumbotron


**name** `jumbotron`

**dynamic** no

**param** fluid (Boolean) - Optional. Renders a fluid jumbotron.

**param** class (String) - Optional. additional classes


### Progress

**name** `progress`

**dynamic** no

**param** value (Number) - Required. Defines a progress value between 0 and 100. Alternative values are allowed but you then need to use `perc` to describe progress width.

**param** perc (Number) - Optional. Defines a progress value if min and/or max are beyond default values of 0 and 100.

**param** type (String) - One of the theme colors. Defaults to primary if none is given.

**param** class (String) - Optional. additional classes

**param** min (Number) - Optional. Defines a min value. Defaults to 0 if none is given.

**param** max (Number) - Optional. Defines a max value. Defaults to 100 if none is given.

**param** label (String) - Optional. Sets a label to be displayed inside the progress bar.

**param** height (String) - Optional. Sets the height of the progress. Note, that you need to provide a css measurement unit, too. Valid examples: "20px" or "4rem" etc.

**param** striped (Boolean) - Optional. Renders a striped background.

**param** animated (Boolean) - Optional. Renders the progress bar background animation.

**example non-dynamic**

```html
{{>progress value=75 striped=true animated=true label="Progress: 75%"}}
```
