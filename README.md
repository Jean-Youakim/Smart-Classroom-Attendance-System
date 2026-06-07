# Smart Classroom Attendance System

A comprehensive **physical digital logic hardware system** designed via schematic block diagrams in **Quartus** to automate and track classroom attendance. This project implements a sophisticated counting and timing system using FPGA logic gates and flip-flops to manage attendance verification with visual LED indicators.

## 📋 Project Overview

The Smart Classroom Attendance System is a hardware-based solution that combines digital logic design principles to create an automated attendance tracking mechanism. The system uses FPGA (Field-Programmable Gate Array) technology implemented in Altera/Intel Quartus to control a countdown timer, bidirectional counter, and seven-segment display output for real-time attendance monitoring.

### Key Features

- **10 to 0 Countdown Timer**: Precise timing mechanism for attendance window
- **0-29 Bidirectional Counter**: Tracks attendance numbers with up/down functionality
- **Seven-Segment Display Interface**: Real-time visualization of count values
- **LED Status Indicators**: Visual feedback with color-coded LEDs (Green, Orange, Red)
- **FPGA Implementation**: Built entirely on programmable logic using Quartus

## 🏗️ System Architecture

The system is composed of four main modules working in concert:

### 1. **FINALLOGIC (10 to 0 Timer)**
**File**: `FINALLOGIC.bdf`

The core timing module that counts down from 10 to 0, providing the attendance window control mechanism.

**Components**:
- **4 JK Flip-Flops (inst, inst1, inst2, inst3)**: Form the basis of the countdown counter
- **NOT Gates (inst5-inst8)**: Provide signal inversion for flip-flop control logic
- **AND Gates**: Control clock gating and output logic
- **NAND Gates**: Enable/disable countable states

**Functionality**:
- Counts down from 10 (binary 1010) to 0 (binary 0000)
- Provides synchronized clock pulses to the system
- Generates control signals for the attendance window
- Outputs: Q0, Q1, Q2, Q3 (4-bit countdown value)
- Status outputs: GreenLED, OrangeLED, RedLED

**Logic Flow**:
```
CLOCK → [JK Flip-Flops] → Countdown Counter (10→0)
                ↓
        LED Status Indicators
        - Green: Attendance Open
        - Orange: Warning (Low Time)
        - Red: Attendance Closed
```

### 2. **Ghady (0-29 Up/Down Counter)**
**File**: `Ghady.bdf`

An up/down counter that maintains the attendance count from 0 to 29, allowing increments and decrements as students are checked in.

**Functionality**:
- Bidirectional counting (up/down operation)
- Range: 0 to 29 students
- Wraparound at boundaries
- Enable/disable control
- Clock-synchronized updates

### 3. **Jason (0-29 to Seven-Segment Converter)**
**File**: `Jason.bdf`

Converts the 5-bit counter output (0-29) into seven-segment display format for visual readout.

**Functionality**:
- Decimal (0-29) to seven-segment encoding
- Standard 7-segment display format (a, b, c, d, e, f, g)
- Supports dual-digit display with tens and units
- Direct FPGA pin mapping to display hardware

### 4. **Final (Integrated System)**
**File**: `Final.bdf`

The complete integrated design combining all modules:
- Timer module (FINALLOGIC)
- Counter module (Ghady)
- Display converter (Jason)
- LED control logic
- Clock distribution and synchronization

## 📊 Component Details

### Flip-Flops
- **Type**: JK Flip-Flops with preset (PRN) and clear (CLRN) inputs
- **Purpose**: Create state memory for counter sequences
- **Active Low**: PRN and CLRN inputs use active-low logic

### Logic Gates
- **AND Gates**: Signal combination and control logic
- **NAND Gates**: Counter output gating
- **NOT Gates**: Signal inversion for complementary logic

### Output Signals

| Output | Function | Active State |
|--------|----------|--------------|
| Q0-Q3 | 4-bit counter output | High (1) |
| GreenLED | Attendance open | High (1) |
| OrangeLED | Warning/Transition | High (1) |
| RedLED | Attendance closed | High (1) |

## 🔧 Design Files

### File Structure

```
Smart-Classroom-Attendance-System/
├── FINALLOGIC.bdf          # 10→0 Countdown Timer Logic
├── Ghady.bdf               # 0-29 Up/Down Counter
├── Jason.bdf               # Seven-Segment Display Converter
├── Final.bdf               # Integrated System Design
├── Logic Final Project.docx # Complete Documentation
└── README.md               # This file
```

### File Types

- **`.bdf`** (Block Diagram Format): Quartus schematic files containing visual gate-level logic
- **`.docx`**: Complete project documentation with design explanations and schematics
- **`.md`**: This README file

## 📖 Documentation

**Main Documentation**: `Logic Final Project.docx`

This file contains:
- Detailed design methodology
- Logic equations and truth tables
- Schematic diagrams
- Design decisions and optimizations
- Simulation results
- Implementation notes

## 🎯 Operation Workflow

### Attendance Cycle

1. **Initialization**
   - System powers on
   - Timers and counters reset to initial states
   - LEDs indicate system ready

2. **Attendance Window Opens**
   - FINALLOGIC countdown begins from 10
   - GreenLED activates (attendance open)
   - Ghady counter enabled for student check-ins

3. **Student Check-In**
   - Ghady counter increments with each student
   - Jason display shows current count (0-29)
   - Clock pulses synchronize all operations

4. **Warning Phase**
   - Timer reaches lower values
   - OrangeLED activates (time running out)
   - System prepares for closure

5. **Attendance Close**
   - Timer reaches 0
   - RedLED activates (attendance closed)
   - Counter freezes at final count
   - Final display shows total attendance

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
- **Inputs**: CLOCK, RESET, HIGH (VCC)
- **Outputs**: Q0, Q1, Q2, Q3, GreenLED, OrangeLED, RedLED
- **Display Output**: Seven-segment encoded pins

## 🚀 Getting Started

### Prerequisites
- **Altera/Intel Quartus Prime**: Latest version (2020 or newer recommended)
- **FPGA Development Board**: Compatible with Quartus (e.g., DE2-115, Cyclone IV)
- **Display Hardware**: 
  - 7-segment display module (2-digit common cathode or anode)
  - LED indicators (Red, Orange, Green)

### Installation & Usage

1. **Open Quartus Prime**
2. **Create New Project**
3. **Import BDF Files**
   - Load `Final.bdf` as top-level design
   - Ensure `FINALLOGIC.bdf`, `Ghady.bdf`, and `Jason.bdf` are in project directory

4. **Configure I/O Pins**
   - Map CLOCK to system clock pin
   - Map RESET to reset button
   - Map LED outputs to physical LED pins
   - Map seven-segment pins to display module

5. **Compile Design**
   - Analyze & Elaborate
   - Place & Route
   - Generate bit file

6. **Program FPGA**
   - Download bit file to FPGA board
   - Verify LEDs and display operation

## 🔍 Signal Flow Diagram

```
┌─────────────┐
│   CLOCK     │
└──────┬──────┘
       │
       ▼
┌──────────────────┐
│ FINALLOGIC       │
│ (10→0 Timer)     │
└────┬──┬──┬──┐────┘
     │  │  │  │
   Q0 Q1 Q2 Q3 (Timer Output)
     │  │  │  │
     └──┴──┴──┘
        │
        ├─────────────────┐
        │                 │
        ▼                 ▼
    ┌────────────┐  ┌──────────────┐
    │  Ghady     │  │ LED Control  │
    │ (Counter)  │  │ Logic        │
    └────┬───────┘  └──────────────┘
         │               │
         ▼               ▼
     ┌─────────┐    ┌──────────────┐
     │  Jason  │    │ RGB LED Out  │
     │ (7-Seg) │    │ (G, O, R)    │
     └─────────┘    └──────────────┘
         │
         ▼
     7-Segment
     Display
```

## 📝 Design Notes

### Optimization Techniques
- **Synchronous Design**: All state changes tied to clock for reliability
- **Active Low Logic**: Reduces gate count for reset/clear operations
- **Cascaded Counters**: Modular design allows independent testing
- **LED Status Encoding**: Three-state indicator system provides clear feedback

### Considerations
- **Metastability**: External inputs synchronized to internal clock
- **Power Consumption**: Optimized gate usage for FPGA efficiency
- **Timing Constraints**: Meets standard 50MHz FPGA clock speeds

## 🐛 Testing & Validation

### Functional Testing Checklist
- [ ] Timer counts down from 10 to 0
- [ ] Counter increments/decrements 0 to 29
- [ ] Seven-segment display shows correct values
- [ ] GreenLED: Timer active
- [ ] OrangeLED: Timer < 3
- [ ] RedLED: Timer = 0
- [ ] Reset button clears all values
- [ ] Clock synchronization stable

## 📚 Additional Resources

- **Quartus Documentation**: [Intel Quartus Prime User Guide](https://www.intel.com/content/www/us/en/develop/documentation/quartus-prime-help.html)
- **FPGA Design Principles**: Digital Logic fundamentals for counter and timer design
- **Seven-Segment Displays**: Standard encoding and multiplexing techniques

## 👥 Project Information

- **Created**: Digital Logic Design Course Project
- **Language**: Quartus Block Diagram Format (BDF)
- **Target Platform**: FPGA (Altera/Intel Cyclone series)
- **Complexity**: Intermediate (Combinational + Sequential Logic)

## 📄 License

This project is provided for educational purposes.

## 🤝 Contributing

This is a course project. For modifications or improvements:
1. Test all changes thoroughly in simulation
2. Verify timing constraints
3. Document any design changes
4. Validate on hardware before deployment

## ❓ FAQ

**Q: Can I modify the countdown range?**
A: Yes, modify FINALLOGIC.bdf to change from 10-0 to any desired range (e.g., 20-0, 60-0).

**Q: How do I add more than 29 students?**
A: Replace Ghady with a counter supporting larger ranges (6-bit for 0-63, etc.) and update Jason display logic.

**Q: What's the maximum clock frequency?**
A: Standard FPGA implementations support up to 50-100MHz depending on board; check timing report after compilation.

**Q: Can I use different LED colors?**
A: Yes, any active-high LED can be used; adjust current-limiting resistors based on LED specifications.

---

**For detailed design explanations and schematics, refer to `Logic Final Project.docx`**
