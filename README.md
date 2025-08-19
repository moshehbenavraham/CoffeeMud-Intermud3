# CoffeeMud Intermud3 Extraction

A comprehensive extraction of the Intermud3 system from the CoffeeMud codebase, creating a standalone multi-protocol inter-MUD communication framework.

## Overview

This project extracts the complete Intermud communication system from CoffeeMud, which includes support for multiple protocols:

- **Intermud 3 (I3)** - The primary intermud protocol with full router capability
- **IMC2** - Inter-MUD Chat version 2 (legacy support)
- **CM1** - CoffeeMud's proprietary protocol
- **Discord** - Modern Discord bot integration
- **Grapevine** - Modern intermud network protocol

## Status

🚧 **Work in Progress** - Currently extracting and refactoring the codebase for standalone use.

## Architecture

The system consists of approximately 150+ files organized as follows:

### Core Components
- **I3 Protocol**: ~50 files including packets, entities, network layer, persistence, router, and server
- **IMC2 Protocol**: 7 files for legacy IMC2 support
- **CM1 Protocol**: 20 files for CoffeeMud's proprietary protocol
- **Modern Integrations**: Discord and Grapevine client implementations
- **Main Interface**: Central IntermudInterface and IntermudClient managing all protocols

### Key Features
- Full I3 router capability (can act as an I3 router for other MUDs)
- 40+ I3 packet types supported
- Bridge pattern for clean protocol separation
- Minimal external dependencies
- Thread-safe concurrent connection handling
- Persistence layer for I3 data
- Channel system integration

## Project Structure

```
/src/main/java/        - Main source code
/src/test/java/        - Test code
/config/               - Configuration files
/lib/                  - External dependencies
/docs/                 - Documentation
PLAN.md               - Detailed extraction plan
```

## Extraction Plan

See [PLAN.md](PLAN.md) for the complete extraction and refactoring plan.

## Original Source

This code is extracted from [CoffeeMud](https://github.com/bozimmerman/CoffeeMud), a powerful and feature-rich MUD engine.

## License

Apache License 2.0 (inherited from CoffeeMud)

## Contributing

This is currently a work in progress. Contributions will be welcome once the initial extraction is complete.