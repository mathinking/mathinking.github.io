---
layout: single
title: "Las 5 preguntas más votadas en nuestra sesión de Q&A sobre IA"
excerpt: Conclusiones sobre una interesante presentación
date:  2021-03-25 7:42:00 +0100
categories: [blog, es]
tags: [ia, deep learning, reinforcement learning, python, matlab]
toc: true
toc_label: En este post encontrarás
toc_sticky: true

header:
  teaser: /assets/images/2021/ask-the-experts-ai/Q&A_banner.png
  overlay_color: "#000"
  overlay_filter: "0.2"
  overlay_image: /assets/images/2021/ask-the-experts-ai/Q&A_banner.png
  
---

El pasado 10 de marzo tuve el placer de co-presentar una sesión de preguntas y respuestas con mi compañero [José Barriga](linkedin.com/in/josébarriga), ingeniero especialista en IA con amplia experiencia en Visión Artificial y Mantenimiento Predictivo. 

La sesión fue un tanto atípica, en tanto en cuanto decidimos no preparar una agenda "clásica" para el evento, partiendo de una aplicación, técnica o temática para una industria concreta. En su lugar, pedimos a los posibles asistentes que nos ayudasen a configurar la agenda en base a sus preguntas e inquietudes a la hora de acometer proyectos en Inteligencia Artificial. Se trataba de llevar el modelo de [aula invertida](https://es.wikipedia.org/wiki/Aula_invertida) a un seminario virtual. O algo similar. Para recoger las preguntas utilizamos la plataforma [socialqa](https://socialqa.com), una sencilla pero robusta plataforma online que nos permitía tanto recoger preguntas como votar por tu pregunta favorita. 

# Preguntas más votadas
En base a las preguntas introducidas a las 12h (CET) del día anterior, organizamos las preguntas y preparamos las respuestas. Decidimos no responderlas en orden de votación, para disponer de un flujo natural, si bien el objetivo era responderlas todas. Teníamos un total de 19(*) preguntas y reservadas 2 horas para la sesión. Dado que algunas preguntas eran similares, pudimos agrupar algunas para dar una respuesta que cubriera varios puntos. Con ello, nuestra intención era dedicar unos 5-10 min por pregunta, de modo que si no te interesaba alguna en particular, eran únicamente unos minutos (ver el correo, ir a por café, etc.) hasta pasar a otro tema. 

![Preguntas de la sesión de Q&A - IA](/assets/images/2021/ask-the-experts-ai/Q&A-2021-03-10.png)
_Captura de las preguntas en socialqa.com a las 12h del 9 de marzo_

A continuación, comentaré brevemente algunas de las preguntas más votadas.


## [29 votos] Cómo puedo compartir mis desarrollos en Python con usuarios de MATLAB? ¿Y al revés?
No nos sorprendió que el interés de comunicar Python con MATLAB y viceversa recibiera el mayor número de votos. 

Tanto Python como MATLAB son dos lenguajes ampliamente utilizados en el desarrollo de aplicaciones para cálculo técnico. Típicamente, el interés de comunicar ambas herramientas puede deberse a alguno de los siguientes motivos:
* Estás trabando en **Python o MATLAB** y: 
  * Quieres llamar a código existente ya desarrollado en MATLAB o Python 
  * Necesitas utilizar funcionalidad únicamente existente en MATLAB o Python

Aquí también debemos distinguir si estamos en la etapa de desarrollo, y por tanto podemos comunicar nuestro código en Python con una sesión "viva" de MATLAB o si nos encontramos en la etapa de despliegue/producción, donde utilizaremos en su lugar un runtime de MATLAB. A continuación, trataré brevemente cada una de las opciones disponibles:
### 1. Desarrollo de aplicaciones
#### 1.1. Intercambio de datos de modo asíncrono mediante ficheros Parquet
La primera manera de comunicar los dos lenguajes es bastante obvia, utilizando ficheros intermedios para almacenar y comunicar los datos entre los dos lenguajes de modo asíncrono. Un modo de hacer esto eficientemente es mediante ficheros tabulares de [Parquet](https://parquet.apache.org/), que permite trabajar con datos tabulares y explotar el ecosistema de Big Data de [Hadoop](https://hadoop.apache.org/).

![Intercambio de datos mediante Parquet](/assets/images/2021/ask-the-experts-ai/parquet.png)

``` 
% En MATLAB
parquetwrite("temperatureFitting.parquet",T)
```
{{ "{% highlight python linenos "}}%}
df = pd.read_parquet("temperatureFitting.parquet")
{{ "{% endhighlight "}}%}
```
# En Python
df = pd.read_parquet("temperatureFitting.parquet")
```

#### 1.2. Llamar a Python desde MATLAB
En primer lugar debemos asegurarnos que MATLAB es capaz de reconocer la instalación de Python. Para ello basta con ejecutar [pyenv](https://www.mathworks.com/help/matlab/ref/pyenv.html):  
```
% En MATLAB
pyenv()
ans = 
  PythonEnvironment with properties:

          Version: "3.7"
       Executable: "C:\anaconda3\python.EXE"
          Library: "C:\anaconda3\python37.dll"
             Home: "C:\anaconda3"
           Status: Loaded
    ExecutionMode: InProcess
        ProcessID: "2680"
      ProcessName: "MATLAB"
```
En versiones anteriores a MATLAB R2019b, habría que utilizar pyversion en su lugar. 

Hacer una llamada a Python desde MATLAB no podía ser más fácil. Simplemente basta con escribir `py.` como prefijo para acceder a cualquier biblioteca de Python y a partir de aquí ya operar como es habitual:
```
% En MATLAB
>> py.math.sqrt(42)
ans =
    6.4807
```
Sin embargo, para quién utilice habitual de Python, y trabaje con alias:
```
>>> import math as mm
```
quizá prefiera escribir:
```
% En MATLAB
>> mm = py.importlib.import_module('math');
```
donde en ambos casos podremos llamar a la función del mismo modo `mm.sqrt(42)`.

Con este mismo procedimiento podemos llamar a cualquier paquete o módulo en Python (propio o no). El principal escollo que nos podemos encontrar en adelante es relativo a la [conversión de tipos](https://www.mathworks.com/help/matlab/matlab_external/passing-data-to-python.html), que debemos tener siempre presente.

### 2. Despliegue de aplicaciones

## [25 votos] ¿Que metodologías IA sirven para desarrollar un controlador en lazo cerrado, inmerso en restricciones y como implementarlas? 

## [19 votos] ¿Que diferencias hay entre construir modelos de IA en Matlab y hacerlo en frameworks como Mindspore, Tensorflow o Pytorch? 

## [14 votos] ¿Se puede integrar MATLAB con Jupyter notebooks? 14 votes

## [14 votos] ¿Cómo puedo elegir el mejor modelo de machine learning para mis datos? 16 votes

(*) _Inevitablemente pasadas las 12h y hasta el comienzo de la sesión, entraron más preguntas, que respondimos sobre la marcha al finalizar la sesión_