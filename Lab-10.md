Partners: Ian Gross, Barry Hu, Kevin Zhang


1) LED blinks. Modified the delay to make it blink faster

2) Printed Hello World. Tried turning off backlight

3) Used "File/LiquidCrystal/SerialDisplay".

![File](https://scontent.xx.fbcdn.net/hphotos-xap1/v/t34.0-12/12233434_1037378216282450_799164861_n.jpg?oh=44e1c0e7d3bccb4de97c7a9016172007&oe=5648FD2A)

4) Part 4 code:

```
unsigned long time;
void setup() { 
  // initialize the serial communications:
  Serial.begin(9600);
  init_LCD();
}
void loop() {
  lcd.home();
  if(Serial.available()){
    lcd.clear();
    char x = Serial.read();
    char y = Serial.read();
    if(x == '\\'){
      if(y=='t'){
        //Serial.print("Hi");
      time = Serial.parseInt();
      //time = millis();
      Serial.print("Set Timer: ");
      Serial.print(time,DEC);
      Serial.print("\n");
      }
      else if(y=='r'){
        
        while(time > 0){
          if(Serial.available()){
            x = Serial.read();
            y = Serial.read();
            if(x=='\\' && y=='y')
              break;
          }
          delay(1000);
          Serial.print(time,DEC);
          Serial.print("\n");
          --time;
        }
        delay(1000);
          Serial.print(time,DEC);
          Serial.print("\n");
      }
      else if(y=='y'){
        
      }
      
    }
    
    
  }
```
  
  
  
Part 5)
