# RISC-V MCU with APB Peripherals on FPGA

This project implements a RISC-V based microcontroller (MCU) on an FPGA, integrating an APB (Advanced Peripheral Bus) system to connect various peripherals such as GPIO, UART, PWM, and sensors.

## Overview
The FPGA-based MCU is designed to execute RISC-V instructions stored in a ROM module, interact with peripherals through an APB master interface, and support external communication via UART, PWM, and sensors.

## Features
- **RISC-V CPU Core**
  - Supports 32-bit instructions
  - Interfaces with instruction memory (ROM)
![Demo Image](Motion_detection_sobel_grayscale/demo/demo.png)

- **APB Bus for Peripheral Communication**
  - Implements an APB master interface to control peripherals
  - Supports read and write operations
 ![Demo Image](Motion_detection_sobel_grayscale/demo/demo.png)
- **Peripheral Modules**
  - General Purpose Output (`GPOA`)
  - General Purpose Input (`GPIB`)
  - General Purpose Input/Output (`GPIOC`)
  - 7-Segment Display (`FND`)
  - UART Communication (`UART`)
  - PWM Output (`PWM`)
  - DHT11 Temperature & Humidity Sensor (`DHT11`)
  - Ultrasonic Sensor (`HC-SR04`)

## System Architecture
The project consists of the following key modules:
![Demo Image](Motion_detection_sobel_grayscale/demo/demo.png)
### 1. **RISC-V Core (`RV32I_Core`)**
   - Fetches instructions from `ROM`
   - Executes RISC-V instructions
   - Reads/Writes data via the APB master interface

### 2. **Memory (`ROM` and `periph_ram`)**
   - `ROM`: Stores instruction code
   - `periph_ram`: Data storage with APB interface

### 3. **APB Master Interface (`APB_Master_Interface`)**
   - Handles APB transactions between the CPU and peripherals
   - Supports multiple APB slaves via selection signals (`PSEL_*`)

### 4. **Peripheral Modules**
Each peripheral connects to the APB bus and responds to CPU requests:

| Peripheral  | Module Name      | Functionality  |
|------------|----------------|---------------|
| GPOA       | `periph_gpo`    | Outputs 8-bit data |
| GPIB       | `periph_gpi`    | Inputs 8-bit data |
| GPIOC      | `periph_gpio`   | Bidirectional 8-bit GPIO |
| FND        | `periph_fnd`    | 7-segment display controller |
| UART       | `periph_uart`   | Serial communication |
| PWM        | `periph_pwm`    | Pulse-width modulation output |
| DHT11      | `periph_dht11`  | Reads temperature & humidity |
| HC-SR04    | `periph_hc_sr04` | Measures distance using ultrasonic sensor |

## Getting Started

### Prerequisites
- FPGA Development Board (e.g., Basys-3 or similar)
- Vivado 2020.2 (or compatible version)
- UART Serial Monitor (e.g., PuTTY)

### Build Instructions
1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/riscv-mcu-fpga.git
   cd riscv-mcu-fpga
   ```
2. Open Vivado and create a new project targeting your FPGA board.
3. Add all Verilog source files (`.v`) from the repository to the project.
4. Add constraint files (`.xdc`) for pin assignments.
5. Synthesize the design and generate the bitstream.
6. Program the FPGA with the generated bitstream.

### Usage
- Connect a serial monitor to communicate via UART.
- Use external sensors (DHT11, HC-SR04) for environmental data.
- Adjust the APB memory-mapped registers for peripheral control.

## Future Enhancements
- Implement additional RISC-V instructions
- Expand APB bus to support more peripherals
- Optimize performance with pipelining in CPU design

## License
This project is licensed under the MIT License. See `LICENSE` for details.
