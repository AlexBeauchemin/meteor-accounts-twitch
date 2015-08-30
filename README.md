# Meteor Acccounts Instagram
#### Twitch account login for meteor

##Install

`cd <your-meteor-project>`

`meteor add alexbeauchemin:accounts-twitch`

and also add following package as pre-req -

`meteor add service-configuration`


##Setup and Usage
1. Register your app with Twitch Developer Site at following url- http://www.twitch.tv/kraken/oauth2/clients/new

2. Fill out the given form but make sure that redirect url as shown as follows-

  OAuth redirect_uri:`<your-server-domain>:<port>/_oauth/twitch?close`

  For e.g.redirect url for localhost : `http://localhost:3000/_oauth/twitch?close`

3. After registration, note down the clientid and client secret.
4. Now in your app do create the `accounts.js` and put following code inside

 so,it file looks in directory tree- `<your-app-directory>/server/accounts.js`  and put the client id and client secret from previous step

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
5. Now, all things are setup, you are ready to use this package
6. Add the default twitch login button by adding this in your page
```
    {{>twitchLoginButton}}
```
or add this code on the click event of your custom button
```
      Meteor.loginWithTwitch(function (err) {
          if (err) console.log('login failed: ' + err)
      });
```