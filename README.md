# USB-C Single-Channel Signal Analyzer & Generator

## Description
This repository contains the hardware design for a **USB-C powered, single-channel Signal Analyzer and Signal Generator** intended for low-frequency (audio-band) applications. The board integrates precision analog signal conditioning, data converters, and a microcontroller to enable waveform generation and signal acquisition through a PC interface.

The project was developed as part of the *Mixed-Signal Hardware Design with KiCad* course by Philip Salmony and focuses on applying **real-world mixed-signal PCB design practices** including power-domain separation, grounding strategies, filtering, biasing, and EMC-aware layout.

The module can function as a compact lab instrument for experimentation, education, and prototyping.

---

## Components

### Microcontroller
- STM32F103 (ARM Cortex-M series)
- USB 2.0 Full-Speed device
- SPI interfaces for ADC and DAC
- SWD interface for programming and debugging
- External crystal for accurate timing

### Analog-to-Digital Converter (ADC)
- 14-bit resolution
- Audio-band sampling rates
- High-impedance buffered input
- AC-coupled front end
- 3rd-order Sallen-Key Butterworth anti-aliasing filter
- Precision voltage reference for improved accuracy

### Digital-to-Analog Converter (DAC)
- 12-bit resolution
- SPI-controlled
- Reconstruction filter to suppress switching artifacts
- 50 Ω output impedance for signal integrity

### Power Architecture
- USB-C input power (5 V, < 500 mA)
- Switching buck regulator for digital 3.3 V rail
- Low-noise LDO regulator for analog 3.3 V rail
- Input LC filtering to suppress USB noise
- Dedicated mid-supply bias generator for single-supply analog stages

### Interfaces & Peripherals
- USB-C with CC resistors and ESD protection
- BNC connectors for signal input and output
- RGB status LED
- Reset and boot configuration buttons
- SWD debug header with protection components

---

## PCB Layout

The PCB was designed following mixed-signal layout best practices:
- Clear separation of analog and digital sections
- Dedicated analog and digital power domains
- Short return paths and solid ground referencing
- Careful placement of ADC/DAC front-end components
- EMI-aware routing for USB and high-speed digital lines

### Top-Level Board Layout
![PCB Layout](mixed-signal-layout.png)

---

## Schematics

### Analog Front-End & ADC
High-impedance input buffer, RF filtering, AC coupling, and 3rd-order Butterworth anti-aliasing filter feeding the 14-bit ADC.

![Analog Front-End & ADC](mixed-signal-adc.png)

---

### DAC & Analog Output Stage
DAC with reconstruction filter, output buffer, and 50 Ω output termination for clean waveform generation.

![DAC & Analog Output](mixed-signal-dac.png)

---

### Microcontroller, USB-C & Debug
STM32 MCU core with USB-C interface, SWD debug circuitry, clocking, reset, and status LEDs.

![MCU & USB](mixed-signal-mcu-usb.png)

---

### Power Supply & Bias Generation
USB-C input filtering, buck regulator for digital rail, LDO for analog rail, and mid-supply bias generator.

![Power & Bias](mixed-signal-power.png)

---

## Use Cases

- **Low-Frequency Signal Analyzer**  
  Capture and inspect audio-band signals with proper buffering, filtering, and quantization.

- **Arbitrary Signal Generator**  
  Generate sine, square, and custom waveforms for testing analog circuits.

- **Educational Mixed-Signal Platform**  
  Demonstrates practical ADC/DAC interfacing, analog front-end design, and power integrity concepts.

- **PC-Based Measurement Tool**  
  Can be used as a simple oscilloscope or waveform generator when paired with host-side software.

---

## References

- Mixed-Signal Hardware Design with KiCad  
  Course by Philip Salmony  
  https://fedevel.com/courses/mixed-signal-hardware-design-with-kicad

- Phil’s Lab  
  https://www.phils-lab.net  
  https://www.youtube.com/@PhilsLab
