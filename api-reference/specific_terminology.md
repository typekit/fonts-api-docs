# Specific terminology

## Browse Modes
Currently we have options to browse in Default mode (all but Japanese-specific glyphs in a font), Japanese (only the Japanese glyph subset), and All (all glyphs and the largest font files). This affects the layout and content of the filters, which are designed for specific browsing needs for each mode, and will also limit the number of fonts available.

## Filters
Metadata that determines how different filtering options work (for example, for font classification). All our fonts contain metadata to work with these filters. We also provide icons. Filters are largely determined by the Browse mode selected.

## Font subsets
A “Subset” refers to a set of the available characters in a typeface. Each Font Variation includes multiple characters, including many that are not commonly used. To include all of these characters increases the size of the font file, so we offer the ability to choose a subset of characters, per Font Family, in each kit.

## Font versioning
Font sync is locked to a specific version. When a font is selected, a particular version of that font file is selected. Font versions occasionally vary as we keep the files updated.

## Kits
A kit is a combination of fonts configured for use on a particular site. From the API, you can view kits to see the fonts in use, create new kits, republish kits to change the fonts in use, and delete kits.

## Variations
A “Font Variation” (or simply, “Variation”) is a particular weight and style of a “Font Family”. Examples include FF Meta Web Pro Bold Italic, Droid Sans Regular, and Coquette Light. Traditionally, this might be referred to as a style or type style. Typekit uses [Font Variation Descriptions](http://typekit.github.io/fvd/) to concisely and unambiguously refer to font variations in the API.


## Web fonts and Sync fonts
Fonts from Typekit can be either embedded in web sites, or used as system fonts on personal computers and devices. To accommodate various browsers, the web font versions are adapted specifically for web use and are different from the corresponding sync font versions. Most endpoints dealing with actual font data require that the purpose is specified as part of the request.
