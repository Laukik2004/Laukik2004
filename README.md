- 👋 Hi, I’m @Laukik2004
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Laukik2004/Laukik2004 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
#define BLYNK_PRINT Serial
#define BLYNK_TEMPLATE_ID ""
#define BLYNK_DEVICE_NAME ""
#define BLYNK_AUTH_TOKEN ""


#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include "DHT.h"
#define DHTPIN D1
#define DHTTYPE DHT11
DHT dht(DHTPIN,DHTTYPE);
char auth[] = "3t-0mu448gEtW-67nPByO0YPhq61owLF";
char ssid[] = "FTTH-A624";
char pass[] = "Admin@1160";


BlynkTimer timer; 
//void randomData(){
//    Serial.println(random(0,100));
//    Blynk.virtualWrite(V0, random(0,100));
// }
//BLYNK_WRITE(V1)
//{   
//  int value = param.asInt(); // Get value as integer
//  digitalWrite(D0,value);
//}
void dhtData(){
  float t=dht.readTemperature();
  float h=dht.readHumidity();
  if(isnan(t) || isnan(h)){
    Serial.println("Data is not available");
    return;
    }
  Serial.print("temperature:");
  Serial.print(t);
  Serial.print("  ");
  Serial.print("humidity:");
  Serial.println(h);
  Blynk.virtualWrite(V0, t);
  Blynk.virtualWrite(V1, h);
}


void setup()
{
  Serial.begin(9600);
  Blynk.begin(auth, ssid, pass);
  dht.begin();
  timer.setInterval(1000L, dhtData); 
  pinMode(D1,OUTPUT);
}


void loop()
{
  Blynk.run();
  timer.run();
}

this code i will used for showing tempreture and humidity on blynk.com but their is an error occured
in serial monitor it shows 

Soft WDT reset
exception(4)
