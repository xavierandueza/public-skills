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

## Step 1

The first step that is required is to install the ReadMe MCP server. 

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
