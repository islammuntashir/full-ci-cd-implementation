# cicd-pipeline-train-schedule-cd

This is a simple train schedule app written using nodejs. It is intended to be used as a sample application for a series of hands-on learning activities.

## Running the app

You need a Java JDK 7 or later to run the build. You can run the build like this:

    ./gradlew build

You can run the app with:

    ./gradlew npm_start
Once it is running, you can access it in a browser at [http://localhost:3000](http://localhost:3000)  

## Senario of CD

Your team is working on the schedule app. A Jenkins Pipeline has already been created for the app, but all it does right now is run a continuous integration build. The team has asked you to add automated deployments to a staging server, and to add a production server to the pipeline. The team has decided to use the master branch of the git repository to control deployments, so only changes to the master branch should be deployed. Whenever there is a change to the master branch, the Pipeline needs to do the following after the CI build is completed:

   1. Deploy the application to a Staging server.
   2. Wait for approval before deploying to Production.
   3. Once approval is provided, deploy to Production.

Begin by creating a fork of the source code at: https://github.com/islammuntashir/full-ci-cd-implementation

In order to complete this activity, you will need to:

  1. Deploy the app to the staging server via the Jenkins pipeline.
  2. Configure the staging and production servers for the Publish Over SSH plugin.
  3. Add a credential to Jenkins called webserver_login to allow Jenkins to authenticate with the web servers. The user has            already been created on the web servers with the username deploy and the password jenkins.
  4. Create a multibranch pipeline project called schedule and set it up to build from your GitHub fork.
  5. Create a stage in the Jenkinsfile to deploy the app to the staging server.
  6. Run the build to deploy to the staging server.
  7. Deploy the app to the production server via the Jenkins pipeline:
  8. Create a stage to deploy to production after awaiting user input.
  9. Run the build.
  10. Approve the deployment to production.
  
A few notes about the this server setup:

1. A systemd service called train-schedule has already been created on both web servers. The train-schedule app can be controlled with systemd using commands like systemctl stop train-schedule and systemctl start train-schedule.
2. The train-schedule service expects the application code to be deployed to /opt/train-schedule.
3. A deployment user has already been created on both web servers. It can write to /opt/train-schedule as well as start and stop the train-schedule service. The username is deploy and the password is jenkins. Jenkins can use these credentials in order to perform the deployment.
4. The Publish Over SSH plugin is already installed on the Jenkins server.
6. The Jenkins server listens on port 8080. Train Schedule, once it is deployed, will listen on port 3000.

