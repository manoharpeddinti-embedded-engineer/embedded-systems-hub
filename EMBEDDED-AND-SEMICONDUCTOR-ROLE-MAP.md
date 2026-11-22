# Embedded and Semiconductor Role Map

Use this guide with the [company directory](EMBEDDED-COMPANY-DIRECTORY.md). Search for the role family that matches your skills and projects—do not apply to a company merely because it is in the same industry.

## 1. Embedded systems roles

### Core firmware, OS, and software

| Role | What the work commonly involves | Search terms / preparation focus |
|---|---|---|
| Firmware Engineer | Bare-metal MCU work, peripherals, register-level code | C, MCU, GPIO, timers, interrupts, UART/SPI/I²C, debugging |
| Embedded Software Engineer | C/C++, embedded application logic, system integration | C/C++, RTOS/Linux depending on product, testing |
| Embedded Systems Engineer | Hardware/software integration and debug | C, schematic reading, peripherals, lab tools, system design |
| Bootloader / BSP Engineer | Board enablement, boot flow, platform configuration | U-Boot, UEFI/XBL/OpenSBI, device tree, Yocto/Buildroot |
| Embedded Linux Kernel / Device Driver Engineer | Kernel-space drivers and Linux hardware interfaces | Linux C, kernel APIs, GPIO/I²C/SPI/UART/USB/PCIe, device tree |
| RTOS Engineer | Scheduling, tasks, synchronization and drivers | FreeRTOS, Zephyr, QNX, ThreadX, VxWorks, race conditions |
| Middleware / Connectivity Engineer | Device communication stacks | BLE, Wi-Fi, Matter, Zigbee, LoRa, CAN/LIN, Ethernet/TSN, TCP/IP |
| Embedded Security / TrustZone Engineer | Device trust, secure lifecycle and update security | Secure boot, TEE/OP-TEE, TrustZone, crypto, signing, OTA |
| Edge AI / Embedded ML Engineer | ML deployment on constrained devices | TinyML, NPU/DSP, quantization, OpenCV, ONNX/TensorRT |
| Embedded Systems Architect | System partitioning and cross-team technical direction | Hardware/software trade-offs, memory, power, reliability; usually experienced-hire level |

### Hardware, board design, and bring-up

| Role | What the work commonly involves | Search terms / preparation focus |
|---|---|---|
| Embedded Hardware Design Engineer | Schematic design, part selection, power trees, MCU/SoC boards | Schematics, datasheets, power, interfaces, component selection |
| PCB Layout / SI/PI Engineer | High-speed layout, impedance, return paths, EMC/EMI | PCB CAD, SI/PI, stack-up, routing, DFM/DFT |
| Board Bring-Up / Hardware Validation Engineer | First board or silicon power-on, lab debug, validation | JTAG/SWD, oscilloscope, logic analyzer, power sequencing |
| Hardware Test / Compliance Engineer | Reliability, thermal, environmental, EMC/EMI, safety testing | Test plans, instrumentation, standards awareness |

### Validation, QA, and automation

| Role | What the work commonly involves | Search terms / preparation focus |
|---|---|---|
| Embedded Validation / Verification Engineer | Functional, stress, stability, and performance tests | Test design, scripting, logs, protocol knowledge |
| HIL / Test Automation Engineer | Automated benches and regression rigs | Python, Robot Framework, CAN tools, hardware-in-the-loop |
| Embedded QA / Release Engineer | Build/release pipelines and firmware quality gates | CI/CD, Git, test suites, release process |

### Customer-facing and application roles

| Role | What the work commonly involves | Search terms / preparation focus |
|---|---|---|
| Field Application Engineer (FAE) | Customer design-in and pre-sales technical support | MCU/SoC/sensor knowledge, communication, demos, debugging |
| Application Engineer (AE) | Reference designs, eval kits, sample code, customer proofs of concept | Hands-on platform skills, documentation, customer support |
| Customer / Technical Support Engineer | Field-bug reproduction and issue triage | Logs, debug workflow, communication, root-cause analysis |
| IoT / Embedded Solutions Architect | Device-to-cloud solution design | Connectivity, security, cloud integration; often experienced-hire level |
| Technical Marketing / Developer Relations Engineer | Developer documentation, examples, workshops | Writing, demos, SDKs, application notes |

## 2. VLSI and semiconductor roles

### Architecture and front-end digital design

| Role | What the work commonly involves | Preparation focus |
|---|---|---|
| SoC / Micro-Architect | Chip specifications, buses, PPA trade-offs | Computer architecture, AMBA/AXI/CHI, performance/power thinking |
| RTL Design Engineer | Hardware RTL for IP, blocks, and SoCs | Verilog/SystemVerilog/VHDL, synthesis, lint, CDC/RDC |
| ASIC Design Engineer | Digital block design through integration | RTL, synthesis, CDC/RDC, lint, constraints |
| FPGA Design / Prototyping Engineer | RTL on FPGA for validation and prototyping | Vivado/Quartus, RTL, constraints, debug |
| CPU / GPU / NPU Core Design Engineer | Pipelines, caches, execution units | Advanced computer architecture, RTL, verification |
| Low-Power Design Engineer | Power intent and low-power implementation | UPF/CPF, clock/power gating, DVFS |

### Verification and pre-silicon emulation

| Role | What the work commonly involves | Preparation focus |
|---|---|---|
| Design Verification (DV) Engineer | UVM testbenches, simulation, coverage | SystemVerilog, UVM, assertions, constrained random, coverage |
| SoC Verification Engineer | Full-chip integration and boot/low-power verification | SV/UVM, C tests, SoC architecture |
| Formal Verification Engineer | Property/equivalence proof | Formal methods, SVA, RTL, tool methodology |
| Emulation Engineer | Full SoC runs on hardware emulators | Hardware/software co-debug, Palladium/ZeBu/Veloce awareness |
| Verification VIP / Methodology Engineer | Reusable verification IP and flows | Protocol knowledge, SV/UVM, PCIe/DDR/USB/CXL/Ethernet |

### DFT, physical design, and signoff

| Role | What the work commonly involves | Preparation focus |
|---|---|---|
| DFT Engineer | Scan, ATPG, BIST/MBIST, JTAG, coverage | DFT theory, scan, ATPG, boundary scan |
| Silicon Debug / Diagnosis Engineer | Relating tester failures to logic defects | DFT, failure analysis, diagnostics |
| Synthesis / STA Engineer | RTL-to-gate, constraints, timing closure | Synthesis, SDC, timing, PrimeTime/Tempus |
| Physical Design Engineer | Floorplan through routing/IR/congestion | PnR, CTS, power integrity, timing closure |
| Physical Verification Engineer | DRC/LVS/ERC/antenna validation | Calibre/ICV, layout, foundry rules |
| CAD / EDA Flow Engineer | Internal automation and PDK/tool flows | TCL, Python, EDA tools, Linux |

### Analog, mixed-signal, RF, and layout

| Role | What the work commonly involves | Preparation focus |
|---|---|---|
| Analog Design Engineer | Op-amps, PLLs, LDOs, converters, SerDes PHY | Analog circuits, SPICE, Cadence/Virtuoso |
| Mixed-Signal Design / Verification Engineer | Analog and RTL co-simulation | Verilog-AMS, real-number modeling, AMS workflows |
| RFIC Design Engineer | Radios, LNAs, mixers, PAs, transceivers | RF circuits, EM, 5G/Wi-Fi/radar concepts |
| Analog / Custom Layout Engineer | Transistor-level layout and matching | Layout, parasitics, EM, matching |
| Standard Cell / Memory Compiler Engineer | SRAM, libraries, characterization | Device/circuit design, characterization, PDKs |

### Post-silicon, test, and manufacturing

| Role | What the work commonly involves | Preparation focus |
|---|---|---|
| Post-Silicon Validation Engineer | Real silicon test across PVT | Board bring-up, Python, lab equipment, debug |
| Silicon Characterization Engineer | Electrical/timing/power measurement | Test methods, statistics, instrumentation |
| Product / Yield Engineer | Yield, binning, reliability, failure analysis | Semiconductor process, yield/reliability, data analysis |
| Test Development Engineer (ATE) | Automated production test programs | ATE, test programming, DFT/product knowledge |
| Packaging / Substrate Engineer | Chip packaging and thermal/mechanical design | 2.5D/3D IC, chiplets, package design |
| Process / Integration Engineer | Foundry process development | Lithography, etch, deposition, device physics |

### Semiconductor customer-facing and support

| Role | What the work commonly involves | Preparation focus |
|---|---|---|
| AE – VLSI / IP / EDA | EDA tool or IP integration support | Protocol/IP knowledge, EDA tools, customer debugging |
| FAE – Semiconductor / EDA | Technical pre-sales for vendors/IP/EDA providers | Technical depth, demos, customer communication |
| Customer / Product Support Engineer | Tool, PDK, or IP issue resolution | Linux, scripts, log triage, customer support |
| Technical Solutions / Foundry Interface Engineer | Fabless-to-foundry coordination | Process/design interface, PDK, documentation, project coordination |

## How to choose a role

1. Start with the work you want to do daily: firmware, board lab work, Linux, silicon RTL, verification, physical design, or customer engineering.
2. Select 15–30 matching companies from the directory.
3. Compare job descriptions, not just titles—titles vary widely between employers.
4. Build one project or portfolio artifact that proves the core skills for that role.
5. Keep adjacent paths as options, but do not dilute your resume by claiming unrelated specializations.
