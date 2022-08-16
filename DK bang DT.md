#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <TimeLib.h>
#include <WidgetRTC.h>

BlynkTimer timer;

WidgetRTC rtc;
char auth[] = "cAQARk6F71mvoGwa5HkvgBFii72XGnWc";
char ssid[] = "Nokia54";
char pass[] = "88888888";
// BlynkTimer timer;
WidgetLCD lcd(V1);

//void clockDisplay()
//{
//  String currentTime = String(hour()) + ":" + minute() + ":" + second();
//  String currentDate = String(day()) + " " + month() + " " + year();
//  Serial.print("Current time: ");
//  Serial.print(currentTime);
//  Serial.print(" ");
//  Serial.print(currentDate);
//  Serial.println();
//  Blynk.virtualWrite(V1, currentTime);
//  Blynk.virtualWrite(V2, currentDate);
//}

BLYNK_CONNECTED() {
  rtc.begin();
}
void setup() {
  Serial.begin (9600);
  Blynk.begin(auth, ssid, pass);
  setSyncInterval(10 * 60); 
//  timer.setInterval(10000L, clockDisplay); 
}

void loop() 
{
  Blynk.run();
  timer.run();
}

BLYNK_WRITE(V0)
{
  int value= param.asInt();
  int pot =analogRead(value);
  Serial.println(value);
  }
