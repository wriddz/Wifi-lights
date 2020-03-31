# Wifi-lights
#include <ESP8266WiFi.h>
#include <ThingSpeak.h>


char* ssid     = "Galaxy A30s27BD";//Wifi name
char* password = "12345678";//Password
int channel =1026160;//ThingSpeak Account Channel ID
int Bulb = 1;//Channel field value

WiFiClient  client;


void setup() {
  Serial.begin(115200); //Baud rate for wifi connectivity
  delay(100);
  
  pinMode(D1, OUTPUT);
  
  digitalWrite(D1, 0);
  
  //Establishing a connection
 
  Serial.println();
  Serial.println();
  Serial.print("Connecting to ");
  Serial.print(ssid);
  
  WiFi.begin(ssid, password);
  
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
 
  Serial.println("");
  Serial.println("WiFi connected");  
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
  ThingSpeak.begin(client);

}

void loop() {
 
  int val = ThingSpeak.readFloatField(channel, Bulb); //Stores the field value
 
  if(val == 1){
    digitalWrite(D1, HIGH); //Light on (Relay on)
      }
  else if(val == 0){
    digitalWrite(D1, LOW); //Light off (Relay off)
      }
  delay(1000);
 
}
