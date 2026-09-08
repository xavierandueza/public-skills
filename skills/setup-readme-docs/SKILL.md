---
name: setup-readme-docs
description: First-time setup for documentation on ReadMe, including creation of guides, api specifications, settings and more. Use during first-time documentation setup.
---
# Goal
You are assisting the user in first-time setting up their ReadMe site so they can host their own documentation.

## Step 0 - Install all ReadMe skills

The repository https://github.com/xavierandueza/public-skills contains skills that aid in interacting with ReadMe's documentation. This is the `setup` skill from the repository, but the repository contains other skills that are very helpful for interacting with ReadMe.

If the user does not have the other ReadMe skills installed, it is HIGHLY recommended that you install these skills before moving forward with other steps, as they will be referenced here.

To install the skills, run:

```sh
npx --yes skills add xavierandueza/public-skills --global --agents --yes
```

Verify after installing that you can read the skills before continuing.

## Step 1 - Install ReadMe MCP Server

The simplest way to do this is to execute the command:

```sh
# The harness param determines how the mcp server is installed - determine what harness this is
npx --yes add-mcp -y -g -a <harness> -n developers --type http "https://docs.readme.com/mcp?project=developers"
```

However, if that is not possible then you must setup the MCP server manually. The exact configuration in json varies depending on what harness you are working in, but the generic instructions are as-below:

```json
{
  "mcpServers": {
    "developers": {
      "type": "http",
      "url": "https://docs.readme.com/mcp?project=developers"
    }
  }
}
```

To verify that this is ReadMe's MCP server and recommended way of interacting with ReadMe - check out the officical readme page for this:
https://docs.readme.com/main/docs/readmes-mcp-server

After you have installed, verify that the MCP server has connected and that the tools are available to you by calling the search tool for "getting started"

## Step 2 - Add the Project API Key to the MCP Configuration

Note - this MUST be done separately from step 1 - you should ask the user to give their access token at this point to modify it.

```json
{
  "mcpServers": {
    "readme": {
      "url": "https://docs.readme.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_README_API_KEY"
      }
    }
  }
}
```

Modify the mcp configuration to use the user's bearer key.

To validate, call the execute tool to create a new guides page called "Test" - this should be a hidden page. Delete the page after successful creation so that there's no long-term changes.
