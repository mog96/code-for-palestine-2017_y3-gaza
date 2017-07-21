# Integrating Parse Server with Android
## 1.
Create a [Heroku](https://www.heroku.com/) account. You will be hosting your Parse Server on Heroku.

## 2.
Create a [new app](https://dashboard.heroku.com/new-app). Choose a good name for it. If the name you want isn't available, try suffixing it with '-server'. For 'Runtime Selection' choose 'Europe'. Then click 'Create App'.

## 3.
Install the [Heroku Command Line Interface (CLI)](https://devcenter.heroku.com/articles/heroku-cli). Follow the installation instructions for your operating system.

## 4.
Open the command line on your computer, and change directory to the directory where you want to store your server code.

## 5.
Clone the Parse Server [example project](https://github.com/parse-community/parse-server-example):
```
$ git clone https://github.com/parse-community/parse-server-example.git
```
**Note:** The `$` indicates that this is a command for your command line. Don't include the `$` with the command.

## 6.
Create an **empty** repository for your server on [GitHub](https://github.com/). (You'll need to create a GitHub account if you don't already have one.) Give the repository the same name as your Heroku app. *Do not* initialize it with a README.

## 7.
Rename the `parse-server-example` directory to the name of your GitHub repository:
```
$ mv parse-server-example name-of-your-github-repo
```

## 8.
Change directory into the repository:
```
$ cd name-of-your-github-repo
```

## 9.
Check the remote url for the repository:
```
$ git remote -v
origin  https://github.com/parse-community/parse-server-example.git (fetch)
origin  https://github.com/parse-community/parse-server-example.git (push)
```
It currently points to the original `parse-server-example` repo.

## 10.
Change the remote url to point to your GitHub repository:
```
$ git remote set-url origin https://github.com/your-username/name-of-your-github-repo.git
```
Verify that this change worked. 
```
$ git remote -v
origin  https://github.com/your-username/name-of-your-github-repo.git (fetch)
origin  https://github.com/your-username/name-of-your-github-repo.git (push)
```

## 11.
Push your repository to GitHub:
```
$ git push
```

## 12.
You should already have the Heroku CLI installed from [Step 3](#3). We are now going to deploy your app to Heroku. First log in to Heroku with this command:
  ```
  $ heroku login 
  ```
  You should be prompted to enter your email and password.

## 13.
Once you have successfully logged in, connect your server repository to Heroku with the following command:
```
$ heroku git:remote -a your-heroku-app-name
```
Verify that this change worked:
```
$ git remote -v
heroku  https://git.heroku.com/name-of-your-github-repo.git (fetch)
heroku  https://git.heroku.com/name-of-your-github-repo.git (push)
origin  https://github.com/mog96/name-of-your-github-repo.git (fetch)
origin  https://github.com/mog96/name-of-your-github-repo.git (push)
```
You should now see a remote called 'heroku' in addition to the remote called 'origin'.

## 14.
Deploy your app to Heroku with the following command:
```
$ git push heroku master
```
You should see lots of logs prefixed with 'remote:' describing the status of the deploy. If the deploy was successful, you should see the following at the very bottom of the logs:
```
remote: Verifying deploy... done.
To https://git.heroku.com/name-of-your-github-repo.git
* [new branch]      master -> master
```
Nice work! You now have a server running on Heroku.

## 15.
Next we need to connect it to a database. Create an [mLab](https://mlab.com/) account.

## 16.
Next create a [new database](https://mlab.com/create/wizard). Select 'Amazon Web Services' as the 'Cloud Provider', and select 'Sandbox' as the 'Plan Type'. Then click 'Contiinue'. Choose 'EU (Ireland)' as the 'AWS Region'. Then click 'Continue'. Enter a name for your database. (Developers sometimes like to name their databases after people.) Click 'Continue'. Confirm all the details about your database, and then click 'Submit Order'.

## 17.
Once the setup of your database has completed, click the database name to go to its home page. In order to enable access to your database you will need to *add a user to the database*. Click the 'Users' tab, and then click 'Add database user'. Enter a username and password. This username and password should be different from your mLab login. We will need this username and password in Step 20. Click 'Create'.

You should now have a database user with 'READ ONLY?' set to 'false'.

## 18.
At the top of the page there should be a URI with the prefix `mongodb://`. Copy the URI.

## 19.
Go to the directory containing your server, and open the `index.js` file. This file contains all of the configuration information for your Parse Server. **Do not** make any changes to this file just yet.

## 20.
As you might have noticed, the MongoDB URI that you copied has a section `<dbuser>:<dbpassword>`, which you need to fill in with your the username and password of the user you added to your database. This is *sensitive information* and should be seen by nobody except you. Therefore, you *do not* want to leave it in your `index.js` file, especially given that this file is visible on GitHub.

To solve this issue, we will set the URI as a 'config var' on Heroku. This will allow Heroku to add the URI to your index.js file when your server is first initialized. To give you an idea of how this works, take a look at the following line near the top of your `index.js` file:
```
var databaseUri = process.env.DATABASE_URI || process.env.MONGODB_URI;
```
You can see here that the `databaseUri` is being set using a value stored in the *environment* in which it is running, `process.env`, in which your server is running. First your code looks for a config var with the name `DATABASE_URI`, and if it isn't found, looks for a config var with the name `MONGODB_URI`.

To set the `DATABASE_URI` config var in Heroku, go to the command line on your computer and run the following command:
```
$ heroku config:set DATABASE_URI=your_mongodb_uri_with_username_and_password_replaced
```
Be sure to replace the `<dbuser>:<dbpassword>` section of the URI with the username and password of the *user you added to your database* (not your mLab account username and password). Remove the `<` and `>` characters as well.

To confirm that you correctly set the `DATABASE_URI` config var, run the following command to list all of the config vars set for your heroku app:
```
$ heroku config
```
Nice work! Your server is now connected to your database.

## 21.
Go back to your `index.js` file. Take a look at this section:
```javascript
var api = new ParseServer ({
  databaseURI: databaseUri,
  ...

});
```
You can here that a new `ParseServer` object is created, representing your server. It takes in the database URI that we set above, as well as several other fields set using the same `process.env.CONFIG_VAR` scheme as our database URI. In order for our server to run correctly we need to set the following config vars at minimum:
- `APP_ID`
- `MASTER_KEY`
- `PARSE_MOUNT`
- `SERVER_URL`

The `APP_ID` and `MASTER_KEY` can be set to any combination of letters, numbers, and special characters that you like. Treat the `APP_ID` as a username, and the `MASTER_KEY` as a password.

The `PARSE_MOUNT` should be set to `/parse`.

The `SERVER_URL` should be set to `http://yourappname.herokuapp.com/parse`. Note that the end of the server URL matches the `PARSE_MOUNT` above.

Set the config vars using the same `heroku config:set` command as before:
```
$ heroku config:set APP_ID=your_app_id
$ heroku config:set MASTER_KEY=your_master_key
$ heroku config:set PARSE_MOUNT=/parse
$ heroku config:set SERVER_URL=http://yourappname.herokuapp.com/parse
```

## 22.
Verify that all your config vars are set correctly:
```
$ heroku config
```

Make sure each of the following config vars appear:
```
APP_ID
DATABASE_URI
MASTER_KEY
PARSE_MOUNT
SERVER_URL
```

## 23.
Test that your server setup is working by storing an object in your database. Paste the following at the command line, with **`myAppId` and `yourappname` replaced with your server's values**:
```
curl -X POST -H "X-Parse-Application-Id: myAppId" \
-H "Content-Type: application/json" \
-d '{"score":1337,"playerName":"Sean Plott","cheatMode":false}' \
https://yourappname.herokuapp.com/parse/classes/GameScore
```
This creates a new GameScore document and stores it in your database.

You should get back something like this:
```
{"objectId":"JzfxQjhleB","createdAt":"2017-07-21T06:14:10.512Z"}
```
Indicating that the store was successful. If you go back to mLab in your browser and refresh your database page, under the `Collections` tab you should now see a collection called `GameScore`. Click on the collection to see its documents. You should see a document in JSON form that contains the same information as was included in the `curl` command above, as well as some additional fields: an ID, created-at time, and updated-at time. It will look something like this:
```json
{
    "_id": "OEf5byC3tH",
    "score": 1337,
    "playerName": "Sean Plott",
    "cheatMode": false,
    "_created_at": {
        "$date": "2017-07-21T09:10:34.577Z"
    },
    "_updated_at": {
        "$date": "2017-07-21T09:10:34.577Z"
    }
}
```

Nice work! You can now store documents in your server.

If you got back something like this:
```
{"code":1,"message":"Internal server error."}
```
It means that your server was not configured correctly. You can get more information about the error from your server's logs with the following command:
```
$ heroku logs
```
A common error is failed MongoDB authentication. Check that the username and password for your database are exactly as you set them in [Step 17](#17).

## 24.
Lastly, before moving on to Android, test that you can read data back from your server. Reading data requires the master key. Paste the following at the command line, with **`myAppId`, `abc` and `yourappname` replaced with your server's values**:
```
curl -X GET -H "X-Parse-Application-Id: myAppId" -H "X-Parse-Master-Key: abc"  \
https://yourappname.herokuapp.com/parse/classes/GameScore
```

You should get back something like this:
```
{"results":[{"objectId":"JzfxQjhleB","score":1337,"playerName":"Sean Plott","cheatMode":false,"createdAt":"2017-07-21T06:14:10.512Z","updatedAt":"2017-07-21T06:14:10.512Z"}]}
```

Nice work! You've now verified that you can both store and retrieve data using your Parse Server's [RESTful API](http://searchcloudstorage.techtarget.com/definition/RESTful-API).

## 25.
Now for integration with Android. Open your Android Studio project and add the following to the `dependencies` section of your app's `build.gradle` file:
```
// For Parse Server.
compile 'com.parse.bolts:bolts-android:1.4.0'
compile 'com.parse:parse-android:1.15.1'
compile 'com.squareup.okhttp3:logging-interceptor:3.6.0' // for logging API calls to LogCat
```
Click 'Sync Now' when it appears.

## 26.
Next you will create a Java class to manage your app's connection to your Parse Server.

Open the project navigator tab and select the folder containing your app's Java files ('app' -->  'java' --> 'com.your.app.name').

Right click this folder, and select 'New' --> 'Java Class'. Enter 'ParseApplication' as the name. Leave all other fields blank and click 'OK'.

Replace the `class` declaration in your new file with the following and follow all of the `TODO`s:
```java
public class ParseApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();

        // Use for troubleshooting.
        // IMPORTANT: Remove this line for production.
        Parse.setLogLevel(Parse.LOG_LEVEL_DEBUG);

        // Use OkHttp for monitoring Parse trafic.       
        // Can be Level.BASIC, Level.HEADERS, or Level.BODY
        // Go to http://square.github.io/okhttp/3.x/logging-interceptor/ to see the options.
        OkHttpClient.Builder builder = new OkHttpClient.Builder();
        HttpLoggingInterceptor httpLoggingInterceptor = new HttpLoggingInterceptor();
        httpLoggingInterceptor.setLevel(HttpLoggingInterceptor.Level.BODY);
        builder.networkInterceptors().add(httpLoggingInterceptor);

        Parse.initialize(new Parse.Configuration.Builder(this)
                .applicationId("myAppId") // TODO: Replace with your app ID.
                .clientKey(null)
                .clientBuilder(builder)
                .server("https://my-parse-app-url.herokuapp.com/parse/").build()); // TODO: Replace with your app URL.
    }
}
```

## 27.
Next you need to tell Android to instantiate your above `ParseApplication` class when your app is initialized. Go to `AndroidManifest.xml`
and add the following attribute `<application>` tag:
```xml
android:name=".ParseApplication"
```

Your `AndroidManifest.xml` should now look something like this:
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.your.app.name">

    <application
        android:name=".ParseApplication"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

## 28.
Next you need to add two permissions to enable Parse. Add the following two lines:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

Such that your `AndroidManifest.xml` looks like this:
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.your.app.name">

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

    <application
        android:name=".ParseApplication"
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

## 29.
Test that you'ce configured your app correctly by adding the following to the end of the `onCreate()` method of your `ParseApplication` class:
```java
// New test creation of object below
ParseObject testObject = new ParseObject("TestObject");
testObject.put("foo", "bar");
testObject.saveInBackground();
```
Make sure these lines come *after* the call to `Parse.initialize()`. Your `onCreate()` should look something like this:
```java
public class ParseApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();

        // Your initialization code from above here
        Parse.initialize(...);

        // New test creation of object below
        ParseObject testObject = new ParseObject("TestObject");
        testObject.put("foo", "bar");
        testObject.saveInBackground();
    }   
}
```

Now build and run your app on an Internet-connected device. Once the app has sucessfully launched, go back to mLab in your browser and refresh your database page. Under the `Collections` tab you should now see a collection called `TestObject`. The collection should contain one document in JSON form that has a field "foo" set to the value "bar", and will look similar to this:
```json
{
    "_id": "bMQLf0CVqm",
    "foo": "bar",
    "_created_at": {
        "$date": "2017-07-21T08:54:31.818Z"
    },
    "_updated_at": {
        "$date": "2017-07-21T08:54:31.818Z"
    }
}
```

In Android Studio, open the Android Monitor, which should have its own tab at the bottom of Android Studio. (If you don't see it, go to View > Tool WIndows > Android Monitor.) You should see some logs like these, that contain the tag `D/OkHttp`:
```
07-21 11:54:31.373 2369-2404/com.your.app.name D/OkHttp: --> POST https://yourappname.herokuapp.com/parse/classes/TestObject http/1.1
07-21 11:54:31.373 2369-2404/com.your.app.name D/OkHttp: Content-Type: application/json
07-21 11:54:31.373 2369-2404/com.your.app.name D/OkHttp: Content-Length: 13
07-21 11:54:31.373 2369-2404/com.your.app.name D/OkHttp: X-Parse-Application-Id: yourappid
07-21 11:54:31.374 2369-2404/com.your.app.name D/OkHttp: X-Parse-Client-Version: a1.15.1
07-21 11:54:31.374 2369-2404/com.your.app.name D/OkHttp: X-Parse-App-Build-Version: 1
07-21 11:54:31.374 2369-2404/com.your.app.name D/OkHttp: X-Parse-App-Display-Version: 1.0
07-21 11:54:31.374 2369-2404/com.your.app.name D/OkHttp: X-Parse-Installation-Id: d922f586-05a7-4855-b0b7-88eed1825614
07-21 11:54:31.374 2369-2404/com.your.app.name D/OkHttp: Host: yourappname.herokuapp.com
07-21 11:54:31.374 2369-2404/com.your.app.name D/OkHttp: Connection: Keep-Alive
07-21 11:54:31.374 2369-2404/com.your.app.name D/OkHttp: Accept-Encoding: gzip
07-21 11:54:31.374 2369-2404/com.your.app.name D/OkHttp: User-Agent: okhttp/3.6.0
07-21 11:54:31.375 2369-2404/com.your.app.name D/OkHttp: {"foo":"bar"}
07-21 11:54:31.375 2369-2404/com.your.app.name D/OkHttp: --> END POST (13-byte body)
07-21 11:54:31.585 2369-2404/com.your.app.name D/OkHttp: <-- 201 Created https://yourappname.herokuapp.com/parse/classes/TestObject (209ms)
07-21 11:54:31.585 2369-2404/com.your.app.name D/OkHttp: Server: Cowboy
07-21 11:54:31.585 2369-2404/com.your.app.name D/OkHttp: Connection: keep-alive
07-21 11:54:31.585 2369-2404/com.your.app.name D/OkHttp: X-Powered-By: Express
07-21 11:54:31.585 2369-2404/com.your.app.name D/OkHttp: Access-Control-Allow-Origin: *
07-21 11:54:31.585 2369-2404/com.your.app.name D/OkHttp: Access-Control-Allow-Methods: GET,PUT,POST,DELETE,OPTIONS
07-21 11:54:31.585 2369-2404/com.your.app.name D/OkHttp: Access-Control-Allow-Headers: X-Parse-Master-Key, X-Parse-REST-API-Key, X-Parse-Javascript-Key, X-Parse-Application-Id, X-Parse-Client-Version, X-Parse-Session-Token, X-Requested-With, X-Parse-Revocable-Session, Content-Type
07-21 11:54:31.585 2369-2404/com.your.app.name D/OkHttp: Location: http://yourappname.herokuapp.com/parse/classes/TestObject/bMQLf0CVqm
07-21 11:54:31.585 2369-2404/com.your.app.name D/OkHttp: Content-Type: application/json; charset=utf-8
07-21 11:54:31.586 2369-2404/com.your.app.name D/OkHttp: Content-Length: 64
07-21 11:54:31.586 2369-2404/com.your.app.name D/OkHttp: Date: Fri, 21 Jul 2017 08:54:31 GMT
07-21 11:54:31.586 2369-2404/com.your.app.name D/OkHttp: Via: 1.1 vegur
07-21 11:54:31.586 2369-2404/com.your.app.name D/OkHttp: {"objectId":"bMQLf0CVqm","createdAt":"2017-07-21T08:54:31.818Z"}
07-21 11:54:31.586 2369-2404/com.your.app.name D/OkHttp: <-- END HTTP (64-byte body)
```
These are from the `OkHttp` logger we set up in [Step 26](#26), before we initializing Parse. These logs will be useful when you are debugging later on.

Nice work! You now have an Android app connected to your Parse Server.

# Sources
### Codepath
- [Configuring a Parse Server](https://github.com/codepath/android_guides/wiki/Configuring-a-Parse-Server)
- [Building Data-Driven Apps with Parse](https://github.com/codepath/android_guides/wiki/Building-Data-driven-Apps-with-Parse)