# Starting a new integration with Typekit

Welcome to our partner network. We love spreading the power of great typography, and look forward to hearing about what you’re working on. Here’s how to get started.

## Choose between Typekit and the Creative SDK
The Typekit Platform described here gives you direct access to Typekit APIs, allowing you to build any sort of Typekit integration you can imagine on web, mobile, or desktop – really, anywhere you can use RESTful APIs. If you’re looking for something a bit more plug and play, we also offer Typekit components in Adobe’s [Creative SDK](https://creativesdk.adobe.com/docs.html) for iOS and Android, allowing you to integrate common Typekit functionalities delivered through ready-to-go UI components with consistent design.

To work directly with Typekit Platform, read on for details on how to register with us. To use the Typekit components in the Creative SDK, visit the [Creative SDK documentation](https://creativesdk.adobe.com/docs.html).

## Register with us
### Use the Console to create an integration
If you want to jump right in, create an integration through the [Console](http://adobe.io/console) and add Typekit as a service. You’ll automatically get a developer key that you can use to start making [API requests](http://docs.typekit.io/) in development mode immediately. While in development mode, your integration can only be used in conjunction with 25 unique Adobe IDs and up to 1,000 pageviews per day of web font previews using our [Preview API](/api-reference/web_font_preview_api.md), but you’ll be able to remove these limits before you launch your integration by following our [approval process](/partnership/approval_process.md).

### Authenticate using the Creative SDK
If your integration aims to give users access to their Typekit accounts by signing in with an Adobe ID, you’ll also need to integrate an [authentication component from the Creative SDK](https://creativesdk.adobe.com/docs.html). To get access to the Creative SDK, use the [Console](http://adobe.io/console) to add it to your integration as a service along side Typekit.

### Request a web font Preview API token
If you need to preview Typekit web fonts in your integration, you'll also need a token for Typekit's web font Preview API. To request your Preview API token, head over to the [Console](http://adobe.io/console) where, in an integration’s Services tab, you'll find a token generator in the “Configure Typekit Platform” area.

## Review our documentation
Take a look at our [design patterns](patterns.md) for ideas about how to integrate Adobe Typekit into your application, our [API reference](api_reference.md) for details on how to build it, and our [demo application](http://demo.typekit.io/) that shows patterns and APIs working together.

While you’re building your product, you can always reach out to us with questions. Send your email to [fontintegrations@adobe.com](mailto:fontintegrations@adobe.com) and we’ll get someone on the case.

## Keep everything legal
Both Typekit and Adobe terms of use apply to your use of the Typekit Platform. If you have any questions about how to properly use fonts from Typekit, we’re happy to get you sorted — start with our [guidelines for permitted use](/partnership/legal.md).

## Ready to launch?
Before you go live, we need to approve your use of Typekit. Send a note to [fontintegrations@adobe.com](mailto:fontintegrations@adobe.com), and we’ll work with you to review how you’re using Typekit in your product or service.

### About our approval process
We’re mainly looking for issues that would put our foundries at risk (of not getting paid properly for their fonts) or our infrastructure under pressure (something that would place enough stress on the system that we’d fear a performance hit). If we find something that concerns us, we’ll discuss it with you like regular people. [See more about what we're looking for](/partnership/approval_process.md).

After you’re approved, remember to let us know when it’s launch day! We often feature new product integrations on the [Typekit blog](http://blog.typekit.com/) and may [tweet](http://twitter.com/typekit) about them. We won’t announce anything until you’re ready, of course.

## Planning for the future
We definitely don’t expect your application to stay static forever, and we hope to grow along with you. If you already have an integration and are considering a substantial change to the way the service works, we’re always happy to chat about how to make the relaunch as smooth as possible. Send an [email](mailto:fontintegrations@adobe.com) our way anytime.

### Something break?
If you notice that something doesn’t seem to be working right, or if you’re getting reports from your customers, our support team is more than happy to help you out. [Email us](mailto:fontintegrations@adobe.com) anytime — yes, even after your launch — and we’ll get right on the issue.
