# 24-Week Embedded Engineer Roadmap

This is a practical path from beginner to interview-ready junior embedded candidate. It is not a promise that someone becomes a complete engineer in 24 weeks. At 12–15 focused hours per week, it builds the common foundation needed to start applying and to choose a specialization deliberately.

## The operating rule

Every week follows this loop:

> Learn → implement → break → debug → explain → document.

Watching courses without writing, measuring, or debugging is not enough for embedded work.

## Target outcome

By the end, you should be able to take a peripheral datasheet, connect it to one MCU, write or adapt a small driver, explain its configuration, handle expected failures, and demonstrate how you debugged it.

## What you need

- One MCU ecosystem only at first: an STM32 Nucleo plus STM32CubeIDE is a solid example, but an equivalent board is fine.
- USB cable, serial terminal, and Git/GitHub.
- Multimeter early; inexpensive logic analyzer once you reach I²C/SPI.
- GCC/toolchain, debugger support (SWD/JTAG if your board supports it), and a text editor/IDE.

Do not buy many boards. One board understood deeply is more useful than five boards used through copied examples.

---

## Phase 0 — Setup and evidence habits

### Week 0 (2–3 days)

**Learn**

- Firmware vs RTOS vs embedded Linux vs PCB vs FPGA roles.
- Electrical and ESD safety, common ground, voltage/current/power, and safe probe grounding.
- How a datasheet, reference manual, board schematic, application note, and errata differ.

**Do**

- Install toolchain, vendor IDE/CLI, serial terminal, Git, and debugger support.
- Read your board pinout, schematic, MCU datasheet table of contents, reference manual table of contents, and current errata.
- Create a lab-notes repository.

**Exit evidence**

- A setup README, board photo/pinout, first commit, and a lab-note template: hypothesis → measurement → result → next action.

---

## Phase 1 — C and Embedded C

### Weeks 1–2: C fundamentals and problem solving

**Learn**

- Types, fixed-width integers, signedness, promotions, casts, operators, control flow, functions, arrays, strings, scope, and `sizeof`.

**Build**

- Small command-line exercises: parser, min/max, frequency counter, string reversal, `strlen`, `strcmp`, matrix operations.

**Exit**

- Explain signed/unsigned bugs, choose `uint32_t` appropriately, and write small C programs without looking up basic syntax.

### Weeks 3–4: pointers, memory, and embedded-important C

**Learn**

- Pointer arithmetic, arrays versus pointers, pointer-to-pointer, `void *`, callbacks/function pointers, NULL/dangling/wild pointers.
- `const`, `volatile`, `static`, `extern`, structures, unions, enums, alignment, padding, macros, and conditional compilation.
- Stack, heap, `.text`, `.rodata`, `.data`, `.bss`, linker basics, map files, startup code, and common undefined behavior.

**Build**

- Ring buffer, generic swap, callback dispatch table, CRC, byte-stream parser, and finite-state machine.
- Host-side unit tests and invalid-input tests for each module.

**Exit**

- Defend each `volatile` use; explain why it is not atomicity or thread safety; read a map-file symbol and diagnose a pointer/memory bug.

**Use alongside**

- [C / Embedded-C Concepts to Master](C-EMBEDDED-C-CONCEPTS.md)
- [150 C / Embedded-C Interview Questions](C-EMBEDDED-C-INTERVIEW-QUESTIONS.md)
- [Hands-on C / Embedded-C Exercises](C-EMBEDDED-C-PRACTICAL-EXERCISES.md)

---

## Phase 2 — Electronics and computer architecture

### Weeks 5–6

**Electronics**

- Ohm’s law, power, pull-up/pull-down, voltage divider, capacitor/RC behavior, diode/transistor/MOSFET basics, digital logic levels, floating inputs, open drain, debounce, 3.3 V vs 5 V compatibility, and schematic reading.

**Computer/MCU architecture**

- Binary/hex/two’s complement, registers, ALU, buses, memory map, Flash, SRAM, MMIO, clocking, program counter, stack pointer, reset, vector table, exceptions, NVIC, endianness, and ARM Cortex-M orientation.

**Labs**

- Calculate and measure LED current.
- Compare pull-up, pull-down, and floating-button behavior.
- Measure PWM frequency/duty cycle.
- Read a sensor’s voltage and logic-level requirements before wiring it.

**Exit**

- Explain a small schematic, identify unsafe voltage-level assumptions, and use a multimeter/logic analyzer safely.

---

## Phase 3 — Bare-metal MCU core

### Week 7: GPIO, clocks, and reset

- Build/flash/debug a GPIO example using the vendor HAL.
- Repeat at register level for at least one peripheral.
- Learn clock source, PLL/clock tree, peripheral clock gating, reset causes, alternate functions, and boot modes.

### Week 8: timers, PWM, and interrupts

- Learn polling vs interrupts, ISR rules, priority, latency, timer prescaler/counter/compare/capture, and PWM.
- Build: button interrupt changes PWM brightness with no blocking delay.

### Week 9: ADC, watchdog, and low power

- Learn ADC resolution, sampling time, reference voltage, quantization, PWM duty cycle, watchdog policy, reset reason, and sleep/wake basics.
- Build: potentiometer → ADC → PWM output; deliberately hang the firmware and prove watchdog recovery.

### Week 10: DMA and fault handling

- Compare CPU transfer, interrupt transfer, and DMA.
- Learn buffers, circular mode, completion events, cache/coherency awareness where applicable, hard faults, stack overflow, and basic fault capture.
- Build: ADC → DMA → RAM → UART telemetry.

**Exit**

- Derive a timer/baud setting, navigate a reference manual, distinguish datasheet from errata, and diagnose wrong clocks, alternate functions, or peripheral-clock configuration.

---

## Phase 4 — Communication protocols and measurement

### Week 11: UART

- Learn framing, baud rate, parity, start/stop bits, overrun/framing errors, polling/IRQ/DMA paths, and ring-buffered receive.
- Build: UART command shell (`status`, `sensor read`, `led on`, `reset`).

### Week 12: SPI

- Learn MOSI/MISO/SCLK/CS, controller/peripheral roles, CPOL/CPHA modes, timing diagrams, multiple peripherals, and device command formats.
- Build: talk to a display, flash, or sensor from its datasheet; verify a transaction with a logic analyzer.

### Week 13: I²C

- Learn open-drain signaling, pull-ups, START/STOP, address, ACK/NACK, repeated START, arbitration, clock stretching, and bus-stuck recovery.
- Build: sensor driver with `init`, `read_register`, `write_register`, and `read_sensor` functions.
- Intentionally test wrong address, NACK, missing pull-up, wrong clock, and disconnected sensor.

**Exit**

- Explain UART/SPI/I²C trade-offs; read a bus capture; identify whether the likely fault is wiring, signal integrity, configuration, protocol sequence, or software.

---

## Phase 5 — Debugging as an engineering skill

### Weeks 14–15

Learn breakpoints, watchpoints, step controls, registers, memory view, call stack, SWD/JTAG, GDB, serial logging, reset reasons, logic analyzer, and oscilloscope basics.

Create a **debug diary** by deliberately causing and fixing:

- Wrong clock or baud rate.
- Wrong pin/alternate function.
- I²C pull-up/address problem.
- SPI mode mismatch.
- Missing `volatile` on asynchronous state.
- Stack overflow/hard fault.
- Buffer overflow or parser corruption.
- Watchdog reset and ISR storm.

**Exit**

- For each fault, record symptom, hypothesis, measurement, cause, fix, and regression test.

---

## Phase 6 — RTOS and real-time design

### Weeks 16–18

**Week 16: scheduling**

- Tasks/threads, task states, cooperative versus preemptive scheduling, priorities, tick, delays, latency, jitter, and deadlines.

**Week 17: synchronization**

- Queues, binary/counting semaphores, mutexes, event flags, task notifications, ownership, timeouts, and ISR-to-task handoff.

**Week 18: failure modes**

- Race conditions, deadlock, starvation, priority inversion/inheritance, stack high-water marks, and watchdog integration.

**Build**

```text
Sensor task → Queue → Processing task → UART task
Button ISR → event/notification
```

Add one mutex-protected resource, one timeout/recovery path, and a documented queue-full policy.

**Exit**

- Justify polling vs IRQ vs DMA vs task context, prove no blocking call occurs in an ISR, and explain mutex versus semaphore through a real design choice.

---

## Phase 7 — Serious portfolio project and quality

### Weeks 19–21

Build one reliable, explainable system—not several copied demos.

### Suggested capstone: multi-sensor data logger

```text
I²C/SPI sensor → acquisition task → queue → processing
                                      ├── SPI storage/display
                                      └── UART command/telemetry
```

Include DMA or interrupts, watchdog, CRC, framed protocol, configuration/versioning, timeout/retry, state machine, fault counters, and logging.

Test: sensor disconnect, invalid command, corrupt frame, queue full, stalled task, power/reset simulation, and UART receive faster than processing.

**Repository standard**

- Problem statement and requirements.
- Architecture diagram and data ownership.
- Hardware/pin table and datasheet links.
- Build/flash/test instructions.
- Protocol specification, timing/memory budget, tests, measurements, failures, known limitations, and demo.
- Formatting, warnings, unit tests, static analysis, CI, and release tag where practical.

---

## Phase 8 — Interview readiness and specialization

### Weeks 22–24

Start interviews before this phase; use these weeks to consolidate and apply.

**Weekly preparation loop**

- Solve five C/Embedded-C questions aloud.
- Complete two timed practical exercises.
- Draw one system/block diagram from memory.
- Explain one protocol trade-off and one debug case.
- Rehearse one project story: problem → architecture → contribution → bug → investigation → result → improvement.

**Choose one primary branch**

### A. MCU / firmware / RTOS

Go deeper into startup, linker scripts, bootloaders, power management, CAN, USB, BLE, Ethernet, OTA, security, and FreeRTOS/Zephyr.

### B. Embedded Linux / BSP / device drivers

Learn shell, processes/threads/IPC, system calls, cross compilation, U-Boot, kernel, root filesystem, device tree, Buildroot/Yocto, kernel modules, and GPIO/I²C/SPI/UART drivers. Budget several additional months; the Linux kernel documentation explicitly treats strong C knowledge as a prerequisite for kernel work.

### C. Hardware / PCB

Go deeper into schematic capture, power tree, component selection, protection, layout/return paths, decoupling, EMI/EMC, DFM/DFT, bring-up, and measurement.

### D. Automotive / safety

Focus on CAN/CAN FD, LIN, UDS concepts, diagnostics, boot/update, AUTOSAR awareness, requirements traceability, static analysis, and functional-safety vocabulary.

### E. FPGA / digital

Learn synchronous RTL, Verilog/SystemVerilog or VHDL, reset/CDC, simulation, constraints, static timing, BRAM/FIFO, and firmware interfaces.

### F. Controls / motor / power

Focus on low-voltage, safety-controlled labs: PWM/dead time, ADC synchronization, PID/control stability, protection paths, and measurement.

---

## What was added beyond a typical beginner roadmap

- **Errata and documentation literacy:** datasheet, reference manual, schematic, application note, and errata solve different problems.
- **Failure-first learning:** every protocol/peripheral must include intentional failures and a measured debug trail.
- **Quality evidence:** test matrix, versioning, static analysis, reproducible builds, and engineering documentation are part of the portfolio.
- **Memory/cache awareness:** after DMA basics, learn cache/coherency only where your MCU/MPU architecture needs it.
- **Security and lifecycle:** secure update, rollback, secrets, debug policy, input validation, and SBOM awareness belong after the universal core.
- **Specialize late:** common skills first, then one deep branch. Do not claim Linux driver, PCB, or safety expertise from a weekend tutorial.

## Official references

- [STMicroelectronics STM32 Step-by-Step](https://wiki.st.com/stm32mcu/wiki/STM32StepByStep%3AGetting_started_with_STM32_%3A_STM32_step_by_step) — hands-on STM32 progression including tools, blink LED, UART, sensors, GPIO, DMA, UART, SPI, I²C, timers, watchdogs, ADC, and DAC.
- [STM32 Online Training](https://www.st.com/content/st_com/en/support/learning/stm32-online-training.html) — official STM32 MOOCs and training, including IDE, CubeMX/HAL, FreeRTOS, boot/startup, security, power, and USB material.
- [Zephyr Project documentation](https://docs.zephyrproject.org/latest/introduction/index.html) — RTOS kernel, synchronization, message queues, power management, device drivers, and devicetree concepts.
- [Linux kernel development HOWTO](https://docs.kernel.org/process/howto.html) — the kernel’s own newcomer guidance and prerequisites for kernel work.
