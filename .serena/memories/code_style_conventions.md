# Code Style and Conventions

## SCSS/CSS Conventions (from .editorconfig)
- **Indentation**: 2 spaces for SCSS files
- **Line endings**: LF (Unix style)
- **Charset**: UTF-8
- **Max line length**: 120 characters
- **Quote style**: Double quotes preferred
- **Property ordering**: Specific order defined (font → position → display → box model → styling)

## File Organization
- **Module System**: Uses modern SCSS `@use` and `@forward` directives
- **Directory Structure**:
  - `/scss/configs/` - Variables, functions, mixins, extends
  - `/scss/base/` - Base styles and resets
  - `/scss/elements/` - HTML element styles
  - `/scss/forms/` - Form components
  - `/scss/components/` - UI components
  - `/scss/grid/` - Grid system
  - `/scss/helpers/` - Utility classes
  - `/scss/layouts/` - Layout components
  - `/scss/themes/` - Theme variations

## Naming Conventions
- **CSS Variables**: `--{prefix}-{component}-{property}` format
- **Functions**: Camel case (e.g., `buildVar`, `getVar`, `buildHsla`)
- **Mixins**: Kebab case with descriptive names (e.g., `register-var`, `register-vars`)
- **File naming**: Kebab case with descriptive names

## SCSS Architecture Patterns
- **CSS Custom Properties**: Heavy use of CSS variables for theming
- **Function-based**: Utility functions for variable management (`buildVar`, `getVar`)
- **Modular imports**: Each directory has an `_index.scss` file for clean imports
- **Forward pattern**: Root `accouter.scss` uses `@use "scss"` which forwards all modules

## Testing Conventions
- **Test files**: Located in `/test/` directory
- **Naming**: `*.scss` files in test directory
- **Framework**: Uses sass-true for unit testing
- **Test structure**: `@include test-module()` and `@include test()` blocks