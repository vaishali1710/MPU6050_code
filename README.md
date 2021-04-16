# MPU6050_code
#include "Wire.h"
#include "I2Cdev.h"
#include "MPU6050.h"
#include "Servo.h"

MPU6050 mpu;
int16_t ax, ay, az;
int16_t gx, gy, gz;
Servo servo1;
Servo servo2;

int val1;
int val2;

int preVal1;
int preVal2;

void setup() 
{
 Wire.begin();
 Serial.begin(9600);
 Serial.println("Initialize MPU");
 mpu.initialize();
 Serial.println(mpu.testConnection()? "connected" : "connection failed");
 servo1.attach(5);
 servo2.attach(6);
}

void loop() 
{
 mpu.getMotion6(&ax, &ay, &az, &gx, &gy, &gz);
 val1=map(ax, -17000, 17000, 0, 179);
 if(val1 != preVal1)
 {
  servo1.write(val1);
  preVal1 = val1;
 }
 val1=map(ay, -17000, 17000, 0, 179);
 if(val2 != preVal2)
 {
  servo2.write(val2);
  preVal2 = val2;
 }
 delay(5);
}
