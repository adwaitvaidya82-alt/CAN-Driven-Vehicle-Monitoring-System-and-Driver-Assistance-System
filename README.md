# CAN-Driven-Vehicle-Monitoring-System-and-Driver-Assistance-System
This three-node CAN-Driven Vehicle Monitoring and Driver Assistance System uses the CAN protocol, LPC2129 microcontrollers, and Embedded-C to monitor engine temperature and fuel levels, manage directional indicators, and provide real-time reverse obstacle detection.

<img width="1280" height="576" alt="IMG-20261003-WA0037 jpg" src="https://github.com/user-attachments/assets/6d28afb1-792d-48c0-bd89-93429bdc83ce" />

<img width="1600" height="900" alt="IMG-20261003-WA0011 jpg" src="https://github.com/user-attachments/assets/64f57775-10de-4c74-96eb-6d1795f1d34b" />

<img width="930" height="517" alt="image" src="https://github.com/user-attachments/assets/6f376d92-34e8-4986-b516-2243282d542b" />


Node 1: Main Node

This is the central controller and dashboard of the project.

Its responsibilities are:

Read engine temperature from the temperature sensor and display it on the LCD.

Receive fuel percentage from the Fuel Node over CAN.

Monitor the mode selection switch through an external interrupt.

In Forward Mode, monitor the left and right indicator switches and send commands to the Indicator Node.

In Reverse Mode, receive the reverse alert status and display SAFE, WARNING, or STOP on the LCD.
The dashboard displays engine temperature, fuel percentage, vehicle mode and reverse alert status.

Node 2: Fuel Node

This node is responsible for fuel monitoring.

The fuel sensor provides an electrical signal corresponding to the fuel level.

The LPC2129's built-in ADC converts the analog input voltage into a digital value.

The program converts the ADC reading into a fuel percentage using the appropriate sensor calibration.

The calculated percentage is periodically transmitted to the Main Node through CAN.

If the fuel percentage changes significantly, the updated value is transmitted immediately.

Example: If the calibrated sensor reading corresponds to 65% fuel, the Fuel Node sends that percentage to the Main Node, which displays it on the LCD.

Node 3: Indicator and Reverse Alert Node

This node handles two different operating modes.

Forward Mode: It receives left/right indicator commands and blinks the corresponding LEDs. An indicator-off command switches off all indicator LEDs. Reverse obstacle detection is disabled.

Reverse Mode: Normal indicator operation is switched off, and the HC-SR05 ultrasonic sensor is enabled to detect obstacles behind the vehicle.

The sensor measures obstacle distance, and the program compares it with predefined distance limits to determine the alert status.
