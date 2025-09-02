# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Accouter** is a semantic, open-source administrative template framework built with SCSS. It provides pre-built components for creating professional administrative interfaces with responsive design and modern CSS3 features.

## Essential Commands

### Development Workflow
```bash
npm run watch           # Full development mode: auto-build SCSS + serve docs + browser-sync
npm run build          # Compile SCSS to CSS and minify
npm test               # Run SCSS unit tests
npm run docfx-serve    # Build and serve documentation with live reload
```

### Build Commands
```bash
npm run build-scss     # Compile SCSS to CSS with source maps
npm run build-minify   # Minify CSS using cssnano
npm run clean          # Remove build artifacts (css/ and _site/ directories)
```

### Documentation
```bash
npm run docfx          # Build documentation site
npm start              # Clean + build + generate documentation
```

## Architecture

### SCSS Module System
The project uses modern SCSS architecture with `@use` and `@forward`:

```
accouter.scss (entry point)
└── scss/_index.scss
    ├── configs/     # Variables, functions, mixins
    ├── themes/      # Color themes and variations  
    ├── base/        # CSS resets and foundation
    ├── elements/    # HTML element styles
    ├── forms/       # Form components
    ├── components/  # UI components (cards, modals, etc.)
    ├── grid/        # Layout grid system
    ├── helpers/     # Utility classes
    └── layouts/     # Page layout templates
```

### Key Architectural Patterns
- **CSS Custom Properties**: Extensive use of CSS variables with `--{prefix}-{property}` naming
- **Utility Functions**: `buildVar()`, `getVar()`, `buildHsla()` for CSS variable management
- **Modular Imports**: Each directory has `_index.scss` using `@forward` for clean imports
- **Component-based Organization**: Logical separation by UI concern

## Code Style

### SCSS Conventions
- **Indentation**: 2 spaces
- **Quotes**: Double quotes preferred  
- **Max line length**: 120 characters
- **Property ordering**: Defined order (font → position → display → box model → styling)
- **File naming**: Kebab-case (e.g., `variables-init.scss`)

### CSS Variable Naming
```scss
--accouter-component-property     # Standard format
--accouter-button-bg-color       # Example
```

## Testing

### Unit Tests
- **Framework**: sass-true (`npm test` runs SCSS compilation tests)
- **Location**: `/test/` directory
- **Pattern**: Use `@include test-module()` and `@include test()` blocks

### Test Example
```scss
@include test-module('Component [function]') {
  @include test('Description of test') {
    @include assert-equal(actual, expected);
  }
}
```

## Task Completion Checklist

When completing any development task:

1. **Build validation**: `npm run build` (must complete without errors)
2. **Test validation**: `npm test` (SCSS syntax and unit tests)  
3. **Documentation**: `npm run docfx` (ensure docs build correctly)

For new components:
- Place in appropriate `/scss/` subdirectory
- Update corresponding `_index.scss` with `@forward` statement
- Follow established naming and architectural patterns
- Add unit tests in `/test/` directory if creating functions/mixins

## Development Notes

- **Main entry**: `accouter.scss` imports everything via `scss/_index.scss`
- **Build outputs**: `/css/accouter.css` (expanded) and `/css/accouter.min.css` (minified)
- **Documentation**: Uses DocFX with custom templates in `/templates/accouter/`
- **Browser support**: See the project's [browserslist configuration](./package.json) for full details. Minimum supported versions:
  - Chrome 90+
  - Firefox 88+
  - Edge 90+
  - Safari 14+
  - (or any browser supporting CSS3 flexbox, grid, and custom properties)