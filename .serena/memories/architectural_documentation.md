# Architectural Documentation Index

## Comprehensive Architecture Documentation

The Accouter framework includes detailed architectural documentation covering all major system components:

### Core Architecture Documents

1. **ARCHITECTURE.md** - Complete architectural overview
   - Overall architectural principles and patterns
   - SCSS module architecture and dependency hierarchy
   - CSS custom properties and theming system
   - Component architecture patterns (ITCSS, Atomic Design)
   - Performance and extensibility architecture
   - Quality assurance and testing architecture

2. **THEMING-ARCHITECTURE.md** - Advanced theming system
   - HSL color decomposition for dynamic theming
   - CSS custom properties architecture
   - Runtime theme switching capabilities
   - Theme validation and performance considerations
   - Browser support and progressive enhancement strategies

3. **BUILD-WORKFLOW-ARCHITECTURE.md** - Build system and development workflow
   - Multi-stage compilation pipeline
   - Parallel development workflow with live reloading
   - Nodemon configuration and file watching strategies
   - Testing integration with sass-true
   - CI/CD integration and quality gates

### Key Architectural Insights

#### Modern SCSS Architecture
- Uses `@use`/`@forward` directives avoiding global namespace pollution
- Explicit dependency management with controlled namespacing
- Layered component architecture following ITCSS principles

#### Hybrid CSS System
- Compile-time SCSS logic for build-time optimizations
- Runtime CSS custom properties for dynamic theming
- HSL color decomposition enabling advanced theming features

#### Enterprise-Grade Tooling
- Sophisticated build pipeline with parallel processing
- Comprehensive testing with sass-true integration
- Living documentation system with DocFX integration
- Multi-device development with browser-sync coordination

#### Quality Assurance
- Multi-level validation (build, test, documentation, style)
- Continuous integration pipeline support
- Performance optimization strategies
- Extensibility patterns for plugin development

### Usage Guidance

These architectural documents provide deep technical insights for:
- **Framework contributors** understanding internal architecture
- **Advanced users** implementing custom extensions
- **Teams** planning enterprise adoption
- **Developers** troubleshooting complex issues

All architectural documentation is located in the `/docs/` directory and should be consulted for advanced framework usage and customization.