// Gas buzzer
#define gas_sensor_pin  34
#define buzzer_pin 26


#define safe_led 5
#define alert_pin 4

int gasThreshold = 1000;
void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  pinMode(buzzer_pin, OUTPUT);
  pinMode(safe_led, OUTPUT);
  pinMode(alert_pin, OUTPUT);
}

void loop() {
  int gaslevel=analogRead(gas_sensor_pin);

  Serial.print("Gas Level: ");
  Serial.println(gaslevel);

  if(gaslevel > gasThreshold){

    digitalWrite(alert_pin,HIGH);
    digitalWrite(safe_led,LOW);
    digitalWrite(buzzer_pin,HIGH);    
    Serial.println("\n Harmful Gas Return");
  }else{
    digitalWrite(alert_pin,LOW);
    digitalWrite(safe_led,HIGH);
    digitalWrite(buzzer_pin,LOW);    
    Serial.println("\n Air Quality is Safe");

  }
  delay(100);
}

/*
connection:
buzzer :
red - > 26
black -> GND

LED 1(red)
Anod -> GND
Cathod -> 4

LED 2(Greeen)
Anod -> GND
Cathod -> 5

Gas sensor :
Dout -> 34
GND -> GND
Vcc -> 5v
*/
// question : 
// smart lighting sysytem using lDR

int LDRPin = 35;
int LEDPin = 5;
int threshold = 1000;


void setup() {
  pinMode(LDRPin,INPUT);
  pinMode(LEDPin,OUTPUT);
  Serial.begin(9600);
}

void loop() {
  
  int LDRValue=analogRead(LDRPin);
  Serial.println(LDRValue);
  
  if(LDRValue < threshold){
    digitalWrite(LEDPin,HIGH);
  }else{
    digitalWrite(LEDPin,LOW);
  }
  delay(100);

}



/*
con:

LDR
vcc - > 5 v
AO -> 35
GND -> GND

LED :
gnd - gnd
catod -> 5 pin
*/
// question
// potenstionmeter with nodeMCU


int LEDPin = 2;
int PIRPin = 5;
int buzzer = 4;

void setup() {
  pinMode(PIRPin, INPUT);
  pinMode(LEDPin, OUTPUT);
  pinMode(buzzer, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int pirvalue=digitalRead(PIRPin);
  Serial.println(pirvalue);
  delay(100);

  if(pirvalue==1){
     
    digitalWrite(LEDPin,HIGH);
    tone(buzzer,1000,1000);
    delay(1000);
     
  }else{
    digitalWrite(LEDPin, LOW);
  }
}



/*
connection

LED:
a-> GND
c-> 2 pin

Potentiometer
+ -> votage ( 3v3)
D -> 5 pin 
-  -> GNd


buzzer:
black to GND
red -> 4 pin
*/// quesiton'
//  temp sensor using thermoster


#include "DHT.h"
DHT dht(19,DHT22);

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  dht.begin();
}

void loop() {
float h = dht.readHumidity();
float t = dht.readTemperature();
Serial.print("Humidity = ");
Serial.print(h);
Serial.print("% /n");
Serial.print("Temperature = ");
Serial.print(t);
Serial.print("%*c ");
delay(500);
}


/* connectuon
:
Vcc -> 3v3
SDA -> 19
GND -> GND
*/

//  question
// Potentiometer with node mCU

const int PM=34;
const int LED=23;

void setup() {
  Serial.begin(115200);
  pinMode(LED, OUTPUT);
}

void loop() {
  int PMValue= analogRead(PM);

  Serial.print("Potentiometer Value: ");
  Serial.println(PMValue);

  int lbright=map(PMValue,0,4095,0,255);
  analogWrite(LED,lbright);

  delay(500);

}

/* connection:
potentionmeter
:

GND -> GND
SIG -> 34
VCC -> 3v3

LED:
a -> GND 
c -> resitror to 23 pin
*/

// push button 

void setup() {
 pinMode(4, OUTPUT);
 pinMode(26, INPUT);
}

void loop() {
  int button = 0;

  button = digitalRead(26);

  if(button == HIGH){
    digitalWrite(4, HIGH);
    
  }else{
    digitalWrite(4, LOW);
  }
  //digitalWrite(4, LOW);
}

// contion :
// a -> gnd 
// c -> 4 pin

// push button :
// cross connection
// 26 pin and another cross GND;
// led blinking

void setup() {
  pinMode(4,OUTPUT);
}

void loop() {
  digitalWrite(4, HIGH);
  delay(1000);

  digitalWrite(4,LOW);
  delay(250);

}

//connection:
// a -> GND
// c -> Resistor -> 4 
