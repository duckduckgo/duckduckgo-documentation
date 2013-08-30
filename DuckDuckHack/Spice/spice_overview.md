# Spice Overview

Spice plugins are triggered by a backend Perl component that then calls the JSON API of an upstream service. The API response is wrapped in a JavaScript function call. You, the plugin author, define this callback function and handle the API's response on the client side, generating the display from the data returned by the API.

