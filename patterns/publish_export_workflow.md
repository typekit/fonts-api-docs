# Publish export workflow

**Fonts used in a design application should persist when work is published or exported**.

When work moves out of a design application to be viewed or continued elsewhere, the fonts it uses need to come along. Published and exported work lives in an environment that is different from a design application, so font licensing and entitlement conditions may need to be reevaluated.

Therefore:

**Settle font licensing entitlement early in the publish or export process, and clearly explain aspects of publishing/exporting that relate to font licensing**.

Make publishing and exporting as easy as possible by telling people about any font entitlements that need to be resolved as early as possible. Consider offering a subtle warning as people [browse fonts](browse_fonts.md), use fonts, or think about publishing/exporting a project.

![Sketch of UI indicating a Typekit connection](../img/publish-export-01.png)

Be especially sure to notify people if this is a blocker to action, such as when someone is trying to publish a project that uses web fonts. Use notification text like this:

_Some fonts may need to be purchased before publishing or exporting your project_.

Offer an action to “Connect Typekit” before publishing. Taking this action should launch the Connecting to Typekit window:

![Sketch showing UI for publishing with fonts from Typekit](../img/publish-export-02.png)

Show the Connecting to Typekit window any time fonts from Typekit are used in a project, even if the user is fully entitled to those fonts. Start by showing the Typekit logo and explaining that publishing and serving web fonts from Typekit requires your Typekit account. Link to details about Typekit in your own application’s help documentation:

### This site will now link to your Typekit account

_Typekit is included with Creative Cloud. Your Typekit account is required to publish sites that use fonts from Typekit, and also required to serve those fonts to that published site on an ongoing basis. [Learn more about your account](https://helpx.adobe.com/x-productkb/policy-pricing/typekit-plan-pageviews.html)_.

Briefly explain why Typekit needs to know the domain of the published work:

### Your site's domain

_We'll need to know your site's domain, so we can confirm that fonts are being used legally_.

If any font entitlements need to be resolved, explain that and list the fonts:

### Some fonts need to be purchased

_While free to use within this application, one or more fonts in this site need to be licensed for web use before publishing, either by upgrading your Typekit subscription or purchasing from Typekit Marketplace_.

_- [Font names]_

The action button at the bottom of this window should say “Get Fonts” if there are any entitlements to resolve, and when clicked should launch a Typekit.com Buy Intent page. Otherwise, it should say “Continue” and should lead to the rest of your application’s publish/export flow. Offer a cancel button in case people want to bail on the publishing/exporting process.
