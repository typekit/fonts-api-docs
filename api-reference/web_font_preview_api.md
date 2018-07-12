# Web Font Preview API

The goal of the Typekit Web Font Preview API is to allow a web app to quickly preview content using a set of fonts from Typekit without actually creating and publishing a kit in order to do it. It was created as an alternative to other approaches that are less ideal.

The solution we’ve created is to use a separate JavaScript API to load the individual fonts that you need on the fly. Named TypekitPreview, this JavaScript API uses the same JavaScript machinery as normal Typekit kits to determine browser support and trigger font events. The difference is that the fonts are loaded from a dynamic endpoint.

The Web Font Preview API is intended only to load web fonts for preview purposes – when, for example, end users of a Typekit integration are browsing available fonts or trying out various fonts on some web content they are about to publish. The Web Font Preview API should never be used to load Typekit fonts for published websites; a published kit must be used there instead. See our [guidelines for permitted use](/partnership/legal.md) for more details.

Using the API requires authentication via an auth_id and auth_token. To get these, register with us by using the Adobe I/O [Console](http://adobe.io/console) to create an integration. Then add an [authentication component](https://creativesdk.adobe.com/docs.html) from the Creative SDK, and return to the [Console](http://adobe.io/console) to request a Web Font Preview API token (in an integration’s Services tab, you'll find a token generator in the “Configure Typekit Platform” area). We’ll set you up in development mode initially, limiting you to 1,000 pageviews per day of web font previews. You’ll be able to remove this limit before you launch your integration by following our [approval process](/partnership/approval_process.md).

## Using the API

In order to use the API, you simply include a JavaScript file in your page:

```HTML
<script src="http://use.typekit.net/previewkits/pk-v1.js"></script>
```

This file makes a global TypekitPreview object available. You should include this JavaScript file from Typekit’s server (instead of copying it to your own server) so that it stays in sync with Typekit’s font-serving endpoint (which the script writes urls for). The script is necessary because it provides Typekit’s standard browser detection and font events for detecting when the requested fonts have loaded.

Once you've added this JavaScript file to your page, call TypekitPreview.setup once per page in order to setup your auth ID and token. This can be done any time after the script tag and before your first call to load fonts:

```JavaScript
// Setup auth ID and token
TypekitPreview.setup({
  'auth_id': 'your auth id',
  'auth_token': 'your auth token',
});
```

You can also pass additional keys to setup to set options for the entire session. Currently, only the default subset is supported (which sets the default subset for all fonts subsequently requested):

```JavaScript
// Setup auth ID and token
TypekitPreview.setup({
  'auth_id': 'your auth id',
  'auth_token': 'your auth token',
  'default_subset': 'all',
});
```

Once you've called setup once, you can call the TypekitPreview.load method in your own JavaScript code to load one or more fonts at a time:

```JavaScript
// Load one font family
TypekitPreview.load([{
  'id': 'ftnk',
  'variations': ['n4','n7'],
  // css_name, subset, and primer are optional
  'css_name': 'futura',
  'subset': 'all',
  'primer': '227b057c6b43daf9ca8e4c8d2e83462476fbdb76283d9b2456567379b7f6d81d'
}], {
  // Font event callbacks (optional)
});

// Load several font families
TypekitPreview.load([
  { 'id': 'ftnk', 'variations': ['n4','n7'],
    'css_name': 'futura'},
  { 'id': 'yqrc', 'variations': ['n4'],
    'css_name': 'ratio'}
], {
  // Font event callbacks (optional)
});
```

The first argument to TypekitPreview.load is either a single associative array or an array of associative arrays. Each associative array represents a font family to load, and must include the 'id' and 'variations' keys. The ID should be a Typekit font family ID as a string and the variations should be an array of font variation description strings.

The additional 'css_name', 'subset', and 'primer' keys are optional. The CSS name is the nice name that you'd like to refer to this family as in your CSS. You can choose whatever string you'd like, but it may contain only lowercase letters (no numbers, punctuation, spaces or other characters). If the CSS name key is not included, then the Typekit ID will be used as the CSS font-family name. The subset overrides the default subset if one was set, and otherwise defaults to the 'default' subset. There are currently two subset options:

* **default** — The default subset contains the Latin-1 character set plus useful typographic marks.
* **all** — The all subset contains every glyph that’s available in the original font. Note that each font has a different overall character set, and not all fonts will contain the glyphs required for a particular language or piece of content.

To create custom subsets you can also use the 'primer' option. This option takes a special subset token that can be used to request fully custom subsets. When present the 'primer' will override any value given to 'subset'. Here are some sample primers:

* Characters A-z and 0-9 without OpenType features: **9f562d6ca39adae019ef00367c3f3deae3c8627f22e3b025ba425fbc2aac6431**
* The default subset with OpenType features: **7cdcb44be4a7db8877ffa5c0007b8dd865b3bbc383831fe2ea177f62257a9191**
* Characters 'A' and 'g' without OpenType features: **227b057c6b43daf9ca8e4c8d2e83462476fbdb76283d9b2456567379b7f6d81d**

We’ll make more primers available in the future.

Because the API uses the same JavaScript machinery as kits, you have access to all of the font events (via JS callbacks and CSS classes) as well. The full complement of options you can use with TypekitPreview.load looks like this:

```JavaScript
TypekitPreview.load([
  { 'id': 'ftnk', 'variations': ['n4','n7'],
    'css_name': 'futura'},
  { 'id': 'yqrc', 'variations': ['n4'],
    'css_name': 'ratio'}
], {
    // Font event callbacks
    loading: function() {
      // Called when these fonts are requested
    },
    active: function() {
      // Called after these fonts are done loading and at least one is active
    },
    inactive: function() {
      // Called after these fonts are done loading and none are active
      // Also called immediately if fonts are not supported
    },
    fontloading: function(fontFamily, fontDescription) {
      // Called as each font is requested
    },
    fontactive: function(fontFamily, fontDescription) {
      // Called after a font finishes loading and is active
    },
    fontinactive: function(fontFamily, fontDescription) {
      // Called after a font fails to load
    }
  }
);
```

And in your CSS, thanks to class names added to, you can write:

```CSS
.wf-loading .my-class {
  <!-- Styles applied to .my-class while any fonts on the page are loading -->
}
.wf-active .my-class {
  <!-- Styles applied to .my-class while at least one font is active -->
}
.wf-inactive .my-class {
  <!-- Styles applied to .my-class while no fonts are active or when fonts are not supported.-->
}
.wf-droidsans-n4-loading .my-class {
  <!-- Styles applied to .my-class while Droid Sans n4 is loading -->
}
.wf-droidsans-n4-active .my-class {
  <!-- Styles applied to .my-class while Droid Sans is active -->
}
.wf-droidsans-n4-inactive .my-class {
  <!-- Styles applied to .my-class while Droid Sans is inactive -->
}
```

## Authentication
An authentication ID and token is passed to the TypekitPreview.setup call. In turn, it’s sent along in requests to the server and verifies that requests for fonts are authorized. When combined, they identify which domains can access the Web Font Preview API, and what fonts can be loaded.

We’ll provide you with an authentication ID and token when we set up your access to the Web Font Preview API.

## A simple use case

To give you an idea of how this API can be used in context, here’s a simple example of some JavaScript (using jQuery) that uses TypekitPreview.load to make a set of links that changes the font on the page. This example assumes that we have a set of links on the page with the class “font-switcher” on the page that have Typekit font family descriptions in their href attributes, like this:

```HTML
<a class="font-switcher" href="#" data-id="ycvr" data-variations="n4:n7:i4:i7"
  data-css-name="museo-sans">Museo Sans</a>
<a class="font-switcher" href="#" data-id="llxb" data-variations="n4:n7:i4:i7"
  data-css-name="museo-slab">Museo Slab</a>
```

The example also assumes that our web application loads the preview JavaScript in the head of the page and then calls the TypekitPreview.setup method with a valid authentication ID and token:

```HTML
<script src="http://use.typekit.net/previewkits/pk-v1.js"></script>
<script type="text/javascript">
  TypekitPreview.setup({
    'auth_id': 'csdv',
    'auth_token': '3bb2a6e53c9684ffdc9a9af31d5b2a624ae8a40',
  });
</script>
```

Assuming that we have these elements in place, we could use this JavaScript on the page to add behavior to these links that switches the fonts used on the page:

```JavaScript
$(function() {
  var $style = $("").appendTo("head");
  $(".font-button").click(function(e) {
    e.preventDefault();
    TypekitPreview.load([{
      "id": $(this).data("id"),
      "variations": $(this).data("variations").split(":"),
      "css_name": $(this).data("css-name"),
    }], {
      active: function() {
        $style.text("body { font-family: " + familyName + ", sans-serif; }");
      }
    };
  };
});
```

## Other alternatives that the Web Font Preview API replaces

The Web Font Preview API was created as an alternative to other approaches that are less than ideal for multiple reasons. Here are a few other approaches to creating a live preview with Typekit fonts that TypekitPreview aims to replace:

### Creating kits on the fly
One potential approach to create a live preview functionality would be to use the Typekit API to create or update a kit on the fly each time a user wants to see a preview. There are downsides to this:

* Kits take a non-trivial amount of time to create and publish, so this isn’t (yet) fast enough for live preview functionality
* The number and frequency of requests necessary to create or update a kit each time the user wants to try a different font can introduce a huge amount of unnecessary load.

### Using pre-generated preview kits
It’s possible to load two different kits on the same page, so another potential approach is to create a kit for each font users can choose from, and then load one or more of these kits together. There are downsides to this too:

* Different kits are only guaranteed to work together if they were published at the same time. This means your preview kits must be republished together. If you load preview kits and individual user kits at the same time, you must keep all of these thousands and thousands of kits in sync. This creates a huge amount of unnecessary load as well.
