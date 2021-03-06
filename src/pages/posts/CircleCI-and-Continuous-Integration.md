---
featured: true
intro: true
title:  "CircleCI and Continuous Integration"
uniqueID: "circleCIAndContinuousIntegration"
description:  "Love to push code? Would you also love to build your application and test it when you do? I thought you might."
shortName: "🧙‍"
banner: "/images/posts/build.jpg"
date: 2017-09-01
tags: ["circleci", "CI", "docker", "pipeline"]
---

## What is it?

> Continuous Integration (CI) is the process of automating the build and testing of code every time a team member commits changes to version control. CI encourages developers to share their code and unit tests by merging their changes into a shared version control repository after every small task completion. Committing code triggers an automated build system to grab the latest code from the shared repository and to build, test, and validate the full master branch (also known as the trunk or main).

[Read more...](https://docs.microsoft.com/en-us/azure/devops/learn/what-is-continuous-integration)

So, I've been messing around with Travis, Hudson, Jenkins for a while now. I've implemented very basic build pipelines to this day and was looking around for the right continuous integration framework. There are no real great differences between the aforementioned and CircleCI and BuildBot, with the exception that the latter two are more customizable and non-GUI oriented.

### CircleCI

I chose CircleCI cause it was really easy to spin up and get functional.

#### Getting Started

You should by now have a GitHub account and a GitHub repository that you want to target for continuous integration. You'll need both of these things if you're following along with the guide, but if you're just here for an overview, carry on.

The easiest way to create your account is to sign up using your GitHub account. So go to the home page at [https://circleci.com](https://circleci.com) and click on **Sign Up**.

Then on the next page click **Start with GitHub**.

Locate the repository that you want to target and click **Setup project**.

You'll be taken to a view where you can configure your project. Here you can choose details like OS, and language.

Here you'll also find instructions for configuring your repository to work with CircleCI.

A this point you can click **Start building**, we'll configure the repository in the following steps.

#### Set Up

Setting up your repository is fairly simple. As long as the configuration file exists, Circle will run your integration.

So let's add the file. You need to create a folder called `.circleci` and add a file called `config.yml`.

```bash
mkdir .circleci
touch .circleci/config.yml
```
Once this is done we'll add some basic configuration.

#### Configuration

Let me begin this step by saying that any useful configuration that you will need is going to be specific to your app. This includes things like building docker images, running unit tests, etc. So I won't be able to provide specifics in this guide for how to accomplish those things, but fortunately the CircleCI docs are adequate.

So we will start with a shell of a config, a sort of "hello world", if you will.

Add the following to the `config.yml` file you just created.

```yaml
version: 2
jobs:
  build:
    docker:
      - image: python:3.5
    working_directory: /code
    steps:
        - checkout
        - run:
            name: Hello world
            command: echo "Hello world"
```

First, the job will be run inside of a docker container. So in the `docker` section we are simply specifying the image that we want to use.

Next, we specify the working directory. For our purposes, this is just an arbitrary directory where the code will be checked out and tests are run.

Next, are the steps. Here is where we'll do all of the important work like building, testing, shipping, etc. But for our simple example, we're just going to checkout the code, and echo "Hello world".

So add this configuration and save the file.

**Note**: If you're application is built using docker, this can be confusing. You'll want to read up on the notion of a primary container and remote docker.

#### Build!

Now add your file, commit your code, and push.

```bash
git add .
git commit -m "added circle config"
git push origin <branch-name>
```

Head to the CircleCI dashboard, and click on **Builds**.

You should see your build added to the top of the list, and it should have a status of **Running**. Since we don't have many steps, this will probably build very quickly and the status should soon be changed to **Success**.

Click on the build to view details. Here you can see things like how long the build took, the steps that were run, and any resources that were used.
