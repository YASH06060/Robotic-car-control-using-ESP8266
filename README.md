# WiFi Remote Control Car Firmware for NodeMCU (ESP8266)

This project implements a WiFi-controlled robotic car using the NodeMCU ESP8266 microcontroller and an L298N motor driver module. The car can be remotely controlled through HTTP commands via a web server hosted on the ESP8266. It supports motor driving commands (forward, backward, turn), speed control, buzzer horn, and LED control.

## Features

- Control two DC motors using L298N driver via ESP8266 GPIO pins.
- Supports directional commands:
  - Forward, Backward
  - Turn Left, Turn Right
  - Forward/Backward Left and Right diagonals
  - Stop
- Speed control via multiple speed levels (0-9, plus max speed).
- Built-in buzzer horn for beep notifications.
- LED control (on/off).
- WiFi connectivity:
  - Connects as a Station (STA) to existing WiFi network (configurable SSID/password).
  - Falls back to Access Point (AP) mode if STA connection fails, with device-hostname-based SSID.
- OTA (Over-The-Air) firmware updates enabled via ArduinoOTA.
- Web server listens on port 80, accepts HTTP requests with control commands.
- WiFi connection status indicated via LED.

## Hardware Connections

| NodeMCU Pin | Function                    |
|-------------|-----------------------------|
| D5          | Motor drive input 1 (in1)   |
| D6          | Motor drive input 2 (in2)   |
| D7          | Motor drive input 3 (in3)   |
| D8          | Motor drive input 4 (in4)   |
| D0          | Buzzer                      |
| D1          | LED                         |
| D2          | WiFi connection status LED  |

> Motors are connected to L298N motor driver inputs controlled by the above pins.

## Usage

1. Set your WiFi network credentials by assigning `sta_ssid` and `sta_password` variables in the source code.
2. Upload the firmware to the ESP8266 NodeMCU using Arduino IDE.
3. Upon powering on, the device attempts to connect to the configured WiFi as a station.
4. If unable to connect within 10 seconds, it switches to Access Point mode with a default hostname-based SSID.
5. Access the IP address displayed in the serial monitor to connect to the web server.
6. Use HTTP requests with command parameters to control the car. Commands are single letters representing actions, e.g.:
   - "F" - Forward
   - "B" - Backward
   - "L" - Turn Left
   - "R" - Turn Right
   - "S" - Stop
   - "V" - Beep horn
   - "W" - Turn LED on
   - "w" - Turn LED off
   - Speed control via digits '0' to '9' and 'q' for max speed.

## Libraries

- ESP8266WiFi
- ESP8266WebServer
- ArduinoOTA

Make sure these libraries are installed in your Arduino IDE prior to compiling.

## Notes

- Adjust motor pins and speeds in the source code if your hardware wiring or motor specs differ.
- Ensure external power supply for motors as needed; NodeMCU's onboard 3.3V pin may not supply enough current.
- The code handles basic input commands via HTTP GET requests; consider adding authentication for security in production use.


---

This project is an excellent example of how to build a WiFi-controlled embedded system with real-time motor control using ESP8266, making it suitable for IoT and robotics learning.

