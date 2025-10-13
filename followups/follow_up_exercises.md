# Follow up Exercises

## Tasks

1. Explain how code on your delivery is packaged and deployed.
2. Explain what you understand of the approach to hosting apps in the course.
3. How does this differ from approaches you've used before? What's the impact of changing our mind? and the benefits?
4. Explain the troubleshooting steps you would use on a failing pipeline, either those you learned on this course or those you have used on your delivery.
5. Identify a problem or improvement you could do on a pipeline on your delivery. What did your team decide to do to fix or improve it (even if it hasn't been prioritised yet)?

## Stretch task

1. Terraform resources to build docker images and push them to ECR is not the only way, it's not even the most usual way using github actions! Try out a new pipeline with different github actions to build and deploy the ex 6 image to the ex 6 ECR. You could start from your ex 3 pipeline syntax to build and test the node code first.
2. If you identified a different approach to hosting apps containers, investigate more and explain your discovered new approach including, what are the pros and cons of adopting it, if our start point is where the course examples left off?

## Add your answers here, or in this folder

1. Bichard is an old, large, and complex project. For testing and continuous integration we use CircleCI. Similarly to Github actions a workflow is created in a config.yml file, and multiple reusable jobs are defined to test different parts of the code. These tests will run on push to the branch and the results can be viewed in the CircleCI console in the browser.
   For deployment, the code is containerised using Docker, and deployed using AWS CodePipeline and CodeBuild. Tests are ran again in different environments and if they all pass they need to go through a manual check gate to be deployed to production.

2. We learned about CI/CD (continuous integration, continuous deployment) and its benefits and how our app can go from code in our IDE to being used by people.
   With CI we can make sure that our code is compatible with the existing codebase and code written by other members of the team, automatically tested, and any errors are detected quickly. The way I understand it, CI is asking the questions "Is the code safe to merge?". By the end of CI we have code that should work, but is not in the hands of the user yet.
   Continuous deployment allows us to deploy code automatically with minimal human interaction (manual approval gates) and makes the process faster. The goal of CD is to get our working code out in the world.
   Containerisation allows us to package our app with all of its dependencies provided with instructions on how to set things up. This means that our process will be more reliable and it won't depend on the local environment.
   AWS is a platform that has a collection of useful resources for hosting apps such ECR (Elastic Container Registry) to store container images, VPCs (Virtual Private Clouds), and S3 buckets, and acts as a server where our app can exist after going through the CI/CD pipeline. This is great because we don't have to have a physical server to host our app and worry about its maintenance.
