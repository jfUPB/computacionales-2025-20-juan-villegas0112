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


Ejecuta el código y muestra una captura de pantalla del objeto en la memoria.
<img width="774" height="163" alt="image" src="https://github.com/user-attachments/assets/dbd88958-e268-44de-bc29-6136608be631" />

¿Qué puedes observar? 
- Que estoy dentro de un método de la clase ofApp y el depurador muestra la variable this. Tambien, se observa que this es un puntero a la instancia actual de ofApp en memoria. Su dirección de memoria es 0x000001dc90bf3b90. Al expandir this el depurador ya muestra uno de sus miembros: particles. Particles es un std::vector<Particle*> y en este momento tiene size = 160, es decir 160 elementos almacenados.

¿Qué información te proporciona el depurador? 
- La ubicación exacta en memoria de la instancia de ofApp, el tipo de dato real del objeto (ofApp*) y el estado interno actual de sus atributos/miembros (en este caso, particles y su tamaño).

¿Qué puedes concluir?
- La instancia de ofApp existe en la memoria y el depurador permite ver su contenido en tiempo de ejecución.
- Usar el depurador permite ver los valores reales de sus atributos y así comprobar si el programa está funcionando como se espera.
- También se puede comprobar el tamaño y existencia de los objetos dinámicos sin necesidad de ver nada en consola.

¿Qué puedes observar en la memoria? 

<img width="1596" height="163" alt="image" src="https://github.com/user-attachments/assets/350899dc-a764-4dc6-9062-3e0062f25c02" />

- Aparece la lista de variables locales actuales:
- particles es el std::vector<Particle*> que contiene todos los punteros a partículas existentes.
- particles[i] es un puntero a una instancia concreta de RisingParticle.
- this es el puntero al objeto ofApp, que tiene como miembro ese vector particles.
- Dentro de particles[i] se  puede ver sus atributos internos, como: position = {x=514.89, y=...} y velocity = {x=-83.00, y=...}


¿Qué información te proporciona el depurador? 
- La dirección de memoria exacta donde está guardado cada objeto.
- El tipo real del objeto
- Los valores en tiempo real de los campos de la clase.
- Que el objeto está en el heap, no en la pila (stack).



¿Qué puedes concluir? 
- Los elementos de particles son punteros a objetos que están almacenados en el heap.
- El depurador permite:
    - Ver su dirección de memoria.
    - Ver sus atributos en tiempo real.
    - Ver su tipo dinámico.




🧐🧪✍️ Captura la _vtable de un objeto CircularExplosion, pega la imagen en tu bitácora, pero observa detenidamente la tabla de funciones. ¿Qué puedes observar?

<img width="535" height="134" alt="image" src="https://github.com/user-attachments/assets/fecd0bb5-be30-44db-8848-d3dc2f9412dc" />

- El _vfptr  dentro del objeto apunta a la vtable de CircularExplosion.
- La vtable contiene varias entradas (cada una es un puntero a código).

🧐🧪✍️ Ahora, captura en memoria la _vtable de un objeto StarExplosion, pega la imagen en tu bitácora y observa detenidamente la tabla de funciones

<img width="529" height="140" alt="image" src="https://github.com/user-attachments/assets/90f88d4b-0e72-4f66-bfe3-48b914ca7aa6" />

🧐🧪✍️ Observa de nuevo ambas tablas y compara. ¿Qué puedes ver? ¿Qué puedes concluir? ¿Qué relación existe entre la tabla de funciones y los métodos virtuales? 

- Ambas tienen una estructura parecida; varios punteros a funciones, pero apuntan a distintas direcciones de memoria, eso significa que apuntan a distintas implementaciones de los métodos.
- Algunas entradas son iguales porque vienen de clases base (como Particle o ExplosionParticle) y otras cambian porque fueron sobrescritas en la clase derivada.

¿Cómo se logra esto? ¿Qué relación existe entre los métodos virtuales y el polimorfismo? Al llamar HacerSonido cómo sabe esta función sobre cuál objeto debe actuar?
- Cuando ee declara un método como virtual, el compilador añade una entrada a la vtable de esa clase con la dirección de esa función.
- Si una clase hija sobrescribe ese método, el compilador reemplaza esa entrada en la vtable de la clase hija con la dirección del nuevo método.
- En cada objeto hay un campo oculto llamado _vptr que apunta a la vtable de su clase.

### Actividad 4
🧐🧪✍️¿Qué sucede? 

Cuando se descomenta las dos líneas que intentan acceder a protectedVar y privateVar, el compilador muestra errores de acceso y no deja compilar el programa.

¿Por qué sucede esto?

Esto ocurre porque:

- public: accesibles desde cualquier parte del programa.
- protected: accesibles solo desde la misma clase o clases hijas (heredadas), pero no desde funciones externas como main.
- private: accesibles únicamente desde dentro de la misma clase que los declara.

Entonces, main no tiene permiso para acceder a protectedVar ni privateVar.

 ¿Qué puedes concluir?
 
Los modificadores de acceso existen para proteger los datos y controlar cómo se usan desde fuera de la clase, cumpliendo con el principio de encapsulación en programación orientada a objetos.

🧐🧪✍️ Compila el programa. ¿Qué pasa?

<img width="630" height="86" alt="image" src="https://github.com/user-attachments/assets/ecb6e1c1-6de1-4248-809d-00318d2e84dd" />

no permite ejecutar

🧐🧪✍️ Compila el programa y ejecuta. ¿Qué puedes concluir?

El programa compila sin errores.

Al ejecutarlo:
<img width="452" height="79" alt="image" src="https://github.com/user-attachments/assets/b4be1b8f-9328-4ed2-95f3-9b9c6cc79f96" />

🧐🧪✍️ En tus palabras, ¿Qué es el encapsulamiento? ¿Por qué es importante?

El encapsulamiento es la capaicdad de acceso que se le puede dar a diferentes procesos de codigo. Es importante porque evita errores y ayuda a tener un mejor orden a la hora de programar.


### Actividad 5



### Actividad 6



## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
