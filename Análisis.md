Análisis

El problema consiste en diseñar un sistema de riego automatizado que funcione en función de dos parámetros principales: la humedad del suelo y el nivel del agua en un recipiente de suministro. El sistema debe ser capaz de:

Medir la humedad del suelo.
Medir el nivel de agua en el recipiente de suministro.
Activar una motobomba para regar la planta cuando la humedad del suelo esté por debajo de un umbral definido.
Evitar la activación de la motobomba si el nivel del agua en el recipiente es insuficiente.
Generar una alerta cuando el nivel del agua en el recipiente esté por debajo de un valor crítico.


Requisitos del Sistema de Riego Automatizado
Sensor de Humedad del Suelo:

Mide la humedad del suelo en la zona de las raíces.
Alta precisión y resolución.
Resistente al entorno.

Sensor de Nivel de Agua:

Mide el nivel de agua en el recipiente de suministro.
Detecta niveles suficientes y críticos.
Impermeable y duradero.

Motobomba:
Capacidad de bombear agua según necesidades de la planta.
Compatible con control automatizado.
Eficiente en consumo energético.

Microcontrolador o PLC:
Entradas suficientes para sensores de humedad y nivel de agua.
Salidas para controlar la motobomba.
Programable para lógica de control.
Capaz de generar alertas.

Algoritmo de Control
Condiciones de Activación:

Activar motobomba si humedad del suelo < umbral definido y nivel de agua > mínimo.
Condiciones de Desactivación:

Desactivar motobomba si humedad del suelo >= umbral o nivel de agua <= mínimo.
Condiciones de Alerta:

Generar alerta si nivel de agua <= crítico.
Sistema de Alerta
Alertas:
Visual, auditiva o remota cuando el nivel de agua es crítico.

Fuente de Energía
Alimentación:
Energía suficiente para el funcionamiento continuo del sistema.
Seguridad y adecuación al entorno.
