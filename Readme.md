# Setting up the CodePipeline

### Requirements

- Configured AWS CLI
- CodeCommit Credentials and access for your account
- EC2 Role for CodeDeploy with Policy AmazonEC2RoleforAWSCodeDeploy.
- Service Role for CodePipeline
- CodeDeploy Role with policy AWSCodeDeployRole
- A Key Pair for accessing the EC2 instance

## Creating and using the CodeCommit Repository

- Clone the Repo to your local folder

```bash
> git clone https://github.com/simorgh1/aws-cf-templates/codestar-sampleapp.git .
```

- Then run the create repository task in the app-deploy folder

```bash
> aws cloudformation deploy --template-file .\create_repository.json --stack-name repo --parameter-overrides RepoName=MyDemoRepo
```

- Then connect your local repo with the newly created CodeCommit repository, and push sample code.

```bash
> git remote add origin https://git-codecommit.us-east-1.amazonaws.com/v1/repos/MyDemoRepo
> git push -u origin master
```

## Preparing the Development and Deployment Environment

The Infrastructure for the Developemnt Environment and it related deployment pipeline will be created using CloudFormation run by an ansible playbook, just fill the parameters and run the playbook.

- Ansible, Python >= 2.8, boto,boto3,botocore should be pre-installed.

```bash
> ansible-playbook site.yml
```

Check CloudFormation page in the aws console, 2 newly created stacks should be completed and the deployment should be already triggered. Once it is finished, go to your EC2 instance and open its public IP, it should show the sample app page.