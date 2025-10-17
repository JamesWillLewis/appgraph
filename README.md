# appgraph

## Intro

AppGraph is a language & framework for expressing an entire web application as a graph of interconnected agentic nodes. Nodes can encapsulate behaviors as complex as a full microservice, and leverages generative AI to perform complex, fully agentic workloads without needing to write any code. 

You can think of AppGraph as a very high-level programming language that allows you to express the behaviors & expectations of a system in natural langauge, and the "compilation" step generates the supporting code & infrastructure through large-language models. 

AppGraph takes care of platform, framework, infrastructure, scaling, security, networking, & CI/CD concerns. Begin with a prompt of what you want the application to do. AppGraph produces a JSON representation of a system graph describing how each component should behave & interact. Refine the graph as needed for your use case, and let AppGraph build out & deploy the entire application. 

The graph is the source of truth - make changes as needed, and AppGraph keeps the service in sync with the specification. The application graph can represent much more than just the intention and interactions of components; it can be used to enforce end-to-end authorization & encryption rules, apply granular scaling policies, provide insights, observability & request tracing, and much more - all through a configurable, open-source plugin interface.

## Variants

AppGraph comes in 2 flavors. 

### Managed AppGraph

In Managed AppGraph, AppGraph handles everything needed to build, host & operate your application. You submit your application graphs through http://appgraph.io, and Managed Appgraph handles all build tasks, infrastructure management, & operations.

### Self Hosted

In Self Hosted mode, you bring your own infrastructure. You pick and choose the specific technologies (language, platform, framework, hosting) you want (where supported). You have complete control over everything. 

## Performance

AppGraph is highly performant because the nodes are just code. Inference is only used to generate the code for the nodes - all actual workloads against the application are handled by code. 

The application graph is essentially "compiled" into real code (& supporting infrastructure) by large-language models.

## Safety & Reliability

AppGraph is spec-driven to ensure applications firmly abide by clearly-specified business rules, and enforces gaurdrails to ensure all networking, security, & auth configurations strictly adhere to policies. 

## Example

Prompt: 
> Build a blog platform where users can sign up, create blog posts, and comment on posts.
> Add moderation for comments and email notifications when someone replies to a comment.

AppGraph might produce something like this:
```
{
  "nodes": [
    {
      "id": "auth-service",
      "type": "auth",
      "name": "Authentication Service",
      "description": "Handles user sign-up, login, and authentication."
    },
    {
      "id": "user-service",
      "type": "data-store",
      "name": "User Service",
      "description": "Stores user profiles and metadata.",
      "dependencies": ["auth-service"]
    },
    {
      "id": "blog-post-service",
      "type": "agentic-service",
      "name": "Blog Post Service",
      "description": "Allows users to create, edit, and delete blog posts.",
      "dependencies": ["auth-service", "user-service"]
    },
    {
      "id": "comment-service",
      "type": "agentic-service",
      "name": "Comment Service",
      "description": "Enables users to comment on blog posts and replies.",
      "dependencies": ["auth-service", "blog-post-service"]
    },
    {
      "id": "moderation-agent",
      "type": "ai-agent",
      "name": "Moderation Agent",
      "description": "Uses generative AI to moderate comments for toxicity and spam.",
      "dependencies": ["comment-service"]
    },
    {
      "id": "notification-agent",
      "type": "ai-agent",
      "name": "Notification Agent",
      "description": "Sends email notifications when someone replies to a comment.",
      "dependencies": ["comment-service", "user-service"]
    },
    {
      "id": "frontend",
      "type": "ui",
      "name": "Frontend App",
      "description": "User interface for interacting with the blog platform.",
      "dependencies": ["auth-service", "blog-post-service", "comment-service"]
    }
  ],
  "metadata": {
    "projectName": "Blog Platform",
    "version": "1.0.0",
    "generatedBy": "AppGraph",
    "createdAt": "2025-10-17T12:00:00Z"
  }
}
```

Refine the graph, verify everything looks good, build, test & deploy.

