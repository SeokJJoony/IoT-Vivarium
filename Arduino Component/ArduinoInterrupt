#include <MsTimer2.h>

#include <DHT.h>
#include <SoftwareSerial.h>

#define DHTTYPE DHT11
#define DHTPIN 4

SoftwareSerial BTSerial(8,9);
DHT dht(DHTPIN,DHTTYPE);

char AppValue=0;
char PreviousAppValue=0;
int dateCh = 0;
int DayCount=0;
int Humi=0;
int Temp=0;
char data[6]={0,};
unsigned long previousMillis = 0;

void Send()
{
  BTSerial.println(data);
  DayCount++;
}

void setup() {
  // put your setup code here, to run once:
   Serial.begin(9600);
   BTSerial.begin(9600);

   MsTimer2::set(3000,Send);
   MsTimer2::start(); 
    
}


void loop() {
  // put your main code here, to run repeatedly:
  
  Temp= dht.readTemperature();
  Humi= dht.readHumidity();
 sprintf(data,"%02d%02d%01d",Humi,DayCount,dateCh);
 if(BTSerial.available()>0)
 { 
 AppValue= BTSerial.read();

 }
 if(AppValue != PreviousAppValue)
 {
 if(AppValue>=0&&AppValue<=127)
 Serial.println(AppValue);
  PreviousAppValue=AppValue;
 }
 if(DayCount%10==0&&DayCount!=0)
 dateCh=1;
 else if(DayCount%10==1)
 dateCh=0;
 else if(DayCount==100)
 {
 DayCount =0;
 }
 }
