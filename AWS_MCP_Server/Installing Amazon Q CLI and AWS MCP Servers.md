

# Installing Amazon Q CLI and AWS MCP Servers

## Overview

This document describes how to:

1. Install **Amazon Q CLI** on a Windows system using WSL
2. Set up the **AWS Model Context Protocol (MCP) Server**
3. Configure an AWS MCP Server (CloudFormation example) for use with Amazon Q

This setup enables Amazon Q to securely interact with AWS services via MCP-compliant servers.

---

## 1. Install Amazon Q CLI (via WSL on Windows)

Amazon Q CLI currently runs in Linux environments. On Windows, the recommended approach is to use **Windows Subsystem for Linux (WSL)**.

### Step 1: Install WSL

Open PowerShell as Administrator and run:

```bash
wsl --install
```

This installs WSL along with a default Linux distribution.

---

### Step 2: Launch Ubuntu in WSL

If Ubuntu is not started automatically:

```bash
wsl -d Ubuntu
```

---

### Step 3: Navigate to Home Directory

Once inside the WSL shell:

```bash
cd
```

---

### Step 4: Install Required Packages

Ensure required utilities are available:

```bash
sudo apt update
sudo apt install -y unzip curl
```

---

### Step 5: Download Amazon Q CLI Installer

Download the latest Amazon Q CLI Linux binary:

```bash
curl --proto '=https' --tlsv1.2 -sSf \
https://desktop-release.codewhisperer.us-east-1.amazonaws.com/latest/q-x86_64-linux-musl.zip \
-o q.zip
```

---

### Step 6: Extract the Installer

```bash
unzip q.zip
cd q
```

---

### Step 7: Install Amazon Q CLI

Make the installer executable and run it:

```bash
chmod +x install.sh
./install.sh
```

---

### Step 8: Reload Shell Environment

Restart the shell so the `q` command is available:

```bash
bash
```

---

### Step 9: Authenticate Amazon Q

Log in using your AWS identity:

```bash
q login
```

This opens a browser-based authentication flow.

---

### Step 10: Start Amazon Q Chat

Verify installation:

```bash
q chat
```

Amazon Q CLI is now ready.

---

## 2. Install AWS MCP Servers

AWS MCP Servers provide **tool-based access to AWS services** using the **Model Context Protocol**.

Official documentation:
[https://awslabs.github.io/mcp/](https://awslabs.github.io/mcp/)

![Image](https://d1.awsstatic.com/solutions/guidance/images/architecture-diagrams/deploying-model-context-protocol-servers-on-aws.ec117d85fbb24044baa453468c44216ad7133190.png)

![Image](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2025/05/23/ML-18605-mcp-architecture.png)

![Image](https://docs.aws.amazon.com/images/amazonq/latest/qdeveloper-ug/images/mcp-response-diagram.png)

---

## 3. Prerequisites for AWS MCP Servers

Before installing MCP servers, ensure:

* AWS CLI is installed and configured
* Valid IAM permissions are available
* An IAM Role or User is configured for MCP access

Example verification:

```bash
aws sts get-caller-identity
```

---

## 4. Install AWS CloudFormation MCP Server

The CloudFormation MCP Server enables Amazon Q to:

* Create
* Update
* Validate
* Inspect CloudFormation stacks

Documentation:
[https://awslabs.github.io/mcp/servers/cfn-mcp-server](https://awslabs.github.io/mcp/servers/cfn-mcp-server)

---

### Step 1: Install the CloudFormation MCP Server

Follow the instructions from the official MCP repository to install the server binary or package.

---

### Step 2: Configure MCP for Amazon Q

Amazon Q uses an MCP configuration file to discover available MCP servers.

Create or update the MCP configuration file (typically in your home directory):

```json
{
  "mcpServers": {
    "cloudformation": {
      "command": "cfn-mcp-server",
      "args": [],
      "env": {
        "AWS_REGION": "us-east-1"
      }
    }
  }
}
```

This configuration:

* Registers the CloudFormation MCP server
* Allows Amazon Q to invoke it as a tool
* Uses standard AWS IAM authentication

---

## 5. Validation

Restart Amazon Q CLI:

```bash
q chat
```

You should now be able to issue commands such as:

* “Create a CloudFormation stack”
* “Validate this template”
* “Explain the failure in my stack”

Amazon Q will route these requests through the MCP server securely.

---


