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

__Class__
######
Nos permiten ejecutar, controlar y contruir la interfaz. Las usadas en el código son:

######
      QApplication()
######
Administra la configuración principal y el flujo de control de una aplicación GUI. Contiene un bucle de eventos principal dentro del cual los eventos generados por elementos de ventana y otras fuentes se procesan y envían. También maneja configuraciones de todo el sistema y de toda la aplicación.

######
      QMainWindow()
######
Qt tiene QMainWindow y sus clases relacionadas para la gestión de la ventana principal. QMainWindow tiene su propio diseño al que puede agregar QToolBars, QDockWidgets, QMenuBar y QStatusBar. El diseño tiene un área central que puede ser ocupada por cualquier tipo de widget, como se ve a continuación.

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/ca638833-7d39-42db-953f-9de63ad3845a)

######
      QWidget()
######
Derivada de las clases QObject y QPaintDevice es la clase base para todos los objetos de la interfaz de usuario.

######
      QVBoxLayout()
######
La clase QBoxLayout alinea los widgets vertical u horizontalmente. Una de sus clases derivadas es QVBoxLayout (para organizar widgets verticalmente).

######
      QFormLayout()
######
Es una forma conveniente de crear un formulario de dos columnas, donde cada fila consta de un campo de entrada asociado con una etiqueta. Como convención, la columna de la izquierda contiene la etiqueta y la columna de la derecha contiene un campo de entrada.

__Widgets__
######

Los widgets son los elementos principales para crear interfaces de usuario en Qt. Pueden mostrar datos e información de estado, recibir información del usuario y proporcionar un contenedor para otros widgets que deben agruparse. Un widget que no está incrustado en un widget principal se denomina ventana.

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/52605366-0d5f-45d1-ba32-2b878b6892a0)

Los utilizados en el código son
######
      QLabel()
######
Un objeto QLabel actúa como un marcador de posición para mostrar texto o imagen no editable, o una película de GIF animado. También se puede utilizar como clave mnemotécnica para otros widgets.

######
      QPushButton()
######
Un botón de comando para invocar la acción

######
      QDial()
######
El objeto de clase QDial presenta al usuario un disco rotatorio sobre el que se puede mover un circulo a su alrededor. Es un widget clásico para controlar un valor acotado.

######
      QLineEdit()
######
El objeto QLineEdit es el campo de entrada más utilizado. Proporciona un cuadro en el que se puede ingresar una línea de texto. Para ingresar texto de varias líneas, se requiere el objeto QTextEdit.

Para más información sobre QtWidgets visite [Qt Widgets 5.15](https://doc.qt.io/qt-5/qtwidgets-index.html). Para leer la información sobre los widgets acceda al apartado <All Qt C++ Classes>.

##### QtCore
Qt Core agrega estas características a C++:

- Un mecanismo muy poderoso para la comunicación fluida de objetos llamado signals y slots.
- Propiedades de objetos consultables y diseñables.
- Árboles de objetos jerárquicos y consultables que organizan.
- Propiedad de objetos de forma natural con punteros protegidos (QPointer).
- Un elenco dinámico que funciona más allá de los límites de la biblioteca.

Para más información viste [QtCore](https://doc.qt.io/qt-5/qtcore-index.html).

##### QtGui
El módulo Qt GUI proporciona clases para la integración del sistema de ventanas, el manejo de eventos, la integración de OpenGL y OpenGL ES, gráficos 2D, imágenes básicas, fuentes y texto. Estas clases son utilizadas internamente por las tecnologías de interfaz de usuario de Qt.

De este modulo se utilizan las siguientes clases.

###### QIcon
Un QIcon puede generar mapas de píxeles más pequeños, más grandes, activos y deshabilitados a partir del conjunto de mapas de píxeles que se le proporcionan. Estos mapas de píxeles son utilizados por los widgets de Qt para mostrar un icono que representa una acción en particular.

Para más información visite [QPixmap](https://doc.qt.io/qt-5/qicon.html).

###### QPixmap
QPixmap está diseñado y optimizado para mostrar imágenes en pantalla. Un QPixmap se puede mostrar fácilmente en la pantalla usando QLabel o una de las subclases de QAbstractButton (como QPushButton y QToolButton). QLabel tiene una propiedad de mapa de píxeles, mientras que QAbstractButton tiene una propiedad de icono.

Para más información visite [QPixmap](https://doc.qt.io/qt-5/qpixmap.html).

###### QImage
La clase QImage proporciona una representación de imagen independiente del hardware que permite el acceso directo a los datos de píxeles y se puede utilizar como paint device.

Para más información visite [QImage](https://doc.qt.io/qt-5/qimage.html).

### Formato .tiff en las imágenes

El formato TIFF es un formato de gráficos antiguo que permite almacenar imágenes de mapas de bits (raster) muy grandes (más de 4 GB comprimidos) sin pérdida de calidad y sin considerar las plataformas o periféricos utilizados (mapa de bits independiente del dispositivo, conocido como DIB). Permite almacenar imágenes en blanco y negro, en colores verdaderos (hasta 32 bits por píxel) y también indexar imágenes utilizando una paleta. Además de esto, el formato TIF permite que se utilicen varios espacios de color: RGB (rojo, verde, azul), CMYK (cian, magenta, amarillo, negro), CIE L*a*b, YUV/YcrCb.

El principio del formato TIF consiste en definir etiquetas (de ahí el nombre formato de archivo de imágenes con etiquetas) que describen las características de la imagen. Las etiquetas permiten almacenar información acerca de las dimensiones de la imagen, la cantidad de colores utilizados, el tipo de compresión (pueden utilizarse varios algoritmos: paquete de bits/CCITT G3y4/RLE/JPEG/LZW/UIT-T) o la corrección de gama.

Por lo tanto, una descripción de imagen que utiliza etiquetas simplifica la programación del software permitiendo guardar información en formato TIF. Por otro lado, la cantidad de opciones es tan amplia que muchos editores de imágenes que admiten el formato TIF no las integran todas. Por ende, algunas veces, una imagen guardada que utiliza el formato TIF no se puede leer por medio de otro editor.

La última revisión del formato es la número 6, del año 1992. Hay algunas extensiones, como las anotaciones que utiliza el Imaging de Microsoft, pero ninguna puede considerarse estándar.

## Métodos

### Filtro: Rotación

Antes de explicar el filtro es importante abordar la definición de _transformación afín_. Una transformación afín $f: A \rightarrow A'$ entre dos espacios afines $(A,E,\gamma)$ y $(A',E',\gamma')$; donde $A$ y $A'$ son subconjuntos no vacíos asociados a los espacios vectoriales $E$ y $E'$, con $\gamma$ y $\gamma'$ el conjunto de todas las traslaciones definidas sobre $A$ y $A'$, respectivamente; es una aplicación sobre los puntos que actúa linealmente sobre los vectores que los unen. Formalmente, $f$ es una transformación afín si existe una aplicación lineal $g$ tal que $\forall p,q \in A$, se cumple $$\vec{{f(p)f(q)}} = g(\vec{{pq}}).$$

En otras palabras, una transformación afín o aplicación afín (también llamada afinidad) entre dos espacios afines consiste en una transformación lineal seguida de una traslación:
$$x \rightarrow Ax+b$$ En el caso de dimensión finita, toda transformación afín puede representarse por una matriz $A$ y un vector $b$ que satisfacen ciertas propiedades.

Geométricamente, una transformación afín en un espacio euclídeo es una transformación que preserva:
- Las relaciones de colinealidad (y coplanaridad) entre puntos, es decir, puntos que recaían sobre una misma línea (o sobre un mismo plano) antes de la transformación, son preservadas tras una transformación afín.
- Las razones entre distancias a lo largo de una línea antes y después de la transformación son iguales.

En el ámbito del procesamiento digital de imágenes, las transformaciones afines son análogas a imprimir en una hoja de goma y estirar los bordes de forma paralela al plano. Esta transformación reubica los píxeles que requieren interpolación de intensidad para aproximar el valor de los píxeles desplazados; la interpolación bicúbica es el estándar para hacer las transformaciones de imágenes en las aplicaciones de procesamiento de la imagen. 

La forma habitual de representar una transformación afín, como parte del proceso de filtrado, es mediante una matriz $2 \times 3$, como se muestra a continuación.

$$ A = \begin{pmatrix}
a_{00} & a_{01} \\
a_{10} & a_{11}
\end{pmatrix},  \qquad b = \begin{pmatrix}
b_{00} \\
b_{10}
\end{pmatrix},$$

$$ M = \begin{bmatrix}
A & b 
\end{bmatrix} =  \begin{pmatrix}
a_{00} & a_{01} & b_{00}\\
a_{10} & a_{11} & b_{01}
\end{pmatrix}$$

Así, para cualquier vector que indique la posición del pixel en la imagen, $ X = \begin{bmatrix}
x \\
y
\end{bmatrix} $, se convertirá bajo la transformación afín a 

$$ T = M \cdot \begin{bmatrix}
x & y \\
\end{bmatrix}^T =
\begin{bmatrix}
a_{00}x + a_{01}y + b_{00}\\
a_{10}x + a_{11}y + b_{01}
\end{bmatrix}.$$

Una de dichas transformaciones es _rotación_. En matemáticas, la rotación es un concepto que tiene su origen en la geometría. Cualquier rotación es un movimiento definido en un determinado espacio que conserva al menos un punto en su posición original. Su matriz asociada recibe el nombre de _matriz de rotación_. No obstante, matriz de rotación en matemáticas difiere en cierto sentido de la utilizada en el procesamiento de imagenes digitales. La matriz de rotación que corresponde a este filtrado es la indicada con anterioridad en Materiales/OpenCV/cv2 justo en la función que ejecuta la transformación.

$$ M = \begin{pmatrix}
\alpha & &\beta & &(1- \alpha) c_x - \beta c_y\\
& & & & \\
-\beta & &\alpha & &\beta c_x + (1- \alpha) c_y
\end{pmatrix} $$

donde
- $\alpha = scale \cdot \cos\theta$.
- $\beta = scale \cdot \sin\theta$.
- $c_x$ y $cy$ son las coordenadas del centro de la imagen.

Por lo que, dado el vector $ X = \begin{bmatrix}
x \\
y
\end{bmatrix} $, se convertirá bajo la transformación afín rotación en 

$$ T = M \cdot \begin{bmatrix}
x & y \\
\end{bmatrix}^T =
\begin{bmatrix}
\alpha x + \beta y + (1- \alpha) c_x - \beta c_y\\
& & & & \\
-\beta x + \alpha  y + \beta c_x + (1- \alpha) c_y
\end{bmatrix}.$$

### Descripción del código
En él se observa la clase "GraphicalInterfaceWindow" en donde se define el constructor, la función "setup_ui" que contendrá las configuraciones de los atributos declarados en el constructor (los widgets y layouts), la función "DialValue" que permitirá al usuario visualizar el ángulo de rotación en un QLineEdit no editable (esto gracias a la función .setDisable(True), que desabilitará poderse editar en la interfaz), la función "UploadImage" que permitirá cargar la imagen a la ventana y finalmente la función "RotateImage" que rotará a la imagen de acuerdo a los valores del QDial. Las funciones "DialValue" y "RotateImage" estarán conectadas al QDial por medio de la función, ya establecida en la documentación, .valueChanged. Por otra parte, la función "UploadImage" está conectada a un QPushButton por medio de .clicked.

### Mockup

Para la creación de nuestra interfaz gráfica se creó un mockup (bosquejo) que nos permitirá delimitar los Widgets y layouts a utilizar:

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/cab7d555-c972-418a-9904-daf9674ad26b)

La siguiente imagen presenta la posición visual los widgets en la interfaz:

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/1053be1f-ae21-4b2a-829c-1f74612e2509)

Por último, esta imagen presenta la disposición de los layouts que contrendrán a los widgets.

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/cca01c81-ab68-4ad9-88bb-00fe397c7435)

## Resultados
Finalmente, la interfaz gráfica terminada:

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/41242178-fbfc-4107-9831-876217e8b5e5)


Al cargar la imagen, la interfaz se visualiza de la siguiente manera:

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/c9117922-79c4-4905-9e88-4f6de6194ac6)


Al posicionar el disco rotatorio a $90$, es decir al indicarle a la computadora que $\theta = 90°$:

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/3f4cfd7c-c9bf-4349-ab26-8566c5f27120)


Notemos que podemos cambiar el valor del ángulo tantas veces queramos, en la siguiente imagen se muestra la imagen presentada al cambiar el ángulo a $\theta =  200°$:

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/ae05fd6d-0e21-407b-9d8e-1cf30bf8c967)


Incluso, podemos subir otra imagen y aplicarle el filtro:

![image](https://github.com/SofiaMendH/Interfaz_grafica/assets/97262885/9dbb822f-7ec7-4048-acf9-7509146f916e)






