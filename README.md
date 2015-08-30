# Meteor Acccounts Twitch
#### Twitch account login for meteor

##Install

`cd <your-meteor-project>`

`meteor add service-configuration`
`meteor add alexbeauchemin:accounts-twitch`

##Setup and Usage
1. Register your app with Twitch Developer Site at following url- http://www.twitch.tv/kraken/oauth2/clients/new

2. Fill out the given form but make sure that redirect url as shown as follows-

  OAuth redirect_uri:`<your-server-domain>:<port>/_oauth/twitch?close`

  For e.g.redirect url for localhost : `http://localhost:3000/_oauth/twitch?close`

3. After registration, note down the client id and client secret.
4. Now in your app do create the `accounts.js` and put following code inside
`<your-app-directory>/server/accounts.js`
and put your client id and client secret

    ```
    ServiceConfiguration.configurations.remove({
      service: "twitch"
    });
    ServiceConfiguration.configurations.insert({
      service: "twitch",
      clientId: "<your-client-id>",
      redirectUri: Meteor.absoluteUrl() + '_oauth/twitch?close',
      scope:'basic',
      secret: "<your-client-secret>"
    });
    ```
5. Add the default twitch login button by adding this in your page
```
    {{>twitchLoginButton}}
```
or add this code on the click event of your custom button
```
      Meteor.loginWithTwitch(function (err) {
          if (err) console.log('login failed: ' + err)
      });
```

Now you should be able to create and account and login with Twitch