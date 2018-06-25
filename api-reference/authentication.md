#Authentication

The Platform API supports both signed out and authenticated modes. When users are in the signed-out state, only the API key is required. You can authenticate as a user by sending a 'X-Typekit-Token' HTTP header.

If your integration aims to give users access to their Typekit accounts by signing in with an Adobe ID, you’ll also need to integrate an authentication component from the Creative SDK. To get access to the Creative SDK, use the Console to add it to your integration as a service along side Typekit.
