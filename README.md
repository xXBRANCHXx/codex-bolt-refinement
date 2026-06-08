# Codex → Bolt → Refinement Tool

A CLI + Next.js integration that leverages OpenAI's Codex for UI generation, uses Bolt for design/spacing/typography, then refines the output with functional reality.

## Workflow

1. **Prompt** → You describe what you want
2. **Codex** → Generates initial React component structure (via CLI)
3. **Bolt Formatting** → Applies professional styling, spacing, typography
4. **Refinement** → Adds functionality, fixes structure, injects your custom logic
5. **Output** → Production-ready Next.js component

## Quick Start

### Prerequisites
- Node.js 18+
- OpenAI Codex API key
- Linux/macOS (CLI-based workflow)

### Installation

```bash
npm install
```

### Usage

```bash
# Generate a UI component
node cli.js --prompt "Create a login form with email and password"

# The tool will:
# 1. Call Codex API
# 2. Format for Bolt
# 3. Apply refinements
# 4. Save to output/
```

## Project Structure

```
.
├── cli.js                 # CLI entry point
├── lib/
│   ├── codex.js          # Codex API integration
│   ├── bolt-formatter.js # Format code for Bolt
│   ├── refiner.js        # Refinement logic
│   └── utils.js          # Helpers
├── templates/
│   ├── system-prompt.txt # Codex system prompt
│   └── refinement-rules.json
├── output/               # Generated components
└── package.json
```

## Configuration

Set your OpenAI API key:
```bash
export OPENAI_API_KEY="your-key-here"
```

## How It Works

### 1. Codex Generation
Sends your prompt + system instructions to Codex to generate React component code optimized for Bolt.

### 2. Bolt Formatting
Structures the output with Bolt's design principles:
- Perfect spacing (rem-based scales)
- Professional typography
- Component hierarchy
- Responsive design foundation

### 3. Refinement
Adds:
- State management hooks
- Event handlers
- Data validation
- Error boundaries
- TypeScript types
- Accessibility attributes

## Example

**Input Prompt:**
```
Create a dashboard card that shows user stats (views, clicks, revenue). 
Include loading state and error handling.
```

**Output:**
A fully functional Next.js component with:
- Proper TypeScript types
- Tailwind/styled-components integration
- Loading skeletons
- Error fallbacks
- Responsive design
- Accessibility (ARIA labels, semantic HTML)

## License

MIT
