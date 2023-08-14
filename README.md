# Arduinorobot-car-2wd-Bluetooth
Arduino robot car 2 wheels - controlled by Bluetooth

[![Watch the video](https://img.youtube.com/vi/ILcZXvUB5gU/0.jpg)](https://youtu.be/ILcZXvUB5gU)

        //  if you need more information https://blog.edafait.com/Post?ID=134
          
          
          #include "BluetoothSerial.h"
          #define ENA   14          // Enable/speed motors Right        GPIO14(D5)
          #define ENB   12          // Enable/speed motors Left         GPIO12(D6)
          #define IN_1  4          // L298N in1 motors Right           GPIO15(D2)
          #define IN_2  13          // L298N in2 motors Right           GPIO13(D7)
          #define IN_3  2           // L298N in3 motors Left            GPIO2(D4)
          #define IN_4  0           // L298N in4 motors Left            GPIO0(D3)
          #define front_light  15   
          #define red_light  5           //back
          char commandm;
           //String to store app command state.
           int speedCar = 1000;         // 400 - 1023.
           int speed_Coeff = 3;

          /* Check if Bluetooth configurations are enabled in the SDK */
          /* If not, then you have to recompile the SDK */
          #if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
          #error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
          #endif

          BluetoothSerial SerialBT;

          void setup() {
         Serial.begin(115200);
          /* If no name is given, default 'ESP32' is applied */
         /* If you want to give your own name to ESP32 Bluetooth device, then */
         /* specify the name as an argument SerialBT.begin("myESP32Bluetooth*/
         SerialBT.begin("Car Domy");// BTName
         SerialBT.begin();
         pinMode(ENA, OUTPUT);
         pinMode(ENB, OUTPUT);  
         pinMode(IN_1, OUTPUT);
         pinMode(IN_2, OUTPUT);
         pinMode(IN_3, OUTPUT);
         pinMode(IN_4, OUTPUT); 
         pinMode(IN_4, OUTPUT); 
         pinMode(red_light, OUTPUT); 
         pinMode(front_light, OUTPUT);
          }
    //  if you need more information https://blog.edafait.com/Post?ID=134
         void loop() {
 
              if (SerialBT.available())
                   {
                     // Serial.write(SerialBT.read());
                     commandm = SerialBT.read();
                   }
               if (commandm == 'F')
                   {
                     Serial.write("walid");
                     goAhead();
                   }
               if (commandm == 'B')
                   {
                    Serial.write("walid");
                    goBack();
                    }
              if (commandm == 'L')
                  {
                   Serial.write("walid");
                  goLeft();
                  }
                 if (commandm == 'R')
                  {
                   Serial.write("walid");
                   goRight();
                   }
               if (commandm == 'I')
                  {
                  Serial.write("walid");
                  goAheadRight();
                  }
               if (commandm == 'I')
                   {
                Serial.write("walid");
                goAheadRight();
                   }
               if (commandm == 'G')
                  {
                 Serial.write("walid");
                 goAheadLeft();
                  }
              if (commandm == 'J')
               {
                 Serial.write("walid");
                 goBackRight();
               }
              if (commandm == 'H')
               {
               Serial.write("walid");
               goBackLeft();
                }
                if (commandm == '0')
                {
                Serial.write("walid");
                speedCar = 400;
                 }
               if (commandm == '1')
                 {
               Serial.write("walid");
               speedCar = 500;
                 }
             if (commandm == '2')
               {
              Serial.write("walid");
              speedCar = 600;
               }
             if (commandm == '3')
               {
              Serial.write("walid");
               speedCar = 650;
              }
            if (commandm == '4')
             {
                Serial.write("walid");
                 speedCar = 700;
                }
             if (commandm == '5')
                  {
                  Serial.write("walid");
                 speedCar = 750;
                    }
                if (commandm == '6')
                  {
                Serial.write("walid");
                 speedCar = 800;
                    }
                 if (commandm == '7')
                      {
                Serial.write("walid");
                 speedCar = 850;
                    }
                   if (commandm == '8')
                      {
                    Serial.write("walid");
                     speedCar = 900;
                        }
                   if (commandm == '9')
                      {
                    Serial.write("walid");
                     speedCar = 950;
                            }
                if (commandm == '10')
                      {
                    Serial.write("walid");
                     speedCar = 1023;
                        }
                  if (commandm == 'S')
                          {
                    Serial.write("walid");
                    stopRobot();
                        }
                  delay(20);
                  }


        void goAhead(){ 
            digitalWrite(IN_1, LOW);
            digitalWrite(IN_2, HIGH);
            analogWrite(ENA, speedCar);

              digitalWrite(IN_3, HIGH);
              digitalWrite(IN_4, LOW);
              analogWrite(ENB, speedCar);
      
  
      
              digitalWrite(red_light, LOW);
             digitalWrite(front_light, HIGH);    
                  }

            void goBack(){ 

            digitalWrite(red_light, HIGH);
            digitalWrite(front_light,LOW );    

              digitalWrite(IN_1, HIGH);
              digitalWrite(IN_2, LOW);
              analogWrite(ENA, speedCar);

              digitalWrite(IN_3, LOW);
              digitalWrite(IN_4, HIGH);
              analogWrite(ENB, speedCar);

      
                  }

            void goRight(){ 
            digitalWrite(front_light,LOW );      
            digitalWrite(red_light, HIGH);

           digitalWrite(IN_1, LOW);
          digitalWrite(IN_2, HIGH);
          analogWrite(ENA, speedCar);

          digitalWrite(IN_3, LOW);
          digitalWrite(IN_4, HIGH);
          analogWrite(ENB, speedCar);
      }

            void goLeft(){
              digitalWrite(front_light,LOW );    
                digitalWrite(red_light, HIGH);

               digitalWrite(IN_1, HIGH);
              digitalWrite(IN_2, LOW);
              analogWrite(ENA, speedCar);

              digitalWrite(IN_3, HIGH);
              digitalWrite(IN_4, LOWnm);
              analogWrite(ENB, speedCar);
              }

                void goAheadRight(){
                  digitalWrite(front_light,LOW );    
                  digitalWrite(IN_1, LOW);
                  digitalWrite(IN_2, HIGH);
                  analogWrite(ENA, speedCar/speed_Coeff);
                  digitalWrite(red_light, HIGH);
                  digitalWrite(IN_3, LOW);
                  digitalWrite(IN_4, HIGH);
                  analogWrite(ENB, speedCar);
               }

                void goAheadLeft(){
              digitalWrite(front_light,LOW );    
              digitalWrite(red_light, HIGH);
              digitalWrite(IN_1, LOW);
              digitalWrite(IN_2, HIGH);
             analogWrite(ENA, speedCar);

            digitalWrite(IN_3, LOW);
              digitalWrite(IN_4, HIGH);
              analogWrite(ENB, speedCar/speed_Coeff);
              }
    //  if you need more information https://blog.edafait.com/Post?ID=134
        void goBackRight(){ 
              digitalWrite(front_light,LOW );    
              digitalWrite(red_light, HIGH);
              digitalWrite(IN_1, HIGH);
              digitalWrite(IN_2, LOW);
              analogWrite(ENA, speedCar/speed_Coeff);

              digitalWrite(IN_3, HIGH);
              digitalWrite(IN_4, LOW);
              analogWrite(ENB, speedCar);
              }

        void goBackLeft(){ 
      digitalWrite(front_light,LOW );    
      digitalWrite(red_light, HIGH);
      digitalWrite(IN_1, HIGH);
      digitalWrite(IN_2, LOW);
      analogWrite(ENA, speedCar);

      digitalWrite(IN_3, HIGH);
      digitalWrite(IN_4, LOW);
      analogWrite(ENB, speedCar/speed_Coeff);
          }

        void stopRobot(){  
      digitalWrite(red_light, LOW);
      digitalWrite(IN_1, LOW);
      digitalWrite(IN_2, LOW);
      analogWrite(ENA, speedCar);
      digitalWrite(front_light,LOW );    
      digitalWrite(IN_3, LOW);
      digitalWrite(IN_4, LOW);
      analogWrite(ENB, speedCar);
         }
