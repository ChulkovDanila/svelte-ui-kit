# Svelte UI Kit

<div align="center">

**Beautiful animated button component for Svelte with slide and arc animations**

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

### Method 1: Copy Component (Recommended - Like shadcn/ui)

This method gives you full control over the component code, just like shadcn/ui. You copy the components directly into your project and can customize them as needed.

1. **Copy the Button component** to your project:

```bash
# Create components directory in your SvelteKit project
mkdir -p src/lib/components/ui

# Copy Button component files
cp -r node_modules/svelte-ui-kit/src/lib/components/Button src/lib/components/ui/
```

Or manually copy the following files:
- `src/lib/components/Button/Button.svelte`
- `src/lib/components/Button/index.ts`

2. **Copy utility functions**:

```bash
# Copy cn utility
cp node_modules/svelte-ui-kit/src/lib/utils/cn.ts src/lib/utils/
```

3. **Copy types** (if using TypeScript):

```bash
# Copy types
cp node_modules/svelte-ui-kit/src/lib/types/index.ts src/lib/types/
```

4. **Install the package** (for types and utilities):

```bash
npm install svelte-ui-kit
```

### Method 2: Direct Import (Standard npm package)

For quick setup without customization, you can import components directly from the package.

```bash
npm install svelte-ui-kit
```

```svelte
<script>
  import { Button } from 'svelte-ui-kit';
</script>

<Button>Click me</Button>
```

---

## 🚀 Quick Start

### Basic Usage

```svelte
<script>
  import { Button } from '$lib/components/ui/Button';
</script>

<Button>Click me</Button>
```

### With Animation Type

```svelte
<script>
  import { Button } from '$lib/components/ui/Button';
</script>

<!-- Slide Animation (horizontal) -->
<Button animationType="slide">Get Started</Button>

<!-- Arc Animation (curved) -->
<Button animationType="arc">Discover</Button>
```

### With Animation Speed

```svelte
<script>
  import { Button } from '$lib/components/ui/Button';
</script>

<Button animationSpeed="fast">Fast Animation</Button>
<Button animationSpeed="medium">Medium Animation</Button>
<Button animationSpeed="slow">Slow Animation</Button>
```

### Button Variants

```svelte
<script>
  import { Button } from '$lib/components/ui/Button';
</script>

<Button variant="default">Default</Button>
<Button variant="outline">Outline</Button>
<Button variant="destructive">Delete</Button>
<Button variant="ghost">Cancel</Button>
```

### Rounded Buttons

```svelte
<script>
  import { Button } from '$lib/components/ui/Button';
</script>

<Button rounded>Rounded Button</Button>
```

### Complete Example

```svelte
<script>
  import { Button } from '$lib/components/ui/Button';
</script>

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

```svelte
<Button animationType="slide">Click me</Button>
```

**GitHub Search Keywords**: `slide animation button`, `horizontal animation button`

### Arc Animation  
Curved movement with rotation - text moves in a semicircle path with rotation effect.

```svelte
<Button animationType="arc">Discover</Button>
```

**GitHub Search Keywords**: `arc animation button`, `curved animation button`

---

## 🎯 Examples

### Different Variants

```svelte
<div class="button-group">
  <Button variant="default">Primary</Button>
  <Button variant="outline">Secondary</Button>
  <Button variant="destructive">Delete</Button>
  <Button variant="ghost">Cancel</Button>
</div>
```

### Different Speeds

```svelte
<div class="button-group">
  <Button animationSpeed="fast">Fast</Button>
  <Button animationSpeed="medium">Medium</Button>
  <Button animationSpeed="slow">Slow</Button>
</div>
```

### Combined Options

```svelte
<Button 
  animationType="arc" 
  animationSpeed="slow" 
  variant="outline" 
  rounded
  class="my-custom-class"
>
  Custom Button
</Button>
```

---

## 🔧 Customization

### Custom Colors

You can customize button colors by modifying the CSS variables or directly editing the component styles:

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

## 📚 TypeScript Types

```typescript
import type { ButtonVariant, ButtonAnimationType } from 'svelte-ui-kit';

// Use types in your code
const variant: ButtonVariant = 'outline';
const animationType: ButtonAnimationType = 'slide';
```

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

## 📹 Demo Videos

Watch our animated button components in action! See all variants and animations in high quality video demonstrations.

### Watch the Showcases

- 🎬 **[Slide Animation Showcase](./videoshowcase/Showcase1.mp4)** - Smooth horizontal text movement
- 🎬 **[Arc Animation Showcase](./videoshowcase/Showcase2.mp4)** - Beautiful curved movement with rotation

*Click the links above to watch the videos in your browser.*

**More details:** See the [SHOWCASE.md](./SHOWCASE.md) document for complete information about what's demonstrated in each video.

---

## 📄 License

MIT License - feel free to use in your projects!

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

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
