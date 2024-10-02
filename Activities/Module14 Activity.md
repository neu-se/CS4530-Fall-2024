---
layout: page
title: Continuous Deployment Pipeline for FakeStackOverFlow
permalink: /activities/continuous-deployment
nav_exclude: true
---
# Activity 14: Continuous Deployment Pipeline for FakeStackOverFlow

In this activity, you will configure a continuous deployment pipeline using MongoDB Atlas and Render.com. Our pipeline will use Render.com to deploy the application, and the MongoDB database will be deployed on the cloud using MongoDB Atlas.

Only one member of each team needs to do these steps - the resulting deployment will be shared by the whole team. But if you would like, you can sit as a team and deploy the application together.

{: .note } We will be concentrating on building a continuous deployment pipeline in this activity, but what about continuous integration? There are a lot of ways to integrate continuous integration into your projects. One such example is automatically running tests after pushing a commit using GitHub Actions. FakeStackOverFlow has this continuous integration, and you can find the workflow in `.github/workflows/main.yml`.

## Pre-Requisites

There are three pre-requisites for this activity.

### GitHub Repository

Your team's deployment must take place within a private GitHub repository in our GitHub Classroom. To create your repository, each member of your team should follow these instructions:

1. Sign in to GitHub.com, and then use our invitation [ADD LINK] to create a repository with the covey.town codebase. Check to see if one of your groupmates has created a group already - if so, select it to join it. Otherwise, create a repo using the following format fall24-team-project-group-xyy where you should enter your group number (e.g. "Group-XYY") as the team name where X is your section number and YY is your group number.

2. Check your email for the invitation to join the repo. After that, refresh the page, and it will show a link to your new repository, for example: https://github.com/neu-cs4530/fall24-team-project-group-xyy. Click the link to navigate to your new repository. This is the repository you will use for the project.

This repository will be private, and visible only to your team and the course staff. After the semester ends, you are welcome to make it public - you have complete administrative control of the repository.

If you run into the error "refusing to allow an OAuth App to create or update workflow" when trying to push to GitHub, the fix is to update your saved authentication credentials for GitHub. For instance, you can follow [these instructions](https://docs.github.com/en/github/using-git/updating-credentials-from-the-macos-keychain) to update your credentials in the MacOS Keychain. If all else fails, you can connect to GitHub with [SSH instead of HTTPS](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh), which will also solve this problem. This error seems to only occur when pushing a change to the GitHub Actions configuration file, so you could also side-step the problem by having a team mate push this change to GitHub instead (who may not run into this issue).

### MongoDB Account

MongoDB Atlas is a cloud-based service that provides fully managed MongoDB databases. It allows you to easily deploy, manage, and scale MongoDB clusters without needing to handle server infrastructure, security, backups, or updates, making database management simpler and more efficient.

To use MongoDB Atlas, create a MongoDB account [here](https://account.mongodb.com/account/register).

After you register you will be asked to verify your email. The steps on how to create a MongoDB database and configure are provided below.

### Render.com Account

Render.com is a cloud platform that simplifies deploying and hosting web applications, APIs, and databases. It automatically manages servers, scaling, and security, allowing developers to easily build, deploy, and run applications without worrying about infrastructure management.

You can create a Render.com account [here]([https://](https://dashboard.render.com/register)). Clicking on the "GitHub" button and sign up using the **same GitHub account** as the one used to create the GitHub project repository.

After you register you will be asked to verify your email.

## Steps

You will first create the MongoDB database, and then setup the continuous deployment pipeline for the server and the client.

### Setup your MongoDB Database

1. Navigate to your [MongoDB Account Profile](https://account.mongodb.com/account/profile/overview).
2. Click on the "Visit MongoDB Atlas" button.
3. Click on the "Create" button on the center of the screen. (If you don't see a "Create" button, make sure you in the "Overview" section on the left navigation and on the "Data Services" tab)
4. In the configuration options:
   1. Choose the "M0" free tier.
   2. For the Name, provide a name such as "db-cs4530-f24-XYY" (where XYY is your group number).
   3. Keep the Provider and Region the default values.
5. Click on "Create Deployment".
6. You will be prompted about connecting to your database. 
   1. Copy the username and password that is automatically generated. You will need this later.
   2. Click on "Create Database User".
   3. Click the "Close" button.
7. Wait for your database cluster to complete creation. Once complete, click on the "Network Access" option in the left navigation.
8. Your current public IP address will be automatically present. Click the "EDIT" button, and then click "ALLOW ACCESS FROM ANYWHERE". Click the "Confirm" button.
9. Click on the "Database" option in the left navigation. Then, click on the "Connect" button.
   1.  Click on "Choose a connection method".
   2.  Click on "Compass".
   3.  If you don't have Compass installed, follow the instructions to install MongoDB Compass and then connect.
   4.  Otherwise, switch to the "I have MongoDB Compass installed" tab and connect.
10. After you have connected to the database on MongoDB Compass, check what collections are created by default.
11. Go to your project repository's server folder and run the `populate_db.ts` script.
```
cd server

npx ts-node populate_db.ts mongodb+srv://<username>:<password>@db-cs4530-f24-xxx.xxxxx.mongodb.net/
```
Make sure you replace the username, password, and xxx values in the connection string. You can find the connection string in the instructions from step 9.


{: .note } For the sake of simplicity and because you are not dealing with sensitive data, the Network Access was set to accept access from anywhere. But when working on other projects with sensitive data you should allow access to only a required scope of IP addresses.


You can connect your locally deployed server to the cloud hosted MongoDB database. This can be useful when you are developing a feature and want to test it out before deploying it. To do this, add an environmental variable with the connection string before starting your server.
```
export MONGODB_URI="<connection string>"
```
Note that if you do not save the env. variable in a ~/.bashrc file or something similar, it will removed every time you close your terminal.

### Setup your Client



