# Hardware

## Design Needs
1. Able to read audio from a 3.5mm tip-ring-sleeve connection.
2. Connect with a pair of Bluetooth earbuds or headphones over classic Bluetooth (BR/BDR).
3. Transmit the read audio to the headphones without a noticable delay (less than 3ms).
4. Be powered by a usb port directly on the piano (~5V 0.5A)
5. Have the flexiblity and processing power to allow for driver exploration and development.
6. Have an interface to troubleshoot Bluetooth connections without having to connect it to an external device.

## Main components

I chose to prioritize Texas-Instrument integrated circuits (ICs) to simplify the selection process and to assure chosen parts have extensive documentation and availability. I also decided to use an STM32 microcontroller to manage the system. Using a microcontroller will provide flexibility to program my own drivers but will also gain me knowledge that could be useful in future projects. I chose to use an STM32 due to its wide availability, extensive documentation, and its use in industry and student design teams.

### 1. Analog to Digital Converter (ADC)
I chose the PCM1808 as the ADC. There were other Texas-Instrument audio ADCs, but through research, I found that the 96KHz sampling rate and 24-bit resolution were more than enough for my project. Additionally, I suspect that the bigger bottlenecks that will be present in my system will be the PCB layout and software. As such, the PCM1808 is a simpler ADC that still will not limit the performance of the project.

### 2. Bluetooth
I chose the CC2564C to allow for Bluetooth communication. It was the only classic Bluetooth-capable transeiver ICs offered by Texas-Instruments. This is an important distinction since some wireless headphones or earbuds do not support audio over Bluetooth low energy (LE) (like the ones I own). There are, for example, Bluetooth-capable STM32s, but they all supported Bluetooth LE and not classic Bluetooth. I wanted to have the possibility to try writing Bluetooth drivers so the transceiver could not have an integrated "upper layer" Bluetooth stack. I had considered using an ESP32 chip and programming it to act as a simple interface, but I wanted to avoid splitting the experimental driver code across multiple devices, complicating the system beyond necessary. Using only an ESP32 would solve this problem, but I wanted to use an STM32 due to the reasons mentioned above.

### 3. Microcontroller
