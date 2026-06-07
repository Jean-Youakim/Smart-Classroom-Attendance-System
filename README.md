# Smart Classroom Attendance System

A comprehensive **physical digital logic hardware system** designed via schematic block diagrams in **Quartus** to automate and track classroom attendance. This project implements a sophisticated state machine-based attendance tracking mechanism with countdown timer, bidirectional counter, and visual feedback.

## 📋 Project Overview

The Smart Classroom Attendance System is a hardware-based solution that combines digital logic design principles with finite state machine (FSM) architecture to create an automated attendance tracking mechanism. The system uses FPGA technology to manage student check-ins within a defined time window with LED status indicators and seven-segment display output.

### Key Features

- **10 to 0 Countdown Timer**: Precise timing mechanism for attendance window
- **0-29 Bidirectional Counter**: Tracks attendance numbers with up/down functionality
- **Seven-Segment Display Interface**: Real-time visualization of count values
- **LED Status Indicators**: Visual feedback with color-coded LEDs (Green, Orange, Red)
- **Finite State Machine**: Controls system operation and transitions
- **FPGA Implementation**: Built entirely on programmable logic using Quartus

## 🏗️ System Architecture

The system is composed of five main modules working in concert:

### 1. **FINALLOGIC (10 to 0 Timer)**
**File**: `FINALLOGIC.bdf`

The core timing module that counts down from 10 to 0, providing the attendance window control mechanism using JK flip-flops and logic gates.

### 2. **Ghady (0-29 Up/Down Counter)**
**File**: `Ghady.bdf`

An up/down counter that maintains the attendance count from 0 to 29, allowing increments and decrements as students are checked in.

### 3. **Jason (0-29 to Seven-Segment Converter)**
**File**: `Jason.bdf`

Converts the 5-bit counter output (0-29) into seven-segment display format for visual readout on a 2-digit display.

### 4. **FSM (Finite State Machine)**
**File**: `FSM.bdf`

Manages system state transitions and controls the overall workflow:
- **Idle State**: System ready, waiting for start
- **Active State**: Attendance window open, counter accepting inputs
- **Warning State**: Timer running low, visual alert active
- **Closed State**: Attendance window closed, counter frozen

### 5. **Final (Integrated System)**
**File**: `Final.bdf`

The complete integrated design combining all modules with clock distribution and synchronization.

## 🔧 Design Files

```
Smart-Classroom-Attendance-System/
├── FINALLOGIC.bdf              # 10→0 Countdown Timer Logic
├── Ghady.bdf                   # 0-29 Up/Down Counter
├── Jason.bdf                   # Seven-Segment Display Converter
├── FSM.bdf                     # Finite State Machine Controller
├── Final.bdf                   # Integrated System Design
├── Logic Final Project.docx    # Complete Documentation
├── Project Presentation.mp4    # Video Presentation
└── README.md                   # This file
```

### File Types

- **`.bdf`** (Block Diagram Format): Quartus schematic files containing gate-level logic
- **`.docx`**: Complete project documentation with design explanations, truth tables, and schematics
- **`.mp4`**: Video presentation of the project design and operation
- **`.md`**: This README file

## 📖 Documentation

**Main Documentation**: `Logic Final Project.docx`

This file contains:
- Detailed design methodology and logic equations
- Schematic diagrams and truth tables
- FSM state diagrams and transitions
- Design decisions and optimizations
- Simulation results and implementation notes

**Video Presentation**: `Project Presentation.mp4`

Overview of the system design and operation workflow.

## 🛠️ Technical Specifications

### Timing
- **Clock Input**: Standard system clock (CLOCK)
- **Counter Range**: 0-29 (5-bit representation)
- **Countdown Range**: 10-0 (4-bit representation)
- **Synchronous Design**: All operations clock-synchronized

### Logic Levels
- **High (1)**: +5V or FPGA high logic
- **Low (0)**: 0V or FPGA low logic
- **Active Low Signals**: PRN, CLRN inputs (inverted logic)

### Pin Configuration
- **Inputs**: CLOCK, RESET, Control signals
- **Outputs**: Q0, Q1, Q2, Q3, GreenLED, OrangeLED, RedLED
- **Display Output**: Seven-segment encoded pins

## 👥 Project Information

- **Created**: Digital Logic Design Course Project
- **Language**: Quartus Block Diagram Format (BDF)
- **Target Platform**: FPGA (Altera/Intel Cyclone series)
- **Complexity**: Intermediate (Combinational + Sequential Logic with FSM)

## 📄 License

This project is provided for educational purposes.


**For detailed design explanations, logic equations, schematics, and simulation results, refer to `Logic Final Project.docx`**

**For a video overview of the system, see `Project Presentation.mp4`**
