# fire-detection
#include<Servo.h>
int red_led=12;//indicates gas
int green_led=11;//indicates normal
int buzz=8;//indicates gas
int smoke = A5;
int temp=A0;//indicates sensor is connected to A5
int sensorThres=40;//The threshold value
Servo s;
void setup()
{
pinMode(red_led,OUTPUT);//red led as output
pinMode(buzz,OUTPUT);// buzz as output
pinMode(green_led,OUTPUT);//green led as output
pinMode(smoke,INPUT);
pinMode(temp,INPUT);//sensor as input
s.attach(3);
Serial.begin(9600);//starts the code
}
void loop()//loops
{
int a=analogRead(smoke);
  int b=map(a,0,1023,0,255);
  Serial.println(b);
 double c=analogRead(temp);
  double d=(((c/1024)*5)-0.5)*100;
  Serial.println(d);//reads sensor value
if (b > sensorThres or d>100)//sees if it reached threshold value
{
digitalWrite(red_led, HIGH);//turns on red led
digitalWrite(green_led, LOW);//turns off green led
digitalWrite( buzz, HIGH);
  for(int i=0;i<=90;i++)
  {
    s.write(i);
    delay(1);
  }//turns on buzzer
}
else//if it hasn't reached threshold value
{
digitalWrite(red_led, LOW);//turns red led off
digitalWrite(green_led, HIGH);//turn green led on
digitalWrite( buzz, LOW);
   for(int i=90;i>=0;i--)
  {
    s.write(i);
    delay(1);
  }///turns buzzer off
}
delay(100);//delay 0.1 sec
}
