# MCP Prompt Server

This is a Model Context Protocol (MCP) based server that provides predefined prompt templates based on user task requirements, helping Cline/Cursor/Windsurf and other editors to execute various tasks more efficiently. The server returns predefined prompts as tools for better integration with editors like Cursor and Windsurf.

## Features

- Provides predefined prompt templates for code review, API documentation generation, code refactoring, and more
- Offers all prompt templates as MCP tools rather than MCP prompts format
- Supports dynamic parameter replacement for flexible prompt templates
- Allows developers to freely add and modify prompt templates
- Provides tool APIs for reloading prompts and querying available prompts
- Optimized for editors like Cursor and Windsurf for better integration experience

## Directory Structure

```
prompt-server/
├── package.json         # Project dependencies and scripts
├── src/                # Source code directory
│   ├── index.js         # Server entry file
│   └── prompts/         # Predefined prompt templates directory
│       ├── code_review.yaml
│       ├── api_documentation.yaml
│       ├── code_refactoring.yaml
│       ├── test_case_generator.yaml
│       └── project_architecture.yaml
└── README.md            # Project documentation
```

## Installation and Usage

1. Install dependencies:

```bash
cd prompt-server
npm install
```

2. Start the server:

```bash
npm start
```

The server will run on standard input/output and can be connected by Cursor, Windsurf, or other MCP clients.

## Adding New Prompt Templates

You can create new prompt templates by adding new YAML or JSON files in the `src/prompts` directory. Each template file should contain the following:

```yaml
name: prompt_name                # Unique identifier for calling this prompt
description: prompt description  # Description of the prompt's functionality
arguments:                       # Parameter list (optional)
  - name: arg_name               # Parameter name
    description: arg description # Parameter description
    required: true/false         # Whether required
messages:                        # Prompt message list
  - role: user/assistant         # Message role
    content:
      type: text                 # Content type
      text: |                    # Text content, can include parameter placeholders {{arg_name}}
        Your prompt text here...
```

After adding new files, the server will automatically load them on next startup, or you can use the `reload_prompts` tool to reload all prompts.

## Usage Examples

### Using Code Review Tool in Cursor or Windsurf

```json
{
  "name": "code_review",
  "arguments": {
    "language": "javascript",
    "code": "function add(a, b) { return a + b; }"
  }
}
```

### Using API Documentation Generation Tool in Cursor or Windsurf

```json
{
  "name": "api_documentation",
  "arguments": {
    "language": "python",
    "code": "def process_data(data, options=None):\n    # Process data\n    return result",
    "format": "markdown"
  }
}
```

## Tool APIs

The server provides the following management tools:

- `reload_prompts`: Reload all predefined prompts
- `get_prompt_names`: Get all available prompt names

Additionally, all prompt templates defined in the `src/prompts` directory are provided as tools to clients.

## Editor Integration

### Cursor

In Cursor, you can connect to this server via MCP and access all predefined prompt tools through the tools panel.

### Windsurf

In Windsurf, you can connect to this server via MCP and call predefined prompt tools through the tools panel or commands.

## Extension Suggestions

1. Add more professional domain-specific prompt templates
2. Implement prompt version control
3. Add prompt categorization and tagging
4. Implement prompt usage statistics and analysis
5. Add user feedback mechanism