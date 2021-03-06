# WordPress.com API Console v3

This is a WIP rewrite in React for the WordPress.com API Console.

## Development

To get up and running:

1. Clone the repository `git clone git@github.com:youknowriad/wp-api-console.git`

2. Install dependencies `npm install`

3. Edit the `src/config.json` (see the "Configuration" section bellow)

3. Run the dev server `npm start`

Visit [http://localhost:3000](http://localhost:3000) in your browser.

Checkout the [this documentation](./DOC.md) for more technical details.

## Configuration

### Using with Wordpress.com APIs

To use with WordPress.com, visit [https://developer.wordpress.com/apps/](WordPress.com Developer Resources) and create an application.

Copy `src/config.sample.json` to `src/config.json` and use your WordPress.com App ID and Redirect URI for the values.

You will also need to add your host to the CORS whitelist in the Application's settings.

```json
{
  "wordpress.com": {
    "clientID": "33333",
    "redirectUrl": "http://localhost:3000"
  }
}
```

### Using with your self hosted WordPress

You can also use this console with your WordPress.org installation but make sure to install the [WP REST API - OAuth 1.0a Server](https://oauth1.wp-api.org/) first, create an app on it and then edit the `src/config.json` like this:

```javascript
{
  "wordpress.org": [
    {
      "name": "Dev",                         // Name to display on the API selector
      "url": "http://wordpress.dev",         // Base URL of your WordPress website
      "clientKey": "PwQXbJdBYrXq",           // Client (public) key of your application
      "secretKey": "XB9oidFfxr3g...",        // Secret key of your application
      "callbackUrl": "http://localhost:3000" // Callback URL where you are running this console
    }
  ]
}
```

Note that your console should not be running on `localhost` to work: the OAuth1 plugin prohibits local URLs by default.

You can also install the
[Application Passwords plugin](https://github.com/georgestephanis/application-passwords/)
and use basic authentication to communicate with your site.  Make sure that
your site is running over https, otherwise this is insecure.  Here are the
config settings for basic auth:

```javascript
{
  "wordpress.org": [
    {
      "name": "Dev (basic)",                 // Name to display on the API selector
      "url": "http://wordpress.dev",         // Base URL of your WordPress website
      "authType": "basic",
      "authHeader": "Basic bWU6bXlwYSBzc3dvIHJk"
    }
  ]
}
```

You can generate the base64-encoded portion of the `authHeader` as follows:

```sh
$ echo -n 'me:mypa sswo rd' | base64
bWU6bXlwYSBzc3dvIHJk
```

## Building

To create a static package you can use anywhere (e.g. Github pages): `npm run build`

The static site is located in `build`


## Deploying

You want to quickly deploy the console to [Surge](https://surge.sh), just run `npm run deploy`

## License

All source code licensed under the [MIT](./LICENSE) open source license.
