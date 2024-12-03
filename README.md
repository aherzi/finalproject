# finalproject
#include <Servo.h>
#include <NewPing.h>
// edit the pin according to your connection
#define ECHO_PIN     A3  // Arduino pin tied to echo pin on the ultrasonic sensor.
#define TRIGGER_PIN  A5 // Arduino pin tied to trigger pin on the ultrasonic sensor.
#define LEFTLEG       5
#define RIGHTLEG     9
#define LEFTFOOT      7
#define RIGHTFOOT     11
#define  HEAD          3
#define MAX_DISTANCE 200 // Maximum distance we want to ping for (in centimeters). Maximum sensor distance is rated at 400-500cm.
int Min_DISTANCE = 10;
NewPing sonar(TRIGGER_PIN, ECHO_PIN, MAX_DISTANCE); // NewPing setup of pins and maximum distance.
Servo Lleg;
Servo Rleg;
Servo Lfoot;
Servo Rfoot;
Servo Head;
int Hcenter = 90;
int RLcenter = 90;
int RFcenter = 90;
int LLcenter = 90;
int LFcenter = 90;
int tAngle = 20;    // tilt angle
int uAngle = 25;    // turn angle
int sAngle = 25;    // swing angle
int Speed = 50;    // Speed of walk 
void Forward(byte Steps, byte Speed){
  Serial.println("Forward"); 
  TiltRightUp(tAngle, Speed);
  for (byte j=0; j<Steps; ++j){
    SwingRight(sAngle, Speed);
    TiltRightDown(tAngle, Speed);
    TiltLeftUp(tAngle, Speed);
    SwingRcenter(sAngle, Speed);
    SwingLeft(sAngle, Speed);
    TiltLeftDown(tAngle, Speed);
    TiltRightUp(tAngle, Speed);
    SwingLcenter(sAngle, Speed);
  }
  TiltRightDown(tAngle, Speed);
}
void TurnLeft(byte Steps, byte Speed){
  Serial.println("TurnLeft"); 
  TiltLeftUp(uAngle, Speed);
  delay(20);
  for (byte j=0; j<Steps; ++j){
    LeftLegIn(sAngle, Speed);
    TiltLeftDown(uAngle, Speed);
    TiltRightUp(uAngle, Speed);
    delay(20);
    LeftLegIcenter(sAngle, Speed);
    RightLegOut(sAngle, Speed);
    TiltRightDown(uAngle, Speed);
    TiltLeftUp(uAngle, Speed);
    delay(20);
    RightLegOcenter(sAngle, Speed);
  }
  TiltLeftDown(uAngle, Speed);
}void TurnRight(byte Stps, byte Speed){
  Serial.println("TurnRight"); 
  TiltRightUp(uAngle, Speed);
  delay(20);
  for (byte f=0; f<=Stps; ++f){
    RightLegIn(sAngle, Speed);
    TiltRightDown(uAngle, Speed);
    TiltLeftUp(uAngle, Speed);
    delay(20);
    RightLegIcenter(sAngle, Speed);
    LeftLegOut(sAngle, Speed);
    TiltLeftDown(uAngle, Speed);
    TiltRightUp(uAngle, Speed);
    delay(20);
    LeftLegOcenter(sAngle, Speed);
  }
  TiltRightDown(uAngle, Speed);
}
void HeadRight() {
  Serial.println("HeadRight"); 
  Head.write(Hcenter - 105);             
  delay(1000);
}
void HeadLeft() {
  Serial.println("HeadLeft"); 
  Head.write(Hcenter + 105);        
  delay(1000);
}
void HeadCenter() {
  Serial.println("HeadCenter"); 
  Head.write(Hcenter);             
  delay(1000);
}
void TiltRightUp(byte ang, byte sp){ 
  //tilt right up
  for (int i=0; i<=ang; i+=5){
    Lfoot.write(LFcenter+i);
    Rfoot.write(RFcenter+i);
    delay(sp);
  }
}
void TiltRightDown(byte ang, byte sp){
  //tilt right down
  for (int i=ang; i>0; i-=5){
    Lfoot.write(LFcenter+i);
    Rfoot.write(RFcenter+i);
    delay(sp);
  }
}
void TiltLeftUp(byte ang, byte sp){
  //tilt left up
  for (int i=0; i<=ang; i+=5){
    Lfoot.write(LFcenter-i);
    Rfoot.write(RFcenter-i);
    delay(sp);
  }
}
void TiltLeftDown(byte ang, byte sp){
  //tilt left down
  for (int i=ang; i>0; i-=5){
    Lfoot.write(LFcenter-i);
    Rfoot.write(RFcenter-i);
    delay(sp);
  }
}
void LeftFootUp(char ang, byte sp){
  //tilt left up
  for (int i=0; i<=ang; i+=5){
    Lfoot.write(LFcenter-i);
    delay(sp);
  }
}
void LeftFootDown(byte ang, byte sp){
  //tilt left down
  for (int i=ang; i>0; i-=5){
    Lfoot.write(LFcenter-i);
    delay(sp);
  }
}
void RightFootUp(byte ang, byte sp){ 
  //tilt right up
  for (int i=0; i<=ang; i+=5){
    Rfoot.write(RFcenter+i);
    delay(sp);
  }
}
void RightFootDown(byte ang, byte sp){
  //tilt right down
  for (int i=ang; i>0; i-=5){
    Rfoot.write(RFcenter+i);
    delay(sp);
  }
}
void SwingRight(byte ang, byte sp){
  //swing right
  for (int i=0; i<=ang; i+=5){
    Lleg.write(LLcenter-i);
    Rleg.write(RLcenter-i);
    delay(sp);
  }
}
void SwingRcenter(byte ang, byte sp){
  //swing r->center
  for (int i=ang; i>0; i-=5){
    Lleg.write(LLcenter-i);
    Rleg.write(RLcenter-i);
    delay(sp);
  }
}
void SwingLeft(byte ang, byte sp){
  //swing left
  for (byte i=0; i<=ang; i=i+5){
    Lleg.write(LLcenter+i);
    Rleg.write(RLcenter+i);
    delay(sp);
  }
}
void SwingLcenter(byte ang, byte sp){
  //swing l->center
  for (byte i=ang; i>0; i=i-5){
    Lleg.write(LLcenter+i);
    Rleg.write(RLcenter+i);
    delay(sp);
  }
}
void RightLegIn(byte ang, byte sp){
  //swing right
  for (int i=0; i<=ang; i+=5){
    Rleg.write(RLcenter-i);
    delay(sp);
  }
}
void RightLegIcenter(byte ang, byte sp){
  //swing r->center
  for (int i=ang; i>0; i-=5){
    Rleg.write(RLcenter-i);
    delay(sp);
  }
}
void RightLegOut(byte ang, byte sp){
  //swing right
  for (int i=0; i<=ang; i+=5){
    Rleg.write(RLcenter+i);
    delay(sp);
  }
}
void RightLegOcenter(byte ang, byte sp){
  //swing r->center
  for (int i=ang; i>0; i-=5){
    Rleg.write(RLcenter+i);
    delay(sp);
  }
}
void LeftLegIn(byte ang, byte sp){
  //swing left
  for (byte i=0; i<=ang; i=i+5){
    Lleg.write(LLcenter+i);
    delay(sp);
  }
}
void LeftLegIcenter(byte ang, byte sp){
  //swing l->center
  for (byte i=ang; i>0; i=i-5){
    Lleg.write(LLcenter+i);
    delay(sp);
  }
}
void LeftLegOut(byte ang, byte sp){
  //swing left
  for (byte i=0; i<=ang; i=i+5){
    Lleg.write(LLcenter-i);
    delay(sp);
  }
}
void LeftLegOcenter(byte ang, byte sp){
  //swing l->center
  for (byte i=ang; i>0; i=i-5){
    Lleg.write(LLcenter-i);
    delay(sp);
  }
}
void setup() {
  Serial.begin(19200);
  Serial.println("Bipedino setup is running.");
  Lleg.attach(LEFTLEG);
  Rleg.attach(RIGHTLEG); 
  Lfoot.attach(LEFTFOOT); 
  Rfoot.attach(RIGHTFOOT); 
  Head.attach(HEAD);
  CenterServos();
  delay(500);
  for (int i = 0; i < 5; ++i) {
    GetSonar();
    delay(1000);
  }
  Serial.println("Bipedino is ready.");
}
void loop() {
  unsigned int cmCenter = MAX_DISTANCE;
  unsigned int cmLeft   = MAX_DISTANCE;
  unsigned int cmRight  = MAX_DISTANCE;
  HeadCenter();
  cmCenter = GetSonar();
  if (cmCenter < Min_DISTANCE) {
    HeadRight();
    cmRight = GetSonar();
    HeadCenter();
    if (cmRight > Min_DISTANCE) {
      TurnRight(5, 50);
    } else {
      HeadLeft();
      cmLeft = GetSonar();
      HeadCenter();
      if (cmLeft > Min_DISTANCE) {
        TurnLeft(5, 50);
      }
    }
  } else {
    int nSteps = cmCenter / 5;
    if (nSteps > 5) {
      nSteps = 5;
    }
    else {
      nSteps = 1;
    } 
    Serial.print("Steps <");
    Serial.print(nSteps);
    Serial.println(">"); 
    for (int n = 0; n < nSteps; n++) {
      Forward(1,50);
    }
  }
}
int GetSonar() {
  unsigned int uS = sonar.ping(); // Send ping, get ping time in microseconds (uS).
  Serial.print("Ping: ");
  Serial.print(uS / US_ROUNDTRIP_CM); // Convert ping time to distance and print   result (0 = outside set distance range, no ping echo)
  Serial.println("cm"); 
  return uS / US_ROUNDTRIP_CM;
}

void CenterServos() {
  Lleg.write(LLcenter);      // tell servo to go to position in variable 'center'
  Rleg.write(RLcenter);      // tell servo to go to position in variable 'center'
  Lfoot.write(LFcenter);     // tell servo to go to position in variable 'center'
  Rfoot.write(RFcenter);     // tell servo to go to position in variable 'center'
  Head.write(Hcenter);        // tell servo to go to position in variable 'center'
  delay(1000);               // waits 100ms for the servos to reach the position
}
