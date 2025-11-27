# 🤖 KUKA KRL Training – Test Program

This repository contains a training program written in **KUKA Robot Language (KRL)**.  
The project is part of my preparation for working in industrial automation and demonstrates understanding of basic robot programming structures used on real KUKA robots.

---

## 📌 Project Overview

The program focuses on fundamental KUKA programming skills:

- Initialization and INI structure
- Defining and activating TOOL and BASE
- Working with Cartesian coordinates `{X, Y, Z, A, B, C}`
- Using predefined E6POS points
- Performing linear and joint motions (LIN / PTP)
- Implementing logic structures (IF / ELSEIF / ELSE)
- Using loops (WHILE, FOR)
- Safe return to HOME position

This is a clean and well-structured example that follows KUKA programming standards.

---

## 📂 Files Included

### **Test1.src**
Main robot program containing:

- INI block
- TOOL and BASE activation
- Basic Cartesian movements
- Logical conditions
- WHILE loop
- FOR loop
- Sequence of E6POS movements
- Final return to HOME

### **Test1.dat**
Data file with:

- Variables (mode, ready)
- Position definitions (P_A, P_B, P_C, P_D)
- Tool definition (TOOL_DATA[1])
- Required BAS external declarations

---

## 🔧 TOOL Configuration

The tool center point (TCP) is defined in `Test1.dat`:

```krl
TOOL_DATA[1] = {X 0, Y 0, Z 200, A 0, B 0, C 0}

