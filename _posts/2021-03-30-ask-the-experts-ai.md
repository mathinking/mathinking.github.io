---
layout: single
title: "Las 5 preguntas más votadas en nuestra sesión de Q&A sobre IA"
excerpt: Breve resumen y conclusiones de una sesión un tanto diferente
date:  2021-03-30 10:00:00 +0100
categories: [blog, es]
tags: [ia, deep learning, reinforcement learning, python, matlab]
toc: true
toc_label: En este post encontrarás
toc_sticky: true

header:
  teaser: /assets/images/2021/ai-autonomous-driving/highway.jpg
  overlay_color: "#000"
  overlay_filter: "0.2"
  overlay_image: /assets/images/2021/ai-autonomous-driving/highway.jpg
  
---

El pasado 10 de marzo tuve el placer de co-presentar una sesión de preguntas y respuestas con mi compañero [José Barriga](linkedin.com/in/josébarriga), ingeniero especialista en IA con amplia experiencia en Visión Artificial y Mantenimiento Predictivo. 

La sesión fue un tanto atípica, en tanto en cuanto decidimos no preparar una agenda "clásica" para el evento, partiendo de una aplicación, técnica o temática para una industria concreta. En su lugar, pedimos a los posibles asistentes que nos ayudasen a configurar la agenda en base a sus preguntas e inquietudes a la hora de acometer proyectos en Inteligencia Artificial. Se trataba de llevar el modelo de [aula invertida](https://es.wikipedia.org/wiki/Aula_invertida) a un seminario virtual. O algo similar. Para recoger las preguntas utilizamos la plataforma [socialqa](https://socialqa.com), una sencilla pero robusta plataforma online que nos permitía tanto recoger preguntas como votar por tu pregunta favorita. 

# Preguntas más votadas
En base a las preguntas introducidas a las 12h (CET) del día anterior, organizamos las preguntas y preparamos las respuestas. Decidimos no responderlas en orden de votación, para disponer de un flujo natural, si bien el objetivo era responderlas todas. Teníamos un total de 19(*) preguntas y reservadas 2 horas para la sesión. Dado que algunas preguntas eran similares, pudimos agrupar algunas para dar una respuesta que cubriera varios puntos. Con ello, nuestra intención era dedicar unos 5-10 min por pregunta (o agrupación de preguntas), de modo que, si no te interesaba alguna en particular, eran únicamente unos minutos (ver el correo, ir a por café, etc.) hasta pasar a otro tema. 

[![Preguntas de la sesión de Q&A - IA](/assets/images/2021/ask-the-experts-ai/Q&A-2021-03-10.png)](/assets/images/2021/ask-the-experts-ai/Q&A-2021-03-10.png)
_Preguntas recibidas en socialqa.com a las 12h del 9 de marzo_

(*) _Inevitablemente pasadas las 12h y hasta el comienzo de la sesión, entraron más preguntas, que respondimos sobre la marcha al finalizar la sesión_

A continuación, comentaré brevemente las 5 preguntas más votadas.

## Cómo puedo compartir mis desarrollos en Python con usuarios de MATLAB? ¿Y al revés?

<link href="/assets/css/votes.css" rel="stylesheet"/>
<a class="fa fa-globe" href="#preguntas-más-votadas">
  <span class="fa fa-comment"></span>
  <span class="num">29</span>
</a>
No nos sorprendió que el interés de comunicar Python con MATLAB y viceversa recibiera el mayor número de votos. 

Tanto Python como MATLAB son dos lenguajes ampliamente utilizados en el desarrollo de aplicaciones para cálculo técnico. Típicamente, el interés de comunicar ambas herramientas puede deberse a que estás trabajando en **Python** (o **MATLAB**) y: 
* Quieres llamar a código existente ya desarrollado en MATLAB (o Python)
* Necesitas utilizar funcionalidad únicamente existente en MATLAB (o Python)

Debemos distinguir si estamos en la etapa de desarrollo, y por tanto podemos comunicar nuestro código en Python con una sesión "viva" de MATLAB o si nos encontramos en la etapa de despliegue/producción, donde utilizaremos en su lugar un runtime de MATLAB. A continuación, trataré brevemente cada una de las opciones disponibles:

### 1. Desarrollo de aplicaciones
#### 1.1. Intercambio de datos de modo asíncrono mediante ficheros Parquet
La primera manera de comunicar los dos lenguajes es bastante obvia, utilizando ficheros intermedios para almacenar y comunicar los datos entre los dos lenguajes de modo asíncrono. Un modo de hacer esto eficientemente es mediante ficheros tabulares de [Parquet](https://parquet.apache.org/), permitiendo explotar el ecosistema de Big Data de [Hadoop](https://hadoop.apache.org/).

![Intercambio de datos mediante Parquet](/assets/images/2021/ask-the-experts-ai/parquet.png)

```
MATLAB:
  >> parquetwrite("temperatureFitting.parquet",T)
```

```
Python:
  >>> df = pd.read_parquet("temperatureFitting.parquet")
```

#### 1.2. Llamar a Python desde MATLAB
En primer lugar, debemos asegurarnos que MATLAB es capaz de reconocer la instalación de Python. Para ello basta con ejecutar [pyenv](https://www.mathworks.com/help/matlab/ref/pyenv.html):  

```
MATLAB:
  >> pyenv()
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
En versiones anteriores a MATLAB R2019b, habría que utilizar `pyversion` en su lugar. 

Hacer una llamada a Python desde MATLAB no podía ser más fácil. Simplemente basta con escribir `py.` como prefijo para acceder a cualquier biblioteca de Python y a partir de aquí ya operar como es habitual:

``` 
MATLAB:
  >> py.math.sqrt(42)
  ans =
      6.4807
```
Sin embargo, para quién utilice habitualmente Python, y trabaje con alias:

```
Python:
  >>> import math as mm
```

quizá prefiera escribir:

```
MATLAB:
  >> mm = py.importlib.import_module('math');
```

donde en ambos casos podremos llamar a la función del mismo modo `mm.sqrt(42)`.

Con este mismo procedimiento podemos llamar a cualquier paquete o módulo en Python (propio o no). El principal escollo que nos podemos encontrar en adelante es relativo a la [conversión de tipos](https://www.mathworks.com/help/matlab/matlab_external/passing-data-to-python.html), que debemos tener siempre presente.

#### 1.3. Llamar a MATLAB desde Python
En esta ocasión, querremos llamar a MATLAB desde nuestro entorno Python preferido (en mi caso sería VS Code). Para ello debemos previamente [instalar](https://www.mathworks.com/help/matlab/matlab_external/install-the-matlab-engine-for-python.html) MATLAB Engine, que nos permitirá, mediante el uso de una API, hacer llamadas de Python a MATLAB. 

Una vez instalado, utilizarlo es tremendamente sencillo:

``` 
Python:
  >>> import matlab.engine as mleng
  >>> eng = mleng.start_matlab()
  >>> x = eng.sqrt(42.0)
  >>> print(x)
  6.48074069840786
  >>> eng.exit()
```

### 2. Despliegue de aplicaciones
A la hora de empaquetar desarrollos realizados en MATLAB y llevarlos a Python, existen varias posibilidades dependiendo de las necesidades del proyecto. 

#### 2.1 Empaquetar la aplicación como un paquete para Python
En la [sección 1.3](#13-llamar-a-matlab-desde-python), veíamos cómo llamar a una sesión "viva" de MATLAB desde Python a través de la API de MATLAB Engine para Python. En esta ocasión, reemplazaremos el uso de la API por una llamada a una biblioteca de Python, donde las funciones han sido desarrolladas en MATLAB y empaquetadas mediante [MATLAB Compiler SDK](https://www.mathworks.com/products/matlab-compiler-sdk.html). 

Aclarar un punto importante: MATLAB Compiler SDK no "convierte" el código MATLAB a Python, sino que crea un _wrapper_ sobre un fichero CTF (fichero con el código MATLAB cifrado) para que pueda ser llamado fácilmente desde Python. En el momento de realizar las llamadas a las funciones de dicho paquete, éstas se realizan sobre un runtime de MATLAB que hemos de instalar previamente. Instalado el runtime y la librería, el procedimiento para llamar a las funciones que hayamos decidido exponer sería:

```
Python
  >>> import <mypackage>
  >>> pkg = <mypackage>.initialize()
  >>> result = pkg.<myfunction>(<arg1>, ..., <argn>)
  >>> pkg.terminate()
```
de modo que el uso de MATLAB Engine es reemplazado por el uso de MATLAB Runtime y el paquete Python creado.

#### 2.2 Desplegar la aplicación como un componente para un servidor de aplicaciones MATLAB
He de reconocer que éste es mi modo preferido de comunicar Python con MATLAB, especialmente a la hora de llevar los desarrollos a producción. Es posible crear tu propio servidor de aplicaciones con MATLAB, aunque si no quieres complicarte la vida, [MATLAB Production Server](https://www.mathworks.com/products/matlab-production-server.html) tiene todo lo que necesitas, y más. Se trata de un servidor de aplicaciones que operacionaliza tus modelos y/o algoritmos como APIs de modo que se integren con los sistemas IT/OT de tu organización. 

Dispone de clientes ligeros para diferentes lenguajes de programación como C#, Java, C/C++ o Python. Pero lo más interesante bajo mi punto de vista es el poder invocar a las funciones mediante una API RESTful a través de _payloads_ en JSON para manejar la entrada y la salida. 

[![Llamada a MATLAB Production Server vía API RESTful](/assets/images/2021/ask-the-experts-ai/postman-mps-small.png)](/assets/images/2021/ask-the-experts-ai/postman-mps.gif)

Si quieres saber más sobre la conexión entre MATLAB y Python, puedes echar un vistazo a este [webinar](https://www.mathworks.com/videos/matlab-and-python-connected--1614871666603.html) o revivir el [directo](https://www.youtube.com/watch?v=RlMgQDvvAFQ) de los brillantes [Heather Gorr](https://twitter.com/HeatherGorr) y [Yann Debray](https://www.linkedin.com/in/yann-debray-70305026).