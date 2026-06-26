A touchscreen-based implementation of the classic Battleship game developed in Embedded C using the STM32 HAL framework for the STM32F429I-DISC1 Discovery Board. The project demonstrates embedded graphics, touchscreen interaction, game-state management, and hardware peripheral integration on an ARM Cortex-M4 microcontroller.

## Hardware Specifications
* Development Board: STM32F429I-DISCO (Discovery kit with STM32F429ZI MCU)
* Core: ARM® Cortex®-M4 with FPU executing at 180 MHz
* Onboard Display: 2.4" QVGA TFT LCD handled via the "LTDC (LCD TFT Controller)" peripheral
* Touchscreen: Resistive touch controller driven via the onboard "I2C interface (STMPE811)"
* External RAM: 64-Mbit external "SDRAM" utilized for application and frame-buffer configurations
* Randomness: On-chip "Hardware TRNG (True Random Number Generator)" utilized for AI decision routing

## Flash Memory & Debugging Configuration
### On-Chip Flash Persistence (`BattleStats.c`)
To preserve user statistics and the global game hit-map across power cycles, this project utilizes the internal Flash sectors of the STM32F429ZI MCU. 
* **Data Retention:** Tracks total games won/lost and coordinate strike mapping.
* **Safety Mechanism:** Implements page-erasure safeguards to ensure game telemetry writes do not overwrite application code execution sectors.

### Debugging & Telemetry Profile
The project was tested and profiled using the integrated **ST-LINK V2-1** debugger.
* **Interface:** SWD (Serial Wire Debug) configured at 4.0 MHz.
* **Core Profiling:** Monitored volatile game arrays dynamically via live expression views to verify the state transitions of the Random Number Generator (RNG) logic.
* **Hardware Intercepts:** System handling routines utilize dedicated hardware interrupt breakpoints (`stm32f4xx_it.c`) to safely log runtime display rendering exceptions.

## Repository Architecture
The codebase is structured into explicit architectural layers, keeping low-level hardware abstractions strictly isolated from core game state logic.

```text
└── Core/
    ├── Inc/                          # Header Interfaces
    │   ├── main.h                    # System clock & peripheral configuration setup
    │   ├── ApplicationCode.h         # High-level application setup & hook entrypoints
    │   │
    │   ├── GameDriver.h              # Central game controller & Finite State Machine (FSM) definitions
    │   ├── OnePlayer.h               # Single-player vs AI engine parameters
    │   ├── TwoPlayer.h               # Local multi-player pass-and-play states
    │   ├── SharedPlayer.h            # Inter-mode shared game-state templates
    │   │
    │   ├── GameDisplay.h             # Game-specific GUI/viewport rendering
    │   ├── LCD_Driver.h              # Low-level graphic primitive drawing utilities
    │   ├── fonts.h                   # Pixel-font lookup matrices for UI text
    │   │
    │   ├── BattleStats.h             # Non-volatile Flash storage telemetry profiles
    │   │
    │   ├── ili9341.h                 # TFT LCD driver controller
    │   ├── stmpe811.h                # Resistive touchscreen controller interface
    │   └── sdram.h                   # External SDRAM expansion parameters
    │
    └── Src/                          # Source Implementations
        ├── main.c                    # Hardware peripheral initializations (RNG, GPIO, timers)
        ├── ApplicationCode.c         # Application-level control orchestration
        │
        ├── GameDriver.c              # Core turn loop, logic arbitration, and game rule evaluation
        ├── Oneplayer.c               # RNG-driven strategic AI hunting/targeting routines
        ├── TwoPlayer.c               # Blind-transition mechanics for multiplayer fog-of-war
        ├── SharedPlayer.c            # Common routine implementations for board configurations
        │
        ├── GameDisplay.c             # Coordinate grid mapping, explosion, and splash rendering
        ├── LCD_Driver.c              # Display drawing pipelines
        ├── fonts.c                   # Static font rendering arrays
        │
        ├── BattleStats.c             # Persistent lifetime telemetry tracking logic
        │
        ├── ili9341.c                 # Display controller initialization sequence commands'''



        ├── stmpe811.c                # Hardware touch polling/coordinate filtering
        └── sdram.c                   # Volatile frame-buffer external RAM configuration
