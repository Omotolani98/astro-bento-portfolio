---
layout: ../../layouts/LayoutBlogPost.astro
title: "Building a Multi-Cloud CLI Tool: The Journey of CloudCrafter"
description: "A simple"
pubDate: 2025-1-7
category: "tutorial"
---

# **CloudCrafter: Simplifying Multi-Cloud Resource Management**

## **Introduction**
Managing resources across multiple cloud platforms can be challenging, especially when dealing with diverse interfaces, APIs, and tools. Enter **CloudCrafter**, a CLI tool designed to simplify the provisioning and management of cloud resources. Available on macOS, Windows, and Linux, CloudCrafter empowers developers and DevOps engineers to work seamlessly across AWS, Azure, and GCP (starting with AWS support).

The name **CloudCrafter** was inspired by Minecraft, a game known for building and creativity, aligning perfectly with the tool's purpose of "crafting" cloud infrastructure. Built with **Golang** for its performance and concurrency capabilities, CloudCrafter is automated through a CI/CD pipeline using **GitHub Actions**. It is also easily installable via **Homebrew** for macOS users.

---

## **Getting Started**

### **Prerequisites**
To use CloudCrafter, you’ll need the following CLI tools installed on your system:
- **AWS CLI**, **Azure CLI**, or **GCP CLI** (currently, only AWS is supported).
- Valid cloud credentials configured for the respective CLI tool.

### **Installation**
For macOS, installation is straightforward with Homebrew:
```bash
brew tap Omotolani98/cloudcrafter
brew install cloudcrafter
```

### **Verify Installation**
Once installed, verify it using:
```bash
cloudcrafter -h
```
This will display the available commands and flags, confirming that CloudCrafter is ready to use.

---

## **Provisioning Resources**

CloudCrafter supports a straightforward workflow for provisioning resources. The first step involves generating a YAML configuration file, which serves as the blueprint for resource creation.

### **Step 1: Generate a YAML Configuration File**
Use the following command to generate a configuration file interactively:
```bash
cloudcrafter generate-yaml -o ~/path/to/config.yaml
```

#### **Command Breakdown**
- `generate-yaml`: Command to generate the configuration file.
- `-o`: Specifies the output path for the generated YAML file.

### **Step 2: YAML Configuration**
A sample YAML file might look like this:
```yaml
provider: aws
resources:
  - vm:
      type: vm
      properties:
        image: ami-123456
        keyName: MacBook Air
        machineType: t2.micro
        name: my-new-server
        region: us-east-1
        securityGroups: sg-123456, sg-654321
        subnet: subnet-123456
  - storage:
      type: storage
      properties:
        bucketName: my-new-bucket
```

#### **Understanding the YAML**
1. **Provider**: Specifies the cloud provider (`aws`, `azure`, or `gcp`). Currently, only AWS is supported.
2. **Resources**: A list of resources to be provisioned, each with:
   - **Type**: Defines the resource type, e.g., `vm` (virtual machine) or `storage`.
   - **Properties**: Configuration details for the resource, such as region, instance type, or bucket name.

### **Step 3: Provision Resources**
Once the YAML file is ready, use the following command to provision resources:
```bash
cloudcrafter provision -f ~/path/to/config.yaml
```
This will parse the YAML file and create the specified resources.

---

## **Managing Resources**

CloudCrafter also provides commands to manage existing resources.

### **List Resources**
To list resources for a specific provider and type:
```bash
cloudcrafter list -p aws -r vm
```

#### **Command Breakdown**
- `list`: Command to list resources.
- `-p`: Specifies the provider (`aws`, `azure`, or `gcp`).
- `-r`: Specifies the resource type (e.g., `vm` or `storage`).

### **Delete Resources**
To delete a specific resource:
```bash
cloudcrafter delete -p aws -r vm -i <resource-id>
```

#### **Command Breakdown**
- `delete`: Command to delete resources.
- `-p`: Specifies the provider.
- `-r`: Specifies the resource type.
- `-i`: Specifies id to be updated e.g. i-136df67gy89h, my-new-bucket

---

## **Conclusion**

Building CloudCrafter has been an incredible learning experience. From diving deep into cloud SDKs to implementing robust CLI features, every step was a journey in crafting a tool that simplifies multi-cloud management.

While AWS is the only supported platform at the moment, plans are already underway to integrate Azure and GCP. With its extensibility and ease of use, CloudCrafter aims to be the go-to CLI for DevOps engineers and developers.

If you’re looking for a streamlined way to manage your cloud resources, give CloudCrafter a try. Your feedback and contributions are always welcome! 🚀