# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **Vibe Coding CN** repository - a comprehensive workflow, toolset, and knowledge base for AI-assisted programming. The project's core value lies in its extensive collection of AI prompts, skills, and methodology for effective AI-human collaboration in software development.

## Key Commands

### Development & Maintenance
```bash
# Lint all markdown files in the repository
make lint

# Build the project (placeholder - add specific build commands)
make build

# Run tests (placeholder - add specific test commands)
make test

# Clean build artifacts (placeholder - add cleanup commands)
make clean

# Show help with available commands
make help
```

### Prompt Library Management
```bash
# Navigate to the prompts library tool
cd libs/external/prompts-library

# Run the interactive conversion tool (Excel ↔ Markdown)
python3 main.py

# Install markdownlint globally (required for make lint)
npm install -g markdownlint-cli
```

### Backup Operations
```bash
# Create a full project backup (respects .gitignore)
bash backups/一键备份.sh

# Quick backup script
python backups/快速备份.py
```

## Architecture & Structure

### Core Components

**1. i18n/zh/prompts/** - The central asset repository:
- `coding_prompts/` - Programming and code generation prompts
- `system_prompts/` - AI behavior and framework definition prompts
- `user_prompts/` - User-defined and commonly used prompts
- `assistant_prompts/` - Support and assistant prompts

**2. i18n/zh/skills/** - Modular skill library:
- Domain-specific knowledge for tools (ccxt, postgresql, telegram-dev, etc.)
- Each skill contains its own `SKILL.md` with detailed context

**3. i18n/zh/documents/** - Knowledge base:
- Methodology, principles, templates, and guides
- Code organization patterns and best practices

**4. libs/external/prompts-library/** - Conversion tool:
- Python-based tool for Excel ↔ Markdown conversion
- Maintains prompt consistency across formats
- Uses pandas, openpyxl, and rich for CLI interface

**5. libs/** - Core library skeleton:
- `common/` - Shared utilities and models
- `database/` - Database-related code
- `external/` - External tools and configurations

### Key Technical Details

1. **Prompt Organization**: Uses `(row,col)_` prefix system for categorization
2. **Language Structure**: User-facing docs in Chinese, code/technical in English
3. **Multi-language Support**: i18n structure with zh/en/he and many other languages
4. **Conversion Pipeline**: Excel ↔ Markdown bidirectional conversion
5. **Backup System**: Scripts for project snapshotting and recovery

## Development Workflow

### Working with Prompts
- Use the prompts-library tool for bulk prompt management
- Maintain consistent naming with `(row,col)_` prefixes
- Run `make lint` after modifying any Markdown files
- Follow the existing categorization system (coding/system/user/assistant)

### Adding New Content
- Place new prompts in appropriate i18n/zh/prompts/ subdirectories
- Add skills to i18n/zh/skills/ with proper SKILL.md documentation
- Update relevant documents in i18n/zh/documents/ for methodology changes
- Use the prompts-library tool for batch operations

### Quality Assurance
- Always run `make lint` before committing changes
- Test prompt conversions in a temporary directory first
- Verify backup scripts work correctly in isolated environments
- Maintain consistent indentation (spaces, no mixing of 2/4 space styles)

## Project Philosophy

This repository embodies the **Vibe Coding** methodology:
- **Planning-driven**: Emphasize structured planning before implementation
- **Modularity**: Break down complex tasks into manageable components
- **AI collaboration**: Leverage AI as a collaborative partner, not just a tool
- **Context preservation**: Maintain consistent context through documentation
- **Iterative refinement**: Continuous improvement through feedback loops

The core workflow follows: **Requirements → Context Documentation → Implementation Plan → Step-by-Step Execution → Self-Testing → Progress Recording**


## 🛡️ Strict Development Rules (Mandatory)

### [ALWAYS] Memory Bank & Context Integrity
**Before writing any code or executing any implementation step, you MUST:**
1.  **Read** `memory-bank/@architecture.md`: Understand the system architecture, data flow, and database schema.
2.  **Read** `memory-bank/@nl-mesh-inspect-design-document.md`: Review the product logic and requirements.
3.  **Validate**: Ensure the current task doesn't conflict with existing architectural patterns.
4.  **Update**: After completing any milestone or significant feature, you **MUST** immediately update `@architecture.md` to reflect changes.

### [ALWAYS] Anti-Monolith & Modularity
-   **No Monolithic Files**: Any file exceeding 300 lines of code must be evaluated for decomposition.
-   **Separation of Concerns**: 
    -   **Frontend**: Separate 3D rendering logic (Three.js), UI components (React/Next.js), and API hooks.
    -   **Backend**: Separate Geometry processing (Trimesh), NLP logic (LangChain), and API routing (FastAPI).
-   **Feature Flags**: New complex features should be developed in separate modules/files before being integrated into the main entry point.

### Technical Best Practices
-   **State Management**: Use localized state (Zustand or React Context) instead of passing props deeply.
-   **Type Safety**: Always use TypeScript for frontend and Type Hints for Python; no `any` types allowed.
-   **Geometry Optimization**: All mesh operations must consider spatial acceleration (`three-mesh-bvh`).
-   **Error Handling**: Wrap LLM tool calls in robust try-catch blocks with clear user feedback.

## Implementation Workflow (Vibe Coding Standard)
1.  **Requirement Sync**: Confirm intent against the Design Doc.
2.  **Architecture Check**: Read Memory Bank.
3.  **Planning**: Generate a step-by-step implementation plan (check for modularity).
4.  **Execution**: Implement in small, testable chunks.
5.  **Documentation**: Update Memory Bank and inline JSDoc/Docstrings.