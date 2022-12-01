
// ---------------------------------------------------------------- // 
// Follower Bot - EGN3000L Teamwork Fabrication Assignmnet
// Created by Mason Kelly
// Using Arduino IDE 1.8.19
// ---------------------------------------------------------------- // 

// define varibales

int echoPin = 8; // attach pin D8 to pin Echo of HC-SR04
int trigPin = 7; // attach pin D7 to pin Trig of HC-SR04
int in1 = 4; // Name variables for motor outputs
int in2 = 5; // Name variables for motor outputs
int in3 = 9; // Name variables for motor outputs
int in4 = 10; // Name variables for motor outputs

int ledpin = 13; //connect pin 13 to LED pin

long duration; // duration of sound wave travel
int gaplength; // legnth of the gap between the sensor and any object

void setup() {

  pinMode (trigPin, OUTPUT) ; // sonar digital pin mode for trig
  pinMode (echoPin, INPUT); // sonar digital pin mode for echo
  
  pinMode (in1, OUTPUT); // make all motor pins outputs
  pinMode (in2, OUTPUT); // make all motor pins outputs
  pinMode (in3, OUTPUT); // make all motor pins outputs
  pinMode (in4, OUTPUT); // make all motor pins outputs
  pinMode (ledpin, OUTPUT) ; // configure LCD pin as an output

  Serial.begin (9600) ; // 9600 baud rate is used for serial communication

  
}


void loop() {
  

  // Establish trigPin conditions
  // trig pin starts LOW
  digitalWrite (trigPin, LOW);
  // 10 microsecond delay for hardware response
  delayMicroseconds (8); 
  // makes trig pin HIGH
  digitalWrite (trigPin, HIGH);
  // trig pin in HIGH state for 10 microseconds
  delayMicroseconds (8) ; 
  // trig pin is LOW after  microseconds
  digitalWrite (trigPin, LOW); 
  // stores duration after echo intercepts pulse
  duration = pulseIn (echoPin, HIGH); 
  // Converts the time of flight to length of gap from sensor to object
  gaplength = duration * 0.034 / 2; 

  // Serial Monitor displays length of gap between sensor and object
  Serial.print ("Gap Length: ");
  Serial.print (gaplength);
  Serial.println(" cm");
  
  // robot turns left if gap length is at most 5 cm
  if (gaplength <= 10) {

    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    digitalWrite(in3, LOW);
    digitalWrite(in4, HIGH);
    
  // robot turns right if gap length is at most 10 cm
  } else if (gaplength <= 20) {

    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);

    // robot moves backward if gap length is at most 20 cm
  } else if (gaplength <= 30) {

    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);

    // robot moves forward if gap length is at most 30 cm
  } else if (gaplength <= 40) {

    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    digitalWrite(in3, LOW);
    digitalWrite(in4, HIGH);

    // robot stays put if there are no objects in range of sensor
  } else {

    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);
    digitalWrite(in3, LOW);
    digitalWrite(in4, LOW);

    
  }
  delay(10);
  
}
