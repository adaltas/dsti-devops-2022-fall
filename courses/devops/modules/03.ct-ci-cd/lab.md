
# Lab

Continuous Testing, Continuous Integration & Continuous Delivery (Deployment) (CI/CD)

## Objectives

1. Part 1. Continuous Testing
2. Part 2. Continuous Integration with GitHub Actions
3. Part 3. Continuous Delivery (Deployment) with Heroku

## Before starting

1. Install Redis database

Installation instructions:

- **Windows:** https://redislabs.com/ebook/appendix-a/a-3-installing-on-windows/a-3-2-installing-redis-on-window/
- **MacOS:** `brew install redis` or https://redis.io/topics/quickstart
- **Linux or MacOS:** https://redis.io/topics/quickstart

After installation starts Redis server:

- **Windows:** double click on `redis-server.exe` file (keep it open)
- **MacOS and Linux:** `redis-server`

Test if the Redis server is running:

- **Windows:** double click on `redis-cli.exe` and run the `ping` command inside this terminal
- **MacOS and Linux:** run in a new terminal window `redis-cli ping` (should answer with "PONG")

2. Install an **IDE or a text editor**, for example, [Atom](https://atom.io/) or [VS Code](https://code.visualstudio.com/)

3. Install **NodeJS**: https://nodejs.org/

## Part 1. Continuous Testing

### 1. Use prepared User API application and run tests

Go to [`assets/userapi`](assets/userapi) folder and explore the project:

```
cd assets/userapi
```

Install application:

```
npm install
```

Run tests:

```
npm test
```

Start application:

```
npm start
```

### 2. Using test-driven development (TDD) create GET user functionality

Create a REST API GET `user` method that retrieves user information from the database.

> Hint. The source code of the example application in the folder `assets/userapi` contains `TODO` comments in the places where you are supposed to make modifications to accomplish these steps.

1) Create `get` user controller:   
  - Create **2 unit tests** (in the file `assets/userapi/test/user.controller.js`):
    - successfully get user
    - cannot get a user when it does not exist
  - Create **the controller method** (in the file `assets/userapi/src/controllers/user.js`)

2) Create GET user REST API method:   
  - Create **2 API tests** (in the file `assets/userapi/test/user.router.js`):
    - successfully get user
    - cannot get a user when it does not exist
  - Create **GET user route** (in the file `assets/userapi/src/routes/user.js`)

## Part 2. Continuous Integration with GitHub Actions

Before starting configuring CI, you need to have a repository on GitHub. Let's create it for the project from Part 1:

- Create a Git repository for the User API project from **Part 1** and commit all the files. 
- Create a remote repository on GitHub, link it with the local one, and push the changes.

1. Read the [introduction to GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/introduction-to-github-actions).

2. Create a CI workflow for the Node.js using this [documentation](https://docs.github.com/en/actions/guides/building-and-testing-nodejs). 

> Note. Don't forget to commit and push your workflow configuration in the `.github/workflows` folder.

Does your workflow work? Is there any problem with the connection to Redis?

3. Improve your Workflow to connect Node.js application to Redis using this documentation:
  - [About service containers](https://docs.github.com/en/actions/guides/about-service-containers)
  - [Creating Redis service containers](https://docs.github.com/en/actions/guides/creating-redis-service-containers)

4. Practice a regular workflow of the software development life cycle. 

Create a pull request to the `master` branch:

- create a new branch and publish it to your remote GitHub repository
- make any change in your source code, commit and push it
- make a **Pull Request** on GitHub
- wait for GitHub Actions to test it (observe the process on GitHub -> Actions page)
- review the commit and Merge this Pull Request into the `master` branch

5. Explore the GitHub Actions log on GitHub (under the "Actions" tab).

## Part 3. Continuous Delivery (Deployment) with Heroku

1. Create an account on [Heroku](https://heroku.com)

2. Create an app on [Heroku](https://dashboard.heroku.com/new-app) and configure it.

Under the "Deploy tab" do:

  - sync the app with the GitHub repository
  - enable the option "Automatic deploys / Wait for CI to pass before deploy"

3. Add Redis service to Heroku deployment - https://elements.heroku.com/addons/heroku-redis

> Note. Redis service on Heroku is free, but it requires adding credit card information. Considering this limitation we will not run Redis on Heroku, and the application will be partially non-functional (it will print the "Hello world!" message on the home page, but the user API will not work). However, it will be enough to experience our CI/CD pipeline.

4. Configure the workflow to deploy to Heroku using [this guide](https://github.com/marketplace/actions/deploy-to-heroku).

5. Practice a regular workflow of the software development life cycle like in Part 2.

6. Test your public domain on Heroku.

## Bonus tasks

1. Integrate Swagger UI using this package - https://www.npmjs.com/package/express-swagger-generator
