# Shadow Alarm: Interactive Light and Sound Alert System
**A Step-by-Step Arduino Starter Project Using Kit 1**

Build an interactive alert system using components from Kit 1. This project reads ambient light levels using a photoresistor. When someone casts a shadow or blocks the light, the Arduino triggers a multi-tone alarm through a passive buzzer.

---

## Step-by-Step Assembly Guide

### Step 1: Gather Your Components
Collect your Arduino Uno R3, USB cable, breadboard, photoresistor, passive buzzer, one 220-ohm resistor (used in place of the 10-ohm for better sensitivity), and several connector wires from Kit 1.

### Step 2: Connect Power to the Breadboard
Plug a wire from the **5V** pin on the Arduino to the positive rail of your breadboard, and a wire from a **GND** pin to the negative rail.

### Step 3: Wire the Photoresistor Circuit
1. Insert the photoresistor into two separate rows on the breadboard.
2. Connect one leg of the photoresistor to the **5V** power rail.
3. Connect the other leg to **Analog Pin A0** on the Arduino.
4. Connect a **220-ohm resistor** from that same photoresistor leg over to the **GND** rail to complete the voltage divider.

### Step 4: Wire the Passive Buzzer
1. Insert the passive buzzer into the breadboard.
2. Connect the positive (longer) leg to **Digital Pin 8** on the Arduino.
3. Connect the negative (shorter) leg to the **GND** rail.

### Step 5: Upload the Code
Connect your Arduino Uno to your computer via USB, open the Arduino IDE, paste the code below, select your board and port, and click Upload. Open the Serial Monitor at 9600 baud to test blocking the sensor.

---

## Arduino Sketch

```cpp
const int photoPin = A0;   
const int buzzerPin = 8;   
int threshold = 500;       

void setup() {
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int lightLevel = analogRead(photoPin);
  Serial.print("Light Level: ");
  Serial.println(lightLevel);

  if (lightLevel < threshold) {
    for (int i = 1000; i <= 2000; i += 100) {
      tone(buzzerPin, i, 100);
      delay(50);
    }
  } else {
    noTone(buzzerPin); 
  }
  
  delay(200);
}
