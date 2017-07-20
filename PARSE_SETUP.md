# Integrating Parse Server with Android
1. Create a [Heroku](https://www.heroku.com/) account. You will be hosting your Parse Server on Heroku.
2. Create a [new app](https://dashboard.heroku.com/new-app). Choose a good name for it. If the name you want isn't available, try suffixing it with '-server'.
3. 
1.
  Clone the Parse Server [example project](https://github.com/parse-community/parse-server-example):
  ```
  $ git clone https://github.com/parse-community/parse-server-example.git
  ```
2.
  Create an **empty** [GitHub](https://github.com/) repository for your server. Do *not* initialize it with a README.
3.
  Rename the `parse-server-example` directory to the name of your repository:
  ```
  $ mv parse-server-example name-of-your-github-repo
  ```
4.
  Change directory into the repository:
  ```
  $ cd name-of-your-github-repo
  ```
5.
  Check the remote url for the repository:
  ```
  $ git remote -v
  origin  https://github.com/parse-community/parse-server-example.git (fetch)
  origin  https://github.com/parse-community/parse-server-example.git (push)
  ```
  It currently points to the original `parse-server-example` repo.
6.
  Change the remote url to point to your repository:
  ```
  $ git remote set-url origin https://github.com/your-username/name-of-your-github-repo.git
  ```
  Verify that this change worked. 
  ```
  $ git remote -v
  origin  https://github.com/your-username/name-of-your-github-repo.git (fetch)
  origin  https://github.com/your-username/name-of-your-github-repo.git (push)
  ```
7.
  Push your repository to GitHub:
  ```
  $ git push
  ```
8.
  Install the [Heroku Command Line Interface](https://devcenter.heroku.com/articles/heroku-cli) (CLI). Follow the instructions for your operating system.
9.
  Once you have Heroku CLI installed, return to the directory containing your repository. Create a new heroku app and run:
  ```
  $ heroku create 
  ```

# Sources
Codepath: [Configuring a Parse Server](https://github.com/codepath/android_guides/wiki/Configuring-a-Parse-Server)