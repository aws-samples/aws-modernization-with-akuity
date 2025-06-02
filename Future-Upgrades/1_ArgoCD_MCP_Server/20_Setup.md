---
title: "Setting Up the Argo CD MCP Server"
chapter: true
weight: 2
---

# 🔌 Setting Up the Argo CD MCP Server

In this section, we'll walk through the process of setting up the Argo CD MCP Server in our workshop environment. This will allow us to interact with our Argo CD instance using natural language through AI assistants.

## Prerequisites

Before we begin, ensure you have:

- Completed the Argo CD setup from Module Two
- Access to your Argo CD instance URL and API token
- Node.js v18 or higher (already available in our workshop environment)

## Getting Your Argo CD API Token

First, we need to obtain an API token from our Argo CD instance:

1. Open the Argo CD UI in your browser

2. Click on the user icon in the top-right corner and select **User Info**

3. Click on **Generate New** to create a new API token

4. Copy the generated token and store it securely - we'll need it for the MCP server configuration

## Installing the Argo CD MCP Server

Let's install the Argo CD MCP Server using npm:

```bash
cd /workshop
npm install -g argocd-mcp
```

## Configuring the MCP Server for VS Code

Since we're using VS Code Server in our workshop environment, we'll configure the MCP server to work with it:

1. Collect your ArgoCD credentials:

   ```bash
   # Collect ArgoCD credentials
   export ARGOCD_URL=$(read -p "Enter your ArgoCD URL (e.g., https://argocd.example.com): " url; echo $url)
   export ARGOCD_TOKEN=$(read -s -p "Enter your ArgoCD API token: " token; echo $token)
   echo # Add a newline after the hidden input
   ```

2. Create the MCP configuration directory in your home directory:

   ```bash
   mkdir -p ~/.vscode
   ```

3. Create the MCP configuration file with your credentials:

   ```bash
   # Create the MCP configuration file with the collected credentials
   cat << EOF > ~/.vscode/mcp.json
   {
     "servers": {
       "argocd-mcp": {
         "type": "stdio",
         "command": "npx",
         "args": [
           "argocd-mcp@latest",
           "stdio"
         ],
         "env": {
           "ARGOCD_BASE_URL": "$ARGOCD_URL",
           "ARGOCD_API_TOKEN": "$ARGOCD_TOKEN"
         }
       }
     }
   }
   EOF

   echo "✅ MCP configuration created with your ArgoCD credentials"
   ```

## Verifying the Installation

To verify that the MCP server is properly installed and configured:

1. Restart VS Code to load the new MCP configuration

2. Open the VS Code Command Palette (Ctrl+Shift+P or Cmd+Shift+P)

3. Type "MCP: List Servers" and press Enter

4. You should see "argocd-mcp" listed as an available server

## Testing the MCP Server

Let's test the MCP server by asking our AI assistant about our Argo CD applications:

1. In the VS Code chat interface, ask:
   ```
   Can you list all my Argo CD applications?
   ```

2. The AI assistant should use the MCP server to query your Argo CD instance and return a list of applications

3. Try another query:
   ```
   What's the sync status of the guestbook-dev application?
   ```

4. The AI assistant should provide details about the guestbook-dev application's sync status

## Troubleshooting

If you encounter issues with the MCP server:

1. Check that your Argo CD URL and token are correct in the MCP configuration:

   ```bash
   # View your current configuration
   cat ~/.vscode/mcp.json
   
   # If needed, update your credentials
   export ARGOCD_URL=$(read -p "Enter your ArgoCD URL (e.g., https://argocd.example.com): " url; echo $url)
   export ARGOCD_TOKEN=$(read -s -p "Enter your ArgoCD API token: " token; echo $token)
   echo # Add a newline after the hidden input
   
   # Update the configuration file
   sed -i "s|\"ARGOCD_BASE_URL\": \".*\"|\"ARGOCD_BASE_URL\": \"$ARGOCD_URL\"|g" ~/.vscode/mcp.json
   sed -i "s|\"ARGOCD_API_TOKEN\": \".*\"|\"ARGOCD_API_TOKEN\": \"$ARGOCD_TOKEN\"|g" ~/.vscode/mcp.json
   ```

2. Ensure that your Argo CD instance is accessible from your workshop environment

3. Verify that the MCP server is properly installed:
   ```bash
   npx argocd-mcp@latest --version
   ```

4. Check the VS Code logs for any MCP-related errors:
   - Open the Command Palette
   - Type "Developer: Open Logs Folder"
   - Look for MCP-related log files

## Next Steps

Now that you have the Argo CD MCP Server set up, you can interact with your Argo CD instance using natural language through your AI assistant. In the next section, we'll explore practical use cases for the MCP server in our GitOps workflows.
