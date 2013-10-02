Ardavan-First-Project
=====================
/* Here is Ardavan Mir's first project code */

const int ledPin2 = 6;
const int ledPin = 13;
const int sensor = 0;
int motor = 3;

int brightness3 = 0;
int brightness2 = 0;
int brightness1 = 0;

int fadeAmount2 = 10;
int fadeAmount = 5;//if smaller, slower in fade in
int fadeAmount3 = 1;

int value2;
int minChange = 1;
int maxChange = 1500;

int val = 0; //it's for button
int button = 4;


void setup()
{
  Serial.begin(9600);
  pinMode(6, OUTPUT);
  pinMode(13, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, INPUT);
}

void loop()
{
  val = digitalRead(4);
  if(val == HIGH){
  
  int distance = analogRead(0)/(2*0.3937); 
   
  Serial.print(distance, DEC);
  Serial.println("cm");
  
  
  if(distance<120){
  analogWrite(6, brightness1);
  brightness1 = brightness1 + fadeAmount2;
  if(brightness1 == 0 || brightness1 == 255)
  {fadeAmount2 = - fadeAmount2;}
  delay(1);
  
  int value2 = analogRead(0);
  value2 = map(value2, 1023, 0, minChange, maxChange);
  analogWrite(3, value2);
  Serial.println(0);}
 
  
  if(distance>=120 && distance<220)
  {
 analogWrite(6, brightness2);
  brightness2 = brightness2 + fadeAmount;
  if(brightness1 == 0 || brightness1 == 255)
  {fadeAmount = - fadeAmount;}
  delay(20);
  }

 if(distance>220 && distance<440){analogWrite(6, brightness3);
  brightness3 = brightness3 + fadeAmount3;
  if(brightness3 == 0 || brightness3 == 255)
  {fadeAmount3 = - fadeAmount3;}
  delay(100);}
  
  if(distance>440){analogWrite(6, LOW);}
  
   }
  else{digitalWrite(4, LOW);
analogWrite(6, LOW);
analogWrite(3, LOW);}
 
}
