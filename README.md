# DevSecOps Project Documentation

This documentation provides an overview of the DevSecOps project, demonstrating the setup of a CI/CD pipeline integrated with security tools for building and deploying applications to Amazon EKS.

---

## AWS EC2 Instance Setup

An EC2 instance was configured in the AWS Console to host essential DevSecOps tools such as Jenkins and Nexus. The instance is a `t2.medium` configured as follows:
This instance forms the backbone of the CI/CD pipeline setup.

![AWS EC2 Instance Setup](images/1-aws-setup-instances.png)


## Jenkins Installation and Configuration

Jenkins, a key component for automation, was installed on the EC2 instance. To unlock Jenkins during the initial setup, an administrator password was retrieved from the server:
The image below shows the Jenkins unlock screen:

![Installing and Configuring Jenkins](images/2-install-jenkins.png)


## Nexus Repository Manager Setup

Nexus Repository Manager OSS was deployed to manage dependencies securely. It supports Maven and NuGet repositories, ensuring secure artifact storage and retrieval. The following dashboard highlights the configured repositories and system health checks:

![Configuring Nexus Repository Manager](images/3-configure-nexus.png)

## Terraform Initialization for EKS

Terraform was initialized using the `terraform init` command to prepare the environment for provisioning the EKS cluster. The process successfully downloaded all required provider plugins, such as HashiCorp AWS.

![Initializing Terraform for EKS Setup](images/4-terraform-init-EKS.png)

## Planning EKS Infrastructure with Terraform

The `terraform plan` command outlined the infrastructure setup, including the creation of a Virtual Private Cloud (VPC), subnets, and related resources essential for the EKS cluster.

![Planning EKS Deployment with Terraform](images/5-terraform-plan.png)

## EKS Cluster Provisioning Using Terraform

Terraform was used to configure the EKS cluster. The setup included defining node groups, scaling configurations, and network policies. This configuration ensures the Kubernetes cluster is ready for secure deployment.

![EKS Cluster Setup Using Terraform](images/6-eks-setup-with-terraform.png)


The `pom.xml` file was edited to include the Nexus repository URLs. This update enables Maven to securely fetch project dependencies from Nexus during builds.

![Editing the POM File for Dependency Management](images/8-edit-pom-xml.png)

## Setting Up Kubernetes RBAC

Role-Based Access Control (RBAC) was configured to manage secure access to Kubernetes resources. This setup ensures that permissions are granted only to authorized users and services.

![Setting Up Role-Based Access Control (RBAC)](images/8-setup-RBAC.png)

## Terraform Execution for EKS Deployment

The final infrastructure was provisioned using the `terraform apply` command. The process successfully created the VPC, subnets, and EKS node groups, completing the cluster setup.

![Terraform Execution for EKS](images/9-terraform-eks.png)

## Verifying EKS Cluster with kubectl

After provisioning, the EKS cluster was verified using the `kubectl get nodes` command. The output confirms that the nodes are up and running, ready for workload deployment.

![Verifying EKS Cluster with kubectl](images/10-kubectl-get-nodes-working.png)

---

## Creating a Service Account

A Kubernetes Service Account was created to enable secure communication between Jenkins and the EKS cluster. This ensures that the CI/CD pipeline can interact with Kubernetes resources securely.

![Creating a Service Account](images/11-create-a-service-account.png)

---

## Creating Roles and Role Bindings

Roles and Role Bindings were defined to provide fine-grained access control to Kubernetes resources. These configurations ensure that the CI/CD pipeline has the necessary permissions to manage deployments.

---

## Creating and Describing Kubernetes Token

A new Kubernetes token was created and its details were described using the `kubectl describe secret` command. This token will be used by Jenkins for cluster access.

![Creating Kubernetes Token](images/13-create-a-token.png)

![Describing Kubernetes Token](images/14-describe-token.png)

---

## Configuring Kubernetes Token in Jenkins

A Kubernetes token was generated and configured in Jenkins. This token allows Jenkins to authenticate with the EKS cluster securely, enabling it to execute deployment tasks.

![Configuring Kubernetes Token in Jenkins](images/13-configure-k8-token.png)

---



