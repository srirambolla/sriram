# Front end Example for Okta Spring Security Resource Server

This front-end sample application can be used to test the [Resource Server](../resource-server) sample application provided in this repo.

## Prerequisites

Before running this sample, you should start the resource server backend.

**backend:**
```bash
cd ../resource-server
mvn -Dokta.oauth2.issuer=https://{yourOktaDomain}.com/oauth2/default
```

> **NOTE:** The above command starts the resource server on port 8000. You can browse to `http://localhost:8000` to ensure it has started. If you get the message "Full authentication is required to access this resource", it indicates that the resource server is up. You will need to pass an access token to access the resource, which will be done by the front-end below.

**front-end:**

To start the front-end, you need to gather the following information from the Okta Developer Console:

- **Client Id** - The client ID of the SPA application that you created earlier. This can be found on the "General" tab of an application, or the list of applications. The resource server will validate that tokens have been minted for this application.
- **Issuer** - This is the URL of the authorization server that minted the tokens.  All Developer Accounts have a "default" authorization server.  The issuer is a combination of your Org URL (found in the upper right of the console home page) and `/oauth2/default`. For example, `https://dev-1234.oktapreview.com/oauth2/default`.

Update the configuration file [`config.js`](./src/main/resources/static/js/config.js) with the client id and base url that you obtained in the previous step.

```javascript
window.oktaSignIn = new OktaSignIn({
  baseUrl: 'https://{yourOktaDomain}.com',
  clientId: '{yourClientId}',
  redirectUri: window.location.href,
  authParams: {
    issuer: 'default',
    responseType: ['id_token', 'token'],
    scopes: ["openid", "profile", "email"]
  }
});
```
Now start the front-end.

```bash
cd front-end
mvn
```

Browse to: `http://localhost:8080/` to login!
