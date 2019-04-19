# Guide to building a web-based integration that offers web fonts

By integrating Typekit Platform into your web-based tool, you can allow people to connect to their Typekit accounts, select fonts to which they are entitled, use their fonts in your application, and publish their fonts in “kits” for use on the web.

_Note: You can also offer different styles of Typekit integration. For example, you can give users access to additional fonts by offering upgrade and purchase workflows. You can also provide access to Typekit on behalf of your users (whether or not they have Typekit accounts). Please [contact us](mailto:fontintegrations@adobe.com) if you’re interested in these different styles of integration_.

This guide will explain key points of integrating the Typekit Platform into your application, including building a Typekit browsing UI, rendering fonts on your application’s design surface, and publishing fonts for use on the web.

Browse fonts view:

![Sketch showing browse fonts view](/img/pattern-sketch-browse-fonts.png)

Family detail view:

![Sketch showing grid and list view](/img/family-detail-view-01.png)

Publish/export workflow:

![Sketch showing publish export workflow](/img/publish-export-02.png)

## Register with Typekit Platform

The first thing to do is register with us by using the Adobe I/O console to create an integration. Then add an authentication component from the Creative SDK, and request a Web Font Preview API token. [This page](partnership.md) explains how to do all of that — start at the “Register with us” section. Once you have done that stuff, return to this guide.

## Introduce your users to Typekit

As part of your application’s typography tools (for picking a font, choosing a size, etc.), offer an action to add more fonts from Typekit. Tell people what Typekit is (a service for finding, getting, and using fonts), and that they will need to sign in with their Adobe ID to access Typekit fonts. Prompt them to sign in (or get an Adobe ID) using the [User Auth UI](https://creativesdk.adobe.com/docs/web/#/articles/userauthui/index.html) component of Adobe’s Creative SDK.

You’re going to need to have this auth token for much of what you want to do in an integration. So keep it handy.

## Let people browse fonts

After people are signed in, show the browse fonts view. Learn more about what this looks like (and why) in our [browse fonts pattern](/patterns/browse_fonts.md), and more granular patterns like the [filter menu](/patterns/filter_menu.md) and [family card](/patterns/family_card.md) pattern, which shows and explains what each family card should be like. You can also study our [browse UI demo app](https://demo.typekit.io/#!/font_list) and its [source code](https://github.com/typekit/platform-demo-browse).

Now let’s build this view.

First, we need to show the entire browse fonts view, with one page of family cards:

* Have a user auth token handy (you got this after the user signed in), in order to limit API request results to the user’s entitlements.
* Use the [/families endpoint](https://docs.typekit.io/#!/%2Ffamilies/getFamilies) to get a list of fonts that your user is entitled to use.
* Use the “page” and “per_page” [parameters of the /families endpoint](https://docs.typekit.io/#!/%2Ffamilies/getFamilies) to limit the number of font cards shown in the browse UI at any one time, and paginate additional results. The browse fonts pattern has a few more details about this.
* Use the “sort” parameter of the [/families endpoint](https://docs.typekit.io/#!/%2Ffamilies/getFamilies) to control the order in which fonts appear.


Next, put filters and search in place to limit the fonts that are shown, paginated, and sorted:

* Build a [filter menu](/patterns/filter_menu.md) as part of the font browsing UI, by requesting a list of available filters and associating them with the appropriate icon and label. When a user activates a filter, get a list of families that match the filter criteria by using the “filters” [parameter of the /families endpoint](https://docs.typekit.io/#!/%2Ffamilies/getFamilies). There’ll be fewer fonts (because not every available Typekit font will match the filter criteria), but paginate and sort them as you normally would.
* Implement a basic search feature. Unlike a search at Typekit.com, which yields a search results page, search within your application’s browse fonts view should act like a filter. When a user searches for, say, “caslon”, return families with names that contain that string — right in the browse fonts view. Just limit what is shown to fonts that match the search.


Then, make the fonts listed in this view look like Typekit font cards:

* Refer to the [family card](/patterns/family_card.md) pattern to learn more about the information that makes up each family card. The data you’ll need to build a card is provided in the [/families](https://docs.typekit.io/#//families) response for the current page of cards.
* Get strings for font card specimen text from the [/previews endpoint](https://docs.typekit.io/#!/%2Fpreviews/getPreviews). This is how people will preview fonts — by seeing how the font looks applied to this text string. You can also, of course, allow users to enter custom sample text.
* Load the fonts, and use them to style family cards’ specimen text strings. Use the [Web Font Preview API](/api-reference/web_font_preview_api.md) to render the specimen text samples in each font a user is entitled to see. Be sure to specify the “default” subset option, so that fonts load more quickly (loading entire font files in the browse UI can be intense). Use [Adobe NotDef](https://github.com/adobe-fonts/adobe-notdef) as a fallback font, in case the Typekit font being displayed does not contain glyphs in the sample text.

## Let people see details about specific fonts

When someone chooses to learn more about a specific type family, show it in a [family detail view](/patterns/family_detail_view.md). This is a view dedicated to information about one specific type family. It should list all of the family’s variations, show family metadata, and link to more details at Typekit.com. This view should also offer a link back to the browse fonts view, and a button to select the family for use.

First, use the [/families/{slug} endpoint](https://docs.typekit.io/#!/%2Ffamilies/) to get a list of all variations in the family. This will also provide metadata like family name, description, foundry name, classification (available via the “filters” parameter), and a link to the corresponding family detail page at typekit.com. Display this metadata in a supplementary area in the [family detail view](/patterns/family_detail_view.md).

Render each variation with sample text from the [/previews endpoint](https://docs.typekit.io/#!/%2Fpreviews/getPreviews), using the [Web Font Preview API](/api-reference/web_font_preview_api.md) as you did in the browse fonts view. Here again, use the “default” subset and [Adobe NotDef](https://github.com/adobe-fonts/adobe-notdef) as a fallback font.

Offer a single button to allow people to select the whole family. Clicking this button should add the family to your application’s font menu. Update the button to show that the font has been selected and is now available to use. More about this in our [family detail view](/patterns/family_detail_view.md) and [font action button](/patterns/font_action_button.md) patterns.


## Let people use the fonts they’ve selected

After someone has selected a type family for use, they might want to use it (right?). Make sure you understand our [guidelines for permitted use](/partnership/legal.md) (for example, while your application may use font previews, your users’ end result designs need to be web pages).

In your application’s font selection UI (for example, a font menu), render fonts the same way you did in the browse UI. Use the [Typekit logo](typekit_assets.md) to differentiate Typekit fonts from other fonts.

On your application’s design surface, when someone applies a Typekit font to some text, load that variation’s full font file by specifying the “all” subset from the [Web Font Preview API](/api-reference/web_font_preview_api.md).

When a user styles some text with a family’s Regular variation, it’s a good idea to load not only that file but also the companion italic, as well as Bold and Bold Italic variations (if they exist). This helps when the content of the published website changes, by providing the type family’s true italic and bold styles so that browsers don’t synthesize those. (You may also want to limit this loading behavior depending on the job the type is doing — we’re happy to discuss this.)

## Guide people through the publish process

When it’s time to publish a project, make sure people who have used Typekit fonts in their projects are signed in, that they remember what Typekit is, and that their Typekit account matters (they’ll need to maintain this for as long as they want their fonts to continue working). In addition, be sure to gather the domain(s) where the kit will be used if your application/service doesn’t provide this automatically — Typekit needs this, so we can be sure that fonts are being used legally.

See the [publish/export workflow pattern](/patterns/publish_export_workflow.md) for some tips, including a sketch about “Connecting to Typekit” and some boilerplate text about what Typekit is and why domains matter. Don’t mind the parts of this pattern about entitlement or purchasing fonts (though if you’re interested in that, email us and we can work with you to enable users to access additional fonts).

Another important aspect of publishing is the font files themselves. You’ll need to decide which variations to publish, and whether to subset any variations. You can provide users with the ability to make these specific decisions, but that also increases the complexity of publishing.

In general, it’s a good idea to publish all variations present in the project on your application’s design surface — plus those extra Italic, Bold, and Bold Italic variations we mentioned.

Whether to subset each published variation depends on what’s important to you and your users. If you automatically publish variations with the “all” subset, this could result in large font file sizes. If you automatically publish the smaller “default” subset, this could result in missing glyphs — especially if the text in your users’ projects is not strictly Latin/western. Note that we do expose language support per font via the [/families endpoint](https://docs.typekit.io/#!/%2Ffamilies/getFamilies)’s languages parameter, so you can get into specifics when making this decision.

However you go about these aspects of the publishing process, a preview mode may help people catch things that don’t seem right prior to actually making their projects live.

## Make a kit for your user

Behind the scenes, what you’ll do when someone publishes their project in your application is create a “kit” using the [/kits endpoint](https://docs.typekit.io/#//kits). You’ll specify their user auth token to ensure they are entitled to publish.

When you do, you’ll receive an HTML tag (called an embed code) to put into their project’s code that will make the fonts load. You can choose between either CSS-only embed codes (using the HTML `<link>` tag) or a JavaScript embed code (using a `<script>` tag). Please note that font events are only supported with JavaScript embed codes. [Learn more](https://helpx.adobe.com/typekit/using/embed-codes.html) about Typekit embed codes.

Your application will also need to publish corresponding CSS for the user's page, to actually apply fonts to elements. Here's some information you may find useful, about [CSS selectors](https://helpx.adobe.com/typekit/using/css-selectors.html) and [font events](https://helpx.adobe.com/typekit/using/font-events.html).

If the project is revised (to include more fonts, or use different fonts), you’ll update the same kit. Details are available in the [/kits endpoint](https://docs.typekit.io/#//kits) of the Typekit Platform API reference.

As a general rule, set the “optimize_performance” parameter to “false”. When true, this parameter sets a very long cache time. While that’s a good thing for high-volume sites that won’t change fonts in the foreseeable future, it’s not good for people who make design adjustments often and publish more frequently (because it could take a week or more to see changes on their website).
