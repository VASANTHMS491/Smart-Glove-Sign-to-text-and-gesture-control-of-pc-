# Smart-Glove-Sign-to-text-and-gesture-control-of-PC
## Description
Smart Glove is an ESP32-based wearable device that operates in two modes: a Sign-to-Text mode that converts hand signs into English alphabets, and a Gesture Control mode where a few predefined hand gestures are used to control the arrow keys of a PC. The system uses low cost DIY touch sensors for touch detection.
## Features
### Sign to text conversion
Detects specific hand sign patterns and prints the corresponding English alphabet.
### Gesture Control
Controls PC functions using gestures (scrolling, navigation etc.)
### DIY touch sensors
Simple aluminium based DIY touch sensors for low-cost and high responsiveness.
## Hardware used
1.ESP-32 Dev module
2.DIY touch sensors(Aluminium foil + wires)
3.Jumper wires
4.Gloves
5.Breadboard
6.Micro USB cable
7.Glue
8.Resistors(10k ohm)
## Software requirements
1.Arduino IDE
2.Python 3
3.Libraries used:
  1.pyserial
  2.pyautogui
  3.time
  4.serial
## Alphabet Mappings (Sensor → Letter Mapping)
  The glove uses **four touch sensors** (Index, Middle, Ring, Pinky).  
Each sensor outputs an analog value, and if it crosses a threshold, that finger is considered **touched (1)**, otherwise **not touched (0)**.
The four sensor states are combined into a **4-bit pattern**:

### Mapping Table

| Pattern (Binary) | Fingers Active         | Letter |
| ---------------- | -------------------- | ------ |
| 0001             | Index                 | A      |
| 0010             | Middle                | B      |
| 0011             | Middle + Index        | C      |
| 0100             | Pinky                 | D      |
| 0101             | Pinky + Index         | E      |
| 0110             | Pinky + Middle        | F      |
| 0111             | Pinky + Middle + Index| G      |
| 1000             | Ring                  | H      |
| 1001             | Ring + Index          | I      |
| 1010             | Ring + Middle         | J      |
| 1011             | Ring + Middle + Index | K      |
| 1100             | Ring + Pinky          | L      |
| 1101             | Ring + Pinky + Index  | M      |
| 1110             | Ring + Pinky + Middle | N      |
| 1111             | All Four Fingers      | O      |

### Notes / Tips

- **Threshold Adjustment:** The analog threshold (`THRESH`) may need calibration depending on sensor sensitivity.  
- **Debouncing:** Short accidental touches can be ignored using a small delay in code.  
- **Extensibility:** Additional letters can be mapped by including the **thumb** or using gesture combinations.

## Gesture Control (Glove → PC Actions)
The smart glove can be used to **control your PC using hand gestures**.  
It uses **four touch sensors** (Index, Middle, Ring, Pinky) connected to an ESP32, which send analog values to a Python script.  
Each sensor value above a threshold (`THRESH = 2000`) is considered **touched (1)**, otherwise **not touched (0)**.
The four sensor states form a **4-bit pattern**, which is mapped to specific PC actions:


### Gesture Mapping Table

| Pattern (Binary) | Fingers Active         | Action (PyAutoGUI) |
| ---------------- | -------------------- | ----------------- |
| 0001             | Index                 | Down Arrow         |
| 0100             | Pinky                 | Left Arrow         |
| 0010             | Middle                | Right Arrow        |
| 1000             | Ring                  | Up Arrow           |
| Others           | Any other combination | None / No Action   |

### Notes / Tips

- **Threshold Adjustment:** The analog threshold (`THRESH`) may need calibration depending on sensor sensitivity.  
- **Single Trigger per Gesture:** The script ensures each gesture triggers **only once** while the fingers remain pressed.  
- **Extensibility:** Additional gestures can be added by detecting more finger combinations or including the thumb.  


## Installation & Running the Project

Follow these steps to get the **Smart Glove** project up and running.

---

### 1. Upload ESP32 Code
1. Open the **Arduino IDE**.  
2. Connect your **ESP32 board** to your PC using a USB cable.  
3. Select the correct **board** and **port** from `Tools → Board` and `Tools → Port`.  
4. Open the provided Arduino/ESP32 sketch (`smart_glove.ino`).  
5. Click **Upload** to flash the code to the ESP32.

> ⚠ Make sure your sensors (Index, Middle, Ring, Pinky) are correctly connected to the analog pins defined in the code.

---

### 2. Connect ESP32 to PC
1. Keep the ESP32 connected via USB.  
2. Note the **COM port** assigned to the board (e.g., `COM6`).  
3. The Python script will read sensor data from this serial port.

---

### 3. Install Python & Dependencies
1. Ensure you have **Python 3.8+** installed. You can download it from [python.org](https://www.python.org/downloads/).  
2. Open a terminal or command prompt and install the required packages:

```
pip install pyserial pyautogui

pyserial → Communicates with the ESP32 over the serial port.
pyautogui → Simulates keyboard/mouse actions for gesture control.



