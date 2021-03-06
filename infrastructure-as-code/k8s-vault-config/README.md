# Kubernetes Vault Authentication Configuration
Terraform configuration for configuring the Vault authentication method for a Kubernetes cluster.

## Introduction
This Terraform configuration configures the [Vault Kubernetes authentication method](https://www.vaultproject.io/docs/auth/kubernetes.html) for use with an existing Kubernetes cluster. It is meant to be used in Terraform Enterprise (TFE).

## Deployment Prerequisites

1. First deploy a Kubernetes cluster with Terraform Enterprise (TFE) by using one of these Terraform repositories and pointing a TFE workspace against it:
    - [tfe-k8s-cluster-aks](../../infrastructure-as-code/k8s-cluster-aks)
    - [tfe-k8s-cluster-gke](../../infrastructure-as-code/k8s-cluster-gke)
1. We assume that you have already satisfied all the prerequisites for deploying a Kubernetes cluster in AKS or GKE described by the above links. That includes setting up a Vault server.
1. We also assume that you have already forked this repository and cloned your fork to your laptop.
1. If you do not already have a Terraform Enterprise (TFE) account, request one from sales@hashicorp.com.
1. After getting access to your TFE account, create an organization in it. Click the Cancel button when prompted to create a new workspace.
1. Configure your TFE organization to connect to GitHub. See this [doc](https://www.terraform.io/docs/enterprise/vcs/github.html).

## Deployment Steps
Execute the following commands to deploy Vault authentication method to your Kubernetes cluster:

1. Create a new TFE workspace called k8s-vault-configuation.
1. Configure your workspace to connect to the fork of this repository in your own GitHub account.
1. Click the "More options" link, set the Terraform Working Directory to "infrastructure-as-code/k8s-vault-configuration".
1. On the Variables tab of your workspace, set the tfe_organization Terraform variable to the name of the TFE organization containing your Kubernetes cluster workspace.
1. On the Variables tab of your workspace, set the k8s_cluster_workspace Terraform variable to the name of the workspace you used to deploy your Kubernetes cluster.
1. Set the VAULT_TOKEN environment variable to your Vault token. Be sure to mark the VAULT_TOKEN variable as sensitive so that other people cannot read it.
1. Queue a plan for the k8s-vault-configuation workspace in TFE by clicking the "Queue Plan" button in the upper right corner of your workspace.
1. On the Latest Run tab, you should see a new run. If the plan succeeds, you can view the plan and verify that the Vault Kubernetes authentication method will be created when you apply your plan.
1. Click the "Confirm and Apply" button to actually deploy the authentication method.

## Cleanup
Execute the following steps to delete Vault Kubernetes authentication method from your Kubernetes cluster.

1. Define an environment variable CONFIRM_DESTROY with value 1 on the Variables tab of your k8s-vault-configuation workspace.
1. Queue a Destroy plan in TFE from the Settings tab of your k8s-vault-configuation workspace.
1. On the Latest Run tab of your k8s-vault-configuation workspace, make sure that the Plan was successful and then click the "Confirm and Apply" button to actually remove the cats-and-dogs pods and services.
