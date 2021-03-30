---
layout: single
title: "Las 5 preguntas más votadas en nuestra sesión de Q&A sobre IA"
excerpt: Breve resumen y conclusiones de una sesión un tanto diferente
date:  2021-03-30 10:00:00 +0100
categories: [blog, es]
tags: [machine learning, deep learning, reinforcement learning, python, matlab]
toc: true
toc_label: En este post encontrarás

toc_sticky: true

header:
  teaser: /assets/images/2021/ask-the-experts-ai/online.jpg
  overlay_color: "#000"
  overlay_filter: "0.2"
  overlay_image: /assets/images/2021/ask-the-experts-ai/online.jpg
   caption: "Photo credit: [Chris Montgomery](https://unsplash.com/@cwmonty?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)" 

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


## ¿Que metodologías IA sirven para desarrollar un controlador en lazo cerrado, inmerso en restricciones y como implementarlas? 
<link href="/assets/css/votes.css" rel="stylesheet" />
<a class="fa fa-globe" href="#preguntas-más-votadas">
  <span class="fa fa-comment"></span>
  <span class="num">25</span>
</a>
Esta pregunta fue subiendo sus votos de modo muy constante durante el tiempo en que estuvo abierta la plataforma socialqa para el evento y ocupando en ocasiones la primera posición. 

En el desarrollo de algoritmos de control existen un amplio número de estrategias que involucran algoritmos de Inteligencia Artificial que podríamos utilizar, incluyendo técnicas de optimización clásica, algoritmos genéticos y otras heurísticas, lógica borrosa, aprendizaje automático, etc. Sin embargo, existe una aproximación que destaca sobre las demás, por ofrecer una solución para problemas extremadamente complejos, que incluyen, por ejemplo, espacios de estados continuos. Se trata del Aprendizaje por Refuerzo (en inglés, _Reinforcement Learning_).

El _Reinforcement Learning_ es un subconjunto de _Machine Learning_ en donde se trabaja con datos de un entorno dinámico. El objetivo no es agrupar o clasificar los datos, sino encontrar la mejor secuencia de acciones que genere el resultado deseado. De todas las definiciones que me he encontrado sobre _Reinforcement Learning_, la que creo que mejor explica su mecánica es la ofrecida por _Sutton_ y _Barto_ en su libro [Reinforcement Learning: An Introduction](http://incompleteideas.net/book/the-book-2nd.html):

> Reinforcement learning is learning what to do—how to map situations to actions—so as to maximize a numerical reward signal.
> 
> The learner is not told which actions to take, but instead must discover which actions yield the most reward by trying them. 

Es decir, encontrar mediante el ensayo y error, las acciones que maximizan una determinada señal de recompensa. 

Hace año y medio, [presenté](https://bit.ly/BIGTH19) en [Big Things Conference](https://www.bigthingsconference.com/) un ejemplo de cómo mediante _Reinforcement Learning_ podíamos reemplazar una estrategia de control clásica enseñar a un robot bípedo a caminar ergido en línea recta. Puedes ver la charla aquí para saber más:

{% include video id="bBnhdj9IqFg" provider="youtube" %}

## ¿Que diferencias hay entre construir modelos de IA en MATLAB y hacerlo en frameworks como MindSpore, TensorFlow o PyTorch? 
<link href="/assets/css/votes.css" rel="stylesheet" />
<a class="fa fa-globe" href="#preguntas-más-votadas">
  <span class="fa fa-comment"></span>
  <span class="num">19</span>
</a>
Esta pregunta me pareció una de las más interesantes y me resulta altamente complicado el dar una respuesta completa, vista la velocidad con la que evolucionan los _frameworks_ en _Deep Learning_ hoy en día. 

Frecuentemente me encuentro con usuarios de TensorFlow o PyTorch (no tanto de MindSpore) que desconocen los avances que han tenido lugar en MATLAB en el ámbito de _Deep Learning_. Pero con esto no quiero decir que deban reemplazar su manera de trabajar. Vayamos por partes. 

Sin lugar a duda, creo que la mayor ventaja de MATLAB para el desarrollo de proyectos en _Deep Learning_ viene dado por su flujo de trabajo:
[![Flujo de trabajo de IA](/assets/images/2021/ask-the-experts-ai/ai-workflow.png)](/assets/images/2021/ask-the-experts-ai/ai-workflow.png)

Esto nos permite no sólo desarrollar modelos de Deep Learning, sino de acompañarlos del resto de elementos que serán necesarios en flujos de trabajo de IA, como son la preparación de los datos, el etiquetado, la generación de datos sintéticos, variaciones y optimización de la arquitectura, integración con el sistema del que forma parte y el despliegue al sistema final (entorno embarcado o servidor).

Antes de entrenar cualquier modelo de _Deep Learning_, necesitaremos, si estamos construyendo un modelo de aprendizaje supervisado, realizar un adecuado etiquetado de los datos. El modelo que entrenemos podrá ser a lo sumo tan bueno como sea nuestro etiquetado, por lo que merece la pena realizar esta tarea [minuciosamente](https://elpais.com/tecnologia/2018/11/19/actualidad/1542642879_092912.html), aunque está claro, que no es la tarea más gratificante del mundo. Para ayudar esta labor, MATLAB incorpora en sus _toolboxes_ herramientas que facilitan el proceso de etiquetado de [imágenes](https://www.mathworks.com/help/vision/ug/get-started-with-the-image-labeler.html), [vídeo](https://www.mathworks.com/help/vision/ug/get-started-with-the-video-labeler.html), [señales](https://www.mathworks.com/help/signal/ug/using-signal-labeler.html), [audio](https://www.mathworks.com/help/audio/ug/audio-labeler-walkthrough.html), [Lidar](https://www.mathworks.com/help/lidar/ug/lidar-labeler-get-started.html), etc. En muchas ocasiones, necesitaremos aumentar nuestro _dataset_ de entrenamiento para mejorar la calidad de nuestro modelo. Es habitual en _Deep Learning_ utilizar técnicas de [_Data Augmentation_](https://www.mathworks.com/help/deeplearning/ug/image-augmentation-using-image-processing-toolbox.html) aplicando transformaciones invariantes a nuestros datos, así como utilizar [GANs](https://www.mathworks.com/help/deeplearning/ug/train-generative-adversarial-network.html) (_Generative Adversarial Networks_) como solución para la generación de datos sintéticos. Además de estas técnicas, es habitual encontrar equipos en ingeniería que generan datos sintéticos a partir de modelos virtuales creados en [Simulink](https://www.mathworks.com/help/driving/ug/visualize-automated-parking-valet-using-3d-simulation.html), e integrándolos, por ejemplo, con simuladores de terceros como Unreal Engine:
![Aparcamiento automático con Simulink y Unreal Engine](/assets/images/2021/ask-the-experts-ai/unreal.png)

Con la versión R2019b, MATLAB liberaba su _extended framework_ para _Deep Learning_, permitiendo crear todo tipo de redes profundas, y ampliando las posibilidades de creación de arquitecturas a cualquier tipo, incluyendo GANs, Siamese Networks o Graph Conv Networks, entre otras. El _extended framework_ ofrece mayor flexibilidad, diferenciación automática, trabajar con múltiples entradas y salidas, etc. Esto permite equiparar MATLAB con otros _frameworks_ Open-Source como TensorFlow o PyTorch, cuya evolución había sido hasta entonces más ágil. 

En el ámbito de la investigación poder reproducir un trabajo/desarrollo es clave para su éxito. Por ello, MathWorks intenta facilitar esta integración desarrollando conectores con frameworks de terceros. Hasta la fecha, existen importadores para [Caffe](https://www.mathworks.com/matlabcentral/fileexchange/61735-deep-learning-toolbox-importer-for-caffe-models), [Keras](https://www.mathworks.com/matlabcentral/fileexchange/64649-deep-learning-toolbox-converter-for-tensorflow-models), [TensorFlow](https://www.mathworks.com/matlabcentral/fileexchange/64649-deep-learning-toolbox-converter-for-tensorflow-models) (TF2) y [ONNX](https://www.mathworks.com/matlabcentral/fileexchange/67296-deep-learning-toolbox-converter-for-onnx-model-format). Asimismo, también podemos exportar modelos de MATLAB hacia estos _frameworks_. Pero en muchos casos, el interés de los usuarios no pasa por entrenar el modelo en MATLAB, sino hacerlo en el _framework_ de origen. En este caso, la conectividad de MATLAB con otros lenguajes, como se vio en la [pregunta 1](#cómo-puedo-compartir-mis-desarrollos-en-python-con-usuarios-de-matlab-y-al-revés) con el caso de Python, nos permite, por ejemplo, preparar y lanzar desde MATLAB la ejecución de un modelo de _Deep Learning_ en PyTorch o TensorFlow y recuperar los resultados de vuelta en MATLAB. 

Pero quizá uno de los aspectos más interesantes de cara a utilizar MATLAB para _Deep Learning_ venga del lado del ecosistema. Dicho modelo de _Deep Learning_, probablemente tenga que "vivir" dentro de un sistema mayor, integrado como parte de un sistema más complejo que incluya algoritmos de planificación, fusión de sensores, localización, navegación, control, etc. Es aquí donde la integración de MATLAB y Deep Learning Toolbox con Simulink es fundamental: 

[![Test bench para seguimiento de carril en autopista](/assets/images/2021/ask-the-experts-ai/lanefollowing.jpg)](/assets/images/2021/ask-the-experts-ai/lanefollowing.jpg)

Por último, una vez entrenado nuestro modelo de _Deep Learning_, debemos poder desplegarlo allí donde vaya a sernos de utilidad. Podemos necesitar llevar nuestro modelo para su ejecución en alta disponibilidad en el Cloud, o ejecutarse en sistemas embebidos, como ARMs, GPUs (familia NVIDIA Jetson) o FPGAs, para lo cual [generaremos código C/C++, CUDA o VHDL](https://www.mathworks.com/videos/deploying-deep-neural-networks-to-gpus-and-cpus-using-matlab-coder-and-gpu-coder-1567105707114.html) para su integración con el resto del proyecto.

## ¿Se puede integrar MATLAB con Jupyter notebooks?
<link href="/assets/css/votes.css" rel="stylesheet" />
<a class="fa fa-globe" href="#preguntas-más-votadas">
  <span class="fa fa-comment"></span>
  <span class="num">14</span>
</a> Sí. Pero antes de contar más detalle quisiera hacer un matiz sobre la pregunta. 

En numerosas ocasiones cuando me han hecho esta pregunta, en realidad lo que querían preguntar es si dispone MATLAB de algún tipo de solución que permita trabajar con cuadernos al estilo de Jupyter notebooks. En el entorno de MATLAB, dicha solución se llama _Live Editor_ y la verdad es que funciona a las mil maravillas. Desde [este enlace](https://www.mathworks.com/products/matlab/live-editor.html#), puedes "cacharrear" para ejecutar un cuaderno de ejemplo desde tu navegador. 

Si la pregunta, por contra, buscaba saber cómo integrar MATLAB con Jupyter, puedes ver cómo hacerlo desde los siguientes repositorios en GitHub: 
* [jupyter-matlab-proxy](https://github.com/mathworks/jupyter-matlab-proxy), permite abrir MATLAB en el navegador, directamente desde tu entorno Jupyter
* [matlab-integration-for-jupyter](https://github.com/mathworks-ref-arch/matlab-integration-for-jupyter), para ejecución de Jupyter con MATLAB, dentro de un contenedor Docker

## ¿Cómo puedo elegir el mejor modelo de Machine Learning para mis datos?
<link href="/assets/css/votes.css" rel="stylesheet" />
<a class="fa fa-globe" href="#preguntas-más-votadas">
  <span class="fa fa-comment"></span>
  <span class="num">14</span>
</a> Esta pregunta no tiene una solución cerrada, como es obvio. Un número elevado de factores pueden influir en la elección del mejor modelo en cada caso, incluyendo la precisión, explicabilidad, rendimiento, huella en memoria, etc. Voy a partir la pregunta en dos partes: 

* ¿Cómo preparar mejor los datos para la utilización de un modelo de _Machine Learning_?

  Cualquier modelo de _Machine Learning_ requerirá de datos de entrada, también conocidos como características (o en inglés, _features_). Para la obtención de dichas características, en muchas ocasiones se utiliza el conocimiento de dominio en la disciplina correspondiente, pero típicamente necesitamos un análisis posterior que nos ayude a seleccionar qué características son más adecuadas. El siguiente diagrama nos ayuda a conocer qué [técnica puede ser más apropiada en cada caso](https://www.mathworks.com/help/stats/feature-selection.html) (en función del tipo de característica):


  [![Taxonomía de la selección de características en MATLAB](/assets/images/2021/ask-the-experts-ai/features.png)](/assets/images/2021/ask-the-experts-ai/features.png)

* ¿Qué herramientas me pueden ayudar a seleccionar el mejor modelo?
  
  MATLAB dispone de varias herramientas en Statistics and Machine Learning Toolbox que facilitan el entrenamiento de modelos de [clasificación](https://www.mathworks.com/help/stats/train-classification-models-in-classification-learner-app.html) y [regresión](https://www.mathworks.com/help/stats/train-regression-models-in-regression-learner-app.html), y la consiguiente selección del modelo (ordenándolos por RSME, MSE, MAE, etc.).

  Adicionalmente, existen técnicas de _Machine Learning_ que reducen o eliminan algunas barreras relativas a los conocimientos necesarios de cara a entrenar modelos predictivos. Se trata del [AutoML](https://www.mathworks.com/help/stats/automated-classifier-selection-with-bayesian-optimization.html) (_Automated Machine Learning_). Con ello, se busca agilizar flujos de trabajo en _Machine Learning_, automatizando la selección y extracción de características, la elección, entrenamiento y optimización del modelo (fases de AutoML indicadas en gris):

  [![Agilización de los flujos de trabajo de aprendizaje automático con AutoML](/assets/images/2021/ask-the-experts-ai/automl.png)](/assets/images/2021/ask-the-experts-ai/automl.png)

  Utilizando funciones como [fitcauto](https://www.mathworks.com/help/stats/fitcauto.html) o [fitrauto](https://www.mathworks.com/help/stats/fitrauto.html) podemos elegir automáticamente el modelo de clasificación o regresión más adecuado con los hiperparámetros optimizados:

  ![Selección de modelo con AutoML](/assets/images/2021/ask-the-experts-ai/automl.gif)

Debo reconocer que disfruté de esta sesión un tanto atípica, dándole la vuelta al tablero y pidiendo a los asistentes configurar la agenda. Si asististe y/o quieres darnos algún tipo de _feedback_, es más que bienvenido :)