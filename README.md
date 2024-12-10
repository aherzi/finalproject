link to video: https://youtu.be/CTGKuwAzFVY

//final project
//Walking mode

#include <Servo.h>
#include <NewPing.h>
 
#define ECHO_PIN     A3   
#define TRIGGER_PIN  A5  
#define LEFTLEG       10
#define RIGHTLEG     9
#define LEFTFOOT      6
#define RIGHTFOOT     13
#define  HEAD          7
#define MAX_DISTANCE 200  
int Min_DISTANCE = 10;
NewPing sonar(TRIGGER_PIN, ECHO_PIN, MAX_DISTANCE);  
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
int tAngle = 20;     
int uAngle = 25;     
int sAngle = 25;     
int Speed = 50;     
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
    
  for (int i=0; i<=ang; i+=5){
    Lfoot.write(LFcenter+i);
    Rfoot.write(RFcenter+i);
    delay(sp);
  }
}
void TiltRightDown(byte ang, byte sp){
    
  for (int i=ang; i>0; i-=5){
    Lfoot.write(LFcenter+i);
    Rfoot.write(RFcenter+i);
    delay(sp);
  }
}
void TiltLeftUp(byte ang, byte sp){
    
  for (int i=0; i<=ang; i+=5){
    Lfoot.write(LFcenter-i);
    Rfoot.write(RFcenter-i);
    delay(sp);
  }
}
void TiltLeftDown(byte ang, byte sp){
    
  for (int i=ang; i>0; i-=5){
    Lfoot.write(LFcenter-i);
    Rfoot.write(RFcenter-i);
    delay(sp);
  }
}
void LeftFootUp(char ang, byte sp){
    
  for (int i=0; i<=ang; i+=5){
    Lfoot.write(LFcenter-i);
    delay(sp);
  }
}
void LeftFootDown(byte ang, byte sp){
    
  for (int i=ang; i>0; i-=5){
    Lfoot.write(LFcenter-i);
    delay(sp);
  }
}
void RightFootUp(byte ang, byte sp){ 
    
  for (int i=0; i<=ang; i+=5){
    Rfoot.write(RFcenter+i);
    delay(sp);
  }
}
void RightFootDown(byte ang, byte sp){
    
  for (int i=ang; i>0; i-=5){
    Rfoot.write(RFcenter+i);
    delay(sp);
  }
}
void SwingRight(byte ang, byte sp){
    
  for (int i=0; i<=ang; i+=5){
    Lleg.write(LLcenter-i);
    Rleg.write(RLcenter-i);
    delay(sp);
  }
}
void SwingRcenter(byte ang, byte sp){
    
  for (int i=ang; i>0; i-=5){
    Lleg.write(LLcenter-i);
    Rleg.write(RLcenter-i);
    delay(sp);
  }
}
void SwingLeft(byte ang, byte sp){
    
  for (byte i=0; i<=ang; i=i+5){
    Lleg.write(LLcenter+i);
    Rleg.write(RLcenter+i);
    delay(sp);
  }
}
void SwingLcenter(byte ang, byte sp){
    
  for (byte i=ang; i>0; i=i-5){
    Lleg.write(LLcenter+i);
    Rleg.write(RLcenter+i);
    delay(sp);
  }
}
void RightLegIn(byte ang, byte sp){
    
  for (int i=0; i<=ang; i+=5){
    Rleg.write(RLcenter-i);
    delay(sp);
  }
}
void RightLegIcenter(byte ang, byte sp){
    
  for (int i=ang; i>0; i-=5){
    Rleg.write(RLcenter-i);
    delay(sp);
  }
}
void RightLegOut(byte ang, byte sp){
    
  for (int i=0; i<=ang; i+=5){
    Rleg.write(RLcenter+i);
    delay(sp);
  }
}
void RightLegOcenter(byte ang, byte sp){
    
  for (int i=ang; i>0; i-=5){
    Rleg.write(RLcenter+i);
    delay(sp);
  }
}
void LeftLegIn(byte ang, byte sp){
    
  for (byte i=0; i<=ang; i=i+5){
    Lleg.write(LLcenter+i);
    delay(sp);
  }
}
void LeftLegIcenter(byte ang, byte sp){
    
  for (byte i=ang; i>0; i=i-5){
    Lleg.write(LLcenter+i);
    delay(sp);
  }
}
void LeftLegOut(byte ang, byte sp){
    
  for (byte i=0; i<=ang; i=i+5){
    Lleg.write(LLcenter-i);
    delay(sp);
  }
}
void LeftLegOcenter(byte ang, byte sp){
    
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
  unsigned int uS = sonar.ping();  
  Serial.print("Ping: ");
  Serial.print(uS / US_ROUNDTRIP_CM);  
  Serial.println("cm"); 
  return uS / US_ROUNDTRIP_CM;
}

void CenterServos() {
  Lleg.write(LLcenter);       
  Rleg.write(RLcenter);       
  Lfoot.write(LFcenter);      
  Rfoot.write(RFcenter);      
  Head.write(Hcenter);         
  delay(1000);                
}

//Dancing of Purrbot
#include <Servo.h>
#include <NewPing.h>

  
#define ECHO_PIN     A3  
#define TRIGGER_PIN  A5
#define LEFTLEG       10    
#define RIGHTLEG     9      
#define LEFTFOOT      6     
#define RIGHTFOOT     13    
#define HEAD          7     

#define MAX_DISTANCE 400 
int Min_DISTANCE = 10;

NewPing sonar(TRIGGER_PIN, ECHO_PIN, MAX_DISTANCE);   
Servo Lleg, Rleg, Lfoot, Rfoot, Head;

int Hcenter = 90;  
int RLcenter = 90, RFcenter = 90, LLcenter = 90, LFcenter = 90;
int tAngle = 20, sAngle = 25, Speed = 50;

void setup() {
  Serial.begin(19200);
  Serial.println("Robot setup is running.");

    
  Lleg.attach(LEFTLEG);
  Rleg.attach(RIGHTLEG);
  Lfoot.attach(LEFTFOOT);
  Rfoot.attach(RIGHTFOOT);
  Head.attach(HEAD);

  CenterServos();    
  delay(500);

  Serial.println("Robot is ready.");
}

void loop() {
  int cmCenter = GetSonar();    
  if (cmCenter < Min_DISTANCE) {
      
    Serial.println("Obstacle detected. Dance faster.");
    FastDance();    
    AvoidObstacle();    
  } else {
      
    Serial.println("No obstacle. Resuming dance.");
    Dance();    
  }
}

int GetSonar() {
  unsigned int uS = sonar.ping(); 
  Serial.print("Ping: ");
  Serial.print(uS / US_ROUNDTRIP_CM); 
  Serial.println(" cm");
  return uS / US_ROUNDTRIP_CM;
}

  
void FastDance() {
    
  Lleg.write(LLcenter);
  Rleg.write(RLcenter);
  Lfoot.write(LFcenter);
  Rfoot.write(RFcenter);
  Head.write(Hcenter);
  delay(500);    
}

void Dance() {
    
  Serial.println("Performing a dance step.");
  for (int i = 0; i < 5; i++) {
    StepForward();    
    delay(500);       
  }
}

void AvoidObstacle() {
  Serial.println("Obstacle detected. Avoiding...");

    
  HeadRight();
  delay(500);  
  int cmRight = GetSonar();
  HeadCenter();  

  if (cmRight > Min_DISTANCE) {
    TurnRight(5, 50);  
  } else {
    HeadLeft();  
    int cmLeft = GetSonar();  
    HeadCenter();  

    if (cmLeft > Min_DISTANCE) {
      TurnLeft(5, 50);
    } else {
      Reverse(5, 50);  
    }
  }
}

void StepForward() {
    
  SwingRight(25, Speed);  
  SwingLeft(25, Speed);
  MoveFeetForward();
  delay(300);    

    
  ResetLegsAndFeet();
  delay(300);    

    
  SwingRightBack(25, Speed);
  SwingLeftBack(25, Speed);
  MoveFeetBack();
  delay(300);    
}

void SwingLeft(byte ang, byte sp) {
    
  for (int i = 0; i <= ang; i += 3) {    
    Lleg.write(LLcenter + i);    
    Rleg.write(RLcenter - i);    
    delay(sp);    
  }
}

void SwingRight(byte ang, byte sp) {
    
  for (int i = 0; i <= ang; i += 3) {    
    Rleg.write(RLcenter + i);    
    Lleg.write(LLcenter - i);    
    delay(sp);    
  }
}

void SwingRightBack(byte ang, byte sp) {
    
  for (int i = ang; i > 0; i -= 3) {  
    Rleg.write(RLcenter + i);  
    Lleg.write(LLcenter - i);  
    delay(sp);  
  }
}

void SwingLeftBack(byte ang, byte sp) {
    
  for (int i = ang; i > 0; i -= 3) {
    Lleg.write(LLcenter + i);  
    Rleg.write(RLcenter - i);  
    delay(sp);  
  }
}

void MoveFeetForward() {
    
  Lfoot.write(LFcenter + 10);    
  Rfoot.write(RFcenter + 10);    
  delay(200);    
}

void MoveFeetBack() {
    
  Lfoot.write(LFcenter);  
  Rfoot.write(RFcenter);  
  delay(200);    
}

void ResetLegsAndFeet() {
    
  Lleg.write(LLcenter);
  Rleg.write(RLcenter);
  Lfoot.write(LFcenter);
  Rfoot.write(RFcenter);
  delay(200);    
}

void TurnLeft(int steps, int speed) {
  for (int i = 0; i < steps; i++) {
    Head.write(90 - 15);    
    delay(speed);
  }
}

void TurnRight(int steps, int speed) {
  for (int i = 0; i < steps; i++) {
    Head.write(90 + 15);    
    delay(speed);
  }
}

void Reverse(int steps, int speed) {
  for (int i = 0; i < steps; i++) {
    SwingLeft(25, speed);
    SwingRight(25, speed);
    delay(200);
  }
}

void HeadRight() {
  Head.write(Hcenter + 30);
  delay(500);
}

void HeadLeft() {
  Head.write(Hcenter - 30);
  delay(500);
}

void HeadCenter() {
  Head.write(Hcenter);
  delay(500);
}

  
void CenterServos() {
    
  Lleg.write(LLcenter);  
  Rleg.write(RLcenter);  
  Lfoot.write(LFcenter);  
  Rfoot.write(RFcenter);  
  Head.write(Hcenter);  
  delay(500);    
}


