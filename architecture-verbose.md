# IND-EDITOR master branch -- design stage
_Below is a brief synopsis on a typical text editor architecture. Case studies will be presented soon_
1. The working action of a text editor can be divided into three aspects:
   * Target output and view manipulation of elements {individual characters | size-bounded blocks}
   * Formatting and fonts.
   * Operations to modify the output that target a specific document portion. *It also includes :*
2. View updation and translation to the desired content and format.
3. Modification of a document involves inserting , editing , move , find and replace
4. Filtering of text processing output is an aspect that involves manipulation on blocks of characters.

=============================================================================================

Conceptual model
[ The abstraction into editing buffer , view buffer and window buffer ] :

__Editing buffer__ depends solely on the input : 

POSITIONING:
1. Positional converters : Mouse / Data Tablet OR Touchpad.
   * Device drivers for these hardware return the positional coordinates of the pointer.
   * These use analog to digital converters to observe user movements.
2. Arrow keys navigate the cursor to specified number of keypresses .
3. Voice input is an add-on feature using speech-to-text converters.

TYPING:
1. Latin characters can be typed directly from the keyboard layout using the ASCII subset of Unicode
2. Devanagari characters and other Indian fonts require additional character encodings and transliterations
that will be defined on a separate mapping file.
3. Unicode encoding is the defacto standard, followed by IAST and ISCII

__Viewing buffer__ is programmaticaly implemented and depends on the transition from input to output.
This includes limiting the number of characters on the screen , scrolling limitations and bounds 
on line size.

__Windowing buffer__ is a rectangular set or subset -- hard copy teletyping , professional workstations , 
and/or other displays.

To summarize : 3 logical views __without__ clear demarcations EDIT | VIEW | DISPLAY

INPUT --> COMMAND LANGUAGE PROCESSOR(CLP)
      OR
  ||  --> LOOSE - SEMANTIC TOKENIZER.
    
CLP --> EDIT BUFFER
     OR
 || --> HYBRID EDIT-VIEW BUFFER (EB)
 
CLP --> TRAVELLING COMPONENT (POSITION OF CURSOR AND / OR MOUSE POINTER )

MEMORY + VIRTUAL MEMORY --> VIEW BUFFER(VB)

VB --> DISPLAY

PAGINATION OF DISPLAY CONTENT 

DISPLAY --> WINDOW.

# DATA STRUCTURES AND OPERATIONS -- Simple grouping of functionalities:
1. _EDIT Buffer_  - Insert , Delete , Backspace , Return , Change Case(If applicable), Paste
2. _VIEW Buffer_  - Find AND Replace , Copy/Yank , Delete Line/BLock , Highlight
3. _DISPLAY Buffer_ - Window Count Maintenance , Font-Rendering , Filename and Status Display ( SAVE BUFFER | UNSAVED BUFFER 
| NEW BUFFER ) , Quit / Terminate, Minimize / Suspend , Maximize / Foreground , Resize Buffer
