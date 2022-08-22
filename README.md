# Deploying a Web Server in Azure: Udacity DevOps Project 1

# Azure Infrastructure Operations Project: Deploying a scalable IaaS web server in Azure

### Introduction
For this project, you will write a Packer template and a Terraform template to deploy a customizable, scalable web server in Azure.

### Getting Started
1. Clone the starter repository

2. Create your infrastructure as code


### Dependencies
1. Create an [Azure Account](https://portal.azure.com) 
2. Install the [Azure command line interface](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
3. Install [Packer](https://www.packer.io/downloads)
4. Install [Terraform](https://www.terraform.io/downloads.html)

### Instructions
To clone the starter repository, a public ssh key needs to be generated for remote authentication to GitHub, via the CLI comnand

````
ssh-keygen -t rsa
````
![image](https://user-images.githubusercontent.com/28298236/185976602-ab944906-2b2b-455a-b01b-a0d39e760a6a.png)

The above command generates the public key which is recovered via:

````
cat /home/odl_user/.ssh/id_rsa.pub
````
![image](https://user-images.githubusercontent.com/28298236/185976911-ec54aa80-c6ef-446e-b43a-c01fde7f14ac.png)

This is copied and pasted [here](https://github.com/settings/keys), select "New SSH key", give it a suitable title e.g "SSH-key-for-Udacity-Access-Lab". Validate it.

Thence, the git clone command will run, unhindered.


```
git clone git@github.com:Benjamin-Ogunsade/Project-1.git
````
![image](https://user-images.githubusercontent.com/28298236/185977312-93211a93-712d-4f06-9cd1-a7315e2d8f38.png)

With the remote repository cloned to the Azure CLI local machine, one could modify files remotely.


### Step 1: Create a policy that denies the creation of the index resources which don't have tags.

This policy definition was implemented with this [model](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F871b6d14-10aa-478d-b590-94f262ecfa99). 

The aim is to ensure that all indexed resourcs in my subscription have tags and deny deployment if they do not.

Firstly, you are admonished to place the policy definition myPolicy.json in the home directory. This file uniquely contains the Policy Rule while every other parameters were parsed into the policy definition and assignment commands via option flags.

Do endeavour to be in the right directory on your CLI for the commands to run correctly. Here are a few lines of AzureCLI Powershell scripts to get the policy up and runnnig:

Next, a policy definition CLI variable is declared

````
$definition = New-AzPolicyDefinition -Name 'tagging-policy' -DisplayName 'Require a tag on resources' -Description 'Enforces existence of a tag only on resources, but not applied to resource groups.' -Policy './myPolicy.json' -Mode 'Indexed' -Metadata '{"version":"1.0.1","category":"Tags"}' -Parameter '{"tagName":{"type":"String","metadata":{"displayName":"environment","description":"environment"}}}'
````

Then, a policy assignment variable is also created. This variable takes the aforementioned policy definition variable as one of its flag options parameter

````
$assignment = New-AzPolicyAssignment -Name 'tagging-policy' -PolicyDefinition $definition
````

Next, the new policy definition' assignment is being applied:

````
echo $assignment
````

The screenshoot of the newly applied policy assignment is given below:


### Step X: Instruction to run the Packer template

### Step X: Customizing the vars.tf file for us


### Step X: Instruction to run the Terraform template
### Deploying the infrastructure

Screenshot for Terraform Apply


### Output
**Your words here**
