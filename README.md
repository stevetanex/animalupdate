#include<SoftwareSerial.h>
SoftwareSerial SIM900A(2,3);
const int pir=5;
const int led=13;
void setup() {
  
 
 pinMode(pir, INPUT);
 SIM900A.begin(9600);
 pinMode(led, OUTPUT);
  Serial.begin(9600);


  delay(1000);

  Serial.println("sys ready");
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);     
       
}


void loop()
{

char inChar=(char)Serial.read();
int data=digitalRead(pir);
Serial.println(data);
if(data==HIGH)
{
digitalWrite(led,HIGH);
//SendMessage();
Makecall();
Serial.println("animal detected in your area");

}
else
{
  digitalWrite(led,LOW);
  Serial.println("no object ");

}
  // put your setup code here, to run onc

}
void SendMessage()
{
  Serial.println ("Sending Message please wait....");
  SIM900A.println("AT+CMGF=1");    //Text Mode initialisation 
  delay(1000);
  Serial.println ("Set SMS Number");
  SIM900A.println("AT+CMGS=\"+916238236007\"\r"); // Receiver's Mobile Number
  delay(1000);
  Serial.println ("Set SMS Content");
  SIM900A.println("Animal is detected in your area... ");// Messsage content
  delay(100);
  Serial.println ("Done");
  SIM900A.println((char)26);//   delay(1000);
  Serial.println ("Message sent succesfully");
}

void Makecall()
{
  Serial.println("mAKING A CALL TO OWNER");
  SIM900A.println("ATD6238922940;");
delay(5000);
}
