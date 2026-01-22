# mcp-use Skills

Official skills collection for the [mcp-use](https://mcp-use.com) framework. Skills are reusable capabilities that enhance Claude's ability to build and work with Model Context Protocol (MCP) servers.

## What are Skills?

Skills are folders containing instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks. Each skill teaches Claude how to complete specific tasks in a repeatable way.

For more information about Agent Skills, visit:
- [agentskills.io](https://agentskills.io) - Official specification
- [skills.sh](https://skills.sh) - Skills platform and leaderboard
- [Anthropic's Skills Guide](https://support.claude.com/en/articles/12512198-creating-custom-skills)

## Available Skills

### mcp-builder

Build production-ready MCP servers with the mcp-use framework. This skill provides:
- Quick start with `npx create-mcp-use-app`
- Defining tools, resources, and prompts
- Local testing with Inspector UI
- Tunneling for testing with ChatGPT
- Deployment to mcp-use Cloud
- Best practices and common patterns

**Use when**: Creating MCP servers, defining tools/resources/prompts, deploying MCP servers, or working with the mcp-use framework.

## Installation

### Claude Code

Register this repository as a marketplace:

```bash
/plugin marketplace add mcp-use/skills
```

Then install skills:

```bash
/plugin install mcp-builder@mcp-use
```

Or browse and install via the UI:
1. Run `/plugin marketplace add mcp-use/skills`
2. Select `Browse and install plugins`
3. Select `mcp-use`
4. Choose a skill to install
5. Select `Install now`

### Via skills.sh

```bash
npx skills add mcp-use/skills
```

### Claude.ai

1. Go to your Claude.ai project settings
2. Navigate to Skills section
3. Upload the `skills/` folder or individual skill folders
4. Skills will be available in your conversations

### Cursor / Windsurf

1. Clone this repository
2. Reference skills in your `.cursorrules` or project settings
3. Skills will be available when working in the IDE

## Creating Your Own Skills

Use the template at `template/SKILL.md` as a starting point:

```bash
cp template/SKILL.md skills/my-new-skill/SKILL.md
```

Then customize:
1. Update the YAML frontmatter with `name` and `description`
2. Write clear instructions in the markdown body
3. Include examples and best practices
4. Add any supporting files (scripts, data, etc.)
5. Test with Claude to ensure it works correctly

See `spec/README.md` for detailed information about the SKILL.md format.

## Repository Structure

```
.
├── .claude-plugin/       # Claude Code marketplace configuration
├── skills/               # Individual skills
│   └── mcp-builder/      # MCP server building skill
│       ├── SKILL.md      # Skill definition
│       └── LICENSE.txt   # Skill license
├── template/             # Template for creating new skills
│   └── SKILL.md
├── spec/                 # Agent Skills specification reference
│   └── README.md
├── LICENSE               # Repository license (Apache 2.0)
└── README.md             # This file
```

## Skills Platform Integration

This repository is compatible with:
- **Claude Code**: Via `.claude-plugin/marketplace.json`
- **skills.sh**: Via `npx skills add mcp-use/skills`
- **Claude.ai**: Manual upload of skill folders
- **Cursor/Windsurf**: Local skill references

## Contributing

Skills follow the [Agent Skills specification](https://agentskills.io). When contributing:

1. Fork this repository
2. Create a new skill folder under `skills/`
3. Include a `SKILL.md` file with proper frontmatter
4. Add a `LICENSE.txt` if using a different license
5. Test thoroughly with Claude
6. Submit a pull request

## Upcoming Skills

- **chatgpt-app-builder**: Build ChatGPT apps with best practices
- More skills coming soon!

## Learn More

- **mcp-use Documentation**: [docs.mcp-use.com](https://docs.mcp-use.com)
- **mcp-use GitHub**: [github.com/mcp-use/mcp-use](https://github.com/mcp-use/mcp-use)
- **Discord**: [mcp-use.com/discord](https://mcp-use.com/discord)
- **MCP Protocol**: [modelcontextprotocol.io](https://modelcontextprotocol.io)

## License

This repository is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.

Individual skills may have their own licenses specified in their respective `LICENSE.txt` files.
