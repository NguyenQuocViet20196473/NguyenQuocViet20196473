#define VAR   A0
#define SW    A1
#define M1    9
#define M2    8


// include the library code:
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

int load;
int temp;
char inByte;
void setup() {
  pinMode(VAR, INPUT);
  pinMode(SW, INPUT_PULLUP);
  pinMode(M1, OUTPUT);
  pinMode(M2, OUTPUT);

  digitalWrite(M1, LOW);
  digitalWrite(M2, LOW);

  Serial.begin(9600);
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
}







void loop() {
  lcd.setCursor(0, 0);
  if(digitalRead(SW)){
    lcd.print("DK bang tay");
    load = analogRead(VAR);
  } else{
      lcd.print("DK bang DT ");
      if (Serial.available()) {
        load = 0;
        while(Serial.available()){
          inByte = Serial.read();
          Serial.write(inByte);
          switch(inByte){
            case '0':   load = 10*load; 
                        break;
            case '1':   load = 10*load +1; 
                        break;
            case '2':   load = 10*load+2; 
                        break;
            case '3':   load = 10*load+3; 
                        break;
            case '4':   load = 10*load+4; 
                        break;
            case '5':   load = 10*load+5; 
                        break;
            case '6':   load = 10*load+6; 
                        break;
            case '7':   load = 10*load+7; 
                        break;
            case '8':   load = 10*load+8; 
                        break;
            case '9':   load = 10*load+9; 
                        break;     
          }
          
        }
        load = map(load, 0, 100, 0, 1023);
      }
  }
  lcd.setCursor(0, 1);
  lcd.print("    ");
  lcd.setCursor(0, 1);
  lcd.print(load);
  analogWrite(M1, load);
  delay(100);
}
