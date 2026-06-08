# Setup Guide

## Prerequisites

- **Node.js 18+** - [Download](https://nodejs.org/)
- **OpenAI Codex API Access** - [Get API key](https://platform.openai.com/api-keys)
- **Linux/macOS** (Windows with WSL supported)

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/xXBRANCHXx/codex-bolt-refinement.git
cd codex-bolt-refinement
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

Create a `.env` file in the root directory:

```bash
cp .env.example .env
```

Edit `.env` and add your OpenAI API key:

```
OPENAI_API_KEY=sk-your-api-key-here
OUTPUT_DIR=./output
BOLT_STYLE_PRESET=modern
```

### 4. Make CLI executable (optional)

```bash
chmod +x cli.js
```

## Usage

### Basic Usage

```bash
node cli.js --prompt "Create a login form with email and password fields"
```

### With Options

```bash
# Specify component name
node cli.js --prompt "Dashboard card" --name "StatCard"

# Specify output directory
node cli.js --prompt "Todo app" --output ./components

# Verbose output
node cli.js --prompt "Button" --verbose
```

### Using stdin (interactive)

```bash
node cli.js
# Paste your prompt and press Ctrl+D
```

## Workflow Explained

### Step 1: Codex Generation
Your prompt is sent to OpenAI's Codex API with a system prompt that instructs it to:
- Generate functional React components
- Use TypeScript/PropTypes
- Include proper hooks usage
- Structure code for Bolt compatibility

### Step 2: Bolt Formatting
The Codex output is processed to ensure:
- Proper Tailwind CSS spacing scales
- Consistent typography with rem-based sizing
- Responsive design (mobile-first)
- Semantic HTML structure
- Color palette consistency

### Step 3: Refinement
Multiple refinement passes add:
- Missing imports and proper hook organization
- Error handling and error boundaries
- Accessibility features (ARIA labels, semantic HTML)
- TypeScript improvements
- Input validation
- JSDoc comments

### Step 4: Output
The final component is saved as a `.tsx` file ready for:
- Direct use in your Next.js project
- Further customization
- Integration with other components

## Output Structure

Generated components will have this structure:

```typescript
import React, { useState, useCallback } from 'react';

interface YourComponentProps {
  // Your props here
}

export default function YourComponent(props: YourComponentProps) {
  const [state, setState] = useState(null);
  const [error, setError] = useState(null);

  const handleEvent = useCallback(() => {
    // Your handler
  }, []);

  if (error) {
    return <div role="alert">{error.message}</div>;
  }

  return (
    <div className="w-full p-4 bg-white rounded-lg shadow-md">
      {/* Component JSX */}
    </div>
  );
}
```

## Integration with Next.js

### 1. Copy generated component to your Next.js project

```bash
cp output/YourComponent.tsx your-nextjs-app/components/
```

### 2. Use in your pages

```typescript
// pages/your-page.tsx
import YourComponent from '@/components/YourComponent';

export default function Page() {
  return (
    <main>
      <YourComponent />
    </main>
  );
}
```

### 3. Customize as needed

The component is fully functional but feel free to:
- Modify styling/colors
- Add more state/props
- Integrate with your data layer
- Extend functionality

## Troubleshooting

### "OPENAI_API_KEY environment variable not set"

Make sure you've created `.env` file with your API key:

```bash
cat .env
# Should show: OPENAI_API_KEY=sk-...
```

### "Invalid OpenAI API key"

1. Check your API key is correct on [OpenAI Dashboard](https://platform.openai.com/account/api-keys)
2. Ensure the key has Codex access enabled
3. Check you're not out of credits

### "Rate limited by OpenAI API"

You've hit the rate limit. Wait a moment and try again. Consider:
- Spacing out requests
- Using a paid API tier for higher limits

### Generated code is incomplete

Try:
- More detailed prompts (e.g., "Create a form with validation")
- Use `--verbose` flag to see raw Codex output
- Increase max_tokens in `lib/codex.js` if needed

### Component looks wrong in Bolt

Check:
- Tailwind CSS is installed in your project
- All required dependencies are present
- No CSS conflicts with existing styles

## Advanced Usage

### Custom system prompt

Edit `templates/system-prompt.txt` to change how Codex generates components.

### Custom refinement rules

Edit `templates/refinement-rules.json` to adjust refinement behavior.

### Batch generation

Create a `prompts.txt` file:

```
Create a login form
Create a navigation bar
Create a dashboard card
```

Then batch generate:

```bash
cat prompts.txt | while read prompt; do
  node cli.js --prompt "$prompt"
done
```

## Tips & Best Practices

1. **Be specific in your prompt**
   - ❌ "Create a form"
   - ✅ "Create a registration form with email, password, and terms checkbox"

2. **Ask for specific features**
   - Include error handling in your prompt
   - Mention loading states
   - Request accessibility features

3. **Review generated code**
   - Always review the generated component
   - Check for security issues
   - Ensure it fits your design system

4. **Iterate**
   - If the result isn't perfect, refine your prompt and regenerate
   - Use the refined component as a starting point

5. **Combine with your workflow**
   - Use for rapid prototyping
   - Combine with manual refinement
   - Build a component library quickly

## Getting Help

- Check generated code with `--verbose` flag
- Review Codex output separately
- Check Tailwind CSS documentation for class names
- Review React best practices

## Next Steps

1. ✅ Set up `.env` with your API key
2. ✅ Run first generation: `node cli.js --prompt "test button"`
3. ✅ Check output in `output/` directory
4. ✅ Copy to your Next.js project
5. ✅ Customize and integrate
