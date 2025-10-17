# appgraph

AppGraph is a language & framework for expressing an entire web application as a graph of interconnected agentic nodes. Nodes can encapsulate behaviors as complex as a full microservice, and leverages generative AI to perform complex, fully agentic workloads without needing to write any code.

AppGraph takes care of platform, framework, infrastructure, scaling, security, networking, & CI/CD concerns. Begin with a prompt of what you want the application to do. AppGraph produces a JSON representation of a system graph describing how each component should behave & interact. Refine the graph as needed for your use case, and let AppGraph build out & deploy the entire application. The graph is the source of truth - make changes as needed, and AppGraph keeps the service in sync with the specification.

## Example

Prompt: "Build a blog platform where users can sign up, create blog posts, and comment on posts. Add moderation for comments and email notifications when someone replies to a comment."

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

