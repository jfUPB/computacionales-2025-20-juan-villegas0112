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

**Qué tal si ensayas. Prueba con esta línea**

// 9) Configura el viewport
glViewport(0, 0, bufferWidth, bufferHeight);

<img width="357" height="360" alt="image" src="https://github.com/user-attachments/assets/7a7634d9-8969-44b1-8019-289f40c96b6c" />




**¿Qué pasa si?**

glViewport(0, bufferHeight/2, bufferWidth/2, bufferHeight/2);

<img width="356" height="351" alt="image" src="https://github.com/user-attachments/assets/6b6586ba-0ca0-4a09-89e6-da60e7da293c" />


**Cambia los valores de bufferWidth y bufferHeight: divide por 2, por 4, multiplica por 2, por 4, etc. ¿Qué pasa? ¿Qué observas? ¿Qué crees que está pasando?**

<img width="355" height="355" alt="image" src="https://github.com/user-attachments/assets/0c83bf4c-e52f-4e49-a044-c86f8ec2d7b8" />

Cuando cambio los valores de la línea glViewport(0, bufferHeight/2, bufferWidth/2, bufferHeight/2);, noto que la ventana no cambia de tamaño, pero el triángulo sí se ve diferente. Al dividir bufferWidth y bufferHeight, el triángulo se ve más pequeño y ocupa solo una parte de la ventana; al multiplicarlos, se ve más grande o incluso recortado.
Esto pasa porque glViewport controla en qué parte del framebuffer se dibuja, no el tamaño de la ventana. Es como si miráramos el dibujo por una ventana: el dibujo sigue siendo el mismo, pero según el tamaño o posición del marco (viewport), vemos más o menos parte de él. En resumen, al cambiar esos valores, lo que hago es escalar y mover el área donde OpenGL dibuja dentro del framebuffer.


***🧐🧪✍️ Reporta en tu bitácora***

**Entonces hagamos “digestión”: en tu bitácora, escribe un resumen de lo que has aprendido hasta ahora y piensa en un experimento del tipo ¿Qué pasaría si?**

Básicamente, lo que he aprendido hasta ahora es que OpenGL no trabaja solo, sino que necesita varios elementos que se conectan entre sí para que todo funcione. Primero está GLFW, que se encarga de crear la ventana y manejar los eventos como el teclado o el mouse, y además crea el contexto OpenGL, que es como el espacio de trabajo donde se van a guardar todas las configuraciones y recursos que se usarán al dibujar. Luego está OpenGL, que actúa como el medio por el cual le damos instrucciones a la GPU, que al final es la que realmente dibuja.

También entendí que el framebuffer es como una hoja invisible donde la GPU pinta los píxeles antes de mostrarlos en pantalla, y que el viewport define qué parte de esa hoja se ve en la ventana. Por eso, cuando uno cambia el tamaño del viewport, lo que realmente está haciendo es modificar la zona en la que se dibuja, no el tamaño de la ventana.

Y pensándolo un poco, mi experimento sería: ¿qué pasaría si cambio el tamaño de la ventana después de crear el contexto? Me da curiosidad saber si el triángulo se adaptaría automáticamente al nuevo tamaño o si quedaría desproporcionado hasta que se actualice el viewport.

Para estos experimentos primero cambié la variable SCR_WIDTH de 400 a 250, y al hacerlo noté que la ventana se hizo más angosta, como si le recortara los lados, pero el triángulo siguió apareciendo centrado dentro del espacio visible, solo que ahora ocupando una proporción mayor del ancho.

<img width="148" height="243" alt="image" src="https://github.com/user-attachments/assets/1866d426-0d93-48d0-b44f-64c891f5b7d4" />


Después quise probar qué pasaba al cambiar SCR_HEIGHT, así que la modifiqué a 200, y en este caso la ventana se volvió más baja, haciendo que el triángulo se viera un poco más “aplastado” verticalmente.

<img width="260" height="123" alt="image" src="https://github.com/user-attachments/assets/8fa7b6a8-0780-4c93-9603-6ee6f99134e1" />


***🧐🧪✍️ Reporta en tu bitácora***

**¿Qué pasa si cambias el primer parámetro de glDrawArrays a GL_LINES? ¿Qué pasa si lo cambias a GL_POINTS? ¿Qué pasa si cambias el tercer parámetro a 2? ¿Qué pasa si lo cambias a 4?**

Cuando cambio el número de vértices a menos de tres, el triángulo desaparece porque no se puede formar una figura con solo dos puntos. Si cambio el primer parámetro a GL_LINES, se dibuja solo una línea; con GL_POINTS, no se ve nada porque los puntos son muy pequeños. Al poner el tercer parámetro en 2, solo se usan dos vértices y el triángulo no aparece; si lo pongo en 4, no cambia nada porque solo hay tres vértices definidos.

<img width="253" height="247" alt="image" src="https://github.com/user-attachments/assets/4e72a984-ef2b-4d0e-9dbe-a634cce034a1" />


<img width="254" height="253" alt="image" src="https://github.com/user-attachments/assets/bed3525f-8b78-4bb1-a050-98f679b734aa" />


***🧐🧪✍️ Reporta en tu bitácora***

**¿Qué es el contexto OpenGL?**
El contexto OpenGL es como el espacio de trabajo donde se guarda todo lo relacionado con lo que se va a dibujar: shaders, texturas, buffers, y el estado actual de OpenGL. Sin él, no se podría ejecutar nada.

**¿Cuál es el rol de la biblioteca GLFW y qué ventaja tiene usarla?**
GLFW se encarga de crear ventanas, manejar eventos del teclado o mouse y crear el contexto OpenGL. La ventaja es que nos ahorra tener que escribir código específico para cada sistema operativo.

**¿Por qué OpenGL necesita un contexto (según la analogía del taller)?**
Porque el contexto es literalmente el “taller” donde el artista (OpenGL) puede trabajar. Sin él, no tiene ni espacio ni herramientas para dibujar.

**¿Qué es el framebuffer y a qué recuerda de las primeras unidades del curso?**
El framebuffer es la memoria donde se dibuja la imagen antes de mostrarse en pantalla. Me recuerda cuando en las primeras unidades dibujábamos píxel por píxel, indicando direcciones de memoria, solo que ahora todo eso lo hace la GPU.

**¿Qué relación hay entre el viewport y el framebuffer?**
El framebuffer es donde se guarda todo lo que se dibuja, mientras que el viewport es la “ventana” por la que vemos esa imagen. El framebuffer contiene el dibujo completo, y el viewport define qué parte se muestra en pantalla.

**¿Qué rol tienen los drivers de la GPU y la GPU misma?**
Los drivers son los que traducen las instrucciones de OpenGL para que la GPU las entienda, y la GPU es la que realmente hace el trabajo pesado: dibujar y procesar los gráficos.

**¿Por qué es necesario activar el VSync?**
Sirve para sincronizar los cuadros generados con la frecuencia de actualización del monitor y evitar el “tearing”. Si no se activa, pueden verse cortes o parpadeos, especialmente cuando la imagen es dinámica.

**¿Qué es OpenGL Legacy y qué diferencia tiene con el moderno?**
OpenGL Legacy es la versión antigua con un pipeline fijo, mientras que el moderno usa un pipeline programable con shaders. Esto permite tener más control y flexibilidad al dibujar.

**¿Qué es el shader program y por qué es importante?**
Es el programa que se ejecuta en la GPU y controla cómo se dibujan los vértices y los colores. Es esencial porque reemplaza las funciones fijas del OpenGL antiguo y permite crear efectos, luces y texturas personalizados.

**¿Qué hace setupTriangle(), y qué son el VAO y el VBO?**
setupTriangle() configura los datos del triángulo y los manda a la GPU. El VBO guarda los vértices en la memoria de la GPU, y el VAO organiza cómo se van a usar esos datos para dibujar la figura.

**¿Es necesario usar el shader program y el VAO en cada loop?**
No siempre. Si la figura no cambia, basta con configurarlos una vez. Pero si se modifican cosas como el color, la forma o los vértices, sí sería necesario actualizarlos dentro del loop.

**¿Por qué es importante glfwSwapBuffers(mainWindow)?**
Porque intercambia los buffers (el que se está mostrando y el que se acaba de dibujar), permitiendo una visualización fluida. Si no se llama, la imagen se congela o parpadea, y el programa puede colapsar.


## Actividad 04

***🧐✍️ Reporta en tu bitácora***

**Luego de estudiar las unidades 1 y 2 de este curso y ver el video, escribe con tus propias palabras ¿Cuál es la diferencia entre una CPU y una GPU?**

Según entendí del video, la diferencia principal entre la CPU y la GPU es la forma en que procesan la información. La CPU trabaja de manera más secuencial, ejecutando pocas tareas a la vez, pero con mucha precisión, ya que se encarga de las funciones generales del sistema, como manejar el sistema operativo y coordinar los procesos. En cambio, la GPU está pensada para el procesamiento masivo en paralelo, lo que le permite ejecutar miles de operaciones al mismo tiempo. Por eso es la indicada para tareas pesadas como los gráficos, los videojuegos o el renderizado 3D, donde se necesitan muchísimos cálculos simultáneamente para mostrar imágenes en tiempo real.


**¿Cuáles son los tres pasos claves del pipeline de OpenGL? Explica en tus propias palabras cuál es el objetivo de cada paso.**

Los tres pasos son Vertex Shading, Rasterization y Fragment Shading.

El Vertex Shading se encarga de calcular la posición de cada vértice y ubicar los objetos en el espacio, transformando la escena 3D a coordenadas que la pantalla pueda mostrar.

La Rasterization convierte esos vértices en fragmentos (como grupos de píxeles), asignándoles color y descartando lo que no se ve desde la cámara.

El Fragment Shading aplica iluminación, sombras y texturas para darle realismo a la imagen final.

**La gran novedad que introduce OpenGL moderno es el pipeline programable. ¿Qué significa esto? ¿Qué diferencia hay entre el pipeline fijo y el programable? ¿Qué ventajas le ves a esto? y si el pipeline es programable, ¿Qué tengo que programar?**

El pipeline programable significa que ahora podemos modificar ciertas etapas del proceso de renderizado usando shaders. Antes, con el pipeline fijo, esas etapas estaban predefinidas por el hardware y no se podían cambiar.
La diferencia es que el pipeline programable nos da flexibilidad: podemos decidir cómo se transforman los vértices, cómo se calculan los colores y qué efectos aplicar.
Las principales ventajas son un mayor control, mejores gráficos y más rendimiento.
Si el pipeline es programable, debo programar los shaders, principalmente el Vertex Shader y el Fragment Shader.

Si fueras a describir el proceso de rasterización ¿Qué dirías?
Diría que es el proceso donde la GPU transforma los vértices en fragmentos (o grupos de píxeles) y decide qué parte de los triángulos será visible en pantalla. También asigna los colores base de cada fragmento según el material o textura del objeto.

**¿Qué son los fragmentos? ¿Es lo mismo un fragmento que un píxel? ¿Por qué?**

No, no son lo mismo. Un fragmento es una unidad de información que contiene datos de color, profundidad y textura que luego se usan para formar un píxel.
En otras palabras, el fragmento es el paso previo al píxel final: de los fragmentos se obtiene el color que finalmente se mostrará en la pantalla.

**Explica qué problema resuelve el Z-buffer y ¿Qué es el depth test?**

El Z-buffer maneja la profundidad de la escena. Guarda la distancia de cada fragmento respecto a la cámara para saber cuál está más cerca y cuál debe mostrarse primero.
El depth test compara esas distancias y decide qué fragmentos deben ser visibles y cuáles se ocultan detrás de otros objetos, evitando que se dibujen cosas que no se ven.

**¿Por qué se presenta el problema del aliasing? ¿Qué es el anti-aliasing?**

El aliasing ocurre porque los objetos 3D se muestran en una pantalla compuesta por píxeles cuadrados, lo que causa que los bordes se vean con “dientes” o irregulares.
El anti-aliasing suaviza esos bordes calculando colores intermedios entre los píxeles, haciendo que las líneas y formas se vean más limpias y naturales.

**¿Qué relación hay entre la iluminación y el fragment shader? ¿Siempre es necesario tener en cuenta la iluminación en un fragment shader o puedo hacer uno sin iluminación? Explica qué implicaciones tiene esto.**

La iluminación se calcula en el fragment shader, ya que ahí se define cómo la luz afecta el color de cada fragmento según su posición y orientación.
No siempre es necesario incluir iluminación; se puede hacer un fragment shader sin ella, pero el resultado será una imagen plana y sin profundidad, con colores fijos y sin sombras, lo que la hace menos realista.

**¿Qué implica para la GPU que una aplicación tenga múltiples fuentes de iluminación?**

Implica que la GPU debe realizar muchos más cálculos para cada fragmento, ya que debe considerar cómo afecta cada luz al color, brillo y sombra del objeto. Esto aumenta la carga de trabajo y el uso de recursos, haciendo que el proceso sea más exigente y consuma más rendimiento.

****🧐✍️ Reporta en tu bitácora***

**Escribe un resumen en tus propias palabras de lo que se necesita para dibujar un triángulo en OpenGL.**

Primero se necesita tener la información de los vértices del triángulo, o sea, las coordenadas de los puntos. Esa info se manda a un VBO (Vertex Buffer Object), que es como una cajita donde se guarda toda esa data. Después hay que configurar un VAO (Vertex Array Object), que básicamente le dice a OpenGL cómo leer los datos del VBO. También hay que activar los atributos de los vértices, usando unas funciones que indican cómo está organizada esa información. Una vez hecho eso, se preparan los shaders y, cuando todo está listo, se llama a una función como glDrawArrays para que se dibuje el triángulo en pantalla.


**Escribe un resumen en tus propias palabras de lo que necesitas para poder usar un shader en OpenGL.**

Los shaders son como mini programas que corren en la GPU. Para usarlos, primero se escribe el código (por ejemplo, en GLSL), y se crean los shaders por separado: uno para los vértices y otro para los fragmentos (o píxeles). Luego se compilan y se enlazan juntos en un programa de shader. Ese programa tiene un ID único, y para activarlo se usa una función como glUseProgram(). Después de eso, todo lo que se dibuje va a pasar por ese shader, y ya se puede controlar cómo se ven las cosas en pantalla.

***🧐🧪✍️ Reporta en tu bitácora***

**Implementa el código anterior en tu máquina y captura pantalla del resultado. Pero antes de hacerlo trata de predecir qué va a pasar.**

Creo que se van a dibujar 3 triángulos, cada uno con su propio shader. Seguro se ven diferentes, tal vez cambie la posición o algo visual, aunque no estoy muy seguro de qué hace cada shader. No parece que cambie el color, así que tal vez solo los mueve o transforma de alguna forma.

<img width="396" height="392" alt="image" src="https://github.com/user-attachments/assets/43a92272-0274-4944-b0d4-2ae315008b95" />


## Actividad 05

***🧐🧪✍️ Reporta en tu bitácora***

**Incluye una captura de pantalla del triángulo interactivo funcionando en tu máquina.**

<img width="359" height="357" alt="image" src="https://github.com/user-attachments/assets/f72b4dfa-7d7e-4e40-bc74-77ff225d55a0" />


<img width="359" height="359" alt="image" src="https://github.com/user-attachments/assets/6b8d2c01-c737-4bb9-860b-5dfa5f8bd454" />


<img width="360" height="360" alt="image" src="https://github.com/user-attachments/assets/51b0c2d6-a673-4412-b632-9edba28233b8" />


<img width="359" height="358" alt="image" src="https://github.com/user-attachments/assets/491d4e30-6dfa-47ea-bd13-bbd60c87f227" />


**Explica el proceso de normalización de las coordenadas del mouse y cómo se relaciona con el sistema de coordenadas de OpenGL.**

La posición del mouse viene en píxeles, así que se normaliza dividiendo entre el ancho y alto de la ventana. Esto convierte los valores a un rango de 0 a 1, que es más fácil de usar con el sistema de coordenadas de OpenGL, ya que trabaja con coordenadas normalizadas.

**Explica el proceso de normalización a coordenadas de dispositivo (NDC) y cómo se relaciona con el sistema de coordenadas de OpenGL.**

OpenGL usa un sistema de coordenadas que va de -1 a 1 en ambos ejes (X y Y). Por eso, cuando tienes coordenadas normalizadas entre 0 y 1 (como las del mouse o los vértices), debes transformarlas para que entren en ese rango.

Para eso, se hace esta transformación:

En X: x * 2 - 1 (convierte 0 en -1, 0.5 en 0, y 1 en 1)

En Y: 1 - y * 2 (convierte 0 en 1, 0.5 en 0, y 1 en -1), además invierte el eje Y porque en pantalla Y crece hacia abajo, pero en OpenGL hacia arriba.

Así, las coordenadas pasan a NDC y OpenGL puede usarlas correctamente para dibujar.

## Actividad 06 APPLY

***🧐🧪✍️ Reporta en tu bitácora***

**Describe brevemente los cambios que realizaste en el código C++ (dónde obtienes el tiempo, cómo y dónde actualizas el uniform).**

- Agregué un uniform llamado time en el fragment shader.
- Obtengo el tiempo usando glfwGetTime() dentro del loop principal.
- Luego, actualizo el uniform con glUniform1f(timeLocation, currentTime) en cada iteración, para enviarle el valor actual del tiempo al shader.

**Pega el código modificado de tu fragment shader.**

```c++
#include <iostream>
#include <glad/glad.h>
#include <GLFW/glfw3.h>


const unsigned int SCR_WIDTH = 800;
const unsigned int SCR_HEIGHT = 600;


void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
    glViewport(0, 0, width, height);
}


void processInput(GLFWwindow* window) {
    if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
        glfwSetWindowShouldClose(window, true);
}


const char* vertexShaderSrc = R"glsl(
    #version 460 core
    layout(location = 0) in vec3 aPos;
    uniform vec2 offset;

    void main() {
        vec3 newPos = aPos;
        newPos.x += offset.x;
        newPos.y += offset.y;
        gl_Position = vec4(newPos, 1.0);
    }
)glsl";

const char* fragmentShaderSrc = R"glsl(
    #version 460 core
    out vec4 FragColor;
    uniform float time;
    uniform vec4 ourColor; // opcional, no se usa directamente aquí

    void main() {
        float r = (sin(time) + 1.0) / 2.0;
        float g = (sin(time + 2.0) + 1.0) / 2.0;
        float b = (cos(time) + 1.0) / 2.0;
        FragColor = vec4(r, g, b, 1.0);
    }
)glsl";


unsigned int VAO, VBO, shaderProg;

unsigned int buildShaderProgram(const char* vSrc, const char* fSrc) {
    int success;
    char log[512];

    unsigned int vs = glCreateShader(GL_VERTEX_SHADER);
    glShaderSource(vs, 1, &vSrc, nullptr);
    glCompileShader(vs);
    glGetShaderiv(vs, GL_COMPILE_STATUS, &success);
    if (!success) {
        glGetShaderInfoLog(vs, 512, nullptr, log);
        std::cerr << "ERROR VERTEX SHADER:\n" << log << "\n";
    }

    unsigned int fs = glCreateShader(GL_FRAGMENT_SHADER);
    glShaderSource(fs, 1, &fSrc, nullptr);
    glCompileShader(fs);
    glGetShaderiv(fs, GL_COMPILE_STATUS, &success);
    if (!success) {
        glGetShaderInfoLog(fs, 512, nullptr, log);
        std::cerr << "ERROR FRAGMENT SHADER:\n" << log << "\n";
    }

    unsigned int prog = glCreateProgram();
    glAttachShader(prog, vs);
    glAttachShader(prog, fs);
    glLinkProgram(prog);
    glGetProgramiv(prog, GL_LINK_STATUS, &success);
    if (!success) {
        glGetProgramInfoLog(prog, 512, nullptr, log);
        std::cerr << "ERROR LINKING PROGRAM:\n" << log << "\n";
    }

    glDeleteShader(vs);
    glDeleteShader(fs);
    return prog;
}


void setupTriangle() {
    float vertices[] = {
        -0.5f, -0.5f, 0.0f,
         0.5f, -0.5f, 0.0f,
         0.0f,  0.5f, 0.0f
    };

    glGenVertexArrays(1, &VAO);
    glGenBuffers(1, &VBO);

    glBindVertexArray(VAO);
    glBindBuffer(GL_ARRAY_BUFFER, VBO);
    glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
    glEnableVertexAttribArray(0);
    glBindVertexArray(0);
}

int main() {
    if (!glfwInit()) {
        std::cerr << "Fallo al inicializar GLFW\n";
        return -1;
    }
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 6);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

    GLFWwindow* window = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Triángulo combinado", nullptr, nullptr);
    if (!window) {
        std::cerr << "Fallo al crear la ventana\n";
        glfwTerminate();
        return -1;
    }

    glfwMakeContextCurrent(window);
    glfwSetFramebufferSizeCallback(window, framebuffer_size_callback);

    if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
        std::cerr << "Fallo al cargar GLAD\n";
        return -1;
    }

    glfwSwapInterval(1); 
    shaderProg = buildShaderProgram(vertexShaderSrc, fragmentShaderSrc);
    setupTriangle();


    glUseProgram(shaderProg);
    int offsetLocation = glGetUniformLocation(shaderProg, "offset");
    int timeLocation = glGetUniformLocation(shaderProg, "time");
    int colorLocation = glGetUniformLocation(shaderProg, "ourColor"); 

    while (!glfwWindowShouldClose(window)) {
        glfwPollEvents();
        processInput(window);

        glClearColor(0.1f, 0.1f, 0.1f, 1.0f);
        glClear(GL_COLOR_BUFFER_BIT);

        
        float currentTime = static_cast<float>(glfwGetTime());
        glUniform1f(timeLocation, currentTime);

        
        double xpos, ypos;
        glfwGetCursorPos(window, &xpos, &ypos);
        float x = static_cast<float>(xpos) / SCR_WIDTH;
        float y = static_cast<float>(ypos) / SCR_HEIGHT;

        
        x = std::min(std::max(x, 0.0f), 1.0f);
        y = std::min(std::max(y, 0.0f), 1.0f);

        
        glUniform2f(offsetLocation, x * 2.0f - 1.0f, 1.0f - y * 2.0f);

        glUniform4f(colorLocation, x, y, 0.5f, 1.0f);

        
        glUseProgram(shaderProg);
        glBindVertexArray(VAO);
        glDrawArrays(GL_TRIANGLES, 0, 3);

        glfwSwapBuffers(window);
    }

  
    glfwMakeContextCurrent(window);
    glDeleteVertexArrays(1, &VAO);
    glDeleteBuffers(1, &VBO);
    glDeleteProgram(shaderProg);
    glfwDestroyWindow(window);
    glfwTerminate();
    return 0;
}

```

**Explica cómo usaste la función de tiempo (sin, cos, u otra) para lograr el efecto de cambio de color cíclico. ¿Qué rango de valores produce tu cálculo y cómo afecta eso al color final?**

Usé sin(time) para el canal rojo y verde, y cos(time) para el azul. Estas funciones oscilan entre -1 y 1, pero como los colores en OpenGL van de 0 a 1, tuve que hacerles una transformación: les sumé 1 y luego los dividí entre 2. Así el rango final queda de 0 a 1. Esto hace que el color cambie de forma suave y cíclica, como si estuviera “respirando”. Si no se hace esa transformación, los valores negativos causarían colores raros o errores.

**Incluye una captura de pantalla o UN ENLACE a un video mostrando el resultado del triángulo con color cambiante.**

<img width="798" height="595" alt="image" src="https://github.com/user-attachments/assets/96b0a2ae-e7ba-4d4f-9124-7aa375a1d5c6" />


<img width="801" height="599" alt="image" src="https://github.com/user-attachments/assets/d3bd1d72-dcc5-4afd-9f29-48006025d8c1" />


<img width="797" height="598" alt="image" src="https://github.com/user-attachments/assets/76882a00-6733-4c35-b378-5a5c5d59b088" />


**Reflexión: ¿Qué otros efectos visuales simples podrías lograr usando el tiempo como uniform? Piensa en la posición, el tamaño o la rotación (aunque no hemos visto rotaciones formalmente, ¡intuitivamente podrías intentarlo!). Anota al menos una idea.**

Con el tiempo se pueden hacer cosas muy interesantes. Por ejemplo, animar la posición de un vértice para que parezca que el triángulo flota o se mueve en círculos. También se puede hacer que cambie de tamaño (como si pulsara) o que gire lentamente. Incluso se podría hacer que reaccione al movimiento del mouse pero con un pequeño retraso, como si colgara. Todo eso usando sin, cos y tiempo.

## Evidencias

### Nota propuesta: 5.0

***La defensa de esa nota para cada actividad.***

Hice todas las actividades correspondientes, incluyendo el apply, las reflexiones, los experimentos, las capturas de pantalla y la autoevaluación. Cada actividad fue completada de forma detallada y en orden, siguiendo las instrucciones dadas y aplicando los conceptos aprendidos sobre OpenGL, shaders, interacción con el mouse y uso del tiempo como uniform.


