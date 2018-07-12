# Visual search coordinates

The results of visual search depend on the image being cropped to a single line of type. The Typekit API’s [visual_search endpoint](https://docs.typekit.io/#!/%2Fvisual_search/getVariationsByImage) affords this cropping by accepting coordinate values. However, these coordinates are optional. If you are implementing a visual search feature, you are not required to pass coordinates (for example, your application may help people crop images even before interacting with the Typekit API).
