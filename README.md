# PUSH-BUTTON-COUNTER-TASK1

*COMPANY*: CODTECH IT SOLUTIONS 
*NAME*: MINUKOORI NAVYA
*INTERN ID*:CT12EHE
*DOMAIN*: EMBEDDED SYSTEMS
*BATCH DURATION*:DECEMBER 17th, 2025 TO FEBURARY 17th, 2025 
*MENTOR NAME*:NEELA SANTOSH KUMAR

# DESCRPITION OF THE TASK
OBJECTIVE:
   The main objective of this project is to design and implement a push-button counter integrated with a temperature sensing system, capable of reading and displaying real-time temperature data. The system utilizes a temperature sensor to capture ambient or object-specific temperature readings, which are then processed and displayed on an LCD screen or communicated via a serial monitor. The push-button functionality enables user interaction, such as toggling between modes, resetting the counter, or updating the display. This project demonstrates the integration of sensing, processing, and display technologies, offering a practical solution for monitoring environmental conditions with user-friendly controls.

INTRODUCTION:
  This project focuses on developing a versatile system that combines a push-button counter with a temperature sensor for real-time monitoring and display of temperature data. The temperature sensor captures accurate environmental readings, which are processed by a microcontroller and displayed on an LCD or transmitted to a serial monitor. The push-button functionality provides user interactivity, enabling actions such as resetting the counter or switching between different display modes. This project highlights the practical integration of sensor technology and user interface components, making it ideal for applications in environmental monitoring, educational tools, and simple IoT solutions.

KEY ACTIVITIES:
1.System Design and Component Selection
Identifying and sourcing the required components such as a temperature sensor (e.g., LM35 or DHT11), microcontroller (e.g., Arduino), push button, LCD display, or serial monitor.

2.Hardware Integration
Connecting the temperature sensor to the microcontroller to capture temperature data.
Integrating a push button to provide user input functionality.
Interfacing the LCD or serial monitor to display the data effectively.

3.Software Development
Writing code to read data from the temperature sensor and process it.
Implementing functionality to count button presses and integrate this feature with temperature readings.
Developing algorithms to update and display the data on the LCD or serial monitor in real time.

4.Testing and Calibration
Calibrating the temperature sensor for accurate readings.
Testing the push-button response and ensuring data consistency across all outputs.

5.Project Assembly and Demonstration
Assembling the system into a cohesive setup.
Demonstrating the functionality, including real-time temperature display and push-button counter operation.
These activities ensure the project is built systematically, focusing on both functionality and reliability.

SOURCE CODE:
#include <LiquidCrystal.h> // Include the library for the LCD

// Pin configuration
const int tempSensorPin = A0; // Analog pin for temperature sensor (e.g., LM35)
const int buttonPin = 2;      // Digital pin for push button
const int lcdRS = 7, lcdEN = 8, lcdD4 = 9, lcdD5 = 10, lcdD6 = 11, lcdD7 = 12; // LCD pins

// LCD object
LiquidCrystal lcd(lcdRS, lcdEN, lcdD4, lcdD5, lcdD6, lcdD7);

// Variables
float temperature = 0.0; // Variable to store temperature value
int buttonPressCount = 0; // Counter for button presses
int lastButtonState = LOW; // Track the last button state
unsigned long debounceDelay = 50; // Debounce time in milliseconds
unsigned long lastDebounceTime = 0; // Last debounce time

void setup() {
  // Initialize the LCD
  lcd.begin(16, 2); // 16x2 LCD
  lcd.print("Temp: --.- C");
  lcd.setCursor(0, 1);
  lcd.print("Count: 0");

  // Set pin modes
  pinMode(tempSensorPin, INPUT);
  pinMode(buttonPin, INPUT_PULLUP); // Use internal pull-up resistor for the button

  // Serial monitor setup
  Serial.begin(9600);
}

void loop() {
  // Read and calculate temperature
  int tempValue = analogRead(tempSensorPin);
  temperature = (tempValue * 5.0 / 1023.0) * 100.0; // For LM35: Temp in Celsius

  // Debounce button press
  int reading = digitalRead(buttonPin);
  if (reading != lastButtonState) {
    lastDebounceTime = millis();
  }

  if ((millis() - lastDebounceTime) > debounceDelay) {
    if (reading == LOW && lastButtonState == HIGH) { // Button pressed
      buttonPressCount++;
    }
  }
  lastButtonState = reading;

  // Display temperature and counter on LCD
  lcd.setCursor(6, 0);
  lcd.print(temperature, 1); // Print temperature with 1 decimal place
  lcd.setCursor(7, 1);
  lcd.print(buttonPressCount);

  // Optional: Print temperature and counter to serial monitor
  Serial.print("Temperature: ");
  Serial.print(temperature, 1);
  Serial.print(" C, Button Presses: ");
  Serial.println(buttonPressCount);

  delay(500); // Delay for stability
}

BLOCK DIAGRAM:https://github.com/minukurinavya/PUSH-BUTTON-COUNTER-TASK1/commit/0258277b4209796dc740aa433460ffb3e076eac6

WORKING EXPLANATION:
The push button is used to activate the system. When the button is pressed, the circuit is powered on, and the microcontroller (e.g., Arduino) begins executing the code.The temperature sensor continuously reads the surrounding temperature. If using a sensor like the LM35, it gives an analog output proportional to the temperature, which is read by the microcontroller's analog input pin.After reading the sensor’s value, the microcontroller converts this raw data into a readable temperature value (in Celsius or Fahrenheit).The LCD or serial monitor displays this temperature reading in real-time. If using an LCD, the microcontroller sends the temperature data to the display, updating it continuously or at a set interval. If using a serial monitor, the data is transmitted over the serial communication line and displayed on the connected computer screen.The push button serves as a trigger to start or reset the process, which is useful for data logging or periodic measurements.This project demonstrates how user input (via the push button) can control the flow of data acquisition and display from a sensor, making it interactive and useful for monitoring environmental conditions.

CONCLUSION:
 The Push Button Counter with a temperature sensor is an effective and interactive project that integrates basic input/output mechanisms with real-world sensor data. By using a push button to trigger the system, users can control when temperature readings are displayed, either on an LCD or through a serial monitor. This setup allows for easy monitoring of temperature fluctuations, making it suitable for applications such as room temperature monitoring, environmental control, or educational purposes in electronics and programming. Additionally, it demonstrates how simple components like sensors, buttons, and displays can work together to provide valuable feedback in an intuitive and user-friendly manner. The project serves as a practical introduction to sensor-based systems, microcontroller programming, and user input handling, offering endless opportunities for further customization and expansion. 

WORKING OUTPUT:https://github.com/minukurinavya/PUSH-BUTTON-COUNTER-TASK1/commit/b8b0cbb300cd2fb2d8d828a7cd211d00e44155cc
