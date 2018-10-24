# Missing fonts workflow

**Sometimes fonts used in a document or system are missing**.

Missing fonts are a problem. This problem often renders documents and systems unusable. If you’re designing, editing, reviewing, or sharing a project and fonts are missing, you can’t see what the work really looks like (and neither can the people with whom you share). Until the fonts you intend are present, the work feels incomplete.

Therefore:

**Offer an option to resolve missing fonts by finding them (if you have them already), getting them (if you don’t yet have them), or replacing them with different fonts**.

The workflow is illustrated below, and goes like this: first, fonts are missing (a); next, the [missing fonts view](missing_fonts_view.md) prompts you to resolve missing fonts (b); then, if necessary, you get missing fonts at Typekit.com (c); and finally, fonts are present (d).

![Missing fonts workflow illustration](../img/missing-fonts-workflow-01.png)

This missing fonts workflow can be triggered by a number of things, such as when a document is opened and contains fonts that are missing, when someone tries to edit a text layer that uses a font that is missing, or when someone chooses a command from your application’s menu.

Make sure people are signed in, so you know which fonts they are entitled to use. See the [note on Authentication](../api-reference/authentication.md) in our API reference.

The [missing fonts view](missing_fonts_view.md) is a pop-up window or modal view in your app. It explains that fonts are missing, and how to resolve them. If a font is not in a person’s library, but is available on Typekit by upgrading or purchasing a license from Typekit Marketplace, this view offers to resolve the missing font at Typekit.com. Resolving missing fonts at Typekit.com happens in a browser window, at a URL provided by the Typekit API.

While people are getting fonts at Typekit.com, have your app poll the Typekit Platform API to check for entitlement changes. Keep the missing fonts view visible until missing fonts are resolved, or until someone dismisses it, so you can show any such entitlement changes. For example, a trial Typekit user may need to upgrade for access to certain fonts; upon upgrading, the fonts will be available to sync, but will not sync automatically. The missing fonts view should remain visible because while this user is now entitled, they have not yet synced to resolve the missing fonts.

After a short period of time, you can stop polling. If the person has given up or become distracted, they can initiate the missing fonts workflow again later.

Gaining access to fonts for sync at typekit.com will trigger a font sync, which means that a person should receive fonts automatically and be able to use them as soon as they finish syncing.

Gaining access to fonts for web at typekit.com will “unlock” those fonts instantly, which means that a person trying to publish a project will be able to do so immediately.
