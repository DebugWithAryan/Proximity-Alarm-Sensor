# Proximity Alarm Sensor

This project implements a **Proximity Alarm Sensor** using an Arduino UNO, an ultrasonic sensor, an LED, and a buzzer. The system detects objects within a specified distance and triggers a visual (LED) and audible (buzzer) alarm.

## Features
- Measures distance using an ultrasonic sensor (HC-SR04).
- Triggers an alarm when an object is detected within a set threshold.
- Simple and easy-to-build circuit with Arduino.

## Components Required

| Component        | Quantity |
|------------------|----------|
| Arduino UNO      | 1        |
| Ultrasonic Sensor (HC-SR04) | 1 |
| LED              | 1        |
| Buzzer           | 1        |
| Resistors (220Ω) | 1        |
| Breadboard       | 1        |
| Jumper Wires     | As needed |

## Circuit Diagram

1. **Ultrasonic Sensor**
   - VCC → 5V (Arduino)
   - GND → GND (Arduino)
   - Trig → Digital Pin 9
   - Echo → Digital Pin 10

2. **LED**
   - Anode → Digital Pin 6 (via 220Ω resistor)
   - Cathode → GND

3. **Buzzer**
   - Positive → Digital Pin 7
   - Negative → GND

## Installation and Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/proximity-alarm-sensor.git
   ```
2. Open the Arduino IDE and upload the code to your Arduino UNO.
3. Connect the components as per the circuit diagram.
4. Power the Arduino and observe the system in action.

## Arduino Code

```cpp
#define TRIG_PIN 9
#define ECHO_PIN 10
#define LED_PIN 6
#define BUZZER_PIN 7

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  long duration, distance;

  // Send a 10µs pulse to the Trig pin
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // Read the Echo pin, and calculate the distance
  duration = pulseIn(ECHO_PIN, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  // Check if the object is within 10 cm
  if (distance > 0 && distance <= 10) {
    digitalWrite(LED_PIN, HIGH); // Turn on LED
    digitalWrite(BUZZER_PIN, HIGH); // Turn on Buzzer
  } else {
    digitalWrite(LED_PIN, LOW); // Turn off LED
    digitalWrite(BUZZER_PIN, LOW); // Turn off Buzzer
  }

  delay(100); // Small delay to stabilize readings
}
```

## How It Works

1. The **ultrasonic sensor** sends out sound waves via the **Trig** pin and waits to receive the reflected waves on the **Echo** pin.
2. The time taken for the sound waves to return is used to calculate the distance to the object.
3. If the distance is within the threshold (e.g., 10 cm), the LED lights up and the buzzer sounds.
4. If the distance exceeds the threshold, both the LED and buzzer turn off.

## Customization

- Adjust the distance threshold by modifying the value in the `if` condition.
- Integrate with a notification system using a Wi-Fi module like ESP8266 for remote alerts.
- Use a portable power source to make the system mobile.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing
Feel free to contribute to this project by submitting issues or pull requests.

## Acknowledgments
- Inspired by various Arduino proximity sensor projects available online.

## Contact
For any queries or feedback, please contact [your-email@example.com](mailto:your-email@example.com).

---
Happy Coding!
