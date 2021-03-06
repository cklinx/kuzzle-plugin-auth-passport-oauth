[![Build Status](https://travis-ci.org/kuzzleio/kuzzle-plugin-auth-passport-oauth.svg?branch=master)](https://travis-ci.org/kuzzleio/kuzzle-plugin-auth-passport-oauth)

# Plugin Passport OAUTH Authentication

This plugin provides an authentication with [Passeport.js strategies](http://passportjs.org/docs).

## Compatibility matrice

| Kuzzle Version | Plugin Version |
| -------------- | -------------- |
| 1.x.x          | 4.x.x          | 
| 2.x.x          | 5.x.x          | 

# Configuration

To edit the configuration of a plugin see [custom plugin configuration](https://docs.kuzzle.io/plugins/2/essentials/getting-started/#configuration).

List of available configurations:

| Name | Default value | Type | Description                 |
|------|---------------|-----------|-----------------------------|
| ``strategies`` | ``{}`` | Object | List of the providers you want to use with passport |
| ``credentials`` | ``{}`` | Object | Credentials provided by the provider |
| ``persist`` | ``{}`` | Object | Attributes you want to persist if the user doesn't exist |
| ``scope`` | ``[]`` | Array | List of fields in the OAUTH 2.0 scope of access |
| ``identifierAttribute`` | | String | Attribute from the profile of the provider to use as Id if you want to persist the user in Kuzzle |
| ``defaultProfile`` | ``"default"`` | Array | Profiles of the new persisted user |
| ``kuzzleAttributesMapping`` | ``{}`` | Object | Mapping of attributes to persist in the user persisted in Kuzzle |
| ``passportStrategy`` | ``''`` | String | Strategy name for passport (eg. google-oauth20 while the name of the provider is google)

Here is an example of a configuration:

```js
{
    "strategies": {
        "facebook": {
            "passportStrategy": "facebook",
            "credentials": {
                "clientID": "<your-client-id>",
                "clientSecret": "<your-client-secret>",
                "callbackURL": "http://localhost:8080/_login/facebook",
                "profileFields": ["id", "name", "picture", "email", "gender"]
            },
            "persist": [
                "login",
                "avatar_url",
                "name",
                "email"
            ],
            "scope": [
                "email",
                "public_profile"
            ],
            "kuzzleAttributesMapping": {
              "userMail": "email" // will store the attribute "email" as "userEmail" into Kuzzle
            },
            "identifierAttribute": "id"
        }
    },
    "defaultProfiles": [
        "default"
    ]
}
```

# Usage

The easiest way to implement an oauth authentication in your front-end is to use the [sdk login oauth popup module](https://github.com/kuzzleio/kuzzle-sdk-login-oauth-popup)

See [Kuzzle API Documentation](https://docs.kuzzle.io/guide/2/essentials/user-authentication/) for more details about Kuzzle authentication mechanism.

# How to create a plugin

See [Kuzzle documentation](https://docs.kuzzle.io/plugins/2/essentials/strategies/) about plugin for more information about how to create your own plugin.
