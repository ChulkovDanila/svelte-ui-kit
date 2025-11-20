# Svelte UI Kit

<div align="center">

**Beautiful animated button component for Svelte with slide and arc animations**

[![npm version](https://img.shields.io/npm/v/@chulkovdanila/svelte-uikit.svg)](https://www.npmjs.com/package/@chulkovdanila/svelte-uikit)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Svelte](https://img.shields.io/badge/Svelte-5.x-orange)](https://svelte.dev)

Easy to use, customizable button component with smooth hover animations - inspired by shadcn/ui style

</div>

---

## ✨ Features

- 🎨 **Two Animation Types**: Slide (horizontal) and Arc (curved) animations
- ⚡ **Three Speed Options**: Fast, Medium, and Slow animations
- 🎯 **Multiple Variants**: Default, Outline, Destructive, and Ghost styles
- 📦 **Easy Installation**: Copy components directly into your project (like shadcn/ui)
- 🔧 **Fully Customizable**: Modify colors, sizes, and animations to fit your design
- 💪 **TypeScript Support**: Full type safety out of the box
- 🎭 **No Dependencies**: Pure Svelte component, no external dependencies

---

## 📦 Installation

### Install from npm

```bash
npm install @chulkovdanila/svelte-uikit
```

### Install from GitHub

```bash
npm install github:ChulkovDanila/svelte-ui-kit
```

---

## 🚀 Quick Start

### Method 1: Direct Import (Recommended)

After installation, import components directly:

```svelte
<script>
  import { Button } from '@chulkovdanila/svelte-uikit';
</script>

<Button>Click me</Button>
```

### Method 2: Copy Component (Like shadcn/ui)

For full control over component code, copy components directly into your project:

1. **Install the package:**

```bash
npm install @chulkovdanila/svelte-uikit
```

2. **Copy Button component:**

```bash
mkdir -p src/lib/components/ui
cp -r node_modules/@chulkovdanila/svelte-uikit/src/lib/components/Button src/lib/components/ui/
```

3. **Copy utilities:**

```bash
mkdir -p src/lib/utils
cp node_modules/@chulkovdanila/svelte-uikit/src/lib/utils/cn.ts src/lib/utils/
```

4. **Copy types (TypeScript):**

```bash
mkdir -p src/lib/types
cp node_modules/@chulkovdanila/svelte-uikit/src/lib/types/index.ts src/lib/types/
```

5. **Import from local:**

```svelte
<script>
  import { Button } from '$lib/components/ui/Button';
</script>

<Button>Click me</Button>
```

---

## 📖 Usage Examples

### Basic Usage

```svelte
<script>
  import { Button } from '@chulkovdanila/svelte-uikit';
</script>

<Button>Click me</Button>
```

### Animation Types

```svelte
<!-- Slide Animation (horizontal) -->
<Button animationType="slide">Get Started</Button>

<!-- Arc Animation (curved) -->
<Button animationType="arc">Discover</Button>
```

### Animation Speeds

```svelte
<Button animationSpeed="fast">Fast</Button>
<Button animationSpeed="medium">Medium</Button>
<Button animationSpeed="slow">Slow</Button>
```

### Button Variants

```svelte
<Button variant="default">Default</Button>
<Button variant="outline">Outline</Button>
<Button variant="destructive">Delete</Button>
<Button variant="ghost">Cancel</Button>
```

### Rounded Buttons

```svelte
<Button rounded>Rounded Button</Button>
```

### Complete Example

```svelte
<Button 
  animationType="slide" 
  animationSpeed="medium" 
  variant="outline" 
  rounded
>
  Learn More
</Button>
```

---

## 📖 Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `animationType` | `'slide' \| 'arc'` | `'slide'` | Animation type: slide (horizontal) or arc (curved) |
| `animationSpeed` | `'fast' \| 'medium' \| 'slow'` | `'fast'` | Animation speed: fast (0.4s), medium (0.7s), or slow (1.2s) |
| `variant` | `'default' \| 'outline' \| 'destructive' \| 'ghost'` | `'default'` | Button style variant |
| `rounded` | `boolean` | `false` | Fully rounded button corners |
| `disabled` | `boolean` | `false` | Disable button interactions |
| `type` | `'button' \| 'submit' \| 'reset'` | `'button'` | HTML button type |
| `class` | `string` | `''` | Additional CSS classes |

---

## 🎨 Animation Types

### Slide Animation
Horizontal text movement - text slides right on hover, new text slides in from left.

**GitHub Search Keywords**: `slide animation button`, `horizontal animation button`

### Arc Animation  
Curved movement with rotation - text moves in a semicircle path with rotation effect.

**GitHub Search Keywords**: `arc animation button`, `curved animation button`

---

## 📚 TypeScript Types

```typescript
import type { ButtonVariant, ButtonAnimationType } from '@chulkovdanila/svelte-uikit';

const variant: ButtonVariant = 'outline';
const animationType: ButtonAnimationType = 'slide';
```

---

## 🔧 Customization

### Custom Colors

You can customize button colors by modifying CSS or using custom classes:

```svelte
<Button class="custom-button">Custom</Button>

<style>
  :global(.custom-button) {
    background-color: #your-color;
    color: #your-text-color;
  }
  
  :global(.custom-button:hover) {
    background-color: #your-hover-color;
  }
</style>
```

---

## 📹 Demo Videos

Watch our animated button components in action!

- 🎬 **[Slide Animation Showcase](./videoshowcase/Showcase1.mp4)** - Smooth horizontal text movement
- 🎬 **[Arc Animation Showcase](./videoshowcase/Showcase2.mp4)** - Beautiful curved movement with rotation

See the [SHOWCASE.md](./SHOWCASE.md) document for complete information.

---

## 🛠️ Development

Clone the repository:

```bash
git clone https://github.com/ChulkovDanila/svelte-ui-kit.git
cd svelte-ui-kit
npm install
```

Run development server:

```bash
npm run dev
```

---

## 📄 License

MIT License - feel free to use in your projects!

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## 🔍 Finding This Component

Search on GitHub using these keywords:
- `slide animation button svelte`
- `arc animation button svelte`
- `curved animation button svelte`
- `horizontal animation button svelte`
- `animated button svelte`
- `svelte ui kit`

---

Made with ❤️ for the Svelte community
