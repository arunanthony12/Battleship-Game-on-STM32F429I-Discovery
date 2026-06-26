A touchscreen-based implementation of the classic Battleship game developed in Embedded C using the STM32 HAL framework for the STM32F429I-DISC1 Discovery Board. The project demonstrates embedded graphics, touchscreen interaction, game-state management, and hardware peripheral integration on an ARM Cortex-M4 microcontroller.

Repository Architecture
├── .gitignore
├── README.md
└── Core/
    ├── Inc/
    │   ├── ApplicationCode.h    <-- High-level application setup / hooks
    │   ├── BattleStats.h        <-- Flash storage / persistent stats tracking
    │   ├── fonts.h              <-- LCD text font definitions
    │   ├── GameDisplay.h        <-- Game-specific UI rendering layer
    │   ├── GameDriver.h         <-- Core game controller & state machine
    │   ├── ili9341.h            <-- Display driver controller header
    │   ├── LCD_Driver.h         <-- Graphic primitive drawing functions
    │   ├── main.h               <-- System initialization & HAL bindings
    │   ├── OnePlayer.h          <-- Single-player vs AI logic
    │   ├── sdram.h              <-- External SDRAM configuration
    │   ├── SharedPlayer.h       <-- Modular components used by both modes
    │   ├── stm32f4xx_hal_conf.h <-- HAL library configuration
    │   ├── stm32f4xx_it.h       <-- Interrupt service routine handlers
    │   ├── stmpe811.h           <-- Touchscreen controller header
    │   └── TwoPlayer.h          <-- Local multi-player logic
    │
    └── Src/
        ├── ApplicationCode.c
        ├── BattleStats.c
        ├── fonts.c
        ├── GameDisplay.c
        ├── GameDriver.c
        ├── ili9341.c
        ├── LCD_Driver.c
        ├── main.c
        ├── Oneplayer.c
        ├── sdram.c
        ├── SharedPlayer.c
        ├── stm32f4xx_hal_msp.c  <-- MCU support package (peripheral pins)
        ├── stm32f4xx_it.c
        ├── stmpe811.c
        ├── sysmem.c             <-- Memory management (malloc/heap allocation)
        ├── system_stm32f4xx.c   <-- System clock configuration setup
        └── TwoPlayer.c
