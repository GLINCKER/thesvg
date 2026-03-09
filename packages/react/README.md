<p align="center">
  <a href="https://github.com/GLINCKER/thesvg">
    <img src="https://raw.githubusercontent.com/GLINCKER/thesvg/main/public/og-image.png" alt="theSVG - 3,847 Brand SVG Icons" width="700" />
  </a>
</p>

# @thesvg/react

Typed React SVG components for all 3,800+ brand icons from [thesvg.org](https://thesvg.org).

- Zero runtime dependencies (React is a peer dep)
- TypeScript strict mode - full `SVGProps<SVGSVGElement>` support
- `forwardRef` on every component for imperative access
- Tree-shakeable ESM - import only what you use
- Individual icon imports for maximum bundle efficiency

## Installation

```bash
npm install @thesvg/react
# or
pnpm add @thesvg/react
# or
yarn add @thesvg/react
```

React 18 or later is required as a peer dependency.

## Usage

### Named import from barrel (convenient, relies on tree-shaking)

```tsx
import { Github, VisualStudioCode, Figma } from '@thesvg/react';

export function MyComponent() {
  return (
    <div>
      <Github width={24} height={24} />
      <VisualStudioCode width={24} height={24} className="text-blue-500" />
      <Figma width={32} height={32} aria-label="Figma" />
    </div>
  );
}
```

### Individual icon import (best for bundle size)

```tsx
import Github from '@thesvg/react/github';
import VisualStudioCode from '@thesvg/react/visual-studio-code';
```

Each icon is a separate module so bundlers that do not support tree-shaking
(e.g. CommonJS environments) will still include only the icons you import.

## Props

Every component accepts all standard SVG props via `SVGProps<SVGSVGElement>`:

| Prop        | Type     | Default                | Description                         |
|-------------|----------|------------------------|-------------------------------------|
| `width`     | `number \| string` | (SVG default) | Icon width                        |
| `height`    | `number \| string` | (SVG default) | Icon height                       |
| `className` | `string` | -                      | CSS class name                      |
| `style`     | `CSSProperties` | -            | Inline styles (prefer className)    |
| `fill`      | `string` | `"none"`               | SVG fill color                      |
| `viewBox`   | `string` | from original SVG      | Override the viewBox                |
| `ref`       | `Ref<SVGSVGElement>` | -          | Forwarded ref                       |
| `aria-label`| `string` | -                      | Accessible label                    |
| ...         | ...      | -                      | Any other `SVGProps<SVGSVGElement>`  |

### Sizing example

```tsx
// Fixed size
<Github width={24} height={24} />

// Responsive via CSS
<Github className="w-6 h-6" />

// Scale with font-size (em units)
<Github width="1em" height="1em" />
```

### Forwarded refs

```tsx
import { useRef } from 'react';
import Github from '@thesvg/react/github';

function MyComponent() {
  const svgRef = useRef<SVGSVGElement>(null);
  return <Github ref={svgRef} width={24} height={24} />;
}
```

### Accessibility

Add `aria-label` or wrap in a `<span>` with an `aria-label` for decorative vs
meaningful icons:

```tsx
// Meaningful icon - label it
<Github aria-label="GitHub" role="img" width={24} height={24} />

// Decorative icon - hide from screen readers
<Github aria-hidden="true" width={24} height={24} />
```

## Component names

Slugs are converted to PascalCase component names:

| Slug                  | Component name         |
|-----------------------|------------------------|
| `github`              | `Github`               |
| `visual-studio-code`  | `VisualStudioCode`     |
| `figma`               | `Figma`                |
| `01dotai`             | `I01Dotai`             |
| `dotnet`              | `Dotnet`               |

Slugs that start with a digit are prefixed with `I` to produce a valid
JavaScript identifier.

## Tree-shaking

When using a bundler with ESM tree-shaking support (Webpack 5, Rollup, Vite,
esbuild), named imports from the barrel (`@thesvg/react`) are tree-shaken
automatically - only the icons you import are included in the final bundle.

For bundlers without tree-shaking support (plain Node.js CJS, older tools),
use individual icon imports instead:

```tsx
// Always tree-shaken regardless of bundler
import Github from '@thesvg/react/github';
```

## Available icons

Over 3,800 brand icons are available. Browse the full list at
[thesvg.org](https://thesvg.org).

## License

MIT - see [LICENSE](./LICENSE).

Brand icons and logos are the property of their respective trademark holders. See [thesvg.org](https://thesvg.org) for details.
