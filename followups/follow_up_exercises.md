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

3. Previously I did most things manually. Ran the tests locally before pushing, then solved merge conflicts manually. Created an EC2 instance manually and SSHd into it. Cloned the repo manually, then built and ran the docker image manually. This method was inconsistent, slow, frustrating, and full of errors.
   Changing from the mannual approach to using CI/CD pipelines was challenging, it requires new theroretical understanding and technical skills to use CI/CD tools like Github Actions, Terraform and AWS tools. We also need to adapt a new mindset to trust and rely on automation instead of doing things manually. However adapting CI/CD will make the process faster, more consistent, and more reliable. Automation reduces human error, and will allow developers to use their time more effectively developing new features instead of repeating time-consumign manual tasks.

4. When a pipeline fails the first things I would do is identify which job failed at which step by looking at the workflow flowchart, and reading the error logs. The error logs can be hit-or-miss, sometimes they clearly indicate what the problem is, for example there might be a typo in a variable in the terraform file, which has already happened to me. Other times they are harder to read, but they still provide contextual information, like if there was a problem with authorisation. Then I can look up the error code or the description online and check the documentation or websites like stack overflow. If the pipeline was working before, I would check if there are any changes in the code and see if restoring it to a previous version solves the issue. I would also have a look at the workflow file which can be found for each task on github. I find it helpful to have a second pair of eyes, so I would ask someone to pair with me on debugging the issue.
