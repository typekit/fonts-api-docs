# Legal

The Typekit Platform enables font browsing, syncing, and kit publishing with Typekit fonts in mobile, web, and desktop apps. We’ve worked hard to make access to these activities free of obstacles, allowing you to get fonts in front of as many people as possible while still allowing us to protect the fonts from unauthorized use.

When developing an integration with Typekit in your app

* Developers are responsible for ensuring that their end users don’t violate our existing terms of use — both [Typekit’s terms](http://www.adobe.com/go/typekit_terms) and [Adobe’s](http://www.adobe.com/legal/terms.html). (We built constraints into the API to avoid this, so you mostly won’t need to worry unless you go out of your way to circumvent them.)
* You will need to indicate in some way that the fonts provided are from Typekit. For example, some of our [patterns](../patterns.md) show places in your UI where the [Typekit logo](../typekit_assets.md) belongs.
* We will need to review your integration and approve it before you launch it. (See more about the [approval process](approval_process.md) here.)

All good? Let’s get into what you can do from here.

## Fonts for Previewing
The Typekit Platform allows apps to load any available Typekit font for preview purposes.

* UIs render a sample of a font in order to help a user evaluate its qualities and decide whether they want to get and use it.
* Does not require user authentication; anyone may browse all Typekit Library and Marketplace fonts before being entitled to use them.
* Platform provides only subsetted versions of preview fonts in some cases, to prevent them from being misused.

For preview fonts that an app needs to download directly (i.e., sync fonts or WOFFs in a mobile or desktop app):

* subset is required limited to a maximum of 50 characters at a time
* The /variations/previews endpoint documentation describes how to work with this subsetting requirement.

For preview fonts that an app loads through Typekit’s ](https://docs.typekit.io/#//previews), common preview subsets are ​supported​ but not required.

* Fonts are only accessible from a small set of domains that you must specify when setting up your access to this service.
* Never use the web font Preview API to load web fonts for published websites; a kit must be used instead.

## Fonts for Authoring
The Platform allows apps to load fonts for authoring purposes under specific circumstances that depend on the type of use.

### Sync fonts
Full sync fonts for document and media authoring purposes can only be downloaded:

* for an authenticated and entitled user, and
* by the Adobe Creative Cloud desktop app and the Adobe Creative SDK.

This means if your app seeks to add Typekit sync fonts to a user’s system fonts (on Mac or Windows) or directly to a Creative SDK-integrated app (on iOS or Android), you should:

* add them to the user’s Typekit “sync selection” via the /selections endpoint, and then
* rely on the Creative Cloud desktop app or the Typekit component of the Creative SDK to actually sync the fonts to the user’s device(s).

At that point, the user may use the fonts as they would any other Typekit fonts synced to their device(s) by any other apps/service. See our [help page on font licensing](https://helpx.adobe.com/typekit/using/font-licensing.html) for a review of how end users may use sync fonts.

### Web fonts
Full WOFF web fonts for web authoring purposes can only be downloaded for an authenticated user, and only by approved Adobe web authoring apps.

Full web fonts loaded by a web app through Typekit’s [web font Preview API](../api-reference/web_font_preview_api.md) for web authoring purposes ​can be loaded for an **unknown, unauthenticated user**. (The fonts are protected, as they are accessible only from a small set of domains that you must specify when setting up your access to that service.)

In both cases, **the user need not be entitled to all the fonts to begin authoring web content with them**. When the user attempts to publish content using a Typekit web font they’re not yet entitled to, they’ll need to resolve their entitlement (typically by upgrading their Typekit subscription plan or by purchasing the font from Typekit’s Marketplace) before your app can publish a kit for them containing the font.

Your app should warn users when they are about to author using a font that they can't yet publish with, so they’re aware of the need to make a Typekit purchase before they invest time in authoring with that font. We recommend workflow and design patterns to manage this in our [design patterns reference](../patterns/publish_export_workflow.md).

Watch for these situations:

* Never use downloaded WOFFs or the web font Preview API to provide web fonts for published websites; a published Typekit kit must be used instead.
* Web fonts must never be converted or rasterized into any other format (e.g., PDF or any graphics format). They are only to be used for web authoring of content that is then published as HTML and includes a Typekit kit.

We’ll confirm that your app handles these issues correctly when we review it prior to approving your launch.
