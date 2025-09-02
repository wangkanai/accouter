# Codebase Structure

## Root Level
- `accouter.scss` - Main entry point, imports all SCSS modules
- `package.json` - npm package configuration and scripts
- `docfx.json` - Documentation generation configuration
- `test.scss` - Test entry point for sass-true testing

## Core Directories

### `/scss/` - Main SCSS source code
- `_index.scss` - Central import file using @forward directives
- **Architecture follows modular pattern with 9 subdirectories:**

#### `/scss/configs/` - Configuration layer
- Variables (init, derived, SCSS-specific)
- Functions and mixins
- Control configurations
- Extends/placeholders

#### `/scss/base/` - Foundation styles
- CSS resets and base element styles
- Typography fundamentals

#### `/scss/elements/` - HTML element styles
- Styled HTML elements (buttons, inputs, etc.)

#### `/scss/forms/` - Form components
- Form controls and form layout components

#### `/scss/components/` - UI components
- Reusable interface components
- Cards, modals, navigation, etc.

#### `/scss/grid/` - Grid system
- Layout grid implementation
- Responsive utilities

#### `/scss/helpers/` - Utility classes
- Helper classes and utility functions

#### `/scss/layouts/` - Layout templates
- Page layout components and patterns

#### `/scss/themes/` - Theme variations
- Color themes and style variations

### `/test/` - Test files
- `array.scss` - Example unit tests using sass-true
- Uses BDD-style testing with `@include test-module()` and `@include test()`

### `/templates/` - Documentation templates
- Custom DocFX templates for documentation site

### `/docs/` - Documentation source
- Markdown files for documentation content

### Build Outputs (Generated)
- `/css/` - Compiled CSS output (created by build process)
- `/_site/` - Generated documentation site (created by docfx)

## Import Hierarchy
```
accouter.scss
└── @use "scss" (scss/_index.scss)
    ├── @forward "configs"
    ├── @forward "themes" 
    ├── @forward "base"
    ├── @forward "elements"
    ├── @forward "forms"
    ├── @forward "components"
    ├── @forward "grid"
    ├── @forward "helpers"
    └── @forward "layouts"
```