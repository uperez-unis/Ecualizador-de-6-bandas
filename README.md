# Ecualizador Analógico de 6 Bandas para Piano Eléctrico

<p align="center">
  <em>Universidad del Istmo de Guatemala</em><br>
  <em>Facultad de Ingeniería</em><br>
  <em>Ecualizador Analógico de 6 Bandas para Piano Eléctrico</em><br>
  <em>Microelectronic Devices</em>
</p>

<div align="center">
  <img src="Imagenes/Logo_UNIS.png" alt="Logo UNIS" width="45%"/>
</div>

<p align="center">
  <em>Uriel Pérez</em><br>
  <em>Diego Lemus</em><br>
  <em>Diego Solis</em><br>
  <em>2026</em>
</p>

## Descripción del Proyecto

Este repositorio contiene el desarrollo de un ecualizador analógico de seis bandas diseñado para el procesamiento de audio de un piano eléctrico. El objetivo principal del proyecto fue diseñar, simular y analizar un sistema capaz de modificar distintas regiones del espectro de frecuencia del instrumento, permitiendo controlar graves, medios, presencia, ataque y brillo de forma independiente.

El circuito se basa en filtros activos pasa-banda construidos a partir de etapas Sallen-Key de segundo orden. Cada banda está formada por la cascada de un filtro pasa-altas y un filtro pasa-bajas, obteniendo así un comportamiento pasa-banda de cuarto orden. Posteriormente, las señales filtradas son enviadas a una etapa sumadora inversora, donde se implementa el control de ganancia de cada banda.

El diseño fue orientado a una respuesta adecuada para piano eléctrico, cuyo rango útil se concentra aproximadamente entre 40 Hz y 6 kHz. Para mejorar la respuesta en la frecuencia central de cada banda, se utilizó un ancho de banda de dos octavas, reduciendo la atenuación en el punto central de cada filtro.

## Objetivo del Proyecto

Diseñar un ecualizador analógico de seis bandas para piano eléctrico que permita amplificar o atenuar diferentes rangos de frecuencia, utilizando filtros activos Sallen-Key, control de ganancia por banda y una etapa de salida capaz de manejar una bocina de 8 Ω.

## Arquitectura del Sistema

El sistema se divide en cuatro etapas principales:

1. **Etapa de acople:** utiliza un seguidor de voltaje para proporcionar alta impedancia de entrada y evitar la pérdida de señal del instrumento.
2. **Etapa de filtrado:** formada por seis ramas pasa-banda activas, cada una construida con filtros Sallen-Key pasa-altas y pasa-bajas.
3. **Etapa de control de ganancia:** permite ajustar la amplificación o atenuación de cada banda mediante potenciómetros.
4. **Etapa de potencia:** utiliza transistores BJT en configuración clase AB para entregar la señal procesada hacia una bocina de 8 Ω.

## Diagrama General

Entrada del Piano Eléctrico  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Buffer de Alta Impedancia  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Seis Filtros Pasa-Banda en Paralelo  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Control de Ganancia por Banda  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Sumador Activo Inversor  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Etapa de Potencia Clase AB  
&nbsp;&nbsp;&nbsp;&nbsp;│  
&nbsp;&nbsp;&nbsp;&nbsp;▼  
Bocina de 8 Ω

## Bandas de Frecuencia

Las bandas fueron seleccionadas tomando en cuenta el comportamiento musical del piano eléctrico y las zonas más importantes de su espectro sonoro.

| Banda | Rango Inicial | Frecuencia Central | Función Musical |
|---:|---:|---:|---|
| 1 | 40 - 80 Hz | 57 Hz | Controla la profundidad y peso de las notas graves |
| 2 | 80 - 200 Hz | 127 Hz | Ajusta el cuerpo y la calidez del instrumento |
| 3 | 200 - 500 Hz | 316 Hz | Ayuda a corregir sonidos opacos o encerrados |
| 4 | 500 - 1500 Hz | 886 Hz | Aporta definición y presencia en la mezcla |
| 5 | 1500 - 3000 Hz | 2121 Hz | Controla el ataque y detalle del sonido |
| 6 | 3000 - 8000 Hz | 4900 Hz | Ajusta el brillo y los armónicos superiores |

## Frecuencias de Corte Utilizadas

Para mejorar el desempeño de cada filtro, se utilizó un ancho de banda de dos octavas alrededor de la frecuencia central. Las frecuencias finales utilizadas para el diseño fueron:

| Banda | Corte Inferior | Corte Superior | Frecuencia Central |
|---:|---:|---:|---:|
| 1 | 28.5 Hz | 114 Hz | 57 Hz |
| 2 | 63.5 Hz | 254 Hz | 127 Hz |
| 3 | 158 Hz | 632 Hz | 316 Hz |
| 4 | 443 Hz | 1772 Hz | 886 Hz |
| 5 | 1060.5 Hz | 4242 Hz | 2121 Hz |
| 6 | 2450 Hz | 9800 Hz | 4900 Hz |

## Construcción de los Filtros

Cada banda del ecualizador está compuesta por:

- Un filtro pasa-altas de segundo orden
- Un filtro pasa-bajas de segundo orden
- Una etapa de control de ganancia
- Una conexión hacia el sumador activo

Al conectar en cascada el filtro pasa-altas y el filtro pasa-bajas, se obtiene una respuesta pasa-banda de cuarto orden. Esta configuración permite una mejor separación entre bandas y una atenuación aproximada de **-40 dB/dec** fuera del rango de paso.

Los filtros fueron diseñados con respuesta tipo Butterworth, usando un factor de calidad aproximado de:

**Q = 0.707**

Este valor permite obtener una respuesta plana en la banda de paso y una atenuación controlada en las frecuencias de corte.

## Topología Sallen-Key

El proyecto utiliza la topología Sallen-Key para implementar los filtros activos de segundo orden. Esta topología fue seleccionada porque permite construir filtros pasa-altas y pasa-bajas con amplificadores operacionales, resistencias y capacitores, manteniendo una estructura sencilla y adecuada para aplicaciones de audio.

Cada filtro fue configurado con ganancia unitaria, dejando el control de nivel de cada banda para una etapa posterior.

## Valores Calculados de Componentes

### Banda 1 - 57 Hz

| Componente | HP2 | LP2 |
|---|---:|---:|
| R1 | 3.9 kΩ | 27 kΩ |
| R2 | 8.2 kΩ | 16 kΩ |
| C1 | 1 µF | 0.1 µF |
| C2 | 1 µF | 0.047 µF |

### Banda 2 - 127 Hz

| Componente | HP2 | LP2 |
|---|---:|---:|
| R1 | 18 kΩ | 12 kΩ |
| R2 | 36 kΩ | 6.8 kΩ |
| C1 | 0.1 µF | 0.1 µF |
| C2 | 0.1 µF | 0.047 µF |

### Banda 3 - 316 Hz

| Componente | HP2 | LP2 |
|---|---:|---:|
| R1 | 6.8 kΩ | 47 kΩ |
| R2 | 15 kΩ | 30 kΩ |
| C1 | 0.1 µF | 0.01 µF |
| C2 | 0.1 µF | 0.0047 µF |

### Banda 4 - 886 Hz

| Componente | HP2 | LP2 |
|---|---:|---:|
| R1 | 24 kΩ | 16 kΩ |
| R2 | 51 kΩ | 10 kΩ |
| C1 | 0.01 µF | 0.01 µF |
| C2 | 0.01 µF | 0.0047 µF |

### Banda 5 - 2121 Hz

| Componente | HP2 | LP2 |
|---|---:|---:|
| R1 | 11 kΩ | 6.8 kΩ |
| R2 | 22 kΩ | 4.3 kΩ |
| C1 | 0.01 µF | 0.01 µF |
| C2 | 0.01 µF | 0.0047 µF |

### Banda 6 - 4243 Hz

| Componente | HP2 | LP2 |
|---|---:|---:|
| R1 | 4.7 kΩ | 30 kΩ |
| R2 | 9.1 kΩ | 18 kΩ |
| C1 | 0.01 µF | 0.001 µF |
| C2 | 0.01 µF | 470 pF |

## Control de Ganancia

La etapa de control de ganancia se implementó mediante un sumador inversor con resistencia de realimentación, resistencia serie y potenciómetro. Esto permite modificar la contribución de cada banda hacia la salida final.

El rango de ganancia diseñado fue aproximadamente de:

**-12 dB a +12 dB**

Los valores comerciales seleccionados fueron:

- Resistencia de realimentación: **Rf = 13.3 kΩ**
- Resistencia serie mínima: **Rs = 3.3 kΩ**
- Potenciómetro por banda: **Rp = 50 kΩ**

Con estos valores se obtiene:

| Condición | Valor de Rp | Ganancia Aproximada |
|---|---:|---:|
| Realce máximo | 0 Ω | +12.12 dB |
| Ganancia unitaria | 10 kΩ | 0 dB |
| Atenuación máxima | 50 kΩ | -12.06 dB |

## Etapa de Salida

Para la salida del sistema se consideró una bocina de:

**8 Ω / 35 W RMS**

Esta bocina fue seleccionada porque permite trabajar con una etapa de potencia clase AB sin requerir corrientes excesivas. Además, proporciona un margen adecuado para evitar saturación o daño ante picos de señal.

El voltaje máximo eficaz permitido por la bocina se calculó mediante:

**Vrms = sqrt(P × R)**

**Vrms = sqrt(35 W × 8 Ω)**

**Vrms ≈ 16.7 V**

Esto permite establecer un límite de seguridad para la señal de salida del ecualizador.

## Simulación en LTspice

El diseño fue simulado en LTspice utilizando modelos de amplificadores operacionales TL081. Las simulaciones incluyeron:

- Análisis individual de filtros pasa-altas y pasa-bajas
- Comparación entre ancho de banda de una octava y dos octavas
- Simulación conjunta de las seis bandas pasa-banda
- Validación de la etapa sumadora inversora
- Evaluación del rango de ganancia de **-12 dB**, **0 dB** y **+12 dB**

Durante el análisis inicial con una octava se observó que la respuesta máxima del filtro no alcanzaba 0 dB, por lo que se ajustó el ancho de banda a dos octavas. Con esta corrección, la atenuación en la frecuencia central se redujo considerablemente.

## Resultados Principales

- Se diseñaron seis bandas de ecualización enfocadas en el rango sonoro del piano eléctrico.
- Cada banda fue implementada como un filtro pasa-banda activo de cuarto orden.
- Se utilizó topología Sallen-Key para los filtros pasa-altas y pasa-bajas.
- El ancho de banda de dos octavas permitió mejorar la respuesta en la frecuencia central.
- La etapa sumadora inversora permitió controlar cada banda dentro de un rango aproximado de ±12 dB.
- La etapa de salida fue diseñada considerando una bocina de 8 Ω y 35 W RMS.
- Las simulaciones en LTspice permitieron comprobar el comportamiento general del sistema.

## Herramientas Utilizadas

- LTspice
- Amplificadores operacionales TL081
- Filtros activos Sallen-Key
- Transistores BJT para etapa clase AB
- Herramienta Okawa-denshi para cálculo de filtros
- Análisis AC para respuesta en frecuencia
- Diseño y análisis de circuitos analógicos


## Integrantes

- Uriel Pérez
- Diego Lemus
- Diego Solis

## Video del Proyecto

En el siguiente enlace se presenta el funcionamiento y explicación general del proyecto:

[Ver video en YouTube](https://youtube.com/shorts/Q-_U898Za5Q)
