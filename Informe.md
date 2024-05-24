# Informe Técnico: Sistema de Riego Automatizado

---

## Descripción del Problema

El proyecto tiene como objetivo desarrollar un sistema de riego automatizado para optimizar el uso del agua en un área de cultivo determinada. Se busca implementar un sistema que pueda monitorear los niveles de agua en el suelo y activar la bomba de riego de manera automática cuando sea necesario, utilizando energía solar para su funcionamiento. Esto permitirá mejorar la eficiencia del riego, reducir el desperdicio de agua y facilitar el cuidado de los cultivos.

## Datos de los Integrantes del Grupo

- **Nombre del Grupo:** [Nombre del grupo]
- **Integrantes:**
  1. Jheferson Navas Doria
  2. Daniel Esteban Álvarez Caro
  3. Iván Darío Ramos Cálao
  4. Samuel David Martinez Gómez

## Componentes Utilizados

- **Bomba:** 6,000
- **Microbit:** 90,000
- **Batería:** 10,000
- **Controlador de Carga:** 3,000
- **Tubo de Agua:** 2,000
- **Terminales, Tornillos y Cables:** 15,000
- **LM7805 (Regulador de Voltaje):** 1,500
- **2N2222 (Transistor):** 1,000
- **Resistencia:** 100
- **Vaquela (Placa de Circuito):** 3,000
- **Cable USB:** 5,000
- **Panel Solar:** 25,000
- **Jarro de Agua (Sensor de Nivel de Agua):** 15,000
- **Sensor de Ultrasonido:** 4,000
- **Cajita para el Sistema:** 1,000

**Subtotal de Componentes:** 181,600

## Proceso de Instalación y Configuración

El proceso de instalación y configuración del sistema de riego automatizado involucra los siguientes pasos:

1. **Ensamblaje de Componentes:** Se ensamblan los componentes según el diseño previamente establecido.

2. **Instalación del Panel Solar:** Se instala el panel solar en una ubicación óptima para captar la mayor cantidad de luz solar posible.

3. **Conexión de Sensores:** Se conectan los sensores de nivel de agua y ultrasonido al microcontrolador.

4. **Configuración del Microbit:** Se programa el microbit para que pueda leer los datos de los sensores y activar la bomba de riego según sea necesario.

5. **Pruebas del Sistema:** Se realizan pruebas para verificar el correcto funcionamiento del sistema en diferentes condiciones.

## Pruebas Realizadas y Resultados Obtenidos

Durante el proceso de desarrollo, se llevaron a cabo diversas pruebas para evaluar el rendimiento y la fiabilidad del sistema de riego automatizado. Estas pruebas incluyeron:

- Pruebas de Funcionamiento: Se verificó que el sistema activara la bomba de riego cuando los niveles de agua en el suelo estuvieran por debajo de un umbral predefinido.

- Pruebas de Eficiencia Energética: Se analizó el consumo energético del sistema y su capacidad para operar de manera autónoma utilizando energía solar.


Los resultados obtenidos de las pruebas demostraron que el sistema de riego automatizado es capaz de mantener niveles óptimos de humedad en el suelo y responder de manera optima a las necesidades de riego de los cultivos.

## Costo de Mano de Obra

El costo de mano de obra para el proyecto fue de 20,000.

## Total del Proyecto

El costo total del proyecto, incluyendo componentes y mano de obra, fue de 201,600.

---

Este informe documenta el proceso de desarrollo del sistema de riego automatizado, las pruebas realizadas y los resultados obtenidos. Se concluye que el sistema implementado cumple con los objetivos establecidos y representa una solución efectiva para optimizar el riego en áreas de cultivo.

## Codigo 

Nivel = 0
distancia = 0
HUMEDAD = 0
timeanddate.set_date(5, 20, 2024)
timeanddate.set24_hour_time(12, 35, 0)
datalogger.set_column_titles("HORA", "HUMEDAD", "NIVEL DE AGUA")

def on_forever():
    global HUMEDAD
    HUMEDAD = pins.map(pins.analog_read_pin(AnalogPin.P0), 0, 1023, 0, 100)
    while distancia >= 15 and distancia <= 18:
        music.play(music.tone_playable(988, music.beat(BeatFraction.WHOLE)),
            music.PlaybackMode.UNTIL_DONE)
    if distancia >= 15 and distancia <= 18:
        pins.digital_write_pin(DigitalPin.P12, 0)
    if HUMEDAD >= 0 and HUMEDAD <= 30:
        pins.digital_write_pin(DigitalPin.P12, 1)
        basic.pause(10000)
        pins.digital_write_pin(DigitalPin.P12, 0)
    elif HUMEDAD >= 31 and HUMEDAD <= 50:
        pins.digital_write_pin(DigitalPin.P12, 1)
        basic.pause(7000)
        pins.digital_write_pin(DigitalPin.P12, 0)
    elif HUMEDAD >= 51 and HUMEDAD <= 80:
        pins.digital_write_pin(DigitalPin.P12, 1)
        basic.pause(5000)
        pins.digital_write_pin(DigitalPin.P12, 0)
    else:
        pins.digital_write_pin(DigitalPin.P12, 0)
        basic.pause(2000)
    basic.pause(5000)
basic.forever(on_forever)

def on_forever2():
    global distancia, Nivel
    distancia = sonar.ping(DigitalPin.P1, DigitalPin.P2, PingUnit.CENTIMETERS)
    Nivel = pins.map(sonar.ping(DigitalPin.P1, DigitalPin.P2, PingUnit.CENTIMETERS),
        2,
        18,
        0,
        100)
    basic.pause(1800000)
basic.forever(on_forever2)

def on_forever3():
    serial.write_number(HUMEDAD)
    serial.write_string("")
    serial.write_number(sonar.ping(DigitalPin.P1, DigitalPin.P2, PingUnit.CENTIMETERS))
    serial.write_string("")
    basic.pause(5000)
basic.forever(on_forever3)

def on_every_interval():
    datalogger.log(datalogger.create_cv("HUMEDAD", HUMEDAD),
        datalogger.create_cv("NIVEL DE AGUA", Nivel),
        datalogger.create_cv("HORA", timeanddate.date_time()))
loops.every_interval(5000, on_every_interval)

Este es el código para la microbit que se utiliza en el sistema de riego automatizado. El 
código se encarga de leer los niveles de humedad del suelo y los niveles de agua en el jarro, y activar la bomba de riego según sea necesario. También registra los datos en un datalogger para su posterior análisis.



