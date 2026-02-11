# 3-Bit Programmable Parity Generator
## Complete Build Guide with Component Analysis

## Table of Contents
- [Project Overview](#project-overview)
- [Component Inventory](#component-inventory)
- [Breadboard Layout](#breadboard-layout)
- [Component Analysis](#component-analysis)
- [Wire-by-Wire Guide](#wire-by-wire-guide)
- [Power Connection System](#power-connection-system)
- [Working Principle](#working-principle)
- [Applications](#applications)
- [Troubleshooting](#troubleshooting)

## Project Overview
This is a 3-bit programmable parity generator that demonstrates error detection in digital communication systems. The circuit calculates parity for 3 data bits and allows selection between even and odd parity modes using a control switch.

## Component Inventory
| Component | Qty | Purpose | Physical Location |
|-----------|-----|---------|-------------------|
| Half-size Breadboard | 1 | Prototyping platform | Entire build area |
| 74LS86 XOR IC | 1 | Logic processing | E10-E16, F10-F16 |
| 4-way DIP Switch | 1 | User input control | E22-E25, F22-F25 |
| LEDs (Red/Green) | 5 | Visual output indicators | Various positions |
| 330Ω Resistors | 5 | Current limiting | Various positions |
| LM7805 Voltage Regulator | 1 | 9V to 5V conversion | A1-A3 |
| 9V Battery | 1 | Power source | External |
| Battery Cap | 1 | Battery connection | External |
| Jumper Wires | 15 | Interconnections | Various positions |

## Breadboard Layout
```
    A B C D E F G H I J
1   + + + + + + + + + +  ← Power Rails
2   + + + + + + + + + +
3   + + + + + + + + + +
4   + + + + + + + + + +
...                    ...
10  . . . . IC . . . . .  ← 74LS86 (E10-F16)
11  . . . . . . . . . . 
12  . . . . . . . . . .
13  . . . . . . . . . .
...                    ...
22  . . . . SW . . . . .  ← DIP Switch (E22-F25)
23  . . . . SW . . . . .
24  . . . . SW . . . . .
25  . . . . SW . . . . .
...                    ...
```

## Component Analysis

### 1. 74LS86 Quad XOR Gate IC
```
Visual Representation:
         ┌──────────┐
   A1 →  │1       14│ ← Vcc (+5V)
   B1 →  │2       13│ ← A4
  Y1 ←   │3       12│ ← B4
   A2 →  │4       11│ ← Y4
   B2 →  │5       10│ ← A3
  Y2 ←   │6        9│ ← B3
  GND →  │7        8│ ← Y3
         └──────────┘
```

| Aspect | Details |
|--------|---------|
| **Purpose** | Performs exclusive-OR operations on binary inputs |
| **Why Used** | XOR is fundamental for parity calculation (odd/even detection) |
| **Advantages** | - 4 gates in one package<br>- Fast propagation (15ns typical)<br>- Low power (2mW per gate)<br>- TTL compatible |
| **Disadvantages** | - Requires clean 5V supply (±0.25V tolerance)<br>- Limited fan-out (10 TTL loads)<br>- Not rail-to-rail output |
| **Parity Logic** | Output = 1 when ODD number of inputs are HIGH |

### 2. LM7805 Voltage Regulator
```
Visual Representation:
    ┌─────────────┐
IN  │1   LM7805  3│ OUT
────┤o           o├────
    │             │
GND │2           │
────┤o           │
    └─────────────┘
```

| Aspect | Details |
|--------|---------|
| **Purpose** | Converts 9V battery voltage to stable 5V |
| **Why Used** | 74LS86 has maximum 5.25V rating; 9V would destroy it |
| **Advantages** | - Simple 3-terminal design<br>- Built-in thermal protection<br>- 1A output capability<br>- 5% output accuracy |
| **Disadvantages** | - Requires 2V dropout (7V minimum input)<br>- Inefficient (dissipates excess as heat)<br>- Needs heatsink for >500mA |
| **Protection Role** | Acts as "bodyguard" for sensitive logic IC |

### 3. 4-Way DIP Switch
```
Visual Representation:
    ┌──┬──┬──┬──┐
    │▒ │▒ │▒ │▒ │  ← Switch buttons
    ├──┼──┼──┼──┤
COM │1 │2 │3 │4 │  ← Common pins (E22-E25)
    ├──┼──┼──┼──┤
NO  │1 │2 │3 │4 │  ← Normally Open (F22-F25)
    └──┴──┴──┴──┘
```

| Aspect | Details |
|--------|---------|
| **Purpose** | User interface for data input and mode selection |
| **Why Used** | - Compact 4-switch package<br>- Easy toggling<br>- Clean breadboard mounting |
| **Advantages** | - Saves space vs individual switches<br>- Consistent spacing<br>- Dust protection<br>- Reliable contacts |
| **Disadvantages** | - Limited to 4 inputs<br>- Cannot be panel-mounted easily<br>- Higher cost than individual switches |
| **Switch Functions** | SW1: Parity mode control (Even/Odd)<br>SW2: Data bit A<br>SW3: Data bit B<br>SW4: Data bit C |

### 4. LEDs with 330Ω Resistors
```
Visual Representation:
    +5V ──[330Ω]──┬── LED ── GND
                  │
               Anode (+)
               Cathode (-)
```

| Aspect | Details |
|--------|---------|
| **Purpose** | Visual indication of logic states and parity |
| **Why Used** | Immediate feedback without measurement tools |
| **Advantages** | - Clear visual indication<br>- Low power consumption<br>- Fast response<br>- Long lifespan |
| **Disadvantages** | - Requires current limiting<br>- Direction sensitive<br>- Limited viewing angle |
| **Current Calculation** | I = (5V - 2V)/330Ω = 9.1mA (safe for LED and IC) |

### 5. Breadboard (Half Size)
```
Visual Representation:
    ┌─────────────────────────────┐
    │ A B C D E F G H I J         │
    ├─────────────────────────────┤
    │       Internal Connections  │
    │ A-E: Vertical strips        │
    │ F-J: Vertical strips        │
    │ +/-: Horizontal rails       │
    └─────────────────────────────┘
```

| Aspect | Details |
|--------|---------|
| **Purpose** | Solderless prototyping platform |
| **Why Used** | - Quick circuit assembly<br>- Easy modifications<br>- Reusable components |
| **Advantages** | - No soldering required<br>- Component reuse<br>- Visual debugging<br>- Modular design |
| **Disadvantages** | - Limited current capacity (~1A)<br>- Loose connections possible<br>- Not for permanent installations |
| **Connection Pattern** | Rows 1-5: Connected A-E<br>Rows 6-10: Connected F-J<br>Top/Bottom: Horizontal power rails |

## Wire-by-Wire Guide

### Power Distribution Wires
```
Wire 1: J10 to Positive Rail (+)
Purpose: Supplies 5V to IC Pin 14 (Vcc)
Visual: 74LS86[14] ──────→ +5V Rail

Wire 2: A16 to Negative Rail (-)
Purpose: Grounds IC Pin 7 (GND)
Visual: 74LS86[7] ──────→ GND Rail

Wire 3-5: H23, H24, H25 to Positive Rail (+)
Purpose: Powers DIP switch common terminals
Visual: DIP[COM] ──────→ +5V Rail
```

### Pull-Down Resistors
```
Resistor 1-3: B23, B24, B25 to Negative Rail (-)
Purpose: Ensures logic LOW when switches are open
Visual: DIP[NO] ─[10kΩ]─→ GND Rail
Why Needed: Prevents floating inputs that act as antennas
```

### Data Input Connections
```
Wire 6: D23 to D10
Purpose: Connects SW2 (Data A) to XOR Gate 1 Input A
Visual: SW2 ──────→ 74LS86[1]

Wire 7: D24 to D11
Purpose: Connects SW3 (Data B) to XOR Gate 1 Input B
Visual: SW3 ──────→ 74LS86[2]

Wire 8: D25 to D14
Purpose: Connects SW4 (Data C) to XOR Gate 2 Input B
Visual: SW4 ──────→ 74LS86[5]
```

### Critical Logic Bridge
```
Wire 9: C12 to C13
Purpose: Cascades XOR Gate 1 output to XOR Gate 2 input
Visual: 74LS86[3] ──────→ 74LS86[4]
Importance: Without this, 3-bit parity calculation fails
Function: Carries (A⊕B) to next stage for (A⊕B)⊕C
```

### Control and Output Wiring
```
Wire 10: D15 to G15
Purpose: Connects XOR Gate 2 output to XOR Gate 3 input A
Visual: 74LS86[6] ──────→ 74LS86[12]

Wire 11: H22 to Positive Rail (+)
Purpose: Powers switch pull-up for control bit
Visual: SW1[COM] ──────→ +5V Rail

Wire 12: D22 to G14
Purpose: Connects SW1 (Control) to XOR Gate 3 input B
Visual: SW1 ──────→ 74LS86[13]
Function: Programmable parity mode selection
```

### LED Connections
```
Odd Parity LED:
Wire 13: J16 to J6 (via resistor)
Wire 14: I6 (LED anode) to Negative Rail (cathode)
Visual: 74LS86[11] ─[330Ω]─→ LED ─→ GND
```

### Regulator Connections
```
Wire 15: C2 to Negative Rail (-)
Purpose: Regulator ground reference
Visual: LM7805[2] ──────→ GND Rail

Wire 16: C3 to Positive Rail (+)
Purpose: Regulator 5V output to power rail
Visual: LM7805[3] ──────→ +5V Rail

Battery: C1 (Red +) to C? (Black -)
Purpose: 9V input to regulator
Visual: 9V+ ──────→ LM7805[1]
        9V- ──────→ GND Rail
```

## Power Connection System
```
Power Flow Diagram:
9V Battery → LM7805 Input → LM7805 Regulator → 5V Output
    ↓                      ↓                      ↓
Battery +              Voltage Drop          Clean 5V
                    (9V→5V, 4V lost as heat)
    
Distribution Network:
+5V Rail ┬──→ 74LS86 Vcc (Pin 14)
         ├──→ DIP Switch Commons
         ├──→ XOR Gate 3 Input Power
         └──→ LED Current Source
         
GND Rail ┬──→ 74LS86 GND (Pin 7)
         ├──→ DIP Switch Pull-downs
         ├──→ LM7805 Ground
         ├──→ LED Cathodes
         └──→ Battery Negative
```

## Working Principle

### Parity Generation Logic
```
Step 1: First XOR Operation
A ⊕ B = Intermediate Result
(Gate 1: Pins 1,2 → Pin 3)

Step 2: Second XOR Operation
(A ⊕ B) ⊕ C = Raw Parity
(Gate 2: Pins 4,5 → Pin 6)
Bridge wire C12→C13 connects Step 1→Step 2

Step 3: Programmable Inversion
Raw Parity ⊕ Control = Final Output
(Gate 3: Pins 12,13 → Pin 11)
Control=0: Even Parity (no inversion)
Control=1: Odd Parity (inversion)
```

### Truth Table Analysis
| Control | A | B | C | Raw Parity | Final Output | LED State |
|---------|---|---|---|------------|--------------|-----------|
| 0 (Even) | 0 | 0 | 0 | 0 | 0 | Even ON |
| 0 (Even) | 0 | 0 | 1 | 1 | 1 | Odd ON |
| 0 (Even) | 0 | 1 | 0 | 1 | 1 | Odd ON |
| 0 (Even) | 0 | 1 | 1 | 0 | 0 | Even ON |
| 1 (Odd) | 0 | 0 | 0 | 0 | 1 | Odd ON |
| 1 (Odd) | 0 | 0 | 1 | 1 | 0 | Even ON |
| 1 (Odd) | 0 | 1 | 0 | 1 | 0 | Even ON |
| 1 (Odd) | 0 | 1 | 1 | 0 | 1 | Odd ON |

### Error Detection Demonstration
```
Transmission Scenario:
Data: 1 0 1 (Odd number of 1's)
Even Parity Mode Selected
Parity Bit Generated: 1
Transmitted: 1 0 1 1 (Even total: 3 ones)

Error Injection (Noise):
Received: 1 1 1 1 (Even total: 4 ones)

Verification:
Recalculated Parity: 0 (1⊕1⊕1=1, Even mode inverts)
Parity Mismatch: Received 1 vs Calculated 0
Conclusion: ERROR DETECTED
```

## Applications

### Real-World Implementations
```
1. Serial Communication (UART)
   Data: 8 bits + Parity + Stop bit
   Purpose: Detect single-bit transmission errors

2. Computer Memory (ECC RAM)
   Extended Version: 64-bit data + 8-bit parity
   Advanced: Hamming codes for error correction

3. Storage Systems (RAID 5)
   Distributed parity across multiple disks
   Single disk failure recovery

4. Network Protocols (Ethernet)
   Frame Check Sequence (32-bit CRC)
   More robust than simple parity
```

### Scalability Options
```
Current: 3-bit parity
Extended: 8-bit using cascaded XOR gates
          74LS86 × 2 = 8-bit parity generator

Advanced: Error Correction
          Hamming(7,4): 4 data + 3 parity bits
          Can detect and correct single errors

Professional: Reed-Solomon codes
             Used in CDs, DVDs, QR codes
             Corrects burst errors
```

## Troubleshooting

### Common Issues and Solutions
```
Problem 1: No Power Anywhere
Check: Battery connection (C1 to regulator)
Check: Regulator orientation (silver back facing out)
Check: Power rail bridges (rows 2-4 connected)

Problem 2: Chip Gets Hot
Check: Voltage at Pin 14 (should be 5V, not 9V)
Check: Output short circuit
Check: Wrong IC type (74LS86, not 74LS00)

Problem 3: LEDs Don't Light
Check: LED polarity (long leg = anode = +)
Check: Resistor values (330Ω, not 10kΩ)
Check: Ground connections (all LEDs to same rail)

Problem 4: Unstable Operation
Check: Missing pull-down resistors (B23-B25)
Check: Loose bridge wire (C12→C13)
Check: Power rail continuity
```

### Voltage Check Points
```
Test Point           Expected Voltage   Tolerance
Battery + to -      9.0V               8.0-9.5V
LM7805 Output       5.0V               4.75-5.25V
74LS86 Pin 14       5.0V               4.75-5.25V
Switch HIGH state   5.0V               >4.5V
Switch LOW state    0.0V               <0.8V
LED Anode           5.0V or 0.0V       Depends on logic
```

### Modification Guide
```
Request: Show both parity states simultaneously
Add: LED from G15 to GND via 330Ω
Result: Shows pre-inversion parity state

Request: Permanent Odd Parity mode
Change: Connect G14 directly to +5V (remove D22→G14)
Result: Always inverted output

Request: 4-bit parity generator
Add: Switch to 74LS86 Pin 9
Add: Bridge from Pin 8 to Pin 12
Result: Extended to 4 data bits
```

## Final Verification Checklist
- [ ] LM7805 properly oriented (silver back outward)
- [ ] 74LS86 notch facing correct direction (Row 10)
- [ ] Bridge wire C12→C13 present and secure
- [ ] All pull-down resistors connected (B23-B25)
- [ ] LED polarities correct (long leg to +)
- [ ] Power rails properly bridged (rows 2-4)
- [ ] Battery connected with correct polarity
- [ ] DIP switch controls functioning
- [ ] Both parity modes selectable via SW1
- [ ] LEDs respond to input combinations

## Learning Outcomes
1. **Parity Theory**: Understanding of error detection principles
2. **XOR Logic**: Application of exclusive-OR for parity calculation
3. **Voltage Regulation**: Importance of proper power supply
4. **Digital Design**: Cascading logic gates for complex functions
5. **Practical Prototyping**: Breadboard assembly and debugging

**Project Complete!** The circuit demonstrates fundamental error detection techniques used in all digital communication systems.
