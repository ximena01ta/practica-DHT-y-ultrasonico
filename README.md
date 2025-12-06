# PRACTICA - DHT Y ULTRASONICO

## Introducción
Los materiales que acontinuación se muestran seran los encargados de mandar señales y visualizarlas en la pantalla LCD, con el fin de obtener resultados de humedad (%) y temperatura (°C) además de proporcionar datos del participante y dar la bienvenida.  

## Materiales
Simulador WOKWI (https://wokwi.com) :
- Tarjeta ESP32
- Sensor DHT22
- LCD 16x2
- Ultrasonico

## Procedimiento 
1. En el buscador ingresar la página https://wokwi.com

![](https://github.com/ximena01ta/practica-DHT-con-LCD/blob/main/Captura%20de%20pantalla%202025-12-05%20010958.png)

2. Seleccionar la opción ``ESP32`` en ambos casos

![](https://github.com/ximena01ta/practica-DHT-con-LCD/blob/main/Captura%20de%20pantalla%202025-12-05%20011019.png)
![](https://github.com/ximena01ta/practica-DHT-con-LCD/blob/main/Captura%20de%20pantalla%202025-12-05%20011217.png)

Nos llevará a la siguiente página:

![](https://github.com/ximena01ta/practica-DHT-con-LCD/blob/main/Captura%20de%20pantalla%202025-12-05%20010757.png)

3. En la parte de ``sketch.ino`` nos muestra el código anterior que debemos borrar para colocar el nuevo a continuación:
````
#include <LiquidCrystal_I2C.h>
#include "DHTesp.h"
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
const int DHT_PIN = 13;
DHTesp dhtSensor;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200); //iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros
TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
    lcd.clear();

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
      lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("BIENVENIDOS");
  lcd.setCursor(0, 1);
  lcd.print("MODULO 5");

delay(2000);
 lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("HELEN XIMENA");
  lcd.setCursor(0, 1);
  lcd.print("ING.MECANICO");
 
delay(2000);
lcd.clear();
lcd.setCursor(0, 1);
  lcd.print("Distancia: ");
  lcd.print(d);      //Enviamos serialmente el valor de la distancia
  lcd.print("cm");
  delay(2000);          //Hacemos una pausa de 100ms

delay(2000);
lcd.clear();
lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
delay(1500);
}
````

4. En ``Library Manager`` en la opción de ``+`` vamos a buscar las siguientes bibliotecas:

![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-06%20014542.png)

5. Para el siguiente paso en la parte de ``Simulation`` en la opción de ``+``

![](https://github.com/ximena01ta/practica-DHT-con-LCD/blob/main/Captura%20de%20pantalla%202025-12-04%20230350.png)

Vamos a buscar las opciones de: 
- DHT22
- LCD 16x2
- Ultrasonico

![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-06%20001953.png)
![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-05%20205947.png)
![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-04%20231406.png)

6. Hacer la conexión del Ultrasonico, LCD 16x2, DHT22 y el sensor ESP32:

![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-06%20014125.png)

7. Iniciamos la simulación con el botón ``play (|>)`` y empezará a visualizarse los lectores del sensor

![](https://github.com/ximena01ta/practica-DHT-con-LCD/blob/main/Captura%20de%20pantalla%202025-12-04%20230350.png)

8. Una vez que ha sido compilado de manera correcta enviara los resultados a la pantalla LCD:

![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-06%20015326.png)

## Resultados

![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-06%20015326.png)
![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-06%20015133.png)
![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-06%20015253.png)
![](https://github.com/ximena01ta/practica-DHT-y-ultrasonico/blob/main/Captura%20de%20pantalla%202025-12-06%20015308.png)


