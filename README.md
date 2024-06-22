<div align="center">
    <img src="https://github.com/Diksha2220/Media/blob/main/moorseCode.gif" alt="Caesar Cipher" width="500"/>
</div>


### Project Idea: 🌐 Morse Code Translator with Arduino Uno and IR Sensor

#### Objective:
Create a Morse code translator using Arduino Uno and an IR sensor to detect eye blinks. This project enables users to input Morse code through eye blinks, which are detected by an IR sensor, and then translate that input into text displayed via serial monitor.

#### Components Needed:
- Arduino Uno board 🛠️
- IR LED and photodiode module 📡
- LEDs (at least two, one for dot and one for dash) 💡
- Resistors (220 ohms for LEDs) ⚡
- Jumper wires 🔗

#### Circuit Setup:
1. **IR Sensor Connections**:
   - Connect the IR LED of the module to digital pin 2 of the Arduino through a current-limiting resistor (typically 220 ohms).
   - Connect the photodiode (receiver) of the module to analog pin A0 of the Arduino.
   - Power and ground connections as per the module specifications.

2. **LED Connections**:
   - Connect one LED (let's call it `dot_led`) to digital pin 3 of the Arduino through a 220-ohm resistor.
   - Connect another LED (let's call it `dash_led`) to digital pin 4 of the Arduino through a 220-ohm resistor.

#### Arduino Sketch (Code):

```cpp
const int ir_led_pin = 2;   // IR LED pin
const int photodiode_pin = A0;  // Photodiode pin
const int dot_led = 3;   // LED pin for dot
const int dash_led = 4;  // LED pin for dash

void setup() {
  Serial.begin(9600);
  pinMode(ir_led_pin, OUTPUT);
  pinMode(dot_led, OUTPUT);
  pinMode(dash_led, OUTPUT);
}

void loop() {
  // Wait for a blink detected by IR sensor
  if (detectBlink()) {
    translateToMorse();
  }
}

bool detectBlink() {
  digitalWrite(ir_led_pin, HIGH);  // Turn on IR LED
  delay(10);  // IR LED stabilization time
  
  int sensor_value = analogRead(photodiode_pin);  // Read photodiode value
  
  digitalWrite(ir_led_pin, LOW);  // Turn off IR LED
  return (sensor_value < 100);  // Adjust this threshold as needed
}

void translateToMorse() {
  String morse_code = "";
  
  while (true) {
    int blink_duration = detectDotOrDash();  // Detect dot or dash duration
    
    if (blink_duration == -1) {
      break;  // End of input (long blink)
    } else if (blink_duration == 1) {
      morse_code += '.';  // Dot
    } else if (blink_duration == 3) {
      morse_code += '-';  // Dash
    }
  }
  
  String text = morseToText(morse_code);  // Translate Morse code to text
  Serial.println("Translated Text: " + text);
}

int detectDotOrDash() {
  unsigned long start_time = millis();
  
  while (true) {
    int sensor_value = analogRead(photodiode_pin);  // Read photodiode value
    
    if (sensor_value < 100) {
      return (millis() - start_time < 500) ? 1 : 3;  // Dot or dash duration
    } else if (millis() - start_time > 1000) {
      return -1;  // End of input (long blink)
    }
  }
}

String morseToText(String morse_code) {
  // Morse code to text translation logic
  // Implement your translation logic here based on previous examples
  // This depends on how you want to handle morse code translation
  
  // Example implementation:
  String translated_text = "";
  // Add translation logic here
  
  return translated_text;
}
```

### How It Works:
- **IR Sensor**: The IR LED and photodiode module is used to detect eye blinks. When the photodiode detects a change in IR light intensity (due to an eye blink), it triggers Morse code detection.
- **Morse Code Detection**: The `detectBlink()` function checks for a blink using the IR sensor. Once a blink is detected, the `translateToMorse()` function converts the blink duration into Morse code dots and dashes (`.` and `-`).
- **Morse Code Translation**: The detected Morse code is then translated into text using the `morseToText()` function, similar to the previous examples.

### Usage:
1. Upload the Arduino sketch to your Arduino Uno.
2. Ensure the IR LED and photodiode module is correctly connected to the Arduino according to the circuit setup.
3. Open the Arduino IDE serial monitor (or any serial monitor application).
4. Blink your eyes in Morse code patterns (short blinks for dots, longer blinks for dashes).
5. The Arduino will detect and translate the Morse code input into text, which will be displayed on the serial monitor.

This project showcases the use of Arduino Uno and IR sensors for real-time communication through eye blinks, making it accessible and interactive for individuals who communicate using eye movements.

📄 [View Main Code File](https://github.com/Diksha2220/Morse_Code_project/blob/main/morse%20code%20report.pdf)
📊 [View Presentaion File](https://github.com/Diksha2220/Morse_Code_project/blob/main/Morse-Code%20.pptx)
🗃️ [View Morse Code Sheet](https://github.com/Diksha2220/Morse_Code_project/blob/main/CodeSheet.jpg)

<div align="center">
    <img src="https://github.com/Diksha2220/Media/blob/main/MCodeAtoZ.gif" alt="Caesar Cipher" width="500"/>
</div>

