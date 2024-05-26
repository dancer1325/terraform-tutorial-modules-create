# Learn Terraform Modules Create
This repo is a companion repo to the [Build a Module tutorial](https://developer.hashicorp.com/terraform/tutorials/modules/module-create).

## Goal
* Terraform modules
  * are
  * how to create submodule / uses S3 bucket resource

## Prerequisites
* Terraform [v1.2+](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) installed locally
* AWS account with [associated credentials](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#authentication-and-configuration)
  * via
    * add in the 'provider' block
    * environment variables
      * 'AWS_ACCESS_KEY_ID'
      * 'AWS_SECRET_ACCESS_KEY'
      * 'AWS_REGION'
    * credential files
      * `aws config` & pass the 'AWS_ACCESS_KEY_ID' & 'AWS_SECRET_ACCESS_KEY'

## How to run?
* `terraform init`
* `terraform get`
  * If you make some adjustment in submodules or consumed modules
* `terraform apply`
  * Problems:
    * Problem1: 'Bucket (robin-test-dec-17-2019): BucketAlreadyExists'
      * Solution: Adjust name by unique
* `aws s3 cp modules/aws-s3-static-website-bucket/www/ s3://$(terraform output -raw website_bucket_name)/ --recursive`
  * upload the content in 'modules/aws-s3-static-website-bucket/www/' to the recently S3 bucket created
* Open in your desired browser 'https://robin-test-may-26-2024.s3-us-west-2.amazonaws.com/' and check the static resources accessibles
  * 'https://robin-test-may-26-2024.s3-us-west-2.amazonaws.com/index.html'
  * 'https://robin-test-may-26-2024.s3-us-west-2.amazonaws.com/error.html'
* Clean up all the infrastructure
  * `aws s3 rm s3://$(terraform output -raw website_bucket_name)/ --recursive`
    * remove all the content within S3 bucket
  * `terraform destroy`

## Notes
* Structure
  * '/modules'
    * submodule of the root module
    * if you want to use it -> in the `module.source` refers to relative path