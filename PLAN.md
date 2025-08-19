# Intermud3 System Extraction Plan

## Overview
The CoffeeMud Intermud3 system is a comprehensive multi-protocol inter-MUD communication framework supporting I3, IMC2, CM1, Discord, and Grapevine protocols. This plan will extract it as a standalone system.

## Phase 1: Core Extraction Structure
1. **Create base project structure**:
   - `/src/main/java/` - Main source code
   - `/src/test/java/` - Test code  
   - `/config/` - Configuration files
   - `/lib/` - External dependencies
   - `/docs/` - Documentation
   - `pom.xml` or `build.gradle` - Build configuration
   - `README.md` - Project documentation
   - `LICENSE` - Apache 2.0 license

## Phase 2: Identify and Extract Core Components

### 2.1 Extract Intermud3 (I3) Implementation
- **Core I3 files** (~50 files):
  - `/i3/` - Main I3 implementation
  - `/i3/entities/` - Channel, MudList, NameServer entities
  - `/i3/net/` - Network layer (ListenThread, NetPeer, etc.)
  - `/i3/packets/` - 40+ packet types
  - `/i3/persist/` - Persistence layer
  - `/i3/router/` - I3 router capability
  - `/i3/server/` - I3 server components

### 2.2 Extract Supporting Protocols
- **IMC2 Protocol** (~7 files)
- **CM1 Protocol** (~20 files)
- **Discord Client** (1 file)
- **Grapevine Client** (1 file)

### 2.3 Extract Interfaces and Main Client
- `IntermudInterface.java` - Main interface
- `IntermudClient.java` - Main implementation
- Bridge classes for each protocol

## Phase 3: Decouple CoffeeMud Dependencies

### 3.1 Replace CoffeeMud Core Dependencies
- Replace `CMLib` calls with standalone implementations
- Extract needed utilities from `com.planet_ink.coffee_mud.core.*`:
  - CMStrings (string utilities)
  - CMath (math utilities)
  - CMParms (parameter parsing)
  - Log (logging)
  - CMSecurity (security checks)
  - CMProps (properties)

### 3.2 Create Abstraction Layer
- Create interfaces for:
  - `MudSystemInterface` - Replace MOB, Room, Area dependencies
  - `ChannelSystemInterface` - Replace ChannelsLibrary
  - `SecurityInterface` - Replace CMSecurity
  - `ConfigurationInterface` - Replace CMProps
  - `LoggingInterface` - Replace Log

### 3.3 Implement Default Providers
- Simple implementations of abstraction interfaces
- Configuration file reader
- Basic logging system
- Simple channel management

## Phase 4: Create Standalone Application

### 4.1 Main Application Components
- `Intermud3Application.java` - Main entry point
- `Intermud3Server.java` - Standalone server
- `Intermud3Client.java` - Client implementation
- `Intermud3Router.java` - Router capability

### 4.2 Configuration System
- `intermud3.properties` - Main configuration
- Support for:
  - I3 router addresses and ports
  - IMC2 hub configuration
  - CM1 server settings
  - Discord bot token
  - Grapevine credentials

## Phase 5: Build and Package System

### 5.1 Build Configuration
- Maven or Gradle build
- Dependencies:
  - Java 8+ compatibility
  - Minimal external dependencies
  - Optional: Discord JDA library
  - Optional: JSON library for Grapevine

### 5.2 Distribution Package
- Standalone JAR with all dependencies
- Example configuration files
- Documentation and examples
- Docker container option

## Phase 6: Testing and Documentation

### 6.1 Create Test Suite
- Unit tests for packet parsing
- Integration tests for protocol communication
- Mock implementations for testing

### 6.2 Documentation
- API documentation
- Integration guide
- Protocol specifications
- Example implementations

## Implementation Steps

1. **Copy all intermud files** from `/COFFEEMUD/com/planet_ink/coffee_mud/Libraries/intermud/` to new project
2. **Copy interface** from `/COFFEEMUD/com/planet_ink/coffee_mud/Libraries/interfaces/IntermudInterface.java`
3. **Copy main client** from `/COFFEEMUD/com/planet_ink/coffee_mud/Libraries/IntermudClient.java`
4. **Extract utilities** from CoffeeMud core libraries
5. **Create abstraction interfaces** to replace CoffeeMud dependencies
6. **Refactor imports** to use new package structure
7. **Create configuration system** independent of CoffeeMud
8. **Build standalone application** with main() entry point
9. **Test all protocols** independently
10. **Package as distributable JAR**

## File List to Extract

### Core Intermud Files (108 files identified)
All files from `/COFFEEMUD/com/planet_ink/coffee_mud/Libraries/intermud/`:
- Main implementations: `IntermudClient.java`, interfaces
- I3 protocol: ~50 files in `i3/` subdirectories
- IMC2 protocol: 7 files in `imc2/`
- CM1 protocol: 20 files in `cm1/`
- Modern protocols: `DiscordClient.java`, `GrapevineClient.java`

### Supporting Files Needed
- Interface: `/COFFEEMUD/com/planet_ink/coffee_mud/Libraries/interfaces/IntermudInterface.java`
- Commands: `/COFFEEMUD/com/planet_ink/coffee_mud/Commands/I3Cmd.java`, `IMC2.java`, `Grapevine.java`
- Application: `/COFFEEMUD/com/planet_ink/coffee_mud/application/I3Router.java`

### Core Utilities to Extract/Adapt
From `/COFFEEMUD/com/planet_ink/coffee_mud/core/`:
- `CMStrings.java` - String utilities
- `CMath.java` - Math utilities  
- `CMParms.java` - Parameter parsing
- `Log.java` - Logging system
- `CMSecurity.java` - Security checks (partial)
- `CMProps.java` - Properties (partial)

## Expected Result
A standalone Intermud3 system that:
- Supports I3, IMC2, CM1, Discord, and Grapevine protocols
- Can be integrated into any Java MUD codebase
- Includes router capability for I3 network
- Has minimal external dependencies
- Provides clean API for MUD integration