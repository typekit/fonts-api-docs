# Visual search results

**Evaluating visual search results is harder if you lose context or don’t know what the next step is**.

The Typekit API’s [visual_search endpoint](https://docs.typekit.io/#!/%2Fvisual_search/getVariationsByImage) returns a list of font variations that we think are visually similar to the text in the input image. But how do you style this list of results? And what are people supposed to do now?

Font names and generic specimen text (“The quick brown fox…”) are not enough to help people decide whether a font is similar to what they were originally looking for (the text from their input image). And once people have identified a font that is promising, they need a way to act on that. What action do they take?

Therefore:

**Present visual search results in a way that is contextually meaningful and prompts relevant action**.

Show visual search results alongside the image that was evaluated, and use OCR text as the specimen text for each font variation. This helps people compare the letterforms and evaluate the quality of results.

![Example of a visual search region, a coordinate-defined area of an image](../img/pattern-visual-search-results.png)

If the visual search was initiated with a specific text element in mind (say, a heading on your application’s canvas), consider using the text from that element as the specimen text for each font variation in the results list. In a case like this, the user cares about the content of the text element for which they’re trying to choose a font more than the content of the visual search image.

Give people a clear next step. Use a [font action button](font_action_button.md) if you intend for people to act on a font in one of the standard Typekit ways (“Sync”, “Add to kit”, etc.), based on their entitlement. If instead your application offers additional actions as part of a visual search workflow, just remember to explain to the user what actions they’re taking with regard to the fonts.
