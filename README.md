# Nova Robot LED Face Controller

This repository contains the Arduino-based LED panel control system developed for the **Nova Robot**, an open-source interactive robot platform designed for educational and engagement-oriented applications.

The system drives a five-panel 8×8 LED matrix array to display expressive facial animations, enabling the robot to communicate emotions and feedback visually.

---

## Overview

The controller enables dynamic facial expressions using serial commands, allowing the robot to respond interactively during demonstrations, workshops, and educational activities.

The implementation demonstrates embedded programming, hardware interfacing, and real-time display control using Arduino and MAX7219-based LED matrices.

---

## Features

- Multiple facial expressions (neutral, happy, sad, surprised, etc.)
- Serial command interface for real-time control
- Designed for five chained MAX7219 8×8 LED matrices
- Modular and extendable animation framework
- Lightweight implementation suitable for low-power microcontrollers

---

## Hardware Setup

- Arduino UNO
- Five MAX7219-based 8×8 LED matrices connected in series
- DIN, CLK, and CS pins wired as specified in the sketch comments
- Panels arranged to form the robot’s facial display

Proper orientation and wiring are required to ensure correct animation alignment.

---

## Usage

1. Connect the LED matrices to the Arduino.
2. Upload `ledcontrol.ino` using the Arduino IDE.
3. Send serial commands to trigger expressions.

The controller can be integrated with higher-level robot software to enable expressive behavior.

---

## Applications

- Educational robotics platforms  
- Interactive display systems  
- Robotics demonstrations and workshops  
- Human–robot interaction experiments  

---

## Contributors

Adithya Pothula  
Siddanth Bhogoju  

---

## Notes

This repository contains the LED display module developed for the Nova Robot platform and is preserved as a reusable embedded subsystem for future robotics and interaction projects.
