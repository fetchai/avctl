# AVCTL - Agentverse Control
[![Official Website](https://img.shields.io/badge/Official%20Website-fetch.ai-blue?style=flat&logo=world&logoColor=white)](https://fetch.ai) [![Twitter Follow](https://img.shields.io/twitter/follow/fetch_ai?style=social)](https://twitter.com/fetch_ai)

## Introduction
`AVCTL` is a powerful Command Line Interface (CLI) tool designed for interacting with the Agentverse ecosystem. It offers a range of functionalities from authorization to hosting management, making it an essential tool for developers of AI Agents.

This repository is intended for hosting the release binaries and any issues or discussions raised by developers.

## Installation

- Using `homebrew` (MacOS, Linux):
   ```bash
   brew tap fetchai/avctl
   brew install avctl
   ```

- Using chocolatey:
   ```
   choco install avctl
   ```

## Get Started

### Individual Agent Management

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


### Multiple agents as a workspace.

1. Authenticate with Agentverse:
    ```bash
    avctl auth login

2. Set Up Your Project Workspace:
    ```bash
    mkdir myworkspace
    cd myworkspace
3. Prepare Your Workspace:
To include all agents in `myworkspace`, ensure each agent folder contains the following three files:

    1. `agent.py`: Contains the agent's main code.
    2. `pyproject.toml`: Specifies the agent's dependencies.
    3. `.env`: Provides information about dependencies on other agent addresses. For example, if the agent depends on `agent-name`, point to its folder by specifying:
    AGENT_ADDRESS={{ .AgentName.Address }}

    Start workspace with:
    ```bash
    avctl hosting init --workspace
    ```
   This initializes the workspace, detecting all agent dependencies in each agent `.env` file, adding them to the configuration file.

4. Deploy all agents to agentverse:
    ```bash
    avctl hosting deploy
    ```
   Deploys agents based on the configuration file and detected dependencies, deploying agents in the correct order according to their dependencies on one another.

NOTE: If you have initialized an agent using `avctl hosting init` and then try running `avctl hosting init --workspace` from the workspace level, it will fail. You can only work with either agent or workspace configurations, not both. A quick fix is to simply delete the .avctl/config.toml file from either the agent or workspace folder, depending on the type of configuration you want to use.

## Commands

Below you'll find a detailed list of avctl commands and their descriptions.

### Authentication Commands

- `auth login` - Log in to the CLI.
- `auth logout` - Log the current user out from the CLI.
- `auth status` - Show the current authorization status.

### Hosting Commands

#### Agent Commands
These commands are used for individual agent management.

- `hosting init` - Initialize template agent.
- `hosting get agents` - Lists deployed agents.
- `hosting get agent` - Prints the selected deployed agent.
- `hosting pull` - Pull agent files from Agentverse.
- `hosting push` - Upload files to Agentverse.
- `hosting sync` - Automatically synchronize your local files with those in Agentverse. This command decides whether to pull or push files based on which location has the most recent changes.
- `hosting logs -f` - Print agent logs (optional `-f` flag to follow logs).
- `hosting run -l` - Run Agent (optional `-l` flag for logs).
- `hosting stop` - Stop Agent.
- `hosting deploy -n <name>` - Deploy an agent to Agentverse (optional `-l` flag to follow logs and `-r` flag to run the agent). This command also updates and restarts the agent if it's already deployed.
- `hosting delete agents` - Delete agents from Agentverse (optional `--all` flag to delete all agents).
- `hosting add secrets <secret_name>` - Add a secret.
- `hosting delete secrets <secret_name>` - Delete a secret.
- `hosting get secrets` - Retrieve names of all secrets.
- `hosting packages` - Lists all supported packages by Agentverse.
- `hosting include <include_path>` - Set the folder containing files to include in your agent.

#### Workspace Commands
These commands are designed to manage multiple agents as a workspace.

- `hosting init --workspace`  
   Initializes the workspace, detecting all agent dependencies in each agent `.env` file, adding them to the configuration file. Make sure to add these manually in the following format: `AGENT_ADDRESS={{ .AgentName.Address }}` when pointing to `agent-name` agent
- `hosting deploy`  
   Deploys agents based on the configuration file and detected dependencies, deploying agents in the correct order according to their dependencies on one another.

With these commands, `avctl` provides flexibility to manage single agents or entire workspaces, allowing you to efficiently build and manage agents in the Agentverse ecosystem.