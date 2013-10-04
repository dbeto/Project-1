proof
=====

#include <Servo.h> 

Servo servo1;

int Redled = 13;

int Greenled = 12;

int Whiteled = 11;

int control= 16;

int controlRead;

int controlmap;

int Lsensor=14;

int lightmap;

int Lsensorvalue;


int Fsensor=15;

int Fsensormap;
int FsensorValue;

int MotDC = 9;

int MotorServo = 3;



void setup(){
Serial.begin(9600);
servo1.attach(MotorServo,500,2500);
pinMode (Redled, OUTPUT);
pinMode (Greenled, OUTPUT);
pinMode (Whiteled, OUTPUT);
pinMode(Lsensor, INPUT);
pinMode(Fsensor, INPUT);
pinMode(MotDC, OUTPUT); 

}



void loop()
{

FsensorValue = analogRead(Fsensor);
Fsensormap = map(FsensorValue,0,1023,0,255);
analogWrite(MotDC, Fsensormap);

controlRead = analogRead(control);
controlmap = map(controlRead,0,1023,0,255);
analogWrite(Whiteled, controlmap);

Lsensorvalue = analogRead (Lsensor);
lightmap = map(Lsensorvalue,0,1023,0,180);
servo1.write(lightmap);



if (controlmap>200){
  digitalWrite(Greenled, HIGH);
digitalWrite(Redled, LOW);
}
else
{
  digitalWrite(Redled, HIGH);
digitalWrite(Greenled, LOW); 

}
 
 
 if (lightmap > 90){
  digitalWrite(Greenled, HIGH);
digitalWrite(Redled, LOW);
}
else
{
  digitalWrite(Redled, HIGH);
digitalWrite(Greenled, LOW); 

}


}
