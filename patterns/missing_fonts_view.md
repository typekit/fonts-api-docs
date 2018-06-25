#missing-fonts-view

When fonts are missing, people need to find them, get them, or replace them.

Someone who is missing a font and going through the missing fonts workflow needs to decide – for each font – whether to get it, replace it with a different font, or choose to proceed without the font.

Therefore:

For each font that is missing from a document or system, explain the ways to resolve this problem and allow people to take action.

Sketch for missing fonts indicators in UI
Present the situation in an organized way. Start with an explanation:

Some fonts are missing

But that’s okay. You can sync, buy, or replace them.

Sync from Typekit: As a Creative Cloud member, you have access to a subscription library of fonts at Typekit. Creative Cloud can sync these fonts for you.

Get from Typekit: If a font is not in your library, but is available on Typekit by upgrading or purchasing a license, Creative Cloud can sync this for you too.

Then list each missing font variation, and for each one offer a drop-down menu full of ways to act.

Sketch of missing fonts UI
Use label text to help clarify the choices people make, and set expectations about what will happen next:

Sync font: Creative Cloud will sync this font when you click “Resolve Fonts”.
Get font: Complete the purchase in a new window, then Creative Cloud will sync this font.
Replace with...: The missing font will be replaced with this one.
Don't resolve: Nothing will happen, unless you try to edit the text. Then a default font will be used.

The Typekit logo should appear next to Typekit-related actions in each drop-down menu.
Finish up with a "Resolve Fonts" button that initializes the various actions a person has decided about via the drop-down menu(s), as well as a “Cancel” button. Include a checkbox option to not trigger the missing fonts workflow when a project or document is opened that contains missing fonts, plus some label text to remind people how to trigger the workflow manually:

[ ] Don't show on document open (Tip: accessible under Type > Resolve Missing Fonts)

When someone selects “Resolve Fonts”, if any drop-down values are “Sync font”, initialize a Typekit font sync for each. If any drop-down values are “Get font”, initialize a single Buy Intent page at Typekit that includes all font variations the person would like to get:

For each missing font, request `/variations/{postscript_font_name}`
Typekit matches the font and returns its description. The `required_action` field will be set to either `upgrade` or `purchase`.
Make a request to either `GET /variations/{tk_font_id}/acquire` (if single font) or `POST /variations/acquire` (if multiple fonts). The response is a URL to the Buy Intent on typekit.com.
Launch a web browser and load the Buy Intent URL.
The user completes the upgrade/purchase workflow on typekit.com, then proceeds with the missing fonts workflow.
