#define TRIG_PIN 10
#define ECHO_PIN 11

#define SOAP_RELAY 6     // Active LOW
#define WATER_RELAY 7    // Active LOW

int getDistance();   // ---- FUNCTION DECLARATION ----

// -------- SETUP --------
void setup() {
  Serial.begin(9600);

  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);

  pinMode(SOAP_RELAY, OUTPUT);
  pinMode(WATER_RELAY, OUTPUT);

  digitalWrite(SOAP_RELAY, HIGH);
  digitalWrite(WATER_RELAY, HIGH);

  Serial.println("Handwash System Ready");
}

// -------- LOOP --------
void loop() {
  int distance = getDistance();

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance > 0 && distance < 12) {

    Serial.println(">>> HAND DETECTED <<<");

    Serial.println("SOAP ON");
    digitalWrite(SOAP_RELAY, LOW);
    delay(2000);
    digitalWrite(SOAP_RELAY, HIGH);
    Serial.println("SOAP OFF");

    Serial.println("RUB TIME");
    delay(5000);

    Serial.println("WATER ON");
    digitalWrite(WATER_RELAY, LOW);
    delay(9000);
    digitalWrite(WATER_RELAY, HIGH);
    Serial.println("WATER OFF");

    Serial.println("WAITING FOR HAND REMOVAL");
    while (getDistance() < 12) {
      delay(100);
    }

    Serial.println("HAND REMOVED");
  }

  delay(100);
}

// -------- ULTRASONIC FUNCTION --------
int getDistance() {
  long duration;

  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  duration = pulseIn(ECHO_PIN, HIGH, 30000);

  if (duration == 0) return 50;   // no echo

  return duration * 0.034 / 2;
}

