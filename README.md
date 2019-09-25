# cicd-pipeline-train-schedule-cd

This is a simple train schedule app written using nodejs. It is intended to be used as a sample application for a series of hands-on learning activities.

## Running the app

You need a Java JDK 7 or later to run the build. You can run the build like this:

    ./gradlew build

You can run the app with:

    ./gradlew npm_start

Once it is running, you can access it in a browser at [http://localhost:3000](http://localhost:3000)

## One Example CI requrement
say team has asked you to configure a Jenkins project to build the this app. The source code for the application is hosted in the GitHub repository at https://github.com/islammuntashir/full-ci-cd-implementation. The app already has build automation set up using gradle wrapper, and can be built with ./gradlew build. The team wants Jenkins to execute this automated build every time changes are pushed to the GitHub repo.

You will need to:

   1. Configure Jenkins to authenticate with GitHub
   2. Create a freestyle project in Jenkins
   3. Configure the project to build the train schedule app
   4. Set up a webhook to trigger the build whenever changes are made to the repo in GitHub
   5. Configure the build to archive theSchedule.zip as a build artifact

## Solution
1. First generate github API key on Github with  admin:repo_hook cheked
2. Go to Manage jenkins > Configuration then to Gihub section and Select Github server. On credential option provide ID and secret with secrete text option, provide api key and add cridential. 
3. Checked manage hooks then test your connection and then save 
4. go to your fork of github and copy the project link
5. Create job on jenkins with free style project
6. Provide Github url to github project
7. Select git in sourcecode management and provide Repository URL. Donot need to provide Credential. As already you given it globally
8. Checkout GitHub hook trigger for GITScm polling
9. Add build steps and select invoked gradle script and then select gradle wrapper and give task name "build" as primary build is Build. then set post build action to archive Artifactto dist/schedule.zip.
