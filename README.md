# DIY-Grand-Digital-Piano (GDP)

## Goal

Build a full-custom hybrid digital piano using a complete grand piano action. Ultimately, I want to create and build every component. This includes both sampled and modelled piano sounds.

In the spirit of "everything worth doing is worth overdoing", the design will be intentionally overdesigned and include many marginally useful features.

This is a hobby and so the approach may be driven primarily by curiosity on a subject, and not by efficiently getting to completion.

## Why?

It is fun.

It is a great way to learn so many new things.

## History

I started this project December 5, 2020.  For the first year I documented on YouTube and then in 2022 started this repository.

It was inspired, in part, by https://github.com/ekumanov/cybrid

Other related projects:
* https://github.com/jkominek/piano-conversion/
* https://github.com/davidedelvento/Mybrid

## Block Diagram
![alt text](block_diagram.png)

## YouTube Documentation

Along the way I have been documenting progress in YouTube:

Step 1 - Architecture https://www.youtube.com/watch?v=P3PVIuGSpIk

1. High-performance digital architecture approach.
2. Selecting the (Arduino) Teensy 4.1 processor.
2. Testing the CNY70 sensor, temporarily using the (Arduino) Teensy internal ADC.
3. Building a single-key action for testing.
4. Writing C++ software on the (Arduino) Teensy and Python on my computer to get something working for the first time.
5. Testing.

Step 2 - Analog Subsystem https://www.youtube.com/watch?v=p1Ko1ZMaAus

(audio was accidentally recorded mono channel)

1. Selecting the Ti ADS131M08 32Ksps 24-bit 8-channel analog-to-digital converter (ADC).
2. Learning the ADC.
3. Building a test system by modifying a Ti Evaluation Module.
4. Connecting the ADC to the (Arduino) Teensy via SPI.
5. Writing ADC SPI driver C++ software on the (Arduino) Teensy.
6. Testing.

Step 3 - Digital Signal Processing https://www.youtube.com/watch?v=5eaIhX29dF4

(audio was accidentally recorded mono channel)

1. Designing an algorithm that converts ADC samples of the hammer position into key strike events and velocities.
2. Implement the algorithm in C++ software on the (Arduino) Teensy.
3. Testing the algorithm with the single-key action and ADC subsystem.

Step 4 - Piano Action Frame https://www.youtube.com/watch?v=5U7LvOMth28

(audio was accidentally recorded mono channel)

1. Designing the physical layout of future PCB boards with respect to a grand piano action.
2. Designing the layout of circuit boards for the analog subsystem and microprocessors.
3. Building a wood frame for a piano action that includes hammer stops and sensor mounts.

Step 5 - Printed Circuit Boards https://www.youtube.com/watch?v=6EG-CYtTOFs

(audio was accidentally recorded mono channel)

1. Partitioning the design into two circuit boards.
2. Hammer Position Sensor (HPS 0.0) PCB: CNY70, biasing resistors, connection to microprocessor.
3. Hammer ENcoder (HEN 0.0) PCB: ADS131M08, power supply, (Arduino) Teensy 4.1.
4. Circuit design for both boards.
5. PCB layout for both boards.
6. Fabrication at OSH Park.
7. Software modifications to support new system.

Step 6 - Learning to Solder https://www.youtube.com/watch?v=wlrAXrDVhN0

(audio was accidentally recorded mono channel)

1. After receiving the circuit boards, I had difficulty hand soldering small surface mount parts.
2. So, I took time to learn the science of soldering.
3. Practicing soldering.

Step 7 - HPS PCB (CNY70) https://www.youtube.com/watch?v=usbgk9fsZ5I

(audio was accidentally recorded mono channel)

1. Finalize selection of biasing resistors.
2. Document design process for selecting biasing resistors.
3. Solder CNY70 and resistors on the board.
4. Testing.

Step 8 - HEN PCB https://www.youtube.com/watch?v=tCwKCgKxA0A

1. Design new (HEN 1.0) circuit board to add a clock and change physical orientation.
2. Circuit design and layout.
3. Soldering parts on the new HEN printed circuit board.
4. Continue C++ software development for the (Arduino) Teensy.
5. Bringing up the board and testing.
6. Full system test with HPS 0.0 and HEN 1.0
8. Write Python software on my computer to generate MIDI signals for sound generation through an external digital keyboard.

Step 9 - Raspberry Pi 4B https://www.youtube.com/watch?v=q-dFU-f_Ju8

1. Investigate the possibility of using a Raspberry Pi 4B in place of the (Arduino) Teensy 4.1.
2. Modify the (Arduino) Teensy C++ software to include a lower layer that abstracts the hardware.
3. Test with Ti Evaluation Module from Step 2.
4. Get system running.
5. Investigate but do not solve challenges with obtaining sufficiently fast real-time performance from Linux.
6. Although I made no physical changes to the Pi, for reference I am calling this the Raspberry Processing System (RPS).

Step 10 - Testing with Piano Action https://www.youtube.com/watch?v=ANJI4KAolEw

1. Layout three new HPS variations: HPS 0.1 changed the header spacing, HPS 0.2 increased the length slightly to get better alignment over the hammer shanks, HPS 0.2D is with the After Dark OSH Park fabrication process.
2. Investigate slight changes to bias resistors. Based on discoveries when tested with piano action.
3. Connect 8 Hammer Position Sensor (HPS, various versions) boards to 1 Hammer ENcoder (HEN 1.0) board.
4. Mount on the frame from Step 4 and place on a physical grand piano action.
5. Precisely locate each hammer stop position to exactly match hammer position when action is in the piano.
6. Continue improving the (Arduino) Teensy (HSP) C++ software and computer Python software.
7. Test.

Step 11 - Latency https://www.youtube.com/watch?v=k5ro7su6gYo

1. Investigate a problem with latency discovered during Step 10.
2. Quickly learn this was due to very large Ethernet packets containing hammer samples for visualization.
3. Remove that software (it was temporary for testing).
4. Measure the system latency.

Step 12 - Board Split https://www.youtube.com/watch?v=3AoEzj19FGQ

1. During the course of this project I am learning that soldering is very time consuming.
2. Want to avoid soldering 88 HPS boards and 11 HEN boards, then needing a board spin.
3. Decide to split the HEN into two boards.
4. New Board #1: (Arduino) Teensy Processing System (TPS) - contains the (Arduino) Teensy, Ethernet, and a new LCD (marginally useful features!).
5. New Board #2: Eight Channel Analog (ECA) - contains the Ti ADS131M08, associated support circuitry, and connections to the HPS.
6. Advantage of the split: TPS is easy to solder and likely to change. ECA is difficult to solder and unlikely to change.
7. Design and layout of TPS 0.0.
8. Soldering and bringing up the TPS.
9. Testing the TPS, discover a problem with the LCD write times.
10. Design a solution to long LCD write times.
11. Changes to (Arduino) Teensy C++ software to work around the write time issue.

Step 13 - Eight Channel Analog https://www.youtube.com/watch?v=e2ARDHr45-I
1. Soldering and bringing up the ECA (version 0.0).
2. Testing the ECA with the TPS and associated (Arduino) Teensy 4.1
3. Testing the ECA with a Raspberry Pi 4B (named the RPS).

Step 14 - Network and PPS https://www.youtube.com/watch?v=ryVUUPXWy0Q

1. Design a network protocol for sending hammer strike events (basically, MIDI information) and high-speed streaming hammer samples (for data analysis and visualization).
2. Design the protocol such that it avoids the latency issues seen in Step 11.
3. Writing protocol C++ software for TPS/RPS.
4. Writing Python for the Piano Processing System (PPS) portion of the design.
5. The PPS is running on another Raspberry Pi 4B and is responsible for converting hammer strike events into piano sounds, the MIDI interface, and other similar features.  The PPS is intended to implement features found on a modern digital keyboard.
6. Presently the PPS only generates MIDI. Other features are for the future.
7. Writing Python and Matlab / Octave software for my desktop computer to receive streaming samples, store them in a temporary cache, and plot the data in real-time. This is all temporary software for testing.
8. Redo the ECA layout so it works better with a Raspberry Pi 4B.
9. Use ECA 0.0 with TPS 0.0 and ECA 0.1 with RPS.
10. Testing.

Step 15 - Dedicated Piano Action https://www.youtube.com/watch?v=xohaQG593e4

1. Kawai KG-3C action with damper rail.
2. New sensor rail.

Step 16 - Thin Film Transistor LCD https://www.youtube.com/watch?v=y42pQxGMDy0

1. Design a different LCD approach, that avoids the timing issues discovered in Step 12.
2. Research LCD options and select the following: 2.8", 240x320 pixel, color, with capacitive touch.
3. For performance add a second processor for graphics processing.
4. Research processor options - select the Teensy 4.1 for graphics processing.
5. Write software for graphics display with Teensy 4.1.

Step 17 - TPS Mechanical https://www.youtube.com/watch?v=PopMsf95C8o

1. Design a physical case set that meets these requirements:
   1. Fits an ECA board, two Teensy 4.1 processing systems, ethernet/power connectors, and the TFT LCD.
   2. Accommodates all wiring - HPS (sensors), ethernet, power, and debugger connections.
   3. Fits within width of piano action.
   4. Meets thermal requirements.
   5. Looks cool.
2. Build cardboard and PCB mock-ups to test various ideas.

Step 18 - Two Teensy PCB https://www.youtube.com/watch?v=M1_228-ClXM

1. Design and write the software for DSP Teensy - GPU Teensy communication.
2. Breadboard test the DSP Teensy and GPU Teensy communication software (and connections).
3. Layout a new TPS (0.1) with DSP and GPU Teensy, that works with ECA 0.1, and fits the physical case.
4. Test new TPS.
5. Mechanical: ECA connection, case modifications, and external power supply.
6. Modifications to PPS Python software to support new features.
7. Full system running with eight piano keys, new boards, and lots of software changes.

Step 19 - Sixteen Key Piano https://www.youtube.com/watch?v=oMMNmDyscmQ

1. HPS 0.3 - Shorten board and build soldering jigs to reduce construction tolerances.
2. ECA 0.2 - Shorten so fits better in previously designed case, add ECA/TPS mounting holes, 0.1" alignment to aid soldering.
3. TPS 0.2 - Modifications for case fit, 0.1" alignment, add missing LED resistors.
4. Shorten LCD side-mounting PCB so fits better in case.  Add 2 LED.

The following are in progress or planned, and the order may change:

1. Resolve unacceptably large variation in hammer height signal.
2. Add more piano keys, eight at a time - probably will continue to spin boards because it's fun.
3. Design, hardware, and software to add pedals.
4. Documentation of software, pushing more to Github.
   1. C++ on DSP TPS ((Arduino) Teensy 4.1) - real-time data processing.
   2. C++ on RPS (Raspberry Pi 4B) - real-time data processing.
   3. C++ on GPU TPS ((Arduino) Teensy 4.1) - graphics processing and display.
   4. Python on PPS (Raspberry Pi 4B) - digital keyboard features.
   5. Matlab / Octave on desktop computer - analytics and visualization.
   6. Python / Javascript on desktop computer - analytics and visualization.
5. PPS software to remove need for external MIDI connection and generate the piano sounds internally.