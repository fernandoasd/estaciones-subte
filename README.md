# 📋 Documentación de DOJO Nº2 SPD Div. 1º G. UTN FRA Grupo Nº 5.  

Prototipo de sistema que permita al usuario saber a qué estación de subte está
llegando realizado en Arduino. Trabajo practico nº 2 de materia SPD, Tecnicatura en Programación UTN FRA.
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
Estas instrucciones te permitirán comprender el funcionamiento del proyecto. Además, se incluye el enlace hacia TinkerCad para poder ver el proyecto armado con sus distintos componentes y poner el código en ejecución. 

[Link del proyecto en www.tinkercad.com](https://www.google.com)

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

## Función principal 🔩

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
  Serial.println("BOZZER ON");
  digitalWrite(BUZZER, 1);
}

void control_display (int numero, int tiempo1, int tiempo2 )
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
      	control_display(i, tiempo1, tiempo2);
    }
    Serial.println("\nESTACION MORENO - LLEGASTE A DESTINO\n");
  }
}
 ~~~

# Explicación de la Función principal.

## Parámetros de la función:
 ~~~ C
 void changeStatusDelay(int nombreLed1,
                       int nombreLed2,
                       int piezoStatus,
                      int timer)
 ~~~
- nombreLed1, nombreLed2:  
pares de leds a encender / apagar 
- piezoStatus:  
2 = sonido alto cada 1 seg  
1 = sonido bajo cada 2 seg  
0 = sin sonido
- timer:  
tiempo dado en milisegundos en el que los leds permanecen encendidos

## Hardcodeo interno de la función:
 ~~~ C
  int prendido_alto = 400;
  int apagado_alto = 600;
  int prendido_bajo = 1000;
  int apagado_bajo = 1000;
  unsigned long tiempo1 = 0;
  unsigned long tiempo2 = 0;
  long lapseTime = 0;
 ~~~

Estas variables marcan los tiempos (en milisegundos) de permanencia cada estado (prendidos y apagado) de 
los sonidos altos y bajos:

- int prendido_alto = 400  
milisegundos en el que el sonido alto esta encendido
- int apagado_alto = 600  
milisegundos en el que el sonido alto esta apagado
- int prendido_bajo = 1000  
milisegundos en el que el sonido bajo esta encendido
- int apagado_bajo = 1000  
milisegundos en el que el sonido bajo esta apagado  
##### Obs: Si se quieren modificar estos tiempos, se debe modificar la función (para este pequeño proyecto no es necesario parametrizarlos).  


## Cuerpo de la función:
~~~ C
  digitalWrite(nombreLed1, 1);
  digitalWrite(nombreLed2, 1);
  lapseTime = 0;
  tiempo1 = millis();
~~~
##### Obs: digitalWrite(nombreled1, 1) es una función de de la librería de Arduino. El primer parámero esta asociado a un pin de la placa de arduino, el segundo, energiza (1 o HIGH) o apaga el mismo (0 o LOW).
- Por lo tanto en nuestra función los dos digitalWrite energizan los leds conectados a los puertos asociados a nombreLed1 y nombreLed2.
- A continuación setea el lapseTime en cero.
- Luego la función millis() guarda el tiempo de desde que se inició el programa en la variable tiempo1.

#### Dependiendo del valor de piezoStatus se abre un `if` que dependiendo del valor de `piezoStatus` se ejecutan 3 ciclos `while`:

### Si `piezoStatus == 2 `:
~~~ C
if (piezoStatus == 2)
 {
     while (lapseTime < timer )
    {
      digitalWrite(ALTO, 1);
      delay(prendido_alto);
      digitalWrite(ALTO, 0);
      delay(apagado_alto);
      tiempo2 = millis();
      lapseTime = (tiempo2 - tiempo1);
      
    }
 }
~~~
- Comienza ciclo while para el ***sonido alto***:   
    - Prende y apaga el sonido alto una vez por ciclo, con los tiempos configurados al principio de la función.
    - Luego, en la variable tiempo2 se guarda el tiempo actual de ejecucion del programa.  
    - Se calcula la diferencia de tiempo entre tiempo2 y tiempo1 y se guarda en la variable lapseTime.  
     -Si ese lapso de tiempo es inferior al timer establecido como argumento `lapseTime < timer` se vuelve a inicar el ciclo hasta dejar de cumplir la condición del while.

### Si `piezoStatus = 1`:
~~~ C
 else
 {
    if (piezoStatus == 1)
    {
       while ( lapseTime < timer )
      {
        digitalWrite(BAJO, 1);
        delay(prendido_bajo);
        digitalWrite(BAJO, 0);
        delay(apagado_bajo);
        digitalWrite(BAJO, 1);
        delay(prendido_bajo);
        digitalWrite(BAJO, 0);
        delay(apagado_bajo);
        digitalWrite(BAJO, 1);
        delay(prendido_bajo);
        digitalWrite(BAJO, 0);
        tiempo2 = millis();
        lapseTime = (tiempo2 - tiempo1);
        
      }
    }
~~~
- Comienza otro ciclo while para el ***sonido bajo***:   
    - Es similar al ciclo anterior,  pero prende y apaga el sonido bajo 3 veces por ciclo.
    - Luego el control de tioempo es igual que en caso anterior.

### Si `piezoStatus = 0`:
~~~ C
else
     {
       if (piezoStatus == 0)
       {
         delay(timer);
       }
     }
   }
~~~
- Caso ***sin sonido***:   
    -  Simplemente ejecuta el timer u cierra la llave del primer if.

### Pie de la función:
~~~ C
    digitalWrite(ALTO, 0);
    digitalWrite(BAJO, 0);
    digitalWrite(nombreLed1, 0);
    digitalWrite(nombreLed2, 0);
  }
~~~
- Sin importar el valor del parametro `piezoStatus`
    siempre se ejecuta el siguiente algoritmo al final de la función (estan fuera del primer `if`):
    - Apaga el sonido y apaga y el apr de leds.
    - La ultima llave indica el cierre de la función.



## 🤖 Link al proyecto 
---

 Proyecto [Semáforo Adaptado ](https://www.tinkercad.com/things/8oHwzMKlTXf-dojo-1-semaforo-adaptado-v1/editel?sharecode=JPbVYoZY0ViAlwjupwjPqmmHtwbsWOnT7YtB-P6JKZs "Enlace del proyecto en Tinkercad") TinkerCad.
 - - - 

##  📘 Fuentes
---
- [Tecnicatura Universitaria en Programación - UTN](http://www.sistemas-utnfra.com.ar/#/pages/carrera/tecnico-programacion/resumen)
- [Consejos para documentar](https://www.sohamkamani.com/how-to-write-good-documentation/#architecture-documentation).

- [Lenguaje Markdown](https://markdown.es/sintaxis-markdown/#linkauto).

- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

- [Emojis](https://gist.github.com/rxaviers/7360908).  
