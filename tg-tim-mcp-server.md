---

copyright:
  years: 2017, 2026
lastupdated: "2026-02-12"

keywords: question about tim mcp server, troubleshooting guide

subcollection: ibm-cloud-provider-for-terraform

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How can I resolve the errors while experimenting with TIM-MCP server?
{: #troubleshoot-tim-mcp-error}

Following are some common errors you might face while experimenting with TIM-MCP server.

## Server not starting
{: #tim-mcp-troubleshoot-server}
{: troubleshoot}

TIM-MCP server fails to start.
{: tsSymptoms}

To resolve this issue, follow these steps:
{: tsResolve}

1. Verify `uv` is installed and in your PATH: `uv --version`
1. Check JSON configuration syntax is valid
1. Review error logs in your AI assistant's console

## No tools appearing
{: #tim-mcp-troubleshoot-tools}
{: troubleshoot}

MCP tools don't appear in AI assistant.
{: tsSymptoms}

To resolve this issue, follow these steps:
{: tsResolve}

1. Restart your IDE or Claude Desktop completely
1. Verify the 🔨 icon appears in the input box
1. Check configuration file location is correct

## Rate limiting errors
{: #tim-mcp-troubleshoot-rate-limit}
{: troubleshoot}

GitHub API rate limit exceeded.
{: tsSymptoms}

To resolve this issue, follow these steps:
{: tsResolve}

1. Add a `GITHUB_TOKEN` environment variable with a valid personal access token
1. Verify token has public repository access permissions
1. Test token manually:

        ```bash
        curl -H "Authorization: token YOUR_TOKEN" https://api.github.com/user
        ```
        {: pre}

## Token authentication fails
{: #tim-mcp-troubleshoot-token}
{: troubleshoot}

GitHub token not working.
{: tsSymptoms}

To resolve this issue, follow these steps:
{: tsResolve}

1. Verify token is valid and not expired
1. Check token has public repository access
1. Ensure token is in quotes in JSON configuration
1. Regenerate token if needed
