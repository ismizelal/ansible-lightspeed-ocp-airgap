# ansible-lightspeed-ocp-airgap
ocp installation in air gap env with ALS with IBM watsonx code assistant
OCP Air-Gapped Installation on Vmware using Ansible Lightspeed
Overview
Welcome to the OCP Air-Gapped Installation on any cloud environement using Ansible Lightspeed repository! The primary goal of this project is to experiment with ways that Ansible Lightspeed with IBM Watson Code Assistant could generate code that could be used to deploy an air-gapped installation of OpenShift Container Platform in any cloud environement

Purpose
The purpose of this repository is to develop a comprehensive data set aimed at assisting product management. To achieve this goal, we furnish a detailed, sequential handbook along with essential utilities for deploying OpenShift within a restricted network or air-gapped environment, leveraging Ansible Lightspeed. In instances where direct internet connectivity is unavailable, Ansible Lightspeed emerges as an indispensable tool. This high-speed and streamlined automation framework facilitate the smooth establishment and arrangement of intricate environments, including the likes of OpenShift.

Benefits
Deploying OpenShift in an air-gapped environment can be a challenging task, but with the powerful combination of Ansible Lightspeed, we can streamline the entire deployment process. The key benefits of using this approach include:

develop a comprehensive data set that could help WCA product management with training and fine-tuning
develop a demo that could be shown to clients
Efficiency Ansible Lightspeed dramatically reduces the time and effort required for deploying OpenShift, even in restricted networks.

Security By eliminating the need for direct internet access during installation, the air-gapped environment remains isolated and secure.

Simplicity The provided instructions and tools make the process straightforward, enabling even those less familiar with OpenShift and Ansible to succeed.

Airgap Installation Guide
This guide will lead you through the process of setting up an airgap installation of OpenShift in your restricted network environment using the Bastion machine, which is equipped with internet access for downloading images. Subsequently, we will implement firewall rules to restrict internet access, enabling efficient image mirroring within your constrained network. Additionally, you have the option to utilize both the Bastion and a Jump Box. The Bastion is responsible for installing the OpenShift cluster and has direct access to the restricted network where the cluster will operate, while the Jump Box acts as a bridge to the internet, allowing direct mirroring (downloading) of public registry software.

Getting Started
To get started with the installation process, follow the instructions and guidelines provided in the repository. You will find all the necessary roles, resources, scripts, and playbooks required for the air-gapped deployment.

Operating your cluster within a network with limited internet access is achievable by deploying the cluster using mirrored OpenShift Container Platform container images stored in a private registry. This registry should remain operational as long as the cluster is active.

Manual tasks
Users are required to perform the following tasks manually.

Add a disk to a virtual machine in VCenter and to resize a logical volume with five simple LVM commands.

Configure the firewall rules on the pfSense Router to block Internet Access.

How to Use this Repository
This repository is organized to make the deployment process as smooth as possible. Here's a brief overview of the contents:

README.md: Find detailed documentation and step-by-step guides on how to prepare your environment and execute the installation.

Ansible Playbooks: Explore the Ansible playbooks specially tailored for the air-gapped installation of OpenShift.

local-playbook.yml: sets up your MacBook Pro
bastion-playbook.yml: sets up the bastion host
cluster-playbook.yml: installs the cluster
install-config.yml: 
firewall-playbook.yml: configures the pfSense firewall for different connection modes
roles: This directory contains additional resources like configuration files, templates, and scripts needed for the deployment. It is used by all of the playbooks. Here is the current roles

add-disk-to-bastion
fulfill-bastion-prerequisites
install-ocp-disconnected-installation-tools
setup-mirror-registry
install-imageset
install-config.yaml
scrape-imageContentSources
build-openshift-cluster
vars: Refers to a file that contains variable definitions used within your playbooks and roles. Vars files are a way to separate data from your Ansible code, making it more modular and easier to manage.

ansible.cfg: This file allows you to customize Ansible's behavior and settings. Define the path where Ansible should look for roles, which are reusable collections of tasks and variables. Configure SSH-related options such as SSH private key file, SSH agent usage, and control connection parameters.

ssh.cfg: Configure SSH-related options such as SSH private key file, SSH agent usage, and control connection parameters.

.gitignore: It is a configuration file used to specify which files or directories should be ignored and not included in the version control system, such as Git. This is important to keep sensitive or unnecessary files out of the Git repository, ensuring that only the essential code and configuration files are tracked and shared among team members.

requirements.yml: Contains additional required Ansible Galaxy collections as well as instructions for how to install them.

secret.json: Create a JSON file (e.g., secret.json) to store your OpenShift Container Platform (OCP) pull secret as a single flattened line of jason and SSH public key securely. This will prevent you from embedding these sensitive details directly in your source code on GitHub.

For example: To securely store sensitive information like your OCP pull secret and SSH public key, follow these steps:

Create a secret.json file in the project directory.
Place your OCP pull secret and SSH public key inside the secret.json file.
Keep this file private and do not commit it to your version control system. See .gitignore to make sure your secrets are not stored in the repo
For Example secret.json format:

{
  "ocp_pull_secret": "your_ocp_pull_secret_here",
  "ssh_public_key": "your_ssh_public_key_here"
}
To pass the secrets via the command line, you can use the --extra-vars flag with your Ansible playbook. See the examples below:

ansible-playbook x.playbook.yml --extra-vars "@secret.json"

ansible-playbook -i inventory playbook.yml --extra-vars "@something-secrets.json"
