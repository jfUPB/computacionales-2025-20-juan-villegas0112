# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**

***Parte 1: recordando los conceptos (en C#)***

**¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.**

🧐 El encapsulamiento es la capacidadad para mostrar solo las cosas necesarias a la hora de crear una clase, es decir, a la hora de la creacion de los atributos y metodos crearles estados de acceso; private, public, etc...

**¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.**

🧐 La herencia es la capacidad de relacionar diferentes clases, permitiendo que una clase obtenga de la otra infromacio como atributos y metodos, es algo muy util, pues ademas de ahorrar tiempo tanmbien genera un orden jerarquico dentro del proyecto. Un ejemplo podria ser la clase Res le hereda a la clase novillo, cebon y ternero unos atributos como: edad, peso, tamaño, etc. Tambien podria heredarle algun metodo como por ejemplo el metodo de cant_alimento para saber cuanto alimento se le debe dar a cada tipo de res, este metodo puede variar con respecto al peso, el tamaño y la edad.

**¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”.**

🧐 Es darle a diferentes clases la capacidad de utilizar un mismo metodo pero que sea unico en cada caso, es decir, un metodo que se adapte a los diferentes atributos que puedan tener varias clases de un mismo proyecto.

***Parte 2: análisis de código (en C#)***

**Encapsulamiento:**

Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es.
```c++
  private string nombre;

  public string Nombre
    {
        get { return nombre; }
        protected set { nombre = value; }
    }
```
🦜 Porque hace que el atributo nombre sea privado y queno se tenga un acceso directo, pero luego en el metodo Nombre permite mediante un proceso de get set que se pueda leer y modificar de forma protegida dentro de las clases que hereden a esta.


¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?

🦜 Ademas de prevenir errores, esto hace como ya lo habia mencionado que solo la clase Figura tenga acceso directo para cmabiar el atributo nombre, esto permite que haya un constructor para las clases que herenden este metodo y que el nombre no tenga un valor no deseado.

**Herencia:**

¿Cómo se evidencia la herencia en la clase Circulo?

```c++
public class Circulo : Figura
```
Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?

🦜.
- nombre.

- Nombre, que expone el valor del nombre.

- El método Dibujar().

El constructor de Figura:
``` c++ 
 public Circulo(double radio) : base("Círculo")
    {
        this.Radio = radio;
    }
```


**Polimorfismo:**

Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión, ¿Cómo crees que funciona esto “por debajo”? No necesitas saber la respuesta correcta, solo quiero que intentes razonar cómo podría ser.

🦜 Esto sucede porque el bucle for eache, por mas que contanga la variable fig que es de tipo Figura, este debe analizar que figura debe genenrar para poder realizar el metodo de dibujar correspondiente a cada una de las clases establecidas que cuentan con la eherencia de Figura.

***Parte 3: hipótesis sobre la implementación***

Esta es la parte más importante. Imagina que eres un diseñador de lenguajes de programación. Tienes que decidir cómo implementar estos conceptos en la memoria y en el procesador. No hay respuestas incorrectas, solo ideas. Dibuja si te ayuda.



Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?

🦜 En memoria, un objeto Rectangulo es un bloque que contiene primero los datos que se heredan de Figura y luego los propios que serian Base y Altura.

El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.

- El compilador crea una lista o tabla de métodos para cada clase, y en tiempo de ejecución se consulta cuál de esos métodos debe usarse según el tipo real del objeto.
  
- Otra posibilidad es que la llamada sea como un “puente”: primero va al método de Figura, pero ahí hay una especie de instrucción que redirige la ejecución hacia la implementación que tenga la subclase.



La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?

- Cuando se escribe el código y se trata de acceder a un private, el compilador detecta que no está permitido y directamente te da un error. O sea, ni siquiera deja que se genere el programa.


***Parte 4: y tu autoevaluación y primeras preguntas***

Has completado el diagnóstico. Ahora, reflexiona sobre tu propia experiencia y basado en esto te propongo dos caminos:

Formula la primer pregunta que comenzarás a investigar. Este será el punto de partida para tu “ruta de exploración personal”. Tu vas definiendo tus propiuas actividades.
Si prefieres la “ruta guiada” adelante. Comienza con la actividad 2.



## 2.  **La pregunta inicial**
¿Como es el correcto funcionamiento del metodo Dibujar y como cambia respecto a la clase que se use?
## 3.  **Registro de exploración:** 

### Actividad 2

> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.

🧐🧪✍️ Analiza el código de la aplicación y trata de explicar en tus propias palabras qué está haciendo, NO USES IA generativa. Captura pantallas de la aplicación funcionando y añádelas a la bitácora de aprendizaje.

- Al leer el codigo y no ejecutarlo supongo, que se trata de la creacion mediante el uso del click, que parten de la parte inferior de la pantalla recorren cierta distancia hacia arriba y luego explotan. Tambien se sabe que las particulas no tienen simepre la misma direccion, color, tamaño de explosion, etc...
```c++
// -------------------------------------------------
// Clase base abstracta: Particle
// -------------------------------------------------
class Particle {
public:
	virtual ~Particle() { }
	virtual void update(float dt) = 0;
	virtual void draw() = 0;
	virtual bool isDead() const = 0;
	// Nuevo método para saber si la partícula (tipo RisingParticle) debe explotar
	virtual bool shouldExplode() const { return false; }
	// Métodos para obtener posición y color, para usarlos en explosiones
	virtual glm::vec2 getPosition() const { return glm::vec2(0, 0); }
	virtual ofColor getColor() const { return ofColor(255); }
};

// -------------------------------------------------
// RisingParticle: Partícula que nace en la parte inferior central y sube
// -------------------------------------------------
class RisingParticle : public Particle {
protected:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float lifetime; // tiempo máximo antes de explotar
	float age;
	bool exploded;
```

- Captura pantallas de la aplicación funcionando
  <img width="1024" height="768" alt="screenshot_3030" src="https://github.com/user-attachments/assets/e4702ec6-2c77-47ea-a712-76899d37d265" />

  <img width="1024" height="768" alt="screenshot_4002" src="https://github.com/user-attachments/assets/3beb7e29-a463-4399-abbd-45912144d0f6" />

  <img width="1024" height="768" alt="screenshot_4403" src="https://github.com/user-attachments/assets/fa594f98-0ddf-4529-b3ce-30d12b23c83d" />

  <img width="1024" height="768" alt="screenshot_4509" src="https://github.com/user-attachments/assets/896368d4-c717-4a73-be2e-d052de01d8ce" />



### Actividad 3

🧐🧪✍️ 
¿Qué esperas ver en memoria (hipótesis)?
En la memoria se deben ver los valores de las variables creadas y los tipos de cada una.

<img width="945" height="175" alt="image" src="https://github.com/user-attachments/assets/fe21e7d5-b860-46f9-aef2-91545f63541d" />

Ejecuta el código y muestra una captura de pantalla del objeto en la memoria. ¿Qué puedes observar? ¿Qué información te proporciona el depurador? ¿Qué puedes concluir?

### Actividad 4


### Actividad 5



### Actividad 6



## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
