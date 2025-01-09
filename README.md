

# **Gas Leakage Detection System** 🚨💨

This project uses a gas sensor and an SMS-based alert system to detect gas leaks and notify the user via a message. It utilizes an **Arduino** board, a **gas sensor**, a **buzzer**, an **LED**, and a **SIM800 GSM module** for sending SMS alerts. The system can be deployed in environments where gas leakage detection is critical, such as in kitchens or industrial settings.

---

## **✨ Features**

- **Gas Detection**: Monitors gas levels using a gas sensor (MQ series) and triggers an alert if the gas concentration exceeds a threshold.
- **SMS Alert System**: Sends an SMS to a predefined phone number using the GSM module (SIM800) when the gas level is too high.
- **Buzzer and LED Indicators**: Provides local audio and visual warnings (Buzzer and LED) when a gas leak is detected.
- **Real-time Monitoring**: Continuously monitors the gas level and displays the status on the Serial Monitor.

---

## **📂 Folder Structure**

- `Gas_Leakage_Detector.ino`  
  - Main Arduino sketch file containing the logic for gas level monitoring and SMS alerting.
- `README.md`  
  - Documentation for the project.
- `LICENSE`  
  - Open-source license details (if applicable).

---

## **🔧 Hardware Components**

- **Arduino Board** (e.g., Arduino Uno)
- **Gas Sensor** (e.g., MQ-2 or MQ-3 for gas detection)
- **SIM800 GSM Module** (for sending SMS alerts)
- **Buzzer**
- **LED**
- **Jumper wires**
- **Breadboard** (optional)
- **Power supply for the Arduino**

---

## **🔌 Circuit Connections**

| Component               | Pin Assignment   |
|-------------------------|------------------|
| **Gas Sensor**           | A0 (Analog Pin)  |
| **Buzzer**               | Pin 4            |
| **LED**                  | Pin 3            |
| **SIM800 GSM Module RX** | Pin 9            |
| **SIM800 GSM Module TX** | Pin 10           |
| **Arduino Board**        | Power Pins       |

---

## **⚙️ Software Requirements**

- Arduino IDE (version 1.8.10 or later)
- **SoftwareSerial Library**:  
  ```bash
  Install from Arduino Library Manager
  ```

---

## **🚀 How to Use**

1. **Setup**  
   - Connect the gas sensor, SIM800 module, buzzer, and LED as per the pin configuration.
   - Ensure the SIM800 GSM module is powered correctly and has a valid SIM card inserted with sufficient balance for sending SMS.
   
2. **Upload Code**  
   - Open the `Gas_Leakage_Detector.ino` file in Arduino IDE.
   - Select the correct board and port under **Tools**.
   - Upload the code to your Arduino board.

3. **Monitor Gas Level**  
   - Open the **Serial Monitor** at a baud rate of **9600** to view the real-time gas levels.
   - When the gas level exceeds the threshold (500), the system triggers the buzzer, LED, and sends an SMS alert.

4. **SMS Alerts**  
   - The system sends a message to the predefined phone number (`1234567890` in the code) when the gas level is too high.

---

## **💡 Code Overview**

### **Gas Level Detection**

The analog reading from the gas sensor is used to determine the gas level. If the reading exceeds the threshold, the system triggers an alert:

```cpp
data = analogRead(gasValue);
Serial.print("Gas Level: ");
Serial.println(data);

if (data > 500) {  // Threshold value for high gas level
  digitalWrite(led, HIGH);
  digitalWrite(Buzzer, HIGH);
  SendMessage();   // Send SMS Alert
  Serial.print("Gas detected");
} else {
  digitalWrite(led, LOW);
  digitalWrite(Buzzer, LOW);
  Serial.println("Gas Level Low");
}
```

### **Sending SMS Alert**

Using the `SoftwareSerial` library, the GSM module sends an SMS to the predefined phone number when the gas level exceeds the threshold:

```cpp
void SendMessage() {
  mySerial.println("AT+CMGF=1"); 
  delay(1000);
  mySerial.println("AT+CMGS=\"1234567890\"");
  delay(1000);
  mySerial.println("Alert!!! Excess Gas Detected");
  delay(100);
  mySerial.println((char)26);  // Send SMS command
  delay(1000);
}
```

---

## **📜 License**

This project is licensed under the **MIT License**. See the `LICENSE` file for details.

---

## **🤝 Contributing**

Contributions are welcome! You can:
- Submit a pull request with new features or bug fixes.
- Open an issue to report bugs or suggest improvements.

---

## **💬 Feedback**

For questions, suggestions, or feedback, feel free to open an issue or contact me directly.

---

Stay Safe! 🚨
