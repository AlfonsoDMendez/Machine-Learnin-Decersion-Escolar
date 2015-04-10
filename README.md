# Machine-Learnin-Decersion-Escolar
pagina de prueba para prediccion de decersion escolar


Universidad politécnica de Tlaxcala
Ingeniería en tecnologías de la información
Minería de datos
Integración de tecnologías machine-learning y web
Profesor:
Pedro Aarón Hernández Avalos
Alumnos	NL
Alfonso de Jesús Mendéz Torres	13
Leonel Hernández Sánchez	10
Dalia Andrea Camacho Plata	2
Brian Iván Rosas Rodríguez	22
Roberto Carlos Cuatepotzo Domínguez	4


Grado: “8”	Grupo: “E”
Fecha: 10/04/15
Introducción
Como es bien sabido la implementación de tecnologías no es tarea sencilla así que se proponen ideas en clase para poder crear una implementación de machine-learning y tecnologías web para poder crear una página que determine el riesgo en algún alumno de sufrir deserción.
Para este plano las tecnologías con las que contamos y el modelado que se pretende hacer es básico a donde podremos experimentar con las librerías de machine-learning.
Estas librerías poseen métodos clasificación, predicción, que nos permitirán crear la página.
Teniendo en cuenta esto se planteó desde inicio del curso detallar y estudia cada uno de estos métodos vistos en clase algunos de ellos son:
Naibe Bayes (redes bayesianas)
K-means (clustering)
KNN (K-nearest neighbors).







En medida y con respecto al análisis se optó por ocupar las librerías de Weka y acoplarlas con lenguaje PHP, de lo cual encontramos manuales que permitían el manejo de los mismos, solo que tenían un inconveniente estas librerías estaban desactualizadas y como tal las nuevas versiones de java no eran soportadas, a tal grado que en la documentación de PHP se retiraron.
Como segunda opción se optó la utilización de Python con algo denominado python-weka-wrapper 0.2.2, el cual disponía del soporte para la creación de aplicaciones con las librerías de Weka, pero existía un inconveniente el servidor para su desarrollo no permita la compatibilidad por completo de las librerías dejando de lado este problema nos topamos con otro obstáculo el cual era el Framework de desarrollo el cual es Django que es exclusivo para el diseño de aplicaciones web.
Django como tal es escalable pero al implementarlo con las librerías de Weka no reconocía todas las funcionalidades, creando conflicto con el modelado de la página, no permitiendo que esta trabajara de manera adecuada, haciendo que cada vez que implementáramos algún cambio se crearan nuevos proyectos, quitando tiempo y esfuerzo.
Por último se decidió deja de lado a Weka y se encontraron alternativas para cumplir con el objetivo deseado entre las cuales encontramos a las librerías que mencionaremos en esta instancia.
Phyton
Para Python existen dos librerías conocidas las cuales son:
•	scikit-learn
•	pybrain
Las cuales tienen una gran ventaja en cuanto al desarrollo de aplicaciones para escritorio, de lo cual se intentó empalmarlas a las librerías web, como tal no se obtuvo el resultado deseado, ya que indagando un poco más se llegó a la conclusión de que no eran compatibles con la librería web de Python y los manuales ya estaban un poco desactualizados.
Ya con las prisas y con el tiempo encima de decide optar por librerías compatibles con javascript entre las cuales tenemos a las siguientes galardonadas.
•	Javascript
•	karpathy
•	harthur
•	machine_learning
De las cuales las primeras dos opciones eran bastante complicadas para descargar como para instalar ya que pedían un ciertos requerimientos para poder lograrlo, sin tanto éxito pero con un poco de paciencia se optó por machine-learning esta librería es sencilla de ocupar y posee cada uno de los aspectos que requiere el proyecto.

Instalación de Machine-Learning
Para poder acceder a las librerías de Machine-Learning tenemos que descargarlas.

Si contamos con Linux basta solo con este comando:
npm install machine_learning
Instalación en Windows 
Como tal la instalación en windos es descargar los scripts y colocarlos en una carpeta donde contengas a los demás scrips de java.


