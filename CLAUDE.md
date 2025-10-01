# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a LoopBack 4 application - a TypeScript/Node.js REST API framework. The application follows the standard LoopBack 4 architecture with dependency injection, decorators, and a component-based structure.

## Architecture

### Core Application Structure

- **Application Class** (`src/application.ts`): `StarterApplication` extends multiple mixins (Boot, Service, Repository, Rest) to provide a full-featured REST API server
- **Request Sequence** (`src/sequence.ts`): `MySequence` extends `MiddlewareSequence` and handles the request/response lifecycle
- **Entry Point** (`src/index.ts`): Configures and starts the server on port 3000 (default) with the REST server at `http://127.0.0.1:3000`

### Key Directories

- `src/controllers/`: REST endpoint handlers (auto-discovered via boot conventions)
- `src/models/`: Domain model definitions
- `src/repositories/`: Data access layer
- `src/datasources/`: Database connection configurations
- `src/__tests__/acceptance/`: End-to-end API tests

### LoopBack 4 Patterns

The application uses LoopBack's boot conventions:
- Controllers are auto-discovered from `src/controllers/` with `.controller.js` extension (after compilation)
- The REST Explorer (API documentation) is available at `/explorer`
- Static files are served from `public/` directory at root path `/`

## Essential Commands

### Building
```bash
yarn build              # Compile TypeScript
yarn build:watch        # Compile in watch mode
yarn rebuild            # Clean and build from scratch
yarn clean              # Remove compiled files
```

### Running
```bash
yarn start              # Rebuild and start server
node .                  # Start without rebuilding (faster)
```

### Testing
```bash
yarn test               # Run full test suite (rebuilds, tests, then lints)
yarn test:dev           # Run tests and lint (for development iteration)
```

Tests are run with Mocha and located in `dist/__tests__/**/*.js` after compilation.

### Linting
```bash
yarn lint               # Run ESLint and Prettier checks
yarn lint:fix           # Auto-fix linting and formatting issues
```

### Other Commands
```bash
yarn migrate            # Run database migrations
yarn openapi-spec       # Generate OpenAPI specification file
```

## Development Workflow

1. **TypeScript Compilation**: Source files in `src/` compile to `dist/`. The application runs from compiled JavaScript.
2. **Adding Controllers**: Create `*.controller.ts` files in `src/controllers/` - they are auto-discovered on boot
3. **Adding Models**: Create model classes in `src/models/`
4. **Adding Repositories**: Create repository classes in `src/repositories/`
5. **Testing**: Write acceptance tests in `src/__tests__/acceptance/` using the test helper

## Node Version

Requires Node.js 20, 22, or 24