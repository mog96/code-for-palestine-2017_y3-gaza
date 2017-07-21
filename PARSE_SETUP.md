# Integrating Parse Server with Android
1. Create a [Heroku](https://www.heroku.com/) account. You will be hosting your Parse Server on Heroku.

2. Create a [new app](https://dashboard.heroku.com/new-app). Choose a good name for it. If the name you want isn't available, try suffixing it with '-server'. For 'Runtime Selection' choose 'Europe'. Then click 'Create App'.

3. Install the [Heroku Command Line Interface (CLI)](https://devcenter.heroku.com/articles/heroku-cli). Follow the installation instructions for your operating system.

4. Open the command line on your computer, and change directory to the directory where you want to store your server code.

5. Clone the Parse Server [example project](https://github.com/parse-community/parse-server-example):
  ```
  $ git clone https://github.com/parse-community/parse-server-example.git
  ```

6. Create an **empty** repository for your server on [GitHub](https://github.com/). Give it the same name as your Heroku app. *Do not* initialize it with a README.

7. Rename the `parse-server-example` directory to the name of your GitHub repository:
  ```
  $ mv parse-server-example name-of-your-github-repo
  ```

8. Change directory into the repository:
  ```
  $ cd name-of-your-github-repo
  ```

9. Check the remote url for the repository:
  ```
  $ git remote -v
  origin  https://github.com/parse-community/parse-server-example.git (fetch)
  origin  https://github.com/parse-community/parse-server-example.git (push)
  ```
  It currently points to the original `parse-server-example` repo.

10. Change the remote url to point to your GitHub repository:
  ```
  $ git remote set-url origin https://github.com/your-username/name-of-your-github-repo.git
  ```
  Verify that this change worked. 
  ```
  $ git remote -v
  origin  https://github.com/your-username/name-of-your-github-repo.git (fetch)
  origin  https://github.com/your-username/name-of-your-github-repo.git (push)
  ```

11. Push your repository to GitHub:
  ```
  $ git push
  ```

12. You should already have the Heroku CLI installed from Step 3. We are now going to deploy your app to Heroku. First log in to Heroku with this command:
  ```
  $ heroku login 
  ```
  You should be prompted to enter your email and password.

13. Once you have successfully logged in, connect your server repository to Heroku with the following command:
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

14. Deploy your app to Heroku with the following command:
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

15. Next we need to connect it to a database. Create an [mLab](https://mlab.com/) account.

16. Next create a [new database](https://mlab.com/create/wizard). Select 'Amazon Web Services' as the 'Cloud Provider', and select 'Sandbox' as the 'Plan Type'. Then click 'Contiinue'. Choose 'EU (Ireland)' as the 'AWS Region'. Then click 'Continue'. Enter a name for your database. (Developers sometimes like to name their databases after people.) Click 'Continue'. Confirm all the details about your database, and then click 'Submit Order'.

17. Once the setup of your database has completed, we can get the URI of your database. Click the database name to go to its home page. At the top of the page there should be a URI with the prefix `mongodb://`. Copy the URI.

18. Go to the directory containing your server, and open the `index.js` file. This file contains all of the configuration information for your Parse Server. **Do not** make any changes to this file just yet.

19. As you might have noticed, the MongoDB URI that you copied has a section `<dbuser>:<dbpassword>`, which you need to fill in with your mLab username and password. This is *sensitive information* and should be seen by nobody except you. Therefore, you *do not* want to leave it in your `index.js` file, especially given that this file is visible on GitHub.

  To solve this issue, we will set the URI as a 'config var' on Heroku. This will allow Heroku to add the URI to your index.js file when your server is first initialized. To give you an idea of how this works, take a look at the following line near the top of your `index.js` file:
  ```
  var databaseUri = process.env.DATABASE_URI || process.env.MONGODB_URI;
  ```
  You can see here that the `databaseUri` is being set using values stored in the *environment*, `process.env`, in which your server is running. First your code looks for a config var with the name `DATABASE_URI`, and if it isn't found, looks for a config var with the name `MONGODB_URI`.

  To set the `DATABASE_URI` config var in Heroku, go to the command line on your computer and run the following command:
  ```
  $ heroku config:set DATABASE_URI=your_mongodb_uri_with_username_and_password_replaced
  ```
  Be sure to replace the `<dbuser>:<dbpassword>` section of your MongoDB URI with your mLab username and password. To confirm that you correctly set the `DATABASE_URI` config var, run the following command to list all of the config vars set for your heroku app:
  ```
  $ heroku config
  ```
  Nice work! Your server is now connected to your database.

17. Go back to your `index.js` file. Take a look at this line and the lines directly below it:
  ```
  var api = new ParseServer ({
    databaseURI: databaseUri,
    ...

  });
  ```
  You can here that a new `ParseServer` object is created, representing your server. It takes in the database URI that we set above, as well as several other fields set using the same `process.env.CONFIG_VAR` scheme as our database URI. In order for our server to run correctly we need to set the following config vars at minimum:
  - APP_ID
  - MASTER_KEY
  - PARSE_MOUNT
  - SERVER_URL

# Sources
Codepath: [Configuring a Parse Server](https://github.com/codepath/android_guides/wiki/Configuring-a-Parse-Server)