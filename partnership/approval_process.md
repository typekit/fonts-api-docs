# Our approval process

When you’re ready to launch with your Typekit integration, contact us and we’ll review it for approval. Email us with your developer number and the name of your integration.

If we see an issue, we’ll let you know about it so you have the opportunity to address it. Here’s what we’ll be looking for.

## Site previews use the Preview API
A “site preview” refers to any live preview of a customer’s website that they can view while trying out different fonts — i.e., before they “save” their font choices for use in the public version of their website. You should use the Preview API (and not a published kit) to dynamically load fonts whenever a user wants to try them on a preview of their site — including when they’re making edits to an existing site.

## Site publishing uses the Kit Publish API
Once a customer’s website is pushed live and publicly available, Typekit font rendering should be provided via a kit that was published using the [Kit Publish API](https://docs.typekit.io/#!/%2Fkits/post_kits_kit_id_publish). We also recommend you only edit a site’s kit once a user has actually committed to a font (e.g., by clicking “save” in their font settings), rather than updating the kit every time a user tries a font on a preview of their site.

## Maintain good kit hygiene
Your application should only create one kit per customer site — and rather than simply creating a new kit when changes are needed, it should explicitly edit the existing kit. This is to ensure that lots of unnecessary kits don’t accumulate in our system. Likewise, when a kit is genuinely no longer needed (because the user removes Typekit fonts from a site, deletes a site, or cancels their account), delete that kit via the API.

## Cover basic error handling
Confirm that your application can appropriately respond to scenarios where Typekit services are unavailable. This is extremely rare, but your application should handle it gracefully when it does occur. For example, if you were to get a 503 Service Unavailable response when trying to publish a kit via the API (in response to a user clicking a save button to save their font settings), then you might want to show a notification that says something like this:

*Your font settings could not be saved due to a network error. Please try again later*.

## Use Font Events for consistent loading
We recommend using Typekit [Font Events](https://helpx.adobe.com/typekit/using/font-events.html) to make font loading behavior consistent across various browsers. This will help avoid a flash of unstyled text the first time your customers load a page containing web fonts.

## Communicate with users about page weight
Mostly for the sake of good performance, you should confirm that the number of fonts per published kit is reasonable. When kit size exceeds 400K on Typekit.com, we automatically warn users that their page load is getting heavy — and we recommend a similar approach for integration partners.

## Include standard weights and styles
We recommend that families used for body text always include regular, bold, and italic variations so that common in-line styling commands will work.

## Authenticate users before they select fonts
When account-level changes are possible through your integration, our Platform will require that users are signed in and authenticated in some way. This includes activities like syncing fonts for use in documents, and publishing kits for use on the web. (Note: authentication may not be required for some situations where the fonts are less exposed — such as browsing available fonts from Typekit without applying them to a document.) To authenticate users, you’ll need to integrate an [authentication component from the Creative SDK](https://creativesdk.adobe.com/docs.html). To get access to the Creative SDK, use the [Console](http://adobe.io/console) to add it to your integration along side Typekit.

## Plan for fonts that become unavailable
Your app must always respect a user’s current Typekit font entitlement, which can change over time. When a user is no longer entitled to a Typekit font, or the font is removed or otherwise unavailable from Typekit, it will be evident when the user’s entitlement is validated, and your application must immediately remove it and otherwise make it unavailable.

Fonts in published web kits are a special case. Once published, a kit containing any revoked font can remain active as long as the user’s subscription remains in good standing and at the same (or greater) level. Such kits may be republished, but if a revoked font is removed from a kit, it cannot be re-added.

## No converting web fonts
Web fonts must never be converted or rasterized into any other format (e.g., PDF or any graphics format). They are only to be used for web authoring of content that is then published as HTML and includes a Typekit kit.
