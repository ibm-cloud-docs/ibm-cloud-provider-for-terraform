---

copyright:
  years: 2026
lastupdated: "2026-03-25"

keywords: Secure AI infrastructure, Terraform IBM Modules, TIM Modules, terraform-ibm-modules, Code Engine, COS, KMS, IaC, Infrastructure as Code, watsonx, AI

subcollection: ibm-cloud-provider-for-terraform

---

{{site.data.keyword.attribute-definition-list}}

# Build secure infrastructure with Terraform IBM Modules for AI Applications
{: #secure-ai-infrastructure}
{: toc-content-type="tutorial"}
{: toc-services="terraform, terraform-ibm-modules, Code Engine, COS, KMS, Watsonx.ai"}
{: toc-completion-time="1h"}

This guide demonstrates how to compose and integrate reusable Terraform modules to build a secure, scalable **Infrastructure as Code** solution on IBM Cloud for AI applications. Learn how to provision infrastructure for the Loan Risk AI Agents application while applying IaC best practices for automation, compliance, and observability.
{: shortdesc}

![Architectural diagram](images/IaC_diag.svg)
{: figure caption="Infrastructure as Code architecture composed of integrated IBM Cloud Terraform modules supporting the Loan Risk AI Agents application."}

## Overview
{: #secure-ai-infrastructure-overview}

This solution demonstrates **composing modular Terraform components**, where each component encapsulates a distinct IBM Cloud service. These modules are integrated through well-defined inputs and outputs to form a complete, secure, and repeatable **Infrastructure as Code deployment pattern**.

The example application simulates a bank loan processing workflow where AI agents evaluate risk and determine interest rates. The source code is available [here](https://github.com/terraform-ibm-modules/sample-iac-solutions/tree/main/secure-infra-ai-app/ai-app-for-loan-risk).
{: note}

### Architecture components
{: #architecture-components}

The deployment architecture uses these core components:

- **Application**: Built using LangGraph and TypeScript/Node.js
- **Compute**: IBM Cloud Code Engine - serverless platform for containerized workloads
- **AI Services**: watsonx.ai - foundation models for natural language processing
- **Storage**: Cloud Object Storage (COS) - unstructured data storage
- **Security**: Key Protect for encryption

### Infrastructure modules
{: #infrastructure-modules}

This solution integrates the following Terraform IBM Modules (TIM):

Module | Purpose
--- | ---
[**Resource Group**](https://github.com/terraform-ibm-modules/terraform-ibm-resource-group) | Logical container for organizing IBM Cloud resources
[**Code Engine Project**](https://github.com/terraform-ibm-modules/terraform-ibm-code-engine/tree/main/modules/project) | Serverless container platform for hosting the application
[**Code Engine Secret**](https://github.com/terraform-ibm-modules/terraform-ibm-code-engine/tree/main/modules/secret) | Secure storage for container registry credentials
[**Container Registry Namespace**](https://github.com/terraform-ibm-modules/terraform-ibm-container-registry) | Organization for container images
[**Code Engine Build**](https://github.com/terraform-ibm-modules/terraform-ibm-code-engine/tree/main/modules/build) | Automated container image builds from source code
[**Key Protect**](https://github.com/terraform-ibm-modules/terraform-ibm-kms-all-inclusive) | Customer-managed encryption keys for data security
[**Cloud Object Storage**](https://github.com/terraform-ibm-modules/terraform-ibm-cos) | Encrypted object storage for AI project data
[**watsonx.ai Project**](https://github.com/terraform-ibm-modules/terraform-ibm-watsonx-ai) | AI workload management with integrated storage
[**Code Engine Application**](https://github.com/terraform-ibm-modules/terraform-ibm-code-engine/tree/main/modules/app) | Scalable deployment of the containerized application

## Deploy the AI application
{: #deploy-ai-application}

For deploying this infrastructure, you can find a complete step-by-step tutorial [here](https://github.com/terraform-ibm-modules/sample-iac-solutions/tree/main/secure-infra-ai-app/README.md).

This tutorial walks you through:

1. Cloning the pre-configured Terraform project
2. Reviewing provider and variable configurations
3. Understanding each infrastructure component
4. Deploying the complete solution
5. Verifying and exploring your deployment

This tutorial includes all necessary Terraform configuration files and detailed explanations of each component.
{: note}

### Modular composition
{: #modular-composition}

This solution demonstrates how to compose multiple Terraform modules into a cohesive infrastructure deployment. Each module:
- Covers a specific IBM Cloud service
- Exposes well-defined inputs and outputs
- Can be reused across different projects
- Maintains clear dependencies with other modules

### Security best practices
{: #security-best-practices}

The architecture implements security best practices:
- **Customer-managed encryption** using Key Protect for data at rest
- **Secure credential management** through Code Engine secrets
- **Private container registry** access with IAM authentication
- **Resource isolation** through dedicated resource groups

## Next steps
{: #secure-ai-next-steps}

- Follow the [complete tutorial](https://github.com/terraform-ibm-modules/sample-iac-solutions/tree/main/secure-infra-ai-app/README.md) to deploy the solution.
- Learn more about [Terraform IBM Modules structure](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-understand-tim-structure).
- Explore [deploying TIM modules](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-deploy-tim-module).
