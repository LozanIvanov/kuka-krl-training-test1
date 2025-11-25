# 🤖 KUKA KRL Training Project – Test1 Program

This repository contains a training program written in **KUKA Robot Language (KRL)**.  
It demonstrates structured robot programming techniques used in real industrial automation.

The project was created and tested using **OrangeEdit** and is compatible with:
- KUKA KRC2  
- KUKA KRC4  
- KUKA.Sim (optional)  
- Any KUKA controller supporting KRL  

---

## 📂 Project Structure

```
/Test1
 ├── Test1.src       # Main robot program (motions + logic)
 └── Test1.dat       # Variable and position declarations
```

---

## 🧠 Concepts Demonstrated

This project includes examples of:

### ✔ Motion Commands
- `PTP` (joint move)
- `LIN` (linear move)
- Movement to multiple positions: P_A, P_B, P_C, P_D

### ✔ Logic and Control Flow
- `IF / ELSEIF / ELSE`
- `mode` variable switching
- `NOT`, `<>` (not equal)
- `BOOL` variable (`ready`)
- `SWITCH / CASE / DEFAULT`
- `WHILE` loops
- `FOR` loops
- Internal variable changes during program execution

### ✔ Data Structures
- `E6POS` position definitions (cartesian + orientation)
- INT, BOOL variables in .dat file

---

## 📝 Program Description

The Test1 program performs the following steps:

1. Moves robot to HOME.
2. Executes an IF/ELSEIF decision based on `mode`.
3. Changes `mode` dynamically and executes another decision.
4. Runs a **SWITCH-CASE** to select motions based on `mode`.
5. Executes a **WHILE loop** repeating motion until a condition is met.
6. Executes a **SWITCH-CASE** again after the loop.
7. Executes a **FOR loop** repeating motion three times.
8. Uses a `BOOL ready = FALSE` boolean check.
9. Executes a final sequence of LIN motions.
10. Returns robot to HOME.

This program shows the core logic patterns used by robot programmers in manufacturing environments.

---

## 📄 Source Code (Test1.src)

```krl
DEF Test1 ( )
;FOLD INI
  ;FOLD BASISTECH INI
    GLOBAL INTERRUPT DECL 3 WHEN $STOPMESS==TRUE DO IR_STOPM ( )
    INTERRUPT ON 3 
    BAS (#INITMOV,0 )
  ;ENDFOLD (BASISTECH INI)
  ;FOLD USER INI
    ;Make your modifications here
  ;ENDFOLD (USER INI)
;ENDFOLD (INI)

;FOLD PTP HOME 
$BWDSTART = FALSE
PDAT_ACT=PDEFAULT
FDAT_ACT=FHOME
BAS (#PTP_PARAMS,100 )
$H_POS=XHOME
PTP  XHOME
;ENDFOLD

IF mode == 1 THEN
   LIN P_A
ELSEIF mode == 2  THEN
   LIN P_C 
ELSE
   LIN P_B   
ENDIF   

mode=2 ;change the mode during the program  
IF mode == 2 THEN
   LIN P_C
ELSE
   LIN P_B
ENDIF

SWITCH mode
CASE 1
   LIN P_A
CASE 2
   LIN P_B
CASE 3
   LIN P_C
DEFAULT
   LIN P_D
ENDSWITCH
  
mode=1
  
WHILE mode<4
   LIN P_A
   mode=mode + 1 
ENDWHILE  

SWITCH mode
CASE 1
   LIN P_C
CASE 2
   LIN P_D
CASE 3
   LIN P_A
DEFAULT
   LIN P_B
ENDSWITCH

FOR i=1 TO 3
   LIN P_D
ENDFOR

IF NOT ready THEN
   LIN P_A
ENDIF 

; <> means NOT EQUAL, example: IF mode <> 1 THEN

LIN P_A
LIN P_B
LIN P_C
LIN P_D
PTP XHOME
END
```

---

## 📄 Data File (Test1.dat)

```krl
DEFDAT Test1 PUBLIC

DECL INT mode = 1
DECL BOOL ready = FALSE

DECL E6POS P_A = {X 3, Y 3, Z 4, A 0, B 0, C 0}
DECL E6POS P_B = {X -2, Y -2, Z -4, A 0, B 0, C 0}
DECL E6POS P_C = {X 1, Y 1, Z 0, A 0, B 0, C 0}
DECL E6POS P_D = {X 3, Y 4, Z 1, A 0, B 0, C 0}

;FOLD EXTERNAL DECLARATIONS
EXT BAS (BAS_COMMAND :IN, REAL :IN)
DECL INT SUCCESS
;ENDFOLD

ENDDAT
```

---

## 🛠 Requirements

- **OrangeEdit** (recommended IDE):  
  https://www.orangeapps.de  
- KUKA KRC2/KRC4 controller or KUKA.Sim for simulation

---

## 📸 Screenshots (optional to add)

You can add screenshots like:

```
/screenshots
 ├── orangeedit-view.png
 ├── program-structure.png
 └── simulation.png
```

---

## 💼 Skills Demonstrated

This project shows abilities in:

- Industrial robot programming  
- KUKA KRL logic and motion  
- Working with .SRC and .DAT files  
- Data structures and coordinate programming  
- Control flow and automation logic  
- Clean code structure for robots  
- Professional documentation  

Excellent for automation technician or robotics job applications.

---

## 📩 Author
Training program created by Lozan Ivanov.  
Use and modify freely for learning or portfolio purposes.
