// DHT sensor library - Version: Latest 
#include <DHT.h>
#include <WiFiNINA.h>
#include <ThingSpeak.h> 
#include <DHT_U.h>

#define DHTPIN 2 // Pin on the Nano 33 IOT 
#define DHTTYPE DHT22 // type of board
 
DHT dht(DHTPIN, DHTTYPE);

WiFiClient client;

char ssid[] = "SSID";
char pass[] = "PASSWORD";
int status = WL_IDLE_STATUS;

unsigned long myChannelNumber = #######;
const char * myWriteAPIKey = "################";

float boardTEMP;
float boardHUMID;

void setup() {
  // Initialize serial and wait for port to open:
  Serial.begin(9600);

  if (WiFi.status() == WL_NO_MODULE){
    Serial.println("Wifi failed");
    while(true);
  }

  Wifi_TurnOn();

  ThingSpeak.begin(client);
  
  dht.begin();
}

void Wifi_TurnOn(){
  while (status != WL_CONNECTED){
    status = WiFi.begin(ssid, pass);
    delay(1000);
  }
}

void loop() {  
  delay(2000);
  boardTEMP = dht.readTemperature(); // Reads Temperature
  boardHUMID = dht.readHumidity(); // Reads Humidity

  ThingSpeak.setField(1, boardTEMP); // Output 1
  ThingSpeak.setField(2, boardHUMID); // Output 2
  ThingSpeak.writeFields(myChannelNumber, myWriteAPIKey);

  delay(20000);  
}
