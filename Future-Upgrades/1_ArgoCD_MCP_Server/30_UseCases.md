---
title: "Practical Use Cases"
chapter: true
weight: 3
---

# 🚀 Practical Use Cases for the Argo CD MCP Server

Now that we have the Argo CD MCP Server set up, let's explore how it can enhance our GitOps workflows in practical scenarios. These use cases build directly on the skills and applications we've developed throughout the workshop.

## Use Case 1: Quick Application Status Checks

When working on our guestbook application, we often need to check its deployment status. Instead of switching to the Argo CD UI, we can simply ask our AI assistant:

```
What's the current status of the guestbook-dev application?
```

The AI assistant will use the MCP server to query Argo CD and provide information such as:
- Sync status (Synced, OutOfSync)
- Health status (Healthy, Degraded, Progressing)
- Last sync time
- Current revision

This allows us to stay in our development environment while monitoring our application's status.

## Use Case 2: Troubleshooting Deployment Issues

If our guestbook application is experiencing issues, we can use the MCP server to help diagnose problems:

```
Show me the logs for the guestbook-dev deployment pods
```

The AI assistant can retrieve logs from the application's pods, helping us identify errors without having to use kubectl commands or navigate through the Argo CD UI.

We can also ask for specific resource information:

```
What events are associated with the guestbook-dev service?
```

This helps us quickly identify issues like configuration problems or resource constraints.

## Use Case 3: Managing Application Syncs

After making changes to our application's configuration in the `guestbook/values-dev.yaml` file, we can use the MCP server to sync our application:

```
Sync the guestbook-dev application
```

The AI assistant will trigger a sync operation through the MCP server, applying our changes to the cluster. We can also ask for more specific sync operations:

```
Sync the guestbook-dev application with prune and force options
```

This is particularly useful when we need to perform more complex sync operations without remembering the exact CLI commands.

## Use Case 4: Exploring Application Resources

To understand our application's structure better, we can ask for its resource tree:

```
Show me the resource tree for the guestbook-dev application
```

The AI assistant will provide a hierarchical view of all resources managed by Argo CD for our application, including:
- Deployments
- Services
- ConfigMaps
- Pods
- Other Kubernetes resources

This gives us a comprehensive overview of our application's components without leaving our IDE.

## Use Case 5: Multi-Environment Management

Building on our Kargo setup for multi-environment promotions, we can use the MCP server to check the status across environments:

```
Compare the guestbook application across dev, staging, and production environments
```

The AI assistant can query all three applications and provide a comparison of:
- Image versions
- Replica counts
- Configuration differences
- Health status

This helps us ensure that our promotion process is working correctly and that our environments are properly configured.

## Use Case 6: Creating New Applications

When we want to deploy a new application to our cluster, we can use the MCP server to create it:

```
Create a new Argo CD application called "new-service" from the Git repository "https://github.com/myuser/new-service" targeting the "development" namespace
```

The AI assistant will use the MCP server to create the application with the specified parameters, saving us time and reducing the chance of errors.

## Use Case 7: Integrating with Our Development Workflow

The MCP server truly shines when integrated into our development workflow. For example, after making changes to our application code:

1. We commit and push our changes to Git
2. We ask our AI assistant: "Has Argo CD detected the changes to the guestbook-dev application?"
3. The AI assistant confirms that the application is OutOfSync
4. We ask: "What changes were detected?"
5. The AI assistant provides a summary of the detected changes
6. We ask: "Sync the application to apply these changes"
7. The AI assistant triggers the sync and reports the result

This entire workflow happens without leaving our IDE, making our GitOps process more efficient.

## Next Steps

In the next section, we'll explore advanced features of the Argo CD MCP Server and how to extend its capabilities for more complex GitOps scenarios.
