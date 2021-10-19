# CodePipeline using Github as source

This SampleApp is hosted in the Github repo [sample-app-html](https://github.com/simorgh1/sample-app-html). The CodePipeline demo creates an Environment for hosting the SampleApp in EC2 and then the Pipeline which will deploy the application using CodeDeploy.

### Requirements

- Configured AWS CLI
- Ansible
- Github oauth token
- A KeyPair for accessing the EC2 instance
- KMS S3 Encryption key
- Email to be confirmed for receiving the alarm notifications

## Preparing the Pipeline

The Infrastructure for the Developemnt Environment and it's related deployment pipeline will be created using CloudFormation run by an ansible playbook, just fill the parameters and run the playbook.

- Ansible, Python >= 2.8, boto,boto3,botocore should be pre-installed.

=> [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu)
=> Install pip for python3

```bash
sudo apt-get install python3-pip -y
```

=> Install required python modules for running cloudformation

```bash
sudo pip install boto boto3 botocore
```

Ansible hosts (/etc/ansible/hosts) should have the default entry

```bash
[all]
localhost
```

## Deploying the infrastructure

Then go ahead and deploy the stacks:


```bash
> ansible-playbook site.yml
```

Check CloudFormation page in the aws console, 2 newly created stacks should be completed and the deployment should be already triggered. Once it is finished, go to the elastic loadbalancer and open its public dns, it should open the sample app page.

## Using SecretManager for storing the secrets

There are several keys and tokens which could be stored in the SecretManager instead of the ansible global variable and retrieved in the cloudformation template using a dynamic reference call.
