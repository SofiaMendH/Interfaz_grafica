# Interfaz gráfica
## Introducción
El ser humano ha estado tratando, durante aproximadamente 60 años, de desarrollar formas para que las máquinas vean y comprendan datos visuales, como lo son las imagenes. La _visión por computadora_; también conocida como _visión artificial_, _visión informática_ o _visión técnica_; es una disciplina científica que incluye métodos para adquirir, procesar, analizar y comprender las imágenes del mundo real con el fin de producir información numérica o simbólica para que puedan ser tratados por un ordenador.

Una imagen puede ser definida como una función de dos dimensiones $f(x,y)$ donde $x$ y $y$ son las coordenadas espaciales (plano) y la amplitud de la función $f$ en algún par de coordenadas $(x,y)$ es llamada intensidad o nivel de gris de la imagen en ese punto. Cuando $x$ y $y$, los valores de la amplitud de la función _f_, son cantidades discretas finitas,
a dicha imagen se le llama _imagen digital_, la cual está compuesta de un número finito de elementos y cada uno tiene una localidad y valor particulares. A éstos elementos se les llama _elementos de la imagen_ o _pixels_; siendo este último el término más usado para denotar los elementos de una imagen digital.

Por medio de la visión por computadora, se puede realizar un procesamiento de imágenes digitales, un conjunto de técnicas que se aplican a las imágenes digitales con el objetivo de mejorar la calidad o facilitar la búsqueda de información. Entre dichas técnicas se halla el _proceso de filtrado_, que es el conjunto de técnicas englobadas dentro del preprocesamiento de imágenes cuyo objetivo fundamental es obtener, a partir de una imagen origen, otra final cuyo resultado sea más adecuado para una aplicación específica, mejorando ciertas características de la misma que posibilite efectuar operaciones del procesado sobre ella. Para poder llevar a cabo dicho proceso se efectúan operaciones _filtro_ a los píxeles de una imagen digital para optimizarla, enfatizar cierta información o conseguir un efecto especial en ella.

Aún cuando las computadoras sean capaces de analizar y procesar imagenes con ciertos algoritmos, no son capaces de decidir por cuenta propia a qué imagen debería aplicarle algún filtro, ni mucho menos la razón de dicha decisión. Es por ello que las interfaces gráficas son de gran importancia.

Una _interfaz gráfica_ de usuario, conocida también como _GUI_ (del inglés _graphical user interface_), utiliza imágenes, iconos y menús para mostrar las acciones disponibles en un dispositivo, entre las que el usuario puede escoger una o varias. Estas incluyen elementos como menús, ventanas, contenido gráfico, cursor, los beeps y algunos otros sonidos que la computadora hace, y en general, todos aquellos canales por los cuales se permite la comunicación entre el ser humano y la computadora.

A continuación se presentará un código en _Python_ de una interfaz gráfica cuyo objetivo es efectuar un proceso de filtrado, _rotación_, en una imagen con formato .tiff.

## Materiales
### Pyhton
Para la realización del código se ha utilizado como lenguaje de programación a _Python_, el cual es un lenguaje de alto nivel de programación interpretado cuya filosofía hace hincapié en una sintaxis muy limpia y un código legible. 

Es un lenguaje dinámico (_el programa se ejecuta de forma inmediata mientras sea sintácticamente corecto_) y multiplataforma. 

Se trata de un lenguaje de programación multiparadigma, ya que soporta parcialmente la programación:
- _Orientada a objetos:_ Se basa en la definición y uso de objetos generados por clases.
- _Imperativa:_ El programa se representa como órdenes dadas a la computadora
- _Funcional:_ Resulta de la programación declarativa, en la cual se le da a la computadora declaraciones que se usan para llegar a la solución. Este tipo lo acepta en menor medida.

Para más información visite [Python](https://www.python.org/).

#### Spyder IDE
Como entorno se ha utilizado a Spyder de Anaconda, el cual es un potente entorno científico escrito en Python, para Python, y diseñado por y para científicos, ingenieros y analistas de datos. Ofrece una combinación única de la funcionalidad avanzada de edición, análisis, depuración y creación de perfiles de una herramienta de desarrollo integral con la exploración de datos, la ejecución interactiva, la inspección profunda y las hermosas capacidades de visualización de un paquete científico.

Para más información visite [spyder](https://pypi.org/project/spyder/).

### Bibliotecas usadas de Python
#### OpenCV
OpenCV es una biblioteca libre de visión artificial originalmente desarrollada por Intel. OpenCV significa Open Computer Vision (Visión Artificial Abierta). Desde que apareció su primera versión alfa en el mes de enero de 1999, se ha utilizado en una gran cantidad de aplicaciones, y hasta 2020 se la sigue mencionando como la biblioteca más popular de visión artificial. Su popularidad se debe a que es:
- _Libre_, publicada bajo licencia BSD, para propósitos comerciales y de investigación.
- _Multiplataforma_, para los sistemas operativos GNU/Linux, Mac OS X, Windows y Android, y para diversas arquitecturas de hardware como x86, x64 (PC), ARM (celulares y Raspberry Pi).
- _Documentada y explicada_, la organización tiene una preocupación activa de mantener la documentación de referencia para desarrolladores lo más completa y actualizada posible. Viste [Documentación principal, referencias y tutoriales](https://docs.opencv.org/4.x/).

OpenCV está totalmente desarrollado en C++, orientado a objetos y con alta eficiencia computacional. Su API es C++ pero incluye conectores para Python.

#### cv2
El módulo cv2 es el módulo principal de OpenCV, que proporciona a los desarrolladores una interfaz fácil de usar para trabajar con capacidades de procesamiento de imágenes y vídeo.

De este módulo utilizaremos las siguientes funciones:

#####
      cv2.imread(img)
#####
Es una función para leer una imagen de un archivo. Toma la ruta del archivo como entrada y devuelve una matriz Numpy que contiene la imagen. Si la imagen no se puede leer (debido a que falta el archivo, permisos incorrectos o formato no compatible o no válido), este método devuelve una matriz vacía.

#####
      cv2.getRotationMatrix2D(center,angle,scale)
#####
Se utiliza para hacer la matriz de transformación $M$ que se utilizará para rotar una imagen. Los parámetros son:
- _center:_ Centro de rotación.
- _angle(_ $\theta$ _):_ Ángulo de rotación. El ángulo es positivo para el sentido contrario a las agujas del reloj y negativo para el sentido de las agujas del reloj.
- _scale:_ Factor que escala la imagen.
Dicha función retorna la matriz $2 \times 3$:

$$ M = \begin{pmatrix}
\alpha & &\beta & &(1- \alpha) c_x - \beta c_y\\
& & & & \\
-\beta & &\alpha & &\beta c_x + (1- \alpha) c_y
\end{pmatrix} $$

donde
- $\alpha = scale \cdot \cos\theta$.
- $\beta = scale \cdot \sin\theta$.
- $c_x$ y $cy$ son las coordenadas del centro de la imagen.

#####
      cv2.warpAffine()
#####
OpenCV proporciona una función cv2.getAffineTransform() que toma la matriz _M_ de transformación anterior como parámetro y retorna la imagen rotada.

####  PYQT5
Qt es un framework multiplataforma orientado a objetos ampliamente usado para desarrollar programas (software) que utilicen interfaz gráfica de usuario. Qt utiliza el lenguaje de programación C++ de forma nativa, adicionalmente puede ser utilizado en varios otros lenguajes de programación a través de bindings.

_PyQt_ es un binding de la biblioteca gráfica Qt para el lenguaje de programación Python. La biblioteca está desarrollada por la firma británica Riverbank Computing y está disponible para Windows, GNU/Linux y Mac OS X bajo diferentes licencias.

PyQt5 es un conjunto completo de enlaces de Python para Qt v5. Se implementa como más de 35 módulos de extensión y puede integrarse en aplicaciones basadas en C++ para permitir a los usuarios configurar o mejorar la funcionalidad de las aplicaciones.

Para mas información visite [PyQt5-PyPI](https://pypi.org/project/PyQt5/).

##### QtWidgets
El módulo QtWidgets proporciona un conjunto de elementos de interfaz de usuario para crear interfaces de usuario clásicas de estilo de escritorio.

###### Widgets
Los widgets son los elementos principales para crear interfaces de usuario en Qt. Pueden mostrar datos e información de estado, recibir información del usuario y proporcionar un contenedor para otros widgets que deben agruparse. Un widget que no está incrustado en un widget principal se denomina ventana.

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/52605366-0d5f-45d1-ba32-2b878b6892a0)

Los utilizados en el código son:




##### QtCore
##### QtGui

### Formato .tiff en las imágenes

## Métodos

### Descripción del método

### Mockup

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/cab7d555-c972-418a-9904-daf9674ad26b)

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/1053be1f-ae21-4b2a-829c-1f74612e2509)

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/cca01c81-ab68-4ad9-88bb-00fe397c7435)

## Resultados

