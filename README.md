# basic-ami-pipeline
Test AMI pipeline

## 1. Identify starting AMI (s-ami)

* Automatic lookup?
  - Pro: Convenient
  - Pro: Automatically up-to-date
  - Con: Increased chanced of manual intervention to fix issues with new OS releases
* Manual lookup?
  - Pro: Pipeline less likely to fail as time passes
  - Con: Falls out of date without manual intervenion depending on OS
  - Con: Inconvenient
* Potential solutions for automatic lookup
  - AWS CLI
  - Hashicorp Terraform

## 2. Launch and mod EC2 based on s-ami

* Credentials
  - Okta/STS
  - Instance role
  - Hardcoded
* Platform for launch and mod
  - AWS CodeBuild
  - Other CI (Travis, Azure Pipelines) - potential for timeout
* Tools for launch and mod
  - Hashicorp Terraform
  - AWS CloudFormation
* Modifications
  - Launch EC2 instance
  - Install patches
  - Install IT agents
  - Apply OS/disk/etc. configurations

## 3. Create modified AMI (m-ami)

* Stop EC2
* Create AMI
  - Hashicorp Packer
  - Hashicorp Terraform
  - AWS CLI

## 4. Test m-ami

* Provide basic testing only if time runs short
* Launch EC2 instance from m-ami
* Run tests on instance

## 5. Publish m-ami

* Extract info used in release (e.g., rpm list) to document
* Copy AMI to supported regions
* Share AMI to supported accounts
* Publish AMI release

## 6. Cleanup

* Ensure AWS resources used in pipelines are deleted
* CloudBuild, Terraform, Packer should handle
* Consider error cases where orphan resources might remain
