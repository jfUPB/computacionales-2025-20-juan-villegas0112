# Bitácora de aprendizaje de la unidad 7

## Actividad 01

***🧐🧪✍️ Reporta en tu bitácora***

**1. Incluye una captura de pantalla del ejemplo funcionando en tu máquina.**

<img width="1031" height="793" alt="image" src="https://github.com/user-attachments/assets/08aedfec-8756-4af4-9680-d610576d5ec6" />



**2. Observa el proyecto, trata de entenderlo, pero ten presente que lo analizaremos más adelante.**

El proyecto genera un triangulo en una ventana nueva, de color naranja con un fondo verde. En el codigo se ve como hay un orden estructurado en el cual se cumplen cierta cantidad de pasos especificos.


**3. ¿Qué preguntas te surgen al ver el código?. Anota al menos tres preguntas que te gustaría investigar más adelante (no te preocupes que la idea de esta unidad es que las resuelvas).**
- ¿Como hacer que el triangulo sea interactivo?
- ¿Que tipo de interactividad tendrá?
- ¿Como funciona el proyecto?

## Actividad 02

***🧐🧪✍️ Reporta en tu bitácora***

**Necesito que hagas digestión de esta información y que la entiendas. Para ello te voy a pedir un resumen en tus propias palabras de lo que acabas de leer. En tu resumen debes tratar de conectar GLFW, opengl32.lib, GLAD, GLM y los drivers de la GPU. ¿Qué rol cumple cada uno? ¿Cómo se relacionan entre sí? Mira, trata de hacer esto de memoria y como si estuvieras contándole a un amigo que quiere aprender OpenGL. Cuando haces el proceso de memoria tu cerebro hace un esfuerzo adicional y eso te ayuda a aprender. Además, si no recuerdas algo quiere decir que no lo entendiste bien y eso es una buena señal para que vuelvas a leerlo.**

Cuando uno crea un proyecto con OpenGL en Windows, no solo es escribir un código en C++; hay que tener varias bibliotecas que se encargan de distintas partes del proceso. Todo empieza con GLFW, que básicamente es la que crea la ventana donde se va a mostrar lo que renderizas y también se encarga de manejar cosas como el teclado y el ratón. Sin GLFW, no podríamos tener ni siquiera una ventana para dibujar.

Pero GLFW por sí sola no puede hacer que OpenGL funcione, porque Windows solo trae una versión viejísima de OpenGL (la 1.1) dentro de opengl32.lib. Esa librería es como una puerta de entrada: te permite crear el contexto inicial de OpenGL, pero las funciones modernas (por ejemplo, de la versión 4.6) no están ahí. Esas funciones viven en los drivers de la tarjeta gráfica (GPU), que son los que realmente implementan las versiones nuevas de OpenGL.

Ahí entra GLAD. GLAD actúa como un intermediario que se encarga de “cargar” las funciones modernas desde los drivers de la GPU. Es decir, cuando tú llamas a una función avanzada de OpenGL en tu programa, GLAD ya la habrá buscado y enlazado desde los drivers. Por eso, en el proyecto se incluye el archivo glad.c, que es el que hace posible esa carga en tiempo de ejecución.

Y luego está GLM, que no es obligatoria, pero es muy útil. GLM es una librería de matemáticas que facilita el trabajo con vectores y matrices, que son cosas que se usan todo el tiempo en gráficos 3D (por ejemplo, para mover, rotar o escalar objetos).

## Actividad 03

***🧐🧪✍️ Reporta en tu bitácora***


