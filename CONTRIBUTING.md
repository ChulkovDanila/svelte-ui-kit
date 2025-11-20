# Contributing Guide

Thank you for your interest in contributing! We welcome all contributions.

## How to Contribute

1. **Fork** the repository
2. Create a **branch** for your feature (`git checkout -b feature/AmazingComponent`)
3. **Commit** your changes (`git commit -m 'Add some AmazingComponent'`)
4. **Push** to the branch (`git push origin feature/AmazingComponent`)
5. Open a **Pull Request**

## Development Guidelines

### Component Structure

Each new component should follow this structure:

```
ComponentName/
  ├── ComponentName.svelte    # Main component
  ├── ComponentName.spec.ts   # Component tests
  ├── index.ts                # Component export
  ├── types.ts                # TypeScript types (optional)
  └── README.md               # Documentation (optional)
```

### Code Style

- Use TypeScript for all components
- Follow the project's code style (ESLint + Prettier)
- Add comments for complex code sections
- Write tests for new components

### Commits

Use clear commit messages:
- `feat: add Button component`
- `fix: fix error in Card component`
- `docs: update documentation`
- `style: format code`

## Testing

Before submitting a Pull Request, make sure:
- All tests pass (`npm run test`)
- Code passes linter checks (`npm run lint`)
- Code is formatted (`npm run format`)

## Questions?

If you have questions, please create an issue in the repository.
