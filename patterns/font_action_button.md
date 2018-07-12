# font-action-button

**When people find a font they want to use, they need a way to take action**.

How someone takes action on a font variation or family depends on what kind of access they have to that asset. For example, someone who is a paying Creative Cloud subscriber may be able to “Sync” a font that someone using a free account must first “Get”. A single button can do any such job, if it knows the user’s entitlement and has the right button text and label.

Therefore:

**Use varying states of the same button to offer every kind of font action a person might need to take**.

“Use font” — Use this button text for web fonts. Clicking it should add the web font to a person’s font menu.
“Remove font” — Use this button text for web fonts. Clicking it should remove the web font from a person’s font menu.
“Sync font” — Use this button text for sync fonts. Clicking it should sync the font.
“Unsync font” — Use this button text for sync fonts. Clicking it should unsync the font.
“Get font” — Use this button text, with the small text label, “at Typekit.com” for a web or sync font to which a person is not entitled. Clicking the button should instantiate a Buy Intent page at Typekit.com.
