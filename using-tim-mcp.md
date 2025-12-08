---

copyright:
  years: 2024, 2025
lastupdated: "2025-12-08"

keywords: terraform mcp, ai assistant, claude, ibm bob, model context protocol, terraform modules, infrastructure as code

subcollection: ibm-cloud-provider-for-terraform

content-type: tutorial
completion-time: 30min

---

{{site.data.keyword.attribute-definition-list}}

# Using TIM-MCP with AI assistants

{: #using-tim-mcp}
{: toc-content-type="tutorial"}
{: toc-completion-time="30min"}

Learn how to set up and use the Terraform IBM Modules MCP Server (TIM-MCP) with AI assistants to accelerate IBM Cloud infrastructure development with best practices and validated module patterns.
{: shortdesc}

Always review AI-generated infrastructure code with skilled practitioners before deploying to any environment.
{: important}

## What is TIM-MCP?

{: #tim-mcp-what-is}

The [Terraform IBM Modules MCP Server (TIM-MCP)](https://github.com/terraform-ibm-modules/tim-mcp){: external} implements the [Model Context Protocol (MCP)](https://modelcontextprotocol.io){: external} to connect AI assistants with the Terraform IBM Modules ecosystem. This integration enables AI models to:

- Search and discover relevant IBM Cloud Terraform modules
- Access accurate module documentation, inputs, and outputs
- Retrieve implementation examples and best practices
- Generate infrastructure code following IBM Cloud standards

### Why use TIM-MCP?

{: #tim-mcp-benefits}

TIM-MCP enhances AI-assisted infrastructure development by:

**Steering toward best practices**
:   Without TIM-MCP, AI models might generate generic or outdated Terraform code. TIM-MCP guides models toward IBM-validated patterns and current best practices.

**Providing contextual guardrails**
:   TIM-MCP helps AI models navigate the complex IBM Cloud ecosystem with structured access to module interfaces, dependencies, and implementation patterns.

**Ensuring accuracy**
:   Foundation models may have limited or outdated knowledge of IBM Cloud modules. TIM-MCP provides real-time access to module details, ensuring accurate parameter usage and proper versioning.

**Unlocking distributed knowledge**
:   By connecting models to documentation across many repositories, TIM-MCP helps AI leverage the collective expertise embedded in the Terraform IBM Modules ecosystem.

## Before you begin

{: #tim-mcp-prereqs}

Before you can use TIM-MCP, you need:

1. **An MCP-compatible AI assistant**
   - [IBM Project Bob](https://www.ibm.com/products/bob){: external}
   - [Claude Desktop](https://claude.ai/download){: external}
   - [VS Code](https://code.visualstudio.com/){: external} with MCP extension
   - [Cursor IDE](https://cursor.sh/){: external}
   - [Claude Code](https://docs.anthropic.com/en/docs/build-with-claude/claude-code){: external}

2. **uv package manager**

   Install uv to run the MCP server:

   **macOS/Linux:**

   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

   {: pre}

   **Windows:**

   ```powershell
   winget install --id=astral-sh.uv -e
   ```

   {: pre}

   Verify installation:

   ```bash
   uv --version
   ```

   {: pre}

3. **GitHub Personal Access Token (optional but recommended)**

   A GitHub token helps avoid API rate limits:
   - Without token: 60 requests/hour
   - With token: 5,000 requests/hour

   To create a token:
   1. Go to [GitHub Settings → Developer settings → Personal access tokens → Fine-grained tokens](https://github.com/settings/tokens?type=beta){: external}
   2. Click **Generate new token**
   3. Configure the token:
      - **Repository access:** Public repositories only
      - **Permissions:** No private access scopes needed
      - **Expiration:** Set to 90 days or longer
   4. Copy and save the token securely

## Installing TIM-MCP for IBM Project Bob

{: #tim-mcp-ibm-bob}
{: step}

IBM Project Bob supports MCP servers through the IBM Project Bob Marketplace or manual configuration files.

### Installing from IBM Project Bob Marketplace

{: #tim-mcp-bob-marketplace}

1. **Open IBM Project Bob Marketplace**:
   - Click the marketplace icon in the Bob pane
   - Navigate to the **MCP** tab

2. **Find and install TIM-MCP**:
   - Search for "Terraform IBM Modules (TIM)"
   - Click **Install** on the TIM-MCP server card

3. **Choose installation method**:
   - **Installation Scope**: Select Project (current workspace) or Global (all workspaces)
   - **Installation Method**: Choose UVX or UVX (Pinned Version)
   - **Version**:
     - For latest version: Leave as "latest"
     - For pinned version (recommended for production): Enter specific version (e.g., "v1.0.0")

4. **Configure GitHub token (optional but recommended)**:
   - In the **GitHub Token** field, enter your GitHub personal access token
   - This helps avoid API rate limits (60 requests/hour without token, 5,000 with token)

5. **Complete installation**:
   - Click **Install**
   - The server will be automatically configured with your settings

### Manual configuration

{: #tim-mcp-bob-manual}

If you prefer manual configuration or need project-specific settings:

**Project-level configuration:**

1. Create `.bob/mcp.json` in your project directory:

   ```bash
   mkdir -p .bob
   ```

   {: pre}

2. Add the configuration:

   ```json
   {
     "mcpServers": {
       "tim-mcp": {
         "command": "uvx",
         "args": [
           "--from",
           "git+https://github.com/terraform-ibm-modules/tim-mcp.git",
           "tim-mcp"
         ],
         "env": {
           "GITHUB_TOKEN": "your_github_token_here"
         }
       }
     }
   }
   ```

   {: codeblock}

**Global configuration:**

1. Open Bob settings in IBM Project Bob IDE
2. Click the ⚙️ icon in the top navigation of the Bob pane
3. Scroll to the bottom of the MCP settings view
4. Click **Edit Global MCP** to open `mcp_settings.json`
5. Add the TIM-MCP configuration using the same JSON format as above

## Installing TIM-MCP for Claude Desktop

{: #tim-mcp-claude-desktop}
{: step}

Claude Desktop is a standalone application that supports MCP servers through JSON configuration.

1. **Locate the configuration file**:
   - **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
   - **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

2. **Add TIM-MCP configuration**:

   **Basic configuration (without GitHub token):**

   ```json
   {
     "mcpServers": {
       "tim-mcp": {
         "command": "uvx",
         "args": [
           "--from",
           "git+https://github.com/terraform-ibm-modules/tim-mcp.git",
           "tim-mcp"
         ]
       }
     }
   }
   ```

   {: codeblock}

   **Recommended configuration (with GitHub token):**

   ```json
   {
     "mcpServers": {
       "tim-mcp": {
         "command": "uvx",
         "args": [
           "--from",
           "git+https://github.com/terraform-ibm-modules/tim-mcp.git",
           "tim-mcp"
         ],
         "env": {
           "GITHUB_TOKEN": "your_github_token_here"
         }
       }
     }
   }
   ```

   {: codeblock}

3. **Restart Claude Desktop** completely

4. **Verify installation**:
   - Look for the 🔨 (hammer) icon in the input box
   - Ask: "What IBM Cloud VPC modules are available?"

## Installing TIM-MCP for VS Code

{: #tim-mcp-vscode}
{: step}

VS Code supports MCP servers through the MCP extension.

1. **Install the MCP extension** from the VS Code marketplace

2. **Configure TIM-MCP** using one of these methods:
   - Create `.vscode/mcp.json` in your project directory
   - Use Command Palette (Ctrl+Shift+P or Cmd+Shift+P) → "MCP: Add Server"

3. **Add the configuration**:

   ```json
   {
     "mcpServers": {
       "tim-mcp": {
         "command": "uvx",
         "args": [
           "--from",
           "git+https://github.com/terraform-ibm-modules/tim-mcp.git",
           "tim-mcp"
         ],
         "env": {
           "GITHUB_TOKEN": "your_github_token_here"
         }
       }
     }
   }
   ```

   {: codeblock}

## Installing TIM-MCP for Cursor

{: #tim-mcp-cursor}
{: step}

Cursor IDE supports MCP servers through configuration files.

1. **Create the configuration file**:
   - Project-level: `.cursor/mcp.json` in your project directory
   - Global: `~/.cursor/mcp.json` for all projects

2. **Add the configuration** using the same JSON format as shown in previous sections

## Installing TIM-MCP for Claude Code

{: #tim-mcp-claude-code}
{: step}

Claude Code supports MCP configuration via CLI or config file.

1. **Navigate to your project directory**:

   ```bash
   cd /path/to/your/project
   ```

   {: pre}

2. **Add TIM-MCP using the CLI**:

   **With GitHub token (recommended):**

   ```bash
   claude mcp add tim-mcp --env GITHUB_TOKEN=your_github_token_here \
     -- uvx --from git+https://github.com/terraform-ibm-modules/tim-mcp.git tim-mcp
   ```

   {: pre}

   **Without GitHub token:**

   ```bash
   claude mcp add tim-mcp -- uvx --from git+https://github.com/terraform-ibm-modules/tim-mcp.git tim-mcp
   ```

   {: pre}

3. **Verify configuration**:

   ```bash
   claude mcp list
   ```

   {: pre}

## Using TIM-MCP with AI assistants

{: #tim-mcp-usage}
{: step}

Once TIM-MCP is configured, your AI assistant can help you build IBM Cloud infrastructure from simple to complex deployments.

### Getting started examples

{: #tim-mcp-examples-basic}

Try these prompts to get started:

**Simple virtual server:**

```text
I want to create a simple basic virtual server on IBM Cloud and SSH to it
```

**OpenShift cluster:**

```text
I am new to IBM Cloud. Help me create a simple and cheap OpenShift cluster and access the console
```

### Enterprise infrastructure examples

{: #tim-mcp-examples-enterprise}

For more complex scenarios:

**VPC with OpenShift:**

```text
Design a VPC + OpenShift: Create a complete container platform with networking,
including multi-zone VPC, subnets, OpenShift/ROKS cluster, and load balancers
```

**Secure landing zone:**

```text
Design a Secure Landing Zone: Implement enterprise-grade security with network
isolation, encryption key management, private endpoints, and security groups
```

**Multi-zone HA database:**

```text
Design a Multi-Zone HA Database: Design resilient database infrastructure across
3+ availability zones with automated failover, backup strategies, and disaster recovery
```

**Financial Services validated architecture:**

```text
Design a FS-Validated Architecture: Deploy compliant infrastructure meeting
Financial Services requirements with HPCS encryption, audit logging, and regulatory controls
```

### Best practices for AI-assisted development

{: #tim-mcp-best-practices}

When using TIM-MCP with AI assistants:

1. **Start with clear requirements**: Describe your infrastructure needs, constraints, and compliance requirements
2. **Review generated code**: Always review AI-generated Terraform code before applying
3. **Test in non-production**: Deploy to development or staging environments first
4. **Validate configurations**: Run `terraform plan` to review changes before applying
5. **Use version pinning**: Pin module versions in production deployments
6. **Follow security best practices**: Review security group rules, IAM policies, and encryption settings
7. **Document customizations**: Add comments explaining any modifications to generated code

## Troubleshooting

{: #tim-mcp-troubleshooting}

### Server not starting

{: #tim-mcp-troubleshoot-server}

**Problem:** TIM-MCP server fails to start

**Solution:**

- Verify `uv` is installed and in your PATH: `uv --version`
- Check JSON configuration syntax is valid
- Review error logs in your AI assistant's console

### No tools appearing

{: #tim-mcp-troubleshoot-tools}

**Problem:** MCP tools don't appear in AI assistant

**Solution:**

- Restart your IDE or Claude Desktop completely
- Verify the 🔨 icon appears in the input box
- Check configuration file location is correct

### Rate limiting errors

{: #tim-mcp-troubleshoot-rate-limit}

**Problem:** GitHub API rate limit exceeded

**Solution:**

- Add a `GITHUB_TOKEN` environment variable with a valid personal access token
- Verify token has public repository access permissions
- Test token manually:

  ```bash
  curl -H "Authorization: token YOUR_TOKEN" https://api.github.com/user
  ```

  {: pre}

### Token authentication fails

{: #tim-mcp-troubleshoot-token}

**Problem:** GitHub token not working

**Solution:**

1. Verify token is valid and not expired
2. Check token has public repository access
3. Ensure token is in quotes in JSON configuration
4. Regenerate token if needed

## Version pinning for production

{: #tim-mcp-version-pinning}

For production use, pin TIM-MCP to a specific version to ensure consistent behavior:

```json
{
  "mcpServers": {
    "tim-mcp": {
      "command": "uvx",
      "args": [
        "--from",
        "git+https://github.com/terraform-ibm-modules/tim-mcp.git@v1.0.0",
        "tim-mcp"
      ],
      "env": {
        "GITHUB_TOKEN": "your_github_token_here"
      }
    }
  }
}
```

{: codeblock}

Check the [TIM-MCP releases page](https://github.com/terraform-ibm-modules/tim-mcp/releases){: external} for the latest version.

## Next steps

{: #tim-mcp-next-steps}

- Explore [Terraform IBM Modules](https://github.com/terraform-ibm-modules){: external}
- Learn about [Model Context Protocol](https://modelcontextprotocol.io){: external}
- Review [IBM Cloud Terraform best practices white paper](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform){: external}
- Join the [Terraform IBM Modules community](https://github.com/terraform-ibm-modules){: external}
