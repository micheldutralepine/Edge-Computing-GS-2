# Edge-Computing-GS-2

Integrantes: Michel Dutra Lepine, Gabriel Fiore, Guilherme Santiago

Sistema de Monitoramento da Saúde do Oceano

1.

Introdução
O projeto de monitoramento da saúde do oceano permite acompanhar a temperatura e o pH dos ocenaos em tempo real. Utilizando um sensor de temperatura DHT22, um potenciometro para simular um sensor de pH e um display LCD I2C, o sistema exibe as medições em um display e utiliza LEDs para indicar condições críticas. Este sistema é ideal para pesquisadores, ambientalistas e qualquer pessoa interessada em monitorar a saúde dos oceanos.

Requesitos:
Sensor de Temperatura DHT22: Medição precisa de temperatura e umidade.
Potenciometro: Representando a acidez/alcalinidade da água.
Display LCD I2C (16x2): Exibição das medições de temperatura e pH.
LEDs (Vermelho e Amarelo): Indicação visual de condições fora do ideal.
LED Vermelho: Acende quando a temperatura está fora do intervalo 3-28°C ou pH está fora do intervalo 7.5-8.5.
LED Amarelo: Acende quando a temperatura está entre 27 e 28°C.
Arduino Uno: Processamento e controle dos sensores e LEDs.
Resistores: Componentes adicionais para a montagem do circuito.

Instruções de Uso
Montagem: Siga as instruções de montagem descritas anteriormente para conectar todos os componentes ao Arduino.
Upload do Código: Use a Arduino IDE para carregar o código fornecido no Arduino.
Monitoramento: Após o upload do código, o display LCD mostrará as medições de temperatura e pH. Observe os LEDs para indicações visuais:
LED Vermelho: Indica que a temperatura ou o pH estão fora dos limites aceitáveis.
LED Amarelo: Indica que a temperatura está em um intervalo crítico (27-28°C).

Demais informações:
Este sistema de monitoramento da saúde do oceano é uma ferramenta útil para avaliar as condições ambientais das águas oceânicas. Com medições em tempo real e indicações visuais claras, ele fornece informações valiosas para a preservação e estudo dos ecossistemas marinhos.

Link do Projeto:
https://wokwi.com/projects/399729739849414657



2. código fonte C++:
   
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>

#define DHTPIN 2
#define DHTTYPE DHT22

#define RED_LED_PIN 9
#define YELLOW_LED_PIN 10

DHT dht(DHTPIN, DHTTYPE);
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  lcd.begin(16, 2);
  lcd.backlight();
  dht.begin();

  pinMode(RED_LED_PIN, OUTPUT);
  pinMode(YELLOW_LED_PIN, OUTPUT);
}

void loop() {
  delay(2000);
  float temp = dht.readTemperature();
  int sensorValue = analogRead(A0);
  float pH = map(sensorValue, 0, 1023, 0, 14);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temp);
  lcd.print(" C");

  lcd.setCursor(0, 1);
  lcd.print("pH: ");
  lcd.print(pH);

  if (temp < 3 || temp > 28 || pH < 7.5 || pH > 8.5) {
    digitalWrite(RED_LED_PIN, HIGH);
  } else {
    digitalWrite(RED_LED_PIN, LOW);
  }


  if (temp >= 27 && temp <= 28) {
    digitalWrite(YELLOW_LED_PIN, HIGH);
  } else {
    digitalWrite(YELLOW_LED_PIN, LOW);
  }
}



Link do Video: https://www.youtube.com/watch?v=edLC1gSc7GY
