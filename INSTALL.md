# Installation Guide - shadcn/ui Style

This guide shows you how to install components by copying them directly into your project (similar to shadcn/ui).

## 🚀 Quick Installation

### Step 1: Install the Package

```bash
npm install @chulkovdanila/svelte-uikit
```

This gives you access to the components, types, and utilities.

### Step 2: Copy Components to Your Project

#### For SvelteKit Projects:

1. **Create components directory** (if it doesn't exist):
```bash
mkdir -p src/lib/components/ui
```

2. **Copy Button component**:
```bash
# Copy the entire Button folder
cp -r node_modules/@chulkovdanila/svelte-uikit/src/lib/components/Button src/lib/components/ui/

# Or manually copy:
# - Button.svelte
# - index.ts
```

3. **Copy utilities** (if you don't have them):
```bash
mkdir -p src/lib/utils
cp node_modules/@chulkovdanila/svelte-uikit/src/lib/utils/cn.ts src/lib/utils/
```

4. **Copy types** (optional, for TypeScript):
```bash
mkdir -p src/lib/types
cp node_modules/@chulkovdanila/svelte-uikit/src/lib/types/index.ts src/lib/types/
```

### Step 3: Update Imports

In your Svelte files, import from your local components:

```svelte
<script>
  import { Button } from '$lib/components/ui/Button';
</script>

<Button>Click me</Button>
```

## 📁 Project Structure

After installation, your project should look like this:

```
your-project/
├── src/
│   ├── lib/
│   │   ├── components/
│   │   │   └── ui/
│   │   │       └── Button/
│   │   │           ├── Button.svelte
│   │   │           └── index.ts
│   │   ├── utils/
│   │   │   └── cn.ts
│   │   └── types/
│   │       └── index.ts
│   └── ...
└── package.json
```

## ✅ Benefits of This Approach

- ✅ Full control over component code
- ✅ Easy customization (modify styles directly)
- ✅ No external dependencies
- ✅ Works offline
- ✅ Fast updates (just modify your local copy)

## 🔄 Updating Components

To update a component:

1. Check the latest version in `node_modules/@chulkovdanila/svelte-uikit`
2. Copy the updated files to your project
3. Test your implementation
4. Customize as needed

## 💡 Tips

- Keep your customizations in a separate file or use CSS variables
- Commit your component files to version control
- Consider creating a script to automate copying components

