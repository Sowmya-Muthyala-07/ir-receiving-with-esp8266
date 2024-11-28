#include <IRremoteESP8266.h>
#include <IRrecv.h>
#include <IRutils.h>


const uint16_t recv_pin = 18;  // Adjust the GPIO pin number for your ESP32 setup
IRrecv irrecv(recv_pin);
decode_results results;


void setup() {
  Serial.begin(115200);
  irrecv.enableIRIn();  // Start the IR receiver
  Serial.println("Ready to receive IR signals...");
}


void loop() {
  if (irrecv.decode(&results)) {
    // Print the HEX code and protocol of the received IR signal
    Serial.print("IR Code Received: ");
    Serial.println(resultToHexidecimal(&results));  // Print received IR code in HEX format
    Serial.print("Protocol: ");
    Serial.println(typeToString(results.decode_type));  // Print protocol type as a string


    // Resume the receiver for the next IR signal
    irrecv.resume();
  }
}
