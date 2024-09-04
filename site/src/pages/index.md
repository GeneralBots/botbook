---
sidebar_position: 0
---

# General Bots Documentation

![General Bots Logo](https://user-images.githubusercontent.com/65977273/94922431-949c3900-0490-11eb-800a-6b478d689f2a.png)

## Introduction

Welcome to the comprehensive General Bots documentation. This guide serves as an essential reference for developers looking to harness the power and flexibility of the General Bots server. Our platform is designed with modularity in mind, allowing for easy customization and extension through various package types.

In this documentation, we'll explore the architecture of the General Bots server, diving deep into its package-based structure. You'll learn how to leverage this modular approach for custom deployments, whether you're working with knowledge bases (.gbkb), themes (.gbtheme), or full-fledged applications (.gbapp).

## Table of Contents

* [Chapter 01 - Run and Talk](docs/chapter-01-run-and-talk)
* [Chapter 02 - About Packages](docs/chapter-02-the-package-based)
* [Chapter 03 - gbkb Reference](docs/chapter-03-gbkb-reference)
* [Chapter 04 - gbtheme Reference](docs/chapter-04-gbtheme-reference)
* [Chapter 05 - gbdialog Reference](docs/chapter-05-gbdialog-reference)
* [Chapter 06 - gbapp Reference](docs/chapter-06-gbapp-reference)
* [Chapter 07 - gbot Reference](docs/chapter-07-gbot-reference)
* [Chapter 08 - Tooling](docs/chapter-08-tooling)
* [Chapter 09 - Feature-Matrix](docs/chapter-09-feature-matrix)
* [Chapter 10 - Contributing](docs/chapter-10-contributing)
* [Apendix I - Database Model](docs/apendix-i-database-model)
* [Glossary](docs/glossary)

## Getting Started

### Prerequisites

Before you embark on your General Bots journey, ensure you have the following tools installed:

- **Node.js (version 20 or later)**: General Bots leverages the latest features of Node.js to provide a robust and efficient runtime environment. Download it from [nodejs.org](https://nodejs.org/en/download/).
- **Git (latest stable version)**: Essential for version control and collaborating on bot projects. Get it from [git-scm.com](https://git-scm.com/downloads).

### Quick Start Guide

Follow these steps to get your General Bots server up and running:

1. Clone the repository:
   ```bash
   git clone https://github.com/GeneralBots/BotServer
   ```
   This command creates a local copy of the General Bots server repository on your machine.

2. Navigate to the project directory:
   ```bash
   cd BotServer
   ```
   This changes your current directory to the newly cloned BotServer folder.

3. Install dependencies and start the server:
   ```bash
   npm install
   npm run start
   ```
   The `npm install` command installs all necessary dependencies for the project. `npm run start` builds your bot server locally and serves it through a development server.

### Accessing Your Bot

Once the server is running, you can access your bot at `http://localhost:4242/`. This local server allows you to interact with your bot and test its functionality in real-time.

To publish bot packages and initiate a conversation with the bot, use the command:

```
/publish
```
This command prepares your bot packages for use and allows you to start interacting with your bot immediately.

## Development Workflow

### 1. Project Structure

The General Bots server follows a modular architecture designed for flexibility and scalability. Here's an overview of the main directories:

```
BotServer/
├── packages/
│   ├── core.gbapp/         # Core bot functionality
│   ├── kb.gbapp/           # Knowledge base packages
├── src /             # Main entry point
└── package.json      # Project configuration
```

This structure allows for easy navigation and management of different aspects of your bot project.

### 2. Creating Custom Packages

One of the strengths of General Bots is its extensibility. You can create custom packages to enhance your bot's capabilities:

- **.gbkb (Knowledge Base packages)**: Store and manage your bot's knowledge and responses.
- **.gbtheme (Theme packages)**: Customize the visual appearance of your bot interface.
- **.gbapp (Application packages)**: Add new features and functionalities to your bot.

Each package type has its own structure and purpose, which we'll explore in depth in their respective chapters.

### 3. API Reference

For detailed information on working with each package type, refer to the following chapters:

- Chapter 3: gbkb Reference - Learn how to create and manage knowledge bases
- Chapter 4: gbtheme Reference - Discover the theming capabilities of General Bots
- Chapter 5: gbdialog Reference - Master the art of creating dynamic conversations
- Chapter 6: gbapp Reference - Explore the full potential of bot applications
- Chapter 7: gbot Reference - Understand the core functionalities of your bot

These chapters provide comprehensive API documentation, usage examples, and best practices for each package type.

### 4. Testing

We strongly encourage writing unit tests for your custom packages to ensure reliability and ease of maintenance. To run tests, use the following command:

```bash
npm run test
```

This command executes the test suites located in the `tests/` directory, allowing you to verify the functionality of your bot components.

### 5. Deployment

When you're ready to deploy your bot to a production environment, the `npm run build` command creates an optimized production build of your bot server.

## Advanced Topics

As you become more familiar with General Bots, you may want to explore these advanced topics:

- **Scalability**: Chapter 9 - Services delves into horizontal scaling options, allowing your bot to handle increased load and user interactions efficiently.
- **Performance Tuning**: Chapter 8 - Tooling offers insights and techniques for optimizing your bot's performance, ensuring smooth operation even under demanding conditions.
- **Security Best Practices**: Chapter 10 - Contributing outlines important security guidelines to keep your bot and its data protected.

These advanced topics will help you take your General Bots implementation to the next level, creating robust, scalable, and secure bot solutions.

## Community and Support

Join our vibrant community of bot developers:

- **GitHub Issues**: For bug reports and feature requests, visit our [issue tracker](https://github.com/GeneralBots/BotServer/issues). Here, you can report problems, suggest improvements, or even contribute code fixes.

## Contributing

We welcome contributions from developers of all skill levels! Whether you're fixing a bug, adding a feature, or improving documentation, your input is valuable. Please read our [Contributing Guide](docs/chapter-10-contributing) for details on our code of conduct and the process for submitting pull requests.

Remember, the General Bots platform is designed to be flexible and extensible. We encourage you to explore its capabilities, experiment with new ideas, and contribute to making it even better. Your creativity and expertise can help shape the future of conversational AI!