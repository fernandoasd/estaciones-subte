# 📋 Documentación de DOJO Nº2 SPD Div. 1º G. UTN FRA Grupo Nº 5.  

Sistema programado en Arduino que indica al usuario de subterraneo la ubicación y la cantidad de estaciones que faltan para llegar a destino.  
 Trabajo práctico Nº 2 de la materia `SPD - Tecnicatura en Programación UTN FA`.  
Mayo 2023

![Imagen no encontrada](./img/ArduinoTinkercad.jpg "banner Intercad")

## Autores ✒️
***
* **Franco Mendieta** 
* **Fernando Malinowski** 
* **Facundo Leonelli** 
* **Carlos Marquez** 
* **Tadeo Iuliani**  

⌨️ con ❤️ por grupo nº5 SPD, DIV G.
## Proyecto: Señalizador de estaciónes de subte.
***
![Imagen no encontrada](./img/Dojo%202%20-%20Estaciones%20de%20subte.png "DOJO Nº1 SPD Div. 1º G. UTN FRA Grupo Nº 5.")

## Comenzando 🚀
***
En este proyecto simula un viaje en la línea C del subterraneo de Buenos Aires,  desde la estación Constitución hasta la de Moreno:
- Al presionar el pulsador da por comienzo la simulación.
- El sistema consta de 3 indicadores:   
  - Luces leds que indican la estación en donde se encuentra el pasajero.  
  - En el display se muestran la cantidad de estaciones faltantes para llegar hasta destino.
  - Una señal sonora (buzzer) indica que el subterraneo llega a una estación. 
 

Las siguientes instrucciones te permitirán comprender el funcionamiento del proyecto. Además, se incluye el enlace del proyecto en TinkerCad para poder copiarlo y modificarlo: 

[Link del proyecto en Tinkercad ](https://www.tinkercad.com/things/11JbVPn2ngt "Enlace del proyecto en Tinkercad")

## Consigna 🔩

Consigna SUBTE:
La empresa  “UTN FRA Robotics” ganó la licitación de un proyecto, y deberá Implementar un sistema que permita al usuario saber a qué estación de subte está llegando, aparte  el sistema muestra las estaciones que faltan hasta llegar a destino, para ello debemos utilizar 4 LEDs y el display de 7 segmentos.  
Esta vez el buzzer deberá emitir un sonido diferente cada vez que se llegue a una estación.
El sistema deberá arrancar apagado, luego de presionar el botón empezará y hará lo pedido.

Para realizar el proyecto deberán usar mínimamente:  
1 ARDUINO UNO.  
1 Display 7 segmentos.  
4 LEDS.  
1 BUZZER (Piezo).  
1 BOTÓN  
RESISTENCIAS NECESARIAS PARA CADA COMPONENTE.

## Código del programa: 🔩

* * *

 ~~~ C (Lenguaje del código)
#define A 12
#define B 13
#define C 2
#define D 3
#define E 4
#define F 11
#define G 10
#define R1 9
#define Y1 8
#define Y2 7
#define Y3 6
#define PULSADOR 14
#define BUZZER 15

//timer segmentos del display:
int tiempo1 = 100; 

//Tiempo de permanencia en estacion = tiempo de viaje
int tiempo2 = 1000; 

void setup()
{
  pinMode(A, OUTPUT);
  pinMode(B, OUTPUT);
  pinMode(C, OUTPUT);
  pinMode(D, OUTPUT);
  pinMode(E, OUTPUT);
  pinMode(F, OUTPUT);
  pinMode(G, OUTPUT);
  pinMode (R1, OUTPUT);
  pinMode (Y1, OUTPUT);
  pinMode (Y2, OUTPUT);
  pinMode (Y3, OUTPUT);
  pinMode (PULSADOR, INPUT);
  pinMode (BUZZER, OUTPUT);
  Serial.begin(9600);
}

void off_all()
{
  digitalWrite(A, 0);
  digitalWrite(B, 0);
  digitalWrite(C, 0);
  digitalWrite(D, 0);
  digitalWrite(E, 0);
  digitalWrite(F, 0);
  digitalWrite(G, 0);
  digitalWrite(R1, 0);
  digitalWrite(Y1, 0);
  digitalWrite(Y2, 0);
  digitalWrite(Y3, 0);
  digitalWrite(BUZZER, 0);
  Serial.println("ALL AFF ---\n");
}

void turn_on_one_by_one(int numero, int timer1)
{
    digitalWrite(numero, 1);
    delay(timer1);
}

void control_leds(int led)
{
  control_buzzer ();
  switch (led)
  {
    case 3:
    Serial.println("Estacion Constitucion");
    	digitalWrite(R1, 1);
    	break;
   	case 2:
    	Serial.println("Estacion San Juan");
    	digitalWrite(Y1, 1);
    	break;
    case 1:
    	Serial.println("Estacion Independencia");
    	digitalWrite(Y2, 1);
    	break;
    case 0:
    	Serial.println("Estacion Moreno");
    	digitalWrite(Y3, 1);
    	break;
  }
}

void control_buzzer ()
{
  Serial.println("BUZZER ON");
  digitalWrite(BUZZER, 1);
}

void control_estaciones (int numero, int tiempo1, int tiempo2 )
{
  control_leds(numero);
  switch(numero)
  {
    case 0:
    	Serial.println("DISPLAY 0");
    	turn_on_one_by_one(F, tiempo1);
    	turn_on_one_by_one(E, tiempo1);
    	turn_on_one_by_one(D, tiempo1);
    	turn_on_one_by_one(C, tiempo1);
    	turn_on_one_by_one(B, tiempo1);
        turn_on_one_by_one(A, tiempo1);
        break;
    
    case 1:
    	Serial.println("DISPLAY 1");
    	turn_on_one_by_one(B, tiempo1);
        turn_on_one_by_one(C, tiempo1);
    	break;
    
    case 2:
    	Serial.println("DISPLAY 2");
    	turn_on_one_by_one(A, tiempo1);
      turn_on_one_by_one(B, tiempo1);
   	turn_on_one_by_one(G, tiempo1);
    	turn_on_one_by_one(E, tiempo1);
    	turn_on_one_by_one(D, tiempo1);
    	break;
    
    case 3:
    	Serial.println("DISPLAY 3");
    	turn_on_one_by_one(A, tiempo1);
      turn_on_one_by_one(B, tiempo1);
   	turn_on_one_by_one(G, tiempo1);
    	turn_on_one_by_one(C, tiempo1);
    	turn_on_one_by_one(D, tiempo1);
    	break;
    case 4:
    	Serial.println("DISPLAY 4");
    	turn_on_one_by_one(F, tiempo1);
      turn_on_one_by_one(G, tiempo1);
   	turn_on_one_by_one(B, tiempo1);
    	turn_on_one_by_one(C, tiempo1);
    	break;
    
    case 5:
    	Serial.println("DISPLAY 5");
    	turn_on_one_by_one(A, tiempo1);
      turn_on_one_by_one(F, tiempo1);
   	turn_on_one_by_one(G, tiempo1);
    	turn_on_one_by_one(C, tiempo1);
    	turn_on_one_by_one(D, tiempo1);
    	break;
    
    case 6:
    	Serial.println("DISPLAY 6");
    	turn_on_one_by_one(A, tiempo1);
        turn_on_one_by_one(F, tiempo1);
    	turn_on_one_by_one(E, tiempo1);
    	turn_on_one_by_one(D, tiempo1);
    	turn_on_one_by_one(C, tiempo1);
    	turn_on_one_by_one(G, tiempo1);
    	break;
    
    case 7:
    	Serial.println("DISPLAY 7");
    	turn_on_one_by_one(A, tiempo1);
        turn_on_one_by_one(B, tiempo1);
    	turn_on_one_by_one(C, tiempo1);
    	break;
    
    case 8:
    	Serial.println("DISPLAY 8");
        turn_on_one_by_one(B, tiempo1);
    	turn_on_one_by_one(A, tiempo1);
        turn_on_one_by_one(F, tiempo1);
        turn_on_one_by_one(G, tiempo1);
        turn_on_one_by_one(C, tiempo1);
        turn_on_one_by_one(D, tiempo1);
        turn_on_one_by_one(E, tiempo1);
    	break;
    
    case 9:
    	Serial.println("DISPLAY 9");
    	turn_on_one_by_one(A, tiempo1);
    	turn_on_one_by_one(F, tiempo1);
    	turn_on_one_by_one(G, tiempo1);
    	turn_on_one_by_one(B, tiempo1);
        turn_on_one_by_one(C, tiempo1);
    	break;

  }
  delay(tiempo2);
  off_all ();
  delay(tiempo2);
}

void loop()
{
  int presiono = digitalRead(PULSADOR);
  if (presiono == 1)
  {
      Serial.println("BUEN VIAJE!!!\n");
      for (int i = 3; i > -1; i--)
    {
      	control_estaciones(i, tiempo1, tiempo2);
    }
    Serial.println("\nESTACION MORENO - FINAL DEL RECORRIDO\n");
  }
}
 ~~~

- numero:  
Es el número que aparecerá en el display.
- tiempo1:  
Es el tiempo dado en milisegundos en que tarda en encender cada segmento del display (por lo que los segmentos se encienden secuencialmente, en un cierto orden establecido en el cuerpo de la función, hasta completar el número)
- tiempo2:  
tiempo dado en milisegundos en el número indicado en el display permanece encendido y luego apagado.  

##### Obs: Estas variables estan declaradas con los valores:
  -tiempo1 = 100  
  -tiempo2 = 1000

## Lamado a la funcion control_leds():
 ~~~ C
  control_leds(numero);
 ~~~

Esta función llama a la funcion `control_buzze()`, esta enciende el buzzer.  
Luego enciende los leds indicadores de la `estación` dependindo del parámetro y lo indica por monitor serial, si:

- numero = 3  
 estacion `Constitución`
- numero = 3    
estacion `San Juan`
- numero = 1    
estacion `Independencia`
- numero = 0    
estacion `Moreno`  


## switch(numero):
~~~ C
  switch(numero)
  {
    case 0:
    	Serial.println("DISPLAY 0");
    	turn_on_one_by_one(F, tiempo1);
    	turn_on_one_by_one(E, tiempo1);
    	turn_on_one_by_one(D, tiempo1);
    	turn_on_one_by_one(C, tiempo1);
    	turn_on_one_by_one(B, tiempo1);
        turn_on_one_by_one(A, tiempo1);
        break;
    
    case 1:
    	Serial.println("DISPLAY 1");
    	turn_on_one_by_one(B, tiempo1);
      turn_on_one_by_one(C, tiempo1);
    	break;
    
    case 2:
    	Serial.println("DISPLAY 2");
    	turn_on_one_by_one(A, tiempo1);
      turn_on_one_by_one(B, tiempo1);
   		turn_on_one_by_one(G, tiempo1);
    	turn_on_one_by_one(E, tiempo1);
    	turn_on_one_by_one(D, tiempo1);
    	break;

      case 3:
    	Serial.println("DISPLAY 3");
    	turn_on_one_by_one(A, tiempo1);
      turn_on_one_by_one(B, tiempo1);
   		turn_on_one_by_one(G, tiempo1);
    	turn_on_one_by_one(C, tiempo1);
    	turn_on_one_by_one(D, tiempo1);
    	break;
      .
      .
      .
~~~
##### Obs: El switch ejecuta hasta el case 9 (en el caso de que se agreguen mas estaciones en el futuro), pero en este proyecto se utiliza hasta el case 3.
- Se enciende el display (del 0 al 9) y lo indica por consola serial: el numero indicado es el del parametro número (cada número se encenderá segmento a segmento en una secuencia predefinida).


### Timer y apagado total:
~~~ C
delay(tiempo2);
off_all ();
delay(tiempo2);
}
~~~
- Se inicia un delay de 'tiempo2' milisegundos. Es el tiempo en que los leds, display y buzzer permanecen encendidos.  
- Llama a la función `off_all()`, esta apago todo: leds, display y buzzer.
- Luego se ejecuta otro timer. Este representa el tiempo en el que se apaga un numero y se enciende el siguiente.

### void loop():
~~~ C
 void loop()
{
  int presiono = digitalRead(PULSADOR);
  if (presiono == 1)
  {
      Serial.println("BUEN VIAJE!!!\n");
      for (int i = 3; i > -1; i--)
    {
      	control_estaciones(i, tiempo1, tiempo2);
    }
    Serial.println("\nESTACION MORENO - LLEGASTE A DESTINO\n");
  }
}
~~~
- Si se presiona el pulsador da comiendo al viaje:   
    - Se anuncia por monitor serial el inicio del viaje.
    - Inicia un contador del 3 al 0 y lo usa como parámetro para la función principal `control_estaciones()` dando por comienzo a la simulación.  
    - El monitor serial anuncia el fin del recorrido.





## 🤖 Link al proyecto 
---

 Proyecto [Estaciones de subte ](https://www.tinkercad.com/things/11JbVPn2ngt "Enlace del proyecto en Tinkercad") TinkerCad.
 - - - 

##  📘 Fuentes
---
- [Tecnicatura Universitaria en Programación - UTN](http://www.sistemas-utnfra.com.ar/#/pages/carrera/tecnico-programacion/resumen).
- [Pushing commits to a remote repository](https://docs.github.com/en/enterprise-server@3.5/get-started/using-git/pushing-commits-to-a-remote-repository "Use git push to push commits made on your local branch to a remote repository.").

- [Consejos para documentar](https://www.sohamkamani.com/how-to-write-good-documentation/#architecture-documentation).

- [Lenguaje Markdown](https://markdown.es/sintaxis-markdown/#linkauto).

- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

- [Emojis](https://gist.github.com/rxaviers/7360908).  
