# Parcial_SPD_Ferrari_Franco
![Hospital](./img/incendio.jpg)


## Creador
  -Franco Ferrari



## Proyecto: Sistema de incendios.
![Tinkercad](./img/SPD_PARCIAL.JPG)


## Descripción
El Programa ejecuta la logica que sigue un sistema alertante de incendios.

Los dispositivos utilizados fueron: 2 Leds (uno rojo y uno azul), 1 contron remoto IR (para apagar o prender el programa y setearlo), 1 sensor IR (para leer las señales del control), 1 sensor de temperatura, 1 LCD 16x2 (para mostrar las salidas de los distintos eventos que ocurren), 1 potenciometro (para encender el lcd), 1 servonmotor (para activar la respuesta al incendio), 1 porotoboard (para realizar las conexiones) y 1 Placa Arduino UNO

Al comienzo del programa se definen constantes para referir los leds y los distintos dispositivos que se encuentran conectados, luego se declaran una serie de banderas para prender o apagar el programa.

## Funciones

A continuación se describen las funciones principales utilizadas en el proyecto:

### `obtener_temperatura()`

Esta función lee el valor del sensor de temperatura y realiza el cálculo necesario para obtener la temperatura en grados Celsius. Devuelve el valor de la temperatura como un número de punto flotante.

### `mostrar_grados(int temp)`

Esta función muestra la temperatura en grados en la pantalla LCD. Recibe como parámetro el valor de la temperatura a mostrar.

### `incendio_led()`

Esta función muestra un mensaje de "CUIDADO INCENDIO" en la pantalla LCD y enciende los LEDs para indicar una situación de incendio.

### `obtener_estacion()`

Esta función utiliza un control remoto infrarrojo para obtener la estación seleccionada por el usuario. Devuelve un número entero que representa la estación seleccionada.

### `encender_leds(int estacion)`

Esta función enciende los LEDs correspondientes a la estación seleccionada. Recibe como parámetro el número de estación y realiza el control de los pines de los LEDs para encenderlos según corresponda.

### `alarma(int maximo, int temp)`

Esta función compara la temperatura actual con un umbral máximo y, si se supera, activa una alarma. Muestra un mensaje en la pantalla LCD y mueve el servo motor a una posición específica para simular la alerta.


### Función principal: `loop()`

El programa principal utiliza un bucle `loop()` para controlar y monitorear la temperatura y la estación seleccionada. Se activa el programa al seleccionar la estación 5 y se desactiva al seleccionar la estación 6. Las acciones correspondientes se ejecutan mediante funciones auxiliares.

void loop() {
  int temp = obtener_temperatura();
  int estacion = obtener_estacion();
  int maximo;

  if (estacion == 5 && !prendido) {
    prendido = true;
    digitalWrite(LED_ROJA, HIGH);
    digitalWrite(LED_AZUL, LOW);
    LCD.setCursor(0, 0);
    LCD.print("Encendido");
    delay(1000);
  } 
  while (prendido) {
    
     temp = obtener_temperatura();
    if (estacion == 1 || estacion == 2) {
      maximo = 70;
    } else {
      maximo = 50;
    }

    encender_leds(estacion);
    delay(10);

    alarma(maximo, temp);
    delay(10);

    estacion = obtener_estacion();
    
    if ((estacion == 6 && prendido) || estacion == 6) {
    prendido = false;
    digitalWrite(LED_ROJA, LOW);
    digitalWrite(LED_AZUL, LOW);
    myservo.write(0);
    LCD.clear();
    LCD.setCursor(0, 0);
    LCD.print("Apagado");
    delay(1000);
  }

  }
}


## :robot: Link al proyecto
- [proyecto](https://www.tinkercad.com/things/7bZRIHKIjyQ-ferrari-franco-spd-parcial-2/editel?sharecode=qG9P9mMPrzOJbCUg4Gs9_MTDmEoVkj-YqJYjIHvC-Xw)
---
### Fuentes

- [Youtube]https://www.youtube.com/@cefuve
- [ChatGPT]https://chat.openai.com/
- [Arduino]https://www.arduino.cc/en/Guide
---
