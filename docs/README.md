# Accouter Framework Documentation

## Overview

This directory contains comprehensive technical documentation for the Accouter SCSS framework, covering architecture, implementation patterns, and development workflows.

## Documentation Index

### 🏗️ Architecture Documentation

#### [ARCHITECTURE.md](./ARCHITECTURE.md)
**Core Framework Architecture**
- Modern SCSS module system using `@use`/`@forward`
- Layered component architecture (ITCSS + Atomic Design)
- CSS custom properties system for dynamic theming
- Performance optimization and extensibility patterns
- Quality assurance and testing architecture

#### [THEMING-ARCHITECTURE.md](./THEMING-ARCHITECTURE.md)
**Advanced Theming System**
- HSL color decomposition for runtime theme manipulation
- CSS custom properties naming conventions and hierarchy
- Dynamic theme switching without recompilation
- Contextual and component-scoped theming strategies
- Browser support and progressive enhancement approaches

#### [BUILD-WORKFLOW-ARCHITECTURE.md](./BUILD-WORKFLOW-ARCHITECTURE.md)
**Build System & Development Workflow**
- Multi-stage compilation pipeline (SCSS → CSS → Documentation)
- Parallel development workflow with live reloading
- Nodemon-based file watching and automated rebuilds
- Testing integration with sass-true framework
- CI/CD pipeline integration and quality gates

## Key Architectural Highlights

### 🎨 **Hybrid CSS System**
Combines compile-time SCSS logic with runtime CSS custom properties for optimal performance and flexibility:

```scss
// Compile-time: SCSS functions and mixins
@function theme-color($name, $lightness: null) {
  @return hsl(var(--accouter-#{$name}-h), var(--accouter-#{$name}-s), $lightness or var(--accouter-#{$name}-l));
}

// Runtime: CSS custom properties for dynamic theming
:root {
  --accouter-primary-h: 220;
  --accouter-primary-s: 70%;  
  --accouter-primary-l: 55%;
}
```

### 🏗️ **Modular SCSS Architecture**
```
scss/
├── configs/      # Variables, functions, mixins (foundation)
├── themes/       # Color systems and variations
├── base/         # Resets and fundamental styles
├── elements/     # HTML element styling  
├── forms/        # Form component patterns
├── components/   # Complex UI components
├── grid/         # Layout system utilities
├── helpers/      # Utility classes
└── layouts/      # Page-level composition
```

### ⚡ **Parallel Development Workflow**
```bash
npm run watch    # Runs 4 parallel processes:
├── watch-scss      # SCSS → CSS compilation
├── watch-style     # CSS → Template integration  
├── watch-serve     # Documentation rebuild
└── watch-browser   # Live reload coordination
```

### 🧪 **Comprehensive Testing**
- **sass-true**: SCSS unit testing framework
- **Build validation**: Compilation must succeed
- **Documentation integration**: DocFX build validation
- **Quality gates**: Multi-level validation pipeline

## Framework Design Principles

### 1. **Modern CSS Architecture**
- Uses latest SCSS module system (`@use`/`@forward`)
- Avoids global namespace pollution
- Explicit dependency management
- Tree-shaking support through selective imports

### 2. **Runtime Customization**
- CSS custom properties for dynamic theming
- No recompilation needed for theme changes
- HSL color decomposition for advanced color manipulation
- Support for dark modes and high contrast themes

### 3. **Developer Experience Focus**
- Sophisticated build tooling with live reload
- Comprehensive documentation with live examples
- Unit testing for SCSS functions and mixins  
- Clear separation of concerns and consistent patterns

### 4. **Enterprise Scalability**
- Component-based architecture supporting large teams
- Extensible plugin system for custom components
- Performance optimization strategies
- CI/CD integration with quality gates

## Getting Started with Architecture

1. **Understanding the Framework**: Start with [ARCHITECTURE.md](./ARCHITECTURE.md)
2. **Implementing Themes**: Read [THEMING-ARCHITECTURE.md](./THEMING-ARCHITECTURE.md)  
3. **Development Workflow**: Follow [BUILD-WORKFLOW-ARCHITECTURE.md](./BUILD-WORKFLOW-ARCHITECTURE.md)
4. **Contributing**: See [CLAUDE.md](../CLAUDE.md) for development guidelines

## Advanced Topics

### Custom Component Development
Follow the established architectural patterns for creating new components:
- Place in appropriate `/scss/` subdirectory
- Use CSS custom properties for theming integration
- Follow naming conventions and dependency patterns
- Add comprehensive tests using sass-true

### Theme System Extension
Leverage the HSL decomposition system for advanced theming:
- Create semantic color mappings
- Implement contextual theme switching
- Support user preference integration
- Maintain performance optimization

### Build System Extension  
Extend the parallel build workflow for custom requirements:
- Add nodemon configurations for new file types
- Integrate additional processing steps
- Maintain parallel execution patterns
- Preserve live reload functionality

## Support and Contribution

This architecture documentation provides the technical foundation for:
- **Framework Contributors**: Understanding internal systems
- **Advanced Users**: Implementing custom extensions  
- **Enterprise Teams**: Planning adoption strategies
- **Developers**: Troubleshooting and optimization

For development guidelines and contribution patterns, see [CLAUDE.md](../CLAUDE.md).

---

**Framework Version**: 0.0.12  
**Documentation Status**: Comprehensive architectural coverage  
**Last Updated**: Architecture analysis and documentation generation