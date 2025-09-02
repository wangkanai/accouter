# Task Completion Checklist

When completing any task in the Accouter project, follow these validation steps:

## Build Validation
1. **Compile SCSS**: Run `npm run build` to ensure all SCSS compiles without errors
2. **Test syntax**: Run `npm test` to validate SCSS syntax and run unit tests
3. **Documentation**: Run `npm run docfx` to ensure documentation builds correctly

## Code Quality Checks
- Verify SCSS follows `.editorconfig` conventions (2 spaces, double quotes, property ordering)
- Ensure new components follow the modular architecture pattern
- Check that CSS custom properties use the established naming convention
- Validate responsive design works across breakpoints

## File Organization
- Place new components in appropriate `/scss/` subdirectory
- Update corresponding `_index.scss` files with `@forward` statements
- Ensure new test files go in `/test/` directory
- Follow kebab-case naming for new files

## Testing Requirements
- Add unit tests for new functions using sass-true framework
- Test color functions and mixins with `@include assert-equal()`
- Validate CSS output matches expected values

## Documentation
- Add component examples to documentation if creating new components
- Update relevant markdown files in `/docs/` directory
- Ensure DocFX can build and serve the updated documentation

## Final Verification
Run the complete development pipeline:
```bash
npm run clean    # Clean previous builds
npm run build    # Full compilation
npm test         # Run tests  
npm run docfx    # Build documentation
```

All commands should complete without errors before considering the task complete.