# MPU6050_code
Interfacing of MPU6050 and arduino
#include <Adafruit_MPU6050.h>
#include <Adafruit_Sensor.h>
#include <Wire.h>
Adafruit_MPU6050 mpu;

void setup() {
  Serial.begin(115200);
  if(!mpu.begin()) {
    Serial.println("Failed to find MPU6050 chip");
    while(1) {
      delay(10);
    }
    Serial.println("MPU6050 found");

    mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
    mpu.setGyroRange(MPU6050_RANGE_500_DEG);
    mpu.setFilterBandwidth(MPU6050_BAND_21_HZ);
    delay(100);
  }

}

void loop() {
  
  sensors_event_t a, g, temp;
  mpu.getEvent(&a, &g, &temp);

  Serial.print("Acceleration X: ");
  Serial.print(a.acceleration.X);
  Serial.print(",Y: ");
  Serial.print(a.acceleration.Y);
  Serial.print(",Z:");
  Serial.print(a.acceleration.Z);
  Serial.print("m/s^2");

  Serial.print("Rotation X:");
  Serial.print(g.gyro.X);
   Serial.print(",Y:");
  Serial.print(g.gyro.Y);
  Serial.print(",Z:");
  Serial.print(g.gyro.Z);
  Serial.println("rad/s");

  Serial.print("Temperature:");
  Serial.print(temp.temperature);
  Serial.println("degC");
  Serial.println(" ");
  delay(500);
}
