# Authentication

The Platform API supports both signed out and authenticated modes. When users are in the signed-out state, only the API key is required. You can authenticate as a user by sending a 'X-Typekit-Token' HTTP header.

If your integration aims to give users access to their Typekit accounts by signing in with an Adobe ID, you’ll need to [use OAuth 2.0 to generate an access token](https://www.adobe.io/authentication/auth-methods.html#!adobeio/adobeio-documentation/master/auth/OAuth2.0Endpoints/web-oauth2.0-guide.md) for the user.
