# Simblee Robot 

## This robot was controlled by a Simblee BLE device. It had a sabertooth motor controller on it. 

~~~
#include <SimbleeForMobile.h>
#include <SabertoothSimplified.h>

SabertoothSimplified ST;

uint8_t ui_button[4];

void setup() {
   SabertoothTXPinSerial.begin(9600);
  ST.drive(0);
  ST.turn(0);
  // put your setup code here, to run once:
  SimbleeForMobile.deviceName = "Robot";
  SimbleeForMobile.advertisementData = "tank";
  SimbleeForMobile.domain = "tank.simblee.com";
  // Begin Simblee UI
  SimbleeForMobile.begin();
}
/*
 * The traditional Arduino loop method
 * 
 * Enable SimbleeForMobile functionality by calling the process method
 * each time through the loop. This method must be called regularly for
 * functionality to work.
 */
void loop() {
  // put your main code here, to run repeatedly:
  // process must be called in the loop for Simblee UI
  SimbleeForMobile.process();  
}
/*
 * SimbleeForMobile UI callback requesting the user interface
 */
void ui()
{  
  SimbleeForMobile.beginScreen();
  SimbleeForMobile.beginScreen(WHITE);
  //SimbleeForMobile.drawText(90,230, "", BLUE, 50);
  ui_button[0] = SimbleeForMobile.drawButton(100,300,85,"FOWARD");
  ui_button[1] = SimbleeForMobile.drawButton(30,350,85,"LEFT");
  ui_button[2] = SimbleeForMobile.drawButton(175,350,85,"RIGHT");
  ui_button[3] = SimbleeForMobile.drawButton(100,400,85,"REVERSE");
     
     SimbleeForMobile.setEvents(ui_button[0], EVENT_PRESS | EVENT_RELEASE);
     SimbleeForMobile.setEvents(ui_button[1], EVENT_PRESS | EVENT_RELEASE);
     SimbleeForMobile.setEvents(ui_button[2], EVENT_PRESS | EVENT_RELEASE);
     SimbleeForMobile.setEvents(ui_button[3], EVENT_PRESS | EVENT_RELEASE);
     
  SimbleeForMobile.endScreen();
}
/*
 * SimbleeForMobile event callback method
 */
void ui_event(event_t &event)
{
  if (event.id == ui_button[0]){
   if (event.type == EVENT_PRESS){
    forward();
  }else{
    quit();
   }
  }
  
   if (event.id == ui_button[1]){
   if (event.type == EVENT_PRESS){
    lift();
  }else{
    quit();
   }
  }
  
   if (event.id == ui_button[2]){
   if (event.type == EVENT_PRESS){
    right();
  }else{
    quit();
   }
  }
  
  if (event.id == ui_button[3]){
   if (event.type == EVENT_PRESS){
    revirce();
  }else{
    quit();
   }
  }
}

void forward(){
  ST.drive(127);
}

void revirce(){
  ST.drive(-127);
}

void lift(){
  ST.turn(127);
}

void right(){
  ST.turn(-127);
}

void quit(){
  ST.drive(0);
  ST.turn(0);
}
~~~
[!IMPORTANT]

 This code is out of date. The Simblee BLE chip is no longer available. 

## [Back](https://tcaviness.github.io/#code)
