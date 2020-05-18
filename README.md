# hello-world
int  ir=A0;//定义光敏电阻的pwm引脚为A0脚;
int YU_light;
int LED=6;//定义LED引脚
int  RED_ir=5;//定义红外避障为4号引脚;
bool RED;//定义布尔量存储
int trig=9;
void setup() {
   Serial.begin(9600);//打开串口序列埠
   pinMode(ir,INPUT);
   pinMode(LED,OUTPUT);
   pinMode(RED_ir,INPUT);
   pinMode(trig,INPUT);
   
}

void loop() {
  RED=digitalRead(RED_ir);//读取红外避障到bool量;
   Serial.println(RED);//输出bool量到串口序列埠中;
   YU_light= analogRead(A0);//读取光敏电阻的pwm值到串口序列埠中(0~1023);
int sensor =  map(YU_light,0,1023,255,0);
int x= map(YU_light,0,1023,255,0);
int LED_light =map(x,255,0,10,0);
int contact =map(YU_light,0,1023,150,255);//给一个触点信号：
   Serial.print("YU_light==");
   Serial.println(YU_light);
   Serial.print("contact==");
   Serial.println(contact);
   Serial.print("LED_light==");
   Serial.println(LED_light);
   Serial.print("x==");
   Serial.println(x);
 if ( RED == 0){
     if(YU_light<=1000){
      analogWrite(trig,contact);
      analogWrite(LED,sensor);
    }
   else {
    analogWrite(trig,LOW);
   }
 }
  else if(RED==1){
      analogWrite(trig,LOW);
  }
    delay(100);
}
