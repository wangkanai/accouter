# Theming Architecture

## Overview

Accouter's theming system is built on a sophisticated CSS custom properties architecture that enables runtime theme customization without SCSS recompilation. This hybrid approach combines compile-time SCSS logic with runtime CSS flexibility.

## Core Theming Concepts

### 1. HSL Color Decomposition

Colors are decomposed into separate HSL components for maximum flexibility:

```scss
// Traditional approach (static)
$primary-color: #3498db;

// Accouter approach (dynamic)
--accouter-primary-h: 211;        // Hue: blue
--accouter-primary-s: 70%;        // Saturation: vibrant
--accouter-primary-l: 55%;        // Lightness: medium

// Runtime color generation
.button-primary {
  background-color: hsl(
    var(--accouter-primary-h),
    var(--accouter-primary-s), 
    var(--accouter-primary-l)
  );
}
```

### 2. Dynamic Color Variations

Generate color variations by manipulating individual components:

```css
/* Base color */
--accouter-primary-l: 55%;

/* Automatic variations */
.button-primary { 
  background: hsl(var(--accouter-primary-h), var(--accouter-primary-s), var(--accouter-primary-l));
}

.button-primary:hover { 
  background: hsl(var(--accouter-primary-h), var(--accouter-primary-s), calc(var(--accouter-primary-l) - 10%));
}

.button-primary:active { 
  background: hsl(var(--accouter-primary-h), var(--accouter-primary-s), calc(var(--accouter-primary-l) - 20%));
}
```

## Theme System Architecture

### Variable Naming Convention

```scss
--{prefix}-{component}-{property}-{modifier}

// Examples:
--accouter-button-bg-color-h           // Button background hue
--accouter-button-bg-color-s           // Button background saturation  
--accouter-button-bg-color-l           // Button background lightness
--accouter-text-primary-color-h        // Primary text hue
--accouter-border-default-color-l      // Default border lightness
```

### Theme Layer Hierarchy

```scss
// 1. System defaults (configs/variables-init.scss)
$system-primary-hue: 220 !default;
$system-primary-saturation: 70% !default;  
$system-primary-lightness: 50% !default;

// 2. Theme variations (themes/)
:root {
  --accouter-primary-h: #{$system-primary-hue};
  --accouter-primary-s: #{$system-primary-saturation};
  --accouter-primary-l: #{$system-primary-lightness};
}

// 3. Component implementations (components/)
.button {
  background: hsl(var(--accouter-primary-h), var(--accouter-primary-s), var(--accouter-primary-l));
}

// 4. User overrides (runtime)
:root {
  --accouter-primary-h: 340;  // Change to pink theme
}
```

## Advanced Theming Features

### 1. Contextual Theme Switching

```css
/* Default theme */
:root {
  --accouter-bg-l: 98%;
  --accouter-text-l: 15%;
}

/* Dark theme context */
[data-theme="dark"] {
  --accouter-bg-l: 8%;
  --accouter-text-l: 85%;
}

/* High contrast theme */  
[data-theme="high-contrast"] {
  --accouter-bg-l: 0%;
  --accouter-text-l: 100%;
  --accouter-primary-s: 100%;
}
```

### 2. Component-Scoped Theming

```css
/* Global theme */
:root {
  --accouter-primary-h: 220;
}

/* Component-specific override */
.marketing-section {
  --accouter-primary-h: 340;  /* Pink for marketing */
}

.dashboard-area {
  --accouter-primary-h: 120;  /* Green for dashboard */
}
```

### 3. Responsive Theme Adaptation

```css
:root {
  --accouter-text-size-base: 16px;
  --accouter-spacing-unit: 8px;
}

@media (max-width: 768px) {
  :root {
    --accouter-text-size-base: 14px;
    --accouter-spacing-unit: 6px;
  }
}

@media (prefers-reduced-motion) {
  :root {
    --accouter-transition-duration: 0s;
  }
}
```

## Theme Implementation Patterns

### 1. Color System Functions

```scss
// Generate color with custom lightness
@function theme-color($name, $lightness: null, $alpha: 1) {
  $l: if($lightness, $lightness, getVar($name, "", "-l"));
  @return hsla(#{getVar($name, "", "-h")}, #{getVar($name, "", "-s")}, #{$l}, #{$alpha});
}

// Usage in components
.alert-success {
  background: theme-color("success", 95%);
  border-color: theme-color("success", 60%);
  color: theme-color("success", 20%);
}
```

### 2. Semantic Color Mapping

```scss
// Abstract color definitions
:root {
  --accouter-blue-h: 220;
  --accouter-blue-s: 70%;
  --accouter-blue-l: 55%;
  
  --accouter-green-h: 120;
  --accouter-green-s: 60%;
  --accouter-green-l: 45%;
}

// Semantic mappings
:root {
  --accouter-primary-h: var(--accouter-blue-h);
  --accouter-primary-s: var(--accouter-blue-s);
  --accouter-primary-l: var(--accouter-blue-l);
  
  --accouter-success-h: var(--accouter-green-h);
  --accouter-success-s: var(--accouter-green-s);
  --accouter-success-l: var(--accouter-green-l);
}
```

### 3. Theme Validation

```scss
@function validate-theme-color($name) {
  $h: var(--accouter-#{$name}-h);
  $s: var(--accouter-#{$name}-s);  
  $l: var(--accouter-#{$name}-l);
  
  @if not $h or not $s or not $l {
    @error "Theme color '#{$name}' is missing required HSL components";
  }
  
  @return hsl($h, $s, $l);
}
```

## Theme Customization Strategies

### 1. Build-Time Theme Generation

```scss
// Generate multiple theme files at build time
$themes: (
  "default": (primary-h: 220, primary-s: 70%, primary-l: 55%),
  "brand-red": (primary-h: 0, primary-s: 75%, primary-l: 50%),  
  "brand-green": (primary-h: 120, primary-s: 65%, primary-l: 45%)
);

@each $theme-name, $theme-config in $themes {
  .theme-#{$theme-name} {
    @each $prop, $value in $theme-config {
      --accouter-#{$prop}: #{$value};
    }
  }
}
```

### 2. Runtime Theme Switching

```javascript
// JavaScript theme controller
const ThemeController = {
  setTheme(themeName) {
    const themes = {
      light: { 'bg-l': '98%', 'text-l': '15%' },
      dark: { 'bg-l': '8%', 'text-l': '85%' },
      blue: { 'primary-h': '220' },
      red: { 'primary-h': '0' }
    };
    
    const theme = themes[themeName];
    Object.entries(theme).forEach(([prop, value]) => {
      document.documentElement.style.setProperty(`--accouter-${prop}`, value);
    });
  }
};
```

### 3. User Preference Integration

```css
/* System preference detection */
@media (prefers-color-scheme: dark) {
  :root {
    --accouter-bg-l: 8%;
    --accouter-text-l: 85%;
  }
}

@media (prefers-contrast: high) {
  :root {
    --accouter-border-width: 2px;
    --accouter-outline-width: 3px;
  }
}

@media (prefers-reduced-motion: reduce) {
  :root {
    --accouter-transition-duration: 0.01ms;
    --accouter-animation-duration: 0.01ms;
  }
}
```

## Performance Considerations

### 1. CSS Custom Property Optimization

- **Inheritance**: Use CSS cascade to minimize property redefinition
- **Scoping**: Apply theme properties only where needed
- **Fallbacks**: Provide fallback values for unsupported browsers

```css
/* Optimized inheritance */
:root {
  --accouter-text-color: hsl(var(--accouter-text-h, 0), var(--accouter-text-s, 0%), var(--accouter-text-l, 15%));
}

.component {
  color: var(--accouter-text-color);  /* Inherits from :root */
}
```

### 2. Theme Bundle Splitting

```scss
// Core theme (always loaded)
@use "themes/core";

// Optional theme extensions (conditionally loaded)
@use "themes/extensions/dark" if $enable-dark-theme;
@use "themes/extensions/high-contrast" if $enable-high-contrast;
@use "themes/extensions/brand" if $enable-brand-themes;
```

## Browser Support Strategy

### Progressive Enhancement Approach

```css
/* Fallback for older browsers */
.button {
  background-color: #3498db;  /* Static fallback */
  background-color: hsl(var(--accouter-primary-h, 211), var(--accouter-primary-s, 70%), var(--accouter-primary-l, 55%));
}

/* Feature detection */
@supports (color: hsl(var(--custom))) {
  .button {
    /* Advanced theming for supporting browsers */
  }
}
```

## Testing Theme Architecture

### 1. Theme Validation Tests

```scss
@include test-module('Theme System') {
  @include test('Should generate valid HSL colors') {
    $result: theme-color("primary");
    @include assert-equal(type-of($result), "color");
  }
  
  @include test('Should handle lightness variations') {
    $light: theme-color("primary", 80%);
    $dark: theme-color("primary", 20%);
    @include assert-not-equal($light, $dark);
  }
}
```

### 2. Runtime Theme Testing

```javascript
// Automated theme testing
describe('Theme System', () => {
  test('should switch themes correctly', () => {
    ThemeController.setTheme('dark');
    const bgColor = getComputedStyle(document.documentElement)
      .getPropertyValue('--accouter-bg-l');
    expect(bgColor.trim()).toBe('8%');
  });
});
```

## Future Considerations

### 1. CSS Color Level 4 Integration

```css
/* Future: Advanced color spaces */
:root {
  --accouter-primary: oklch(65% 0.15 220);  /* OKLCH color space */
}

/* Future: Relative color syntax */
:root {
  --accouter-primary-hover: from var(--accouter-primary) oklch(calc(l - 0.1) c h);
}
```

### 2. Theme Animation Support

```css
/* Smooth theme transitions */
* {
  transition: 
    background-color var(--accouter-theme-transition-duration, 200ms),
    color var(--accouter-theme-transition-duration, 200ms),
    border-color var(--accouter-theme-transition-duration, 200ms);
}
```

The theming architecture provides a robust foundation for dynamic, accessible, and maintainable color systems while maintaining excellent performance and developer experience.