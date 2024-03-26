# AVCTL - Agentverse Control
[![Official Website](https://img.shields.io/badge/Official%20Website-fetch.ai-blue?style=flat&logo=world&logoColor=white)](https://fetch.ai) [![Twitter Follow](https://img.shields.io/twitter/follow/fetch_ai?style=social)](https://twitter.com/fetch_ai)

## Introduction
`AVCTL` is a powerful Command Line Interface (CLI) tool designed for interacting with the Agentverse ecosystem. It offers a range of functionalities from authorization to hosting management, making it an essential tool for developers of AI Agents.

This repository is intended for hosting the release binaries and any issues or discussions raised by developers.

Installation (Not yet available, but coming soon)

1. Using `homebrew` (MacOS, Linux):
   ```bash
   brew install avctl

## Quick Start

1. Authenticate with Agentverse:
    ```bash
    avctl auth login

2. Set Up Your Project Workspace:
    ```bash
    mkdir myagent
    cd myagent
3. Prepare Your Agent:
    At this stage, you have two options to start with your agent:

    Option A: Initialize a New Template Agent
    If you're starting a new project, initialize it with a template to lay down foundational code and configuration files:
    ```bash
    avctl hosting init
    ```
    Option B: Retrieve an Existing Agent
    Alternatively, if you wish to work with an existing agent from Agentverse, you can pull it into your local directory:
    ```bash
    avctl hosting pull <agent_address>
    ```
    You can get your existing agent addresses by running `avctl hosting get agents`.
    After pulling an existing agent, you can proceed to run any of the listed commands.
4. Deploy your agent to agentverse:
    ```bash
    avctl hosting deploy
    ```
    If the agent is already deployed, this will only update and restart the agent.

## Commands

Below you'll find a detailed list of avctl commands and their descriptions.

### Authentication Commands

- `auth login` - Log in to the CLI.
- `auth logout` - Log the current user out from the CLI.
- `auth status` - Print out the current status of the authorization.

### Hosting Commands

- `hosting init` - Initialize template agent.
- `hosting get agents` - Lists deployed agents.
- `hosting get agent` - Prints the selected deployed agent.
- `hosting pull` - Pull agent files from Agentverse.
- `hosting push` - Upload files to Agentverse.
- `hosting sync` - Automatically synchronize your local files with those in Agentverse. This command decides whether to pull or push files based on which location has the most recent changes.
- `hosting logs -f` - Print agent logs (optional `-f` flag to follow logs).
- `hosting run -l` - Run Agent (optional `-l` flag for logs).
- `hosting stop` - Stop Agent.
- `hosting deploy -n <name>` - Deploy an agent to Agentverse. This command also updates and restarts the agent if it's already deployed
- `hosting delete` - Delete an agent from Agentverse.
- `hosting secrets add <secret_name>` - Add a secret.
- `hosting secrets delete <secret_name>` - Delete a secret.
- `hosting secrets get` - Retrieve names of all secrets.
- `hosting packages` - Lists all supported packages by Agentverse.

