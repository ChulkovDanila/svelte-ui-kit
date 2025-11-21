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

- 🎨 **Two Button Components**: HorizontalSlideButton with slide/arc animations and VerticalSlideButton with vertical letter animation
- ⚡ **Three Speed Options**: Fast (1s), Medium (2s), and Slow (3s) animations
- 🎯 **Multiple Variants**: Default, Outline, Destructive, and Ghost styles for HorizontalSlideButton
- 🎭 **VerticalSlideButton**: Clean text-only button with customizable colors, sizes, and smooth vertical letter animations
- 📦 **Easy Installation**: Copy components directly into your project (like shadcn/ui)
- 🔧 **Fully Customizable**: Modify colors, sizes, fonts, and animations to fit your design
- 💪 **TypeScript Support**: Full type safety out of the box
- 🚫 **No Dependencies**: Pure Svelte components, no external dependencies

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
  import { HorizontalSlideButton, VerticalSlideButton } from '@chulkovdanila/svelte-uikit';
</script>

<HorizontalSlideButton>Click me</HorizontalSlideButton>
<VerticalSlideButton>Hover me</VerticalSlideButton>
```

### Method 2: Copy Component (Like shadcn/ui)

For full control over component code, copy components directly into your project:

1. **Install the package:**

```bash
npm install @chulkovdanila/svelte-uikit
```

2. **Copy components:**

```bash
mkdir -p src/lib/components/ui
cp -r node_modules/@chulkovdanila/svelte-uikit/src/lib/components/HorizontalSlideButton src/lib/components/ui/
cp -r node_modules/@chulkovdanila/svelte-uikit/src/lib/components/VerticalSlideButton src/lib/components/ui/
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
  import { HorizontalSlideButton } from '$lib/components/ui/HorizontalSlideButton';
  import { VerticalSlideButton } from '$lib/components/ui/VerticalSlideButton';
</script>

<HorizontalSlideButton>Click me</HorizontalSlideButton>
<VerticalSlideButton>Hover me</VerticalSlideButton>
```

---

## 📖 Usage Examples

### Basic Usage

```svelte
<script>
  import { HorizontalSlideButton, VerticalSlideButton } from '@chulkovdanila/svelte-uikit';
</script>

<HorizontalSlideButton>Click me</HorizontalSlideButton>
<VerticalSlideButton>Hover me</VerticalSlideButton>
```

### VerticalSlideButton Component

VerticalSlideButton is a clean, text-only button with vertical letter animation on hover:

```svelte
<VerticalSlideButton 
  color="#000000" 
  hoverColor="#666666" 
  fontSize="2rem"
  animationSpeed="medium"
>
  Click me
</VerticalSlideButton>
```

### Animation Types

```svelte
<!-- Slide Animation (horizontal) -->
<HorizontalSlideButton animationType="slide">Get Started</HorizontalSlideButton>

<!-- Arc Animation (curved) -->
<HorizontalSlideButton animationType="arc">Discover</HorizontalSlideButton>
```

### Animation Speeds

```svelte
<HorizontalSlideButton animationSpeed="fast">Fast</HorizontalSlideButton>
<HorizontalSlideButton animationSpeed="medium">Medium</HorizontalSlideButton>
<HorizontalSlideButton animationSpeed="slow">Slow</HorizontalSlideButton>
```

### HorizontalSlideButton Variants

```svelte
<HorizontalSlideButton variant="default">Default</HorizontalSlideButton>
<HorizontalSlideButton variant="default-rounded">Default Rounded</HorizontalSlideButton>
<HorizontalSlideButton variant="outline">Outline</HorizontalSlideButton>
<HorizontalSlideButton variant="outline-rounded">Outline Rounded</HorizontalSlideButton>
<HorizontalSlideButton variant="destructive">Delete</HorizontalSlideButton>
<HorizontalSlideButton variant="destructive-rounded">Delete Rounded</HorizontalSlideButton>
<HorizontalSlideButton variant="ghost">Cancel</HorizontalSlideButton>
<HorizontalSlideButton variant="ghost-rounded">Cancel Rounded</HorizontalSlideButton>
```

### Rounded Buttons

```svelte
<HorizontalSlideButton variant="default-rounded">Rounded Button</HorizontalSlideButton>
<HorizontalSlideButton variant="outline-rounded">Outline Rounded</HorizontalSlideButton>
<HorizontalSlideButton variant="destructive-rounded">Destructive Rounded</HorizontalSlideButton>
```

### Complete Examples

```svelte
<HorizontalSlideButton 
  animationType="slide" 
  animationSpeed="medium" 
  variant="outline-rounded"
>
  Learn More
</HorizontalSlideButton>

<VerticalSlideButton 
  color="#ff0000" 
  hoverColor="#cc0000" 
  fontSize="1.5rem"
  animationSpeed="slow"
>
  Hover Me
</VerticalSlideButton>
```

---

## 📖 Props

### HorizontalSlideButton Component

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `animationType` | `'slide' \| 'arc'` | `'slide'` | Animation type: slide (horizontal) or arc (curved) |
| `animationSpeed` | `'fast' \| 'medium' \| 'slow'` | `'fast'` | Animation speed: fast (1s), medium (2s), or slow (3s) |
| `variant` | `'default' \| 'default-rounded' \| 'outline' \| 'outline-rounded' \| 'destructive' \| 'destructive-rounded' \| 'ghost' \| 'ghost-rounded'` | `'default'` | Button style variant with optional rounded corners |
| `disabled` | `boolean` | `false` | Disable button interactions |
| `type` | `'button' \| 'submit' \| 'reset'` | `'button'` | HTML button type |
| `class` | `string` | `''` | Additional CSS classes |

### VerticalSlideButton Component

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `animationSpeed` | `'fast' \| 'medium' \| 'slow'` | `'fast'` | Animation speed: fast (1s), medium (2s), or slow (3s) |
| `color` | `string` | `'#000000'` | Text color |
| `hoverColor` | `string` | `'#666666'` | Text color on hover |
| `disabledColor` | `string` | `'#999999'` | Text color when disabled |
| `fontSize` | `string` | `'2rem'` | Font size |
| `fontWeight` | `number \| string` | `700` | Font weight |
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

Available types are exported from `HorizontalSlideButton/types`.

---

## 🔧 Customization

### Custom Colors

You can customize button colors by modifying CSS or using custom classes:

```svelte
<HorizontalSlideButton class="custom-button">Custom</HorizontalSlideButton>

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

For VerticalSlideButton, use props:

```svelte
<VerticalSlideButton 
  color="#your-color" 
  hoverColor="#your-hover-color"
  disabledColor="#your-disabled-color"
>
  Custom Colors
</VerticalSlideButton>
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
