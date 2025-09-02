# Suggested Commands

## Development Commands

### Testing
```bash
npm test                    # Run SCSS unit tests (compiles test.scss)
```

### Building
```bash
npm run build              # Full build: SCSS compilation + minification
npm run build-scss         # Compile SCSS to CSS with source maps
npm run build-minify       # Minify CSS using cssnano
```

### Documentation
```bash
npm run docfx             # Build documentation site
npm run docfx-serve       # Build and serve documentation with live reload
npm start                 # Clean build + documentation generation
```

### Development Workflow
```bash
npm run watch             # Watch mode: auto-build on changes + serve docs + browser sync
npm run clean             # Clean all build artifacts (css/ and _site/ directories)
```

### Individual Watch Commands
```bash
npm run watch-scss        # Watch SCSS files and auto-build
npm run watch-style       # Watch for style changes and copy to templates
npm run watch-serve       # Watch and serve documentation
npm run watch-browser     # Start browser-sync server
```

## Utility Commands (Darwin/macOS)
- `ls -la` - List files with details
- `find . -name "*.scss"` - Find SCSS files
- `grep -r "pattern" scss/` - Search in SCSS directory
- `sass --watch input.scss output.css` - Watch single SCSS file

## Quality Assurance
When completing tasks, always run:
1. `npm run build` - Ensure SCSS compiles without errors
2. `npm test` - Run unit tests
3. `npm run docfx` - Verify documentation builds correctly