# // Motor pins
#define IN1 9
#define IN2 8
#define IN3 7
#define IN4 6

// IR Sensor pins
#define LEFT_SENSOR A0
#define RIGHT_SENSOR A1

void setup() {
  // Motor pins as output
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);

  // IR Sensor pins as input
  pinMode(LEFT_SENSOR, INPUT);
  pinMode(RIGHT_SENSOR, INPUT);
}

void loop() {
  int left = digitalRead(LEFT_SENSOR);
  int right = digitalRead(RIGHT_SENSOR);

  if (left == LOW && right == LOW) {
    // Both sensors on black → go forward
    forward();
  } else if (left == LOW && right == HIGH) {
    // Left on black, right on white → turn left
    turnLeft();
  } else if (left == HIGH && right == LOW) {
    // Right on black, left on white → turn right
    turnRight();
  } else {
    // Both on white → stop or search
    stopMotors();
  }
}

void forward() {
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void turnLeft() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void turnRight() {
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
}

void stopMotors() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
}