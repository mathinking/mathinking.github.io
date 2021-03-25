---
layout: single
title: "El papel de la Inteligencia Artificial en la Conducción Autónoma"
excerpt: Versión extendida del artículo divulgativo publicado el 16 de marzo de 2021 en elEconomista.es
date:  2021-03-25 07:31:00 +0100
categories: [blog, es]
tags: [ia, deep learning, automated driving]
toc: true
toc_label: En este post encontrarás
toc_sticky: true

header:
  teaser: /assets/images/2021/ai-autonomous-driving/highway.jpg
  overlay_color: "#000"
  overlay_filter: "0.3"
  overlay_image: /assets/images/2021/ai-autonomous-driving/highway.jpg
  caption: "Photo credit: [FLY:D](https://unsplash.com/@flyd2069?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  actions:
    - label: "Descarga la revista Digital 4.0"
      url: "https://bit.ly/3cgAm6v"
  
---
_Artículo publicado el 16 de marzo de 2021 en [elEconomista.es](https://revistas.eleconomista.es/digital/2021/marzo/el-papel-de-la-inteligencia-artificial-en-la-conduccion-autonoma-YG6822515)_

## Historia y contexto
El sueño de la conducción autónoma no es algo reciente. Hace ya más de 80 años, General Motors presentó en la exposición universal de Nueva York de 1939 su visión de un mundo futuro que incluía carreteras inteligentes y coches autónomos. Y, a pesar de que no vivamos aún en ese paisaje futurista, la tecnología de los coches sin conductor ha avanzado considerablemente. Precisamente en ese mismo año, las divisiones de Cadillac y Oldsmobile de General Motors desarrollaron la transmisión automática, que eliminaba la necesidad de cambiar manualmente de marcha. Sin saberlo, se comenzaban a dar los primeros pasos en el desarrollo del coche autónomo. 

Muchos progresos en el desarrollo de Sistemas Avanzados de Asistencia a la Conducción (ADAS, por sus siglas en inglés) han surgido de comprobar que hacemos una conducción ineficiente. En los años 40, Ralph Teetor, quien no podía conducir por ser invidente, notó una tendencia en su abogado ─quien conducía─ a reducir la velocidad al hablar y acelerar al escuchar. Su invención dio lugar al control de crucero moderno. Sin embargo, el avance más relevante en el desarrollo de la conducción autónoma y la industria de la automoción llegaría cuando comenzamos a poner ordenadores en los vehículos en los años 70 y 80. Estos microprocesadores o unidades de control electrónico (ECU, por sus siglas en inglés) iniciarían una profunda transformación de la industria automovilística, donde la electrónica pasaba a tener un papel predominante frente a la mecánica. Desde entonces, se han ido sucediendo una gran cantidad de innovaciones, donde la inteligencia artificial (IA) ha ido cobrando un papel protagonista. Quizá el primer ejemplo en el que la electrónica del vehículo podía percibir el mundo que le rodeaba fue el sistema de advertencia de cambio involuntario de carril, desarrollado para el Mercedes-Benz Actros a principios de la década de los 2000. Se comenzaban a desarrollar soluciones que permitían dotar de inteligencia al vehículo, mejorando la seguridad al volante. 

El factor humano, es decir, aquellos aspectos que están de mano del conductor ─conducción distraída, uso del teléfono móvil, sueño, velocidad y alcohol─ siguen estando detrás de alrededor del 90% de los siniestros, de acuerdo con la DGT. Una tecnología del vehículo que pueda “ver” a su alrededor mejor que una persona y reaccionar más rápido podría reducir significativamente estos accidentes. De hecho, expertos en seguridad vial cuantifican que los sistemas ADAS pueden salvar en España alrededor 25.000 vidas en los próximos 15 años.

Aunque parece que hay consenso en la industria de automoción en cuanto a que la tecnología podrá superar la habilidad humana para percibir, planificar y controlar la mayor parte de situaciones al volante, la IA deberá sortear algunos obstáculos en su camino hacia la conducción autónoma.

## Los retos de la Inteligencia Artificial para el desarrollo del coche autónomo
Los avances en investigación en el campo de las redes neuronales artificiales, junto con la rápida evolución del software y hardware, que permiten implementar algoritmos cada vez más complejos, están favoreciendo una aceleración en la tecnología necesaria para el desarrollo del coche autónomo. Sin embargo, quedan algunos retos por superar:

### 1. La sensorización
Para poder actuar es necesario sentir. Es decir, el sistema autónomo debe ser capaz de comprender su entorno para tomar una decisión. Los avances en la tecnología de lidar, radar, ultrasonidos y video, entre otros, están permitiendo dotar al vehículo de los datos de entrada necesarios. 

El lidar (del inglés Light Detection and Ranging) es un dispositivo de 360 grados alrededor del vehículo que continuamente dispara rayos de luz láser, midiendo el tiempo en que la luz tarda en regresar al sensor. Esto permite reconstruir el escenario de conducción mediante una nube de puntos 3D. Pese a tener un buen comportamiento tanto de día como de noche, el lidar convencional tiene algunas limitaciones: su desempeño con condiciones meteorológicas adversas (nieve, niebla, lluvia), la falta de información sobre el contraste y color de los objetos, su notable tamaño y su alto precio. El radar tradicional, por otro lado, puede ver a través de la nieve, es excelente a grandes distancias, y puede juzgar la velocidad relativa de los objetos, pero por sí solo no puede distinguir cuáles son esos objetos. Los sensores de ultrasonidos hacen un buen desempeño a la hora de detectar objetos próximos, como son maniobras de adelantamiento o aparcamiento, pero su alcance es reducido. Por último, las cámaras pueden recoger la información necesaria para detectar y clasificar peatones, otros vehículos, señales de tráfico, etc., pero las condiciones cambiantes de luz pueden afectar notablemente las detecciones.
Por ahora ningún sensor puede realizar el trabajo por sí solo, siendo necesario que trabajen conjuntamente. Esta técnica, en la que la información de múltiples sensores es necesaria para lograr la tarea en cuestión, se conoce como fusión de sensores. 

### 2. La batalla de los datos
En el desarrollo del coche autónomo será necesario recoger, almacenar, analizar e interpretar una ingente cantidad de datos al volante. Ello permitirá diseñar algoritmos que puedan reaccionar ante situaciones comunes y casos frontera, situaciones que no se dan a menudo. Sin embargo, recoger todos estos datos puede tener un alto coste para las compañías (debido a los miles de millones de kilómetros que será necesario recorrer). Complementar los datos reales con datos sintéticos, entornos de simulación fotorrealistas, puede servir para probar los sistemas autónomos en situaciones difíciles o muy costosas de reproducir.

### 3. Deep Learning
La definición de la IA acuñada en los años 50 y aún en uso es “la capacidad de una máquina para imitar el comportamiento humano inteligente”. La IA se vuelve aún más interesante cuando la máquina no sólo puede imitar, sino igualar o incluso superar el rendimiento humano, dándonos la oportunidad de que hagan trabajos más seguros y eficientes. En este sentido, hay mucho entusiasmo hoy en día sobre un tipo de aprendizaje automático llamado Deep Learning, donde se utilizan redes neuronales artificiales. Se trata de un modelo matemático, donde mediante un proceso en el que mostramos a la red diferentes experiencias o ejemplos (proceso conocido como entrenamiento), conseguimos que la red aprenda las relaciones entre, por ejemplo, la imagen que le enseñamos y el objeto en cuestión que está presente en esta imagen. 
![Efecto de un sistema basado en Deep Learning a su paso por el Paseo de la Castellana en Madrid](/assets/images/2021/ai-autonomous-driving/castellana-deep-learning.jpg)
_Efecto de un sistema basado en Deep Learning a su paso por el Paseo de la Castellana en Madrid_

De este modo, tras mostrarle una cantidad importante de experiencias, este modelo matemático habrá aprendido todas esas relaciones y lo podremos utilizar para clasificar los objetos que deseemos, como vehículos, peatones, etc. Sin embargo, estos modelos matemáticos por sí solos poco podrán hacer. Debemos poder integrarlos como parte de un sistema mayor. 

### 4. Despliegue
Automatizar los flujos de trabajo de la IA con herramientas y APIs específicas puede acelerar significativamente el desarrollo de los productos, reducir riesgos, fomentar la colaboración entre equipos y, sobre todo, mejorar los resultados finales. Estos sistemas impulsados por IA son integraciones complejas, donde serán necesarias plataformas de computación que permitan, en primer lugar, probar los modelos en simulaciones cerradas, para después desplegar los prototipos y embarcarlos en el hardware del vehículo, de cara a continuar con las pruebas. Dado que, en última instancia, será necesario integrar estos modelos de IA en el software del vehículo, disponer de la capacidad de generar automáticamente código optimizado que pueda ejecutarse sobre la plataforma hardware de destino podrá ahorrar un valioso tiempo de implementación, a la vez que reduce enormemente el error humano resultado de recodificar los algoritmos. 
Asimismo, estos modelos deberán ser refinados a medida que se recorren más y más kilómetros. Esto implica disponer de mecanismos que automaticen la recogida y preparación de los datos, el entrenamiento de los modelos, la generación de código y realización de todas las pruebas, antes de actualizar el software del vehículo, previsiblemente con una actualización OTA (del inglés Over-The-Air).

### 5. Regulación y aceptación social
Es necesario disponer de un marco regulatorio para continuar avanzando en el desarrollo de coches autónomos y que se legisle la circulación de este tipo de vehículos. En este sentido, países como China o algunos estados en Estados Unidos, llevan una notable ventaja con respecto a los países de la Unión Europea. Sin regulación y normativa, ningún vehículo que conduzca por sí solo podrá circular por la vía pública. Los retos tecnológicos discutidos en los puntos anteriores ya están siendo resueltos a distintos niveles para el desarrollo de sistemas ADAS en vehículos disponibles hoy día y para vehículos totalmente autónomos en zonas o recintos controlados. Para enfrentarse a estos retos, ingenieros de automoción utilizan MATLAB y Simulink, que les permiten avanzar rápidamente desde el prototipo al entorno de producción. A este complejo y, previsiblemente, largo proceso regulatorio, debemos añadir la aceptación social. Ya hemos reemplazado en el pasado actividades que realizábamos los humanos por una automatización en la que la máquina pasa a ser la responsable del proceso. Éste será sin duda otro cambio disruptivo, que en este caso vendrá a transformar por completo nuestra movilidad. ¿Estará la sociedad preparada para aceptar un sistema de transporte totalmente automatizado en la carretera?