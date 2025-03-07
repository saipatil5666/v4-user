---
sidebarDepth: 1
---

# 🔌 Popup Upload Plugin

The popup upload plugin (PUP) is a small file that allows to provide external image uploading via a small JavaScript file.

::: tip
When PUP is enabled, the route `/plugin` shows the instructions in how to add image uploading functionality to other websites.
:::

## How it works

PUP binds user-editable content with an upload button that will trigger an image upload dialog and it will auto handle the codes needed for image insertion. End-users will experience a fluid and neat process without leaving the original website.

## Supported devices

PUP should work in any modern web browser (HTML 5) regardless of the user device (that includes mobile devices). It has been tested and confirmed to work on Windows, Mac, Linux and Android (Chrome).

## Installation

Basic installation is easy as copy the following code into any HTML section of the target website. You can add custom options right on this code.

```html
<script async src="//demo.chevereto.com/sdk/pup.js" data-url="https://demo.chevereto.com/upload"></script>
```

**Note:** You need to edit `src` and `data-url` to match your Chevereto website.

PUP works on the DOM so it doesn't have any server-side dependencies and it can be installed on any website.

## Customization

All plugin customizations are handled via [data attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*) that you must add to PUP base code. As an example, to use the red color palette the code should look like this:

```html
<script async src="//demo.chevereto.com/sdk/pup.js" data-url="https://demo.chevereto.com/upload" data-palette="red"></script>
```

This applies to all PUP options. The format is **data-_key_** where **_key_** is the target option key, in this case the palette option is being declared as the `data-palette` attribute value.

### Options

This is the list of all the plugin key options available.

### `url`

URL of the target Chevereto website.

| Type   | Example                    |
| ------ | -------------------------- |
| String | https://demo.chevereto.com |

### `palette`

Named color palette of the button or a comma-separated list of colors (HEX, RGB, etc.). When using a comma-separated list of colors, the system will bind each color to a `%n` color index (starting at `%1`) that you can use with custom CSS.

| Type   | Values                                                                                                  | Default   |
| ------ | ------------------------------------------------------------------------------------------------------- | --------- |
| String | `default` `clear` `turquoise` `green` `blue` `purple` `darkblue` `yellow` `orange` `red` `grey` `black` | `default` |

### `auto-insert`

  Embed codes to auto insert in the target editable content. Codes using `full`, `medium` or `thumbnail` will link to the image viewer page.

  Use `0` to disable auto insert.

| Type   | Values                                                                                                                                                                                                                                                                                  | Default               |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| String | `0` `viewer-links` `direct-links` `html-embed` `html-embed-full` `html-embed-medium` `html-embed-thumbnail` `bbcode-embed` `bbcode-embed-full` `bbcode-embed-medium` `bbcode-embed-thumbnail` `markdown-embed` `markdown-embed-full` `markdown-embed-medium` `markdown-embed-thumbnail` | `bbcode-embed-medium` |

### `sibling`

Sibling CSS selector to use it as a reference to the DOM node where the button should be inserted. By default, the button will be placed relative to the editable content. When the sibling is defined, the plugin will search for that element and it will use it as the reference for button insertion.

| Type   | Example    |
| ------ | ---------- |
| String | `.sibling` |

### `sibling-pos`

Position relative to the sibling to place the button.

| Type   | Values           | Default |
| ------ | ---------------- | ------- |
| String | `before` `after` | `after` |

### `vendor`

Named vendor string.

| Type   | Values                                                                                                       | Default |
| ------ | ------------------------------------------------------------------------------------------------------------ | ------- |
| String | `bbpress` `discourse` `discuz` `ipb` `mybb` `nodebb` `phpbb` `smf` `vanilla` `vbulletin` `woltlab` `xenforo` | `auto`  |

### `mode`

Plugin mode. By default, the plugin binds to any matching editor box. Use `manual` mode to explicitly insert the button and stop any automatic binding.

| Type   | Values          | Default |
| ------ | --------------- | ------- |
| String | `auto` `manual` | `auto`  |

### `target`

CSS selector for target editable content. Use it when manually inserting the button.

| Type   | Example     | Default |
| ------ | ----------- | ------- |
| String | `.selector` | `auto`  |

### `lang`

Button language for two-letter and four-letter language codes.

| Type   | Values                                                                         | Default |
| ------ | ------------------------------------------------------------------------------ | ------- |
| String | `ar` `cs` `de` `es` `fi` `fr` `id` `it` `ja` `nl` `pt_BR` `ru` `zh_CN` `zh_TW` | `auto`  |

### `container-class`

Custom button container class name. It binds `%cClass` to the template stack.

| Type   | Example     | Default                   |
| ------ | ----------- | ------------------------- |
| String | `className` | `chevereto-pup-container` |

### `button-class`

Custom button class name. It binds `%bClass` to the template stack.

| Type   | Example     | Default                |
| ------ | ----------- | ---------------------- |
| String | `className` | `chevereto-pup-button` |

### `html`

[Custom HTML](#custom-html).

| Type | Example |
| ---- | ------- ||
| String | `<div>Button<div>` |

### `css`

[Custom HTML](#custom-html).

| Type   | Example                |
| ------ | ---------------------- |
| String | `.div { color: red; }` |

### `fit-editor`

A boolean indicating if the plugin should fit the button to the target editor toolbar.

When disabled, the plugin won't fit the button styling to the target editor (override valid only for supported vendors).

| Type    | Values  |
| ------- | ------- |
| Integer | `0` `1` |

### `observe`

CSS selector for elements that on click event will trigger sibling observation and then button insertion (live append). Useful for dynamic editors that generate editor boxes on the fly.

| Type | Example |
| ---- | ------- ||
| String | `.selector` |

### `observe-cache`

A boolean indicating if a matched observed element should be cached.

When enabled, it will stop observing the matched observed element click events. Always disable observe cache if the editor is dynamically generated and not stored as a DOM node.

| Type    | Values  | Default |
| ------- | ------- | ------- |
| Integer | `0` `1` | `1`     |

### Custom HTML and CSS

PUP supports template placeholders, which is a special string that PUP will convert into usable markup.

Template placeholders available:

| Tag      | Description                                                 |
| -------- | ----------------------------------------------------------- |
| %x       | PUP button observer (must be used to trigger button action) |
| %cClass  | Container class name                                        |
| %bClass  | Button class name                                           |
| %iClass  | Icon class name                                             |
| %iconSvg | Vector icon in the form of a ready-to-use SVG HTML tag      |
| %text    | Translated button text                                      |

For custom CSS, you can also use color palette placeholders in the form of `%n` where **n** is the color palette index. It binds `%1`, `%2`, ..., `%n` placeholders.

Custom HTML works by indicating the template string as an option attribute. In this example, this is the custom HTML that we want to use:

```html
<a %x title='%text' class='%bClass'>%iconSvg</a>
```

To use this template, simply assign `data-html` right into the plugin code:

```html
<script async src="//demo.chevereto.com/sdk/pup.js" data-url="https://demo.chevereto.com/upload" data-html="<a %x title='%text' class='%bClass'>%iconSvg</a>"></script>
```

Custom CSS works exactly the same as custom HTML but it uses `data-button-css` and color palette placeholders (`%1`, `%2`, ..., `%n`). In this example, this is the custom CSS that we want to use:

```
li.%cClass .%bClass{background:%1;color:%2;text-indent:unset;border-radius:3px;position:relative}li.%cClass a.%bClass:hover{background:%3;color:%4;border-color:%5}.%cClass .%bClass svg{font-size:15px;width:1em;height:1em;-webkit-transform:translate(-50%,-50%);-ms-transform:translate(-50%,-50%);transform:translate(-50%,-50%);position:absolute;left:50%;top:50%;fill:currentColor}
```

To use this template, simply assign `data-css` right into the plugin code:

```html
<script async src="//demo.chevereto.com/sdk/pup.js" data-url="https://demo.chevereto.com/upload" data-css="li.%cClass .%bClass{background:%1;color:%2;text-indent:unset;border-radius:3px;position:relative}li.%cClass a.%bClass:hover{background:%3;color:%4;border-color:%5}.%cClass .%bClass svg{font-size:15px;width:1em;height:1em;-webkit-transform:translate(-50%,-50%);-ms-transform:translate(-50%,-50%);transform:translate(-50%,-50%);position:absolute;left:50%;top:50%;fill:currentColor};"></script>
```

**Important:** For both custom HTML and CSS make sure to don't break the syntax when using quotes.

### Manual button binding

To manually bind a button, simply create your own button make sure to add `data-chevereto-pup-trigger` and `data-target` attributes. This is an example of a manually inserted button:

```html
<div id="editor" contenteditable></div>
<button data-chevereto-pup-trigger data-target="#editor">Custom button</button>
```

Manually inserted buttons get the same popup dialog functionality and binding. However, manually inserted buttons won't use any of the plugin options or templating.

## Core features

This plugin has very neat functions and takes advantage of modern standards to provide its core functionality. These are some of the features shape the PUP core.

### Native JavaScript

PUP is written in modern JavaScript standard and it doesn't require any external library or server module. The code is about 18KB and gzipped should be around just 6KB. The source is minified using [Google Closure compiler](https://developers.google.com/closure/compiler/) but object names aren't touched so you can inspect the source and easily understand the code.

It works async so it doesn't matter where you place the insertion code and it won't render block the load of the target website at all.

### Smart load and dynamic trigger observer

PUP is designed to observe the DOM until the target sibling element is available and soon as that happens, it will initiate its process and it will stop any additional DOM node observation. For dynamically generated editor boxes, PUP has a complimentary load option that observes the click event on a defined selector element. Any click on that element will trigger PUP's sibling observation and it will stop soon as the sibling gets found. This allows PUP to work in static or dynamic editor boxes.

Since some dynamic editor boxes will be generated just once and then stored as DOM nodes (XenForo) and others will be always re-parsed (Discourse, NodeBB), you can indicate if PUP should cache or not the observed triggered bindings. XenForo, Discourse and NodeBB vendors are configured to observe certain selectors just in case you want to learn how this works.

### Closure

The source is all wrapped in a JavaScript closure meaning that the internal variables can't be tempered. This aims to avoid hijacking via browser console exploits or DOM manipulation. This closure also grants that all the variables handled by PUP won't conflict with any of the scripts running on the target website.

### postMessage

PUP uses [postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) API to keep an active communication with the target Chevereto website. Options and embed codes are safely handled using this API which restricts the origin of the posted messagese and on top of that, PUP validates each message to ensure that there's no tempering on those either. PUP will only listen to messages from the target Chevereto website.

### Multiple instances

PUP supports multiple unlimited instances. You can cast multiple buttons at the same time and all instance ids are referenced using the [GUID algorithm](https://en.wikipedia.org/wiki/Universally_unique_identifier).

### Template cache

PUP will cache the button template so it won't unnecessarily re-process the template placeholders. This grants super fast performance even in multiple instances.
