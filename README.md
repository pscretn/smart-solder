# smart-solder<br><br>
## program
```cpp

const unsigned long interval=1800000; //wait time start counting ,when there is absence of touch input , delay is 30 minutes
const unsigned long ldint=1000; // delay for led indicator
unsigned long previoustime=0;
unsigned long prev=0;
int solder=0;
int led=1;
void setup() {
  // put your setup code here, to run once:
  pinMode(13, OUTPUT);
  pinMode(12, OUTPUT);
  digitalWrite(13,HIGH);
  digitalWrite(12,HIGH);
  solder=1;
  }

void loop() {
  //conditional statement for solder 
 unsigned long currenttime=millis(); //here we use millis() function to avoid hardware delay 
if (touchRead(T6)<40 ){  //touchRead() function is used measure sensor value when user touches on touch pin of ESP 32 , T6 is GPIO pin 14 on ESP32
    digitalWrite(13,HIGH);
    previoustime=currenttime;
    solder=1;
    digitalWrite(12,HIGH);  
 }

  else if ((touchRead(T6)>40)and(currenttime - previoustime >= interval) and solder==1 ){
   digitalWrite(13,LOW);
    solder=0;
}
//conditional statement for indicator led
unsigned long ct=millis();
 if ((ct - prev >= ldint)and(currenttime - previoustime >= interval)){
  if(led == 0){
     digitalWrite(12,HIGH);
      prev=ct;
      led=1;
  }
  else{
     digitalWrite(12,LOW);
      prev=ct;
      led=0;
  }
 }
}
  ```
