---
title: Continuous Testing, Continuous Integration & Continuous Delivery (CI/CD) - Travis CI and Heroku
---

# Continuous Testing

## Types of tests

### Unit tests

- Lowest level of testing
- Test an individual unit (or function) of a software
- Tests are run in very controlled environment

### Functional tests

- Higher level function testing
- Test outside dependencies
- Example: get a specific value from a database, API

### Integration tests

- Assemble project modules
- Test how microservices work together
- Example: database connection

### End-To-End tests

- Test the application in a real environment
- Use production-like database
- UI testing
- Acceptance testing

gatsby-slide

# Continuous Testing

## Test driven development (TDD)

- Write test before writing the associated function
- Make sure all the tests are successful

## Test Automation

- Run tests on a server with specific configuration specified in your tests
- Run the tests on different version of the code
  - Condition for PullRequest merge
  - On each commit
- Run on your own server

gatsby-slide

# Continuous Integration and Delivery (CI/CD)

## Continuous Integration (CI)

This is a software development practice in which members of a team integrate their work frequently, at least daily, leading to multiple integrations per day.

## Continuous Delivery (CD)

This is a software development discipline where software is built in a manner that allows for deploying to customers at any time.

##  Continuous Deployment

This extends Continuous Delivery by automating the deployment process so that code is automatically deployed to production after it passes automated testing.

gatsby-slide

# What is the CI/CD Pipeline?

**CI/CD pipeline** - an automated sequence of events that is initiated after you update the code.

These events take care of the work that you would otherwise need to perform manually:
- previewing your in-development site
- testing your new code
- deploying it to your production server

gatsby-slide

# CI/CD with Travis CI and deployment platforms

[Travis CI Tutorial](https://docs.travis-ci.com/user/tutorial/)

## CD using Heroku

[Heroku Deployment](https://docs.travis-ci.com/user/deployment/heroku/)

[Automatically deploy with Travis CI and Heroku (article)](https://medium.com/@felipeluizsoares/automatically-deploy-with-travis-ci-and-heroku-ddba1361647f)

## CD using Netlify

[Netlify Drop](https://app.netlify.com/drop)

[Netlify Drop Deployment](https://docs.travis-ci.com/user/deployment-v2/providers/netlify/)

gatsby-slide

# The CI/CD Pipeline Sequence

The flow of events:

1. You create a new branch in your local Git repository and make code changes to your Gatsby project.

2. You push your branch to your GitHub repository and create a pull request.

3. Netlify automatically creates a preview of the site with a unique URL that can be shared.

4. Travis CI automatically builds the site in an isolated container and runs any declared tests.

5. When all tests pass, you merge the PR into the repository’s master branch, which automatically triggers a deployment to your production.

gatsby-slide

# Your work

## 1. CI part - Travis CI

1. Go to [travis-ci.com](https://travis-ci.com/) and sing up with GitHub account

2. Sync GitHub account with Travis CI account

3. Create `.travis.yml` configuration file under the root of your project repo:

```
language: node_js
node_js:
- '12'
- '13'
script:
- echo 'Starting'
- npm install
- echo 'Testing'
- npm test
```

And push it to the remote master.

5. Create a pull request to master branch:

- create a new branch and publish it to your remote
- make some change, commit it and push to the remote
- make a Pull Request using GitHub
- wait until Travis will test it
- review the commit and Merge this Pull Request

6. Check the Travis CI build log.

gatsby-slide

# Your work

## 2. CD part - Travis CI and Heroku

1. Create an account on [Heroku](https://heroku.com)

2. Create an app on [Heroku](https://dashboard.heroku.com/new-app) and configure it

Under the "Deploy tab":

  - sync the app with the GitHub repository
  - enable option "Automatic deploys / Wait for CI to pass before deploy"

4. Configure `.travis.yml` with Heroku

**Install CLIs:**

  - [`travis`](https://github.com/travis-ci/travis.rb#installation)
  - [`heroku`](https://devcenter.heroku.com/articles/heroku-cli)

**Configuration:**

Link to configuration instruction - [Heroku Deployment](https://docs.travis-ci.com/user/deployment/heroku/)

You can use this command:

```
travis setup heroku
```

After that in the `.travis.yml` will be appended something like:

```
deploy:
  provider: heroku
  api_key:
    secure: N2vEDW5kJSmMYsxQLJCxoNoGZFmpMM4Hpc6Rf1FdsHqtbgXgmX6gbu48mo1ZIF0FFDJEDG4lES2FbFcjxfNpvH7r9zpuTffHe8p3Cbq5Y5C+X5m0fCWUoQGPgL/qczoN/Xla/J0U8DN14cX2+f9OSWmjAcTFzogG6AEm4XOHCzhY7tSYbGP65N40SWxKIcMQ48wKGifeeQSB2vbm4Lu9SKHiLFo1VyQN3o5Ziu+f9NoByIcKtyEnjAfyWdZ8uAea1ZXH/HqivpFCAgPIoaw5qJcRcCIlj84qteLbdtbYCWB2MMyWZ0XQ0TCrI8TUNefqbM+AaS3OgAb+z/CAHPVgfJuEt6vfq9asH6aVDhTIva/whjS2S4JXeZUNNkBdp3IEeYKwpu6uNXAqjZ05132Gq/RiRAeqOXcWj+FgCZ2F/EjmXiP3Vpm8k5/cPOt+7ilrXc27XF3HoHs+AKFaMc75aa+0Rx2GSAw1+WSyBrFTLFKqBG0QzGsiBjUyrc+9bEj9NEte/mbYLJuna2D+JzwXaZdv3s3Cjpnz0xxQaDgt8xeuFz/StzB/6DZfgpBWIvIMzW6hTERTtuToxS8BjhnIvfoGC2eiI2jM0keZrzf/eTyizwfjxEXhFOamnGmmQx903jXlTmPZ8rTyUFhJr68T9i3MlDp6M4EwLsqzExUUiGo=
  app: ece-devops-si02
  on:
    repo: sergkudinov/ece-userapi-grSI02
```

And push it to the remote master.

**Note!**

If you have an error like *"Message: Invalid credentials provided."* in your Travis CI log, [read this](https://stackoverflow.com/questions/51925918/issues-with-deploying-to-heroku-via-travis-ci?answertab=votes#tab-top).

5. Create a pull request to the master branch to test your CI/CD pipeline.

6. Test your public domain on Heroku.
