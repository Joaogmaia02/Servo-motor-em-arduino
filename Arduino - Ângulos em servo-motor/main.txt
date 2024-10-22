//Bibliotecas do servo-motor e do monitor LCD
#include <Servo.h>
#include <Adafruit_LiquidCrystal.h>

//Variáveis e pinos dos botões
#define btnAnguloA  5
#define btnAnguloB  6
#define btnNome  7

Adafruit_LiquidCrystal lcd_1(0);

//Variáveis e pinos do ângulo e do servo-motor
Servo servo1;
int angulo = 0;
int pino_servo = 2;

void inicio()
{
    lcd_1.clear();//Limpar tela LCD
    angulo = 0;//Declaração do ângulo desejado
    servo1.write(angulo);//Uso do ângulo desenjado no servo-motor

    //Escrita do ângulo no monitor serial
    Serial.print("Angulo = ");
    Serial.println(angulo);

    //Escrita do ângulo no monitor LCD
    lcd_1.print("Angulo = ");
    lcd_1.print(angulo);
    delay(1000);
}

void movimentoA()
{
    lcd_1.clear();//Limpar tela LCD
    angulo = 90;//Declaração do ângulo desejado
    servo1.write(angulo);//Uso do ângulo desenjado no servo-motor

    //Escrita do ângulo no monitor serial
    Serial.print("Angulo = ");
    Serial.println(angulo);

    //Escrita do ângulo no monitor LCD
    lcd_1.print("Angulo = ");
    lcd_1.print(angulo);
    delay(1000);
}

void movimentoB()
{
    lcd_1.clear();//Limpar tela LCD
    angulo = 180;//Declaração do ângulo desejado
    servo1.write(angulo);//Uso do ângulo desenjado no servo-motor

    //Escrita do ângulo no monitor serial
    Serial.print("Angulo = ");
    Serial.println(angulo);

    //Escrita do ângulo no monitor LCD
    lcd_1.print("Angulo = ");
    lcd_1.print(angulo);
    delay(1000);
}

void NomeRA()
{
    lcd_1.clear();//Limpar tela LCD

    //Escrita do nome e do RA no monitor serial
    Serial.println("Joao G. = 009923");

    //Escrita do nome e do RA no monitor LCD
    lcd_1.setCursor(0, 0);  
    lcd_1.print("Joao G. Maia");
    lcd_1.setCursor(0, 1);
    lcd_1.print("0099/23");
    delay(1000);
}

void setup()
{
    //Declaração dos botões "btnAnguloA" e "btnAnguloB"
    pinMode(btnAnguloA, INPUT);
    pinMode(btnAnguloB, INPUT);
    pinMode(btnNome, INPUT);

    servo1.attach(pino_servo);//Associação do servo-motor a variável "pino_servo"

    //Configurações do monitor LCD
    lcd_1.begin(16, 2);
    lcd_1.setCursor(0, 0);
    Serial.begin(9600);
}

void loop()
{
    //Condição para quando nenhum dos botões são apertados
    if ((digitalRead(btnAnguloA) == HIGH) && (digitalRead(btnAnguloB) == HIGH) && (digitalRead(btnNome) == HIGH))
    {
      inicio();//Executar a void "inicio"
    } 

    //Condição para CASO o botão da esquerda for apertado
    else if (digitalRead(btnAnguloA) == LOW)
    {
      movimentoA();//Executar a void "movimentoA"
    }

    //Condição para CASO o botão do meio for apertado
    else if (digitalRead(btnAnguloB) == LOW)
    {
      movimentoB();//Executar a void "movimentoB"
    }
  
  	//Condição para CASO o botão da direita for apertado
    else if (digitalRead(btnNome) == LOW)
    {
      NomeRA();//Exibe a void "NomeRA"
    }
    delay (1000);
}