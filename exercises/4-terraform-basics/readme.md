# Terraform basics

In later exercises we will be using aws s3 as a state provider for our terraform

**NB.**

- If your github handle is longer than 19 characters, speak up as this might cause issues for task 2
- The aws sandbox account gets cleared down every Friday, re-running exercises after that will fail unless you run these 2 tasks again first

## Tasks

1. Set up a state bucket. Local terraform state for this bootstrap task is fine.
   - Clone this repo: https://github.com/tess-barnes-uk/terraform-s3-bootstrap
   - Follow the readme instructions to create an s3 bucket for your own statefiles, we will use these in later exercises.
2. Set up a github/aws link, This will allow your github repo to act on the aws sandbox account via pipelines, using the restricted permission role given.
   - In the `github_aws/` folder, update variables file with the values matching the comments
   - Validate, plan and apply the terraform in `github_aws/` to the sandbox account from your machine. The inner readme will help.

## Outputs

Keep a note of the following to use later:

- the state bucket name,
- the name of your key alias for your state bucket
- the role _arn_ that the github/aws link can assume.

## Notes

Add your thoughts and questions here

Created terraform.tfvars and changed the values of the variables
s3_bucket_name = "your-s3-bucket-name" ## Needs to be unique on the whole sandbox account!
aws_region = "your-aws-region" ## Get this from .aws/config
owner = "your-name" ## might need to be all lowecase?
kms_alias_name = "alias/your-memorable-name"

Initalised terraform:
aws-vault exec {profile-name} -- terraform init

Applied terraform configuration:
aws-vault exec {profile-name} -- terraform validate ## Checks syntax basically
aws-vault exec {profile-name} -- terraform plan ## Create terraform plan
What does terraform plan do?
Do we need to save the plan? Why?
aws-vault exec {profile-name} -- terraform apply -auto-approve ## Actually executes the plan?

How do terraform statefiles get added to the s3 bucket?

Ensure that your AWS credentials have the necessary permissions to create and manage S3 buckets
I assume I have permissions because I was able to create the bucket but I'm not sure where I could check if I didn't

What does terraform destroy do?
Destroys things associated with the terraform configuration in the currect pipeline
Got this error when trying to run: aws-vault exec {profile-name} -- terraform destroy
Resource module.s3.aws_s3_bucket.bootstrap_s3_bucket has lifecycle.prevent_destroy set, but the plan calls for this resource to be destroyed. To avoid this error and continue with the plan, either disable lifecycle.prevent_destroy or reduce the scope of the plan using the -target option.
Fix: manually destroy the bucket on the aws console and
in s3.tf change prevent_destroy = true to false then create the
bucket again

Set up a github/aws link
Updated vars.auto.tfvars.example, ran terraform init, terraform plan, terraform appy.
