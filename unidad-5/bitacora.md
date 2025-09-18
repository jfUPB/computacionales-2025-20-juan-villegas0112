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

🧐🧪✍️ captura de nuevo la memoria que ocupa el objeto CircularExplosion compara la jerarquía de clases con los campos en memoria del objeto. ¿Qué puedes observar? 
<img width="542" height="178" alt="image" src="https://github.com/user-attachments/assets/96be5cd8-88fe-4ede-8e6a-d5d1fac0a149" />

Se muestran todos los campos heredados de Particle, después los de ExplosionParticle, y finalmente los de CircularExplosion.

¿Qué información te proporciona el depurador? 

- El tipo real del objeto almacenado en el vector.
- La disposición de los miembros en memoria, mostrando primero los campos heredados y luego los propios.
- El tamaño y dirección de memoria de cada campo, lo cual ayuda a entender cómo se construye el objeto en memoria.
- El contenido actual de cada variable.
- La existencia del __vfptr, que confirma que hay herencia polimórfica y que el objeto sabe a qué implementación concreta de los métodos virtuales debe llamar.

¿Qué puedes concluir?
La memoria del CircularExplosion contiene primero la parte correspondiente a Particle, luego la de ExplosionParticle y finalmente su propia parte.

🧐🧪✍️ ¿Cómo se implementa la herencia en C++?

La herencia en C++ se implementa por composición de memoria y tablas virtuales:
el compilador combina todos los miembros de la clase base y los coloca en el objeto de la clase derivada, y si hay funciones virtuales, añade el mecanismo de vtable para permitir el polimorfismo en tiempo de ejecución.


### Actividad 6

🧐🧪✍️¿Qué puedes observar? 

<img width="608" height="92" alt="image" src="https://github.com/user-attachments/assets/9a18ec8c-8e6f-4d59-a785-6b177c7fa6b1" />
- Aunque todos los elementos están guardados como Particle* dentro del vector particles, cada uno recuerda de qué tipo real es en verdad. Entonces, cuando el programa llama a particles[i]->update(dt), no ejecuta siempre el mismo update()

¿Qué información te proporciona el depurador?
- Muestra en tiempo de ejecución qué implementación concreta de update() está siendo llamada en cada iteración.
- Confirma que el polimorfismo dinámico está funcionando, ya que la decisión de qué método llamar no se hace en compilación sino en ejecución.
- Te deja ver que objetos distintos dentro del mismo vector llaman métodos distintos, a pesar de tener el mismo tipo de puntero (Particle*).

🧐🧪✍️ Realiza un dibujo con el cuál expliques cómo se implementa el polimorfismo en tiempo de ejecución. Utiliza el concepto de métodos virtuales y la tabla de funciones virtuales. ¿Qué puedes concluir?

<img width="718" height="483" alt="image" src="https://github.com/user-attachments/assets/10813042-1c4e-4c63-a201-9bef4950145e" />

🧐🧪✍️ ¿Qué relación existe entre los métodos virtuales y el polimorfismo?

Los métodos virtuales hacen posible el polimorfismo porque permiten que la decisión sobre qué versión del método ejecutar se haga en tiempo de ejecución, basándose en el tipo real del objeto.

###Actividad 07

- Agrega dos nuevos tipos de Particle diferentes a RisingParticle.
- Implementar un nuevo modo de explosión.

ofApp.h
```cpp
#pragma once
#include "ofMain.h"
#include <vector>

// -------------------------------------------------
// Clase base abstracta: Particle
// -------------------------------------------------
class Particle {
public:
	virtual ~Particle() { }
	virtual void update(float dt) = 0;
	virtual void draw() = 0;
	virtual bool isDead() const = 0;
	virtual bool shouldExplode() const { return false; }
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
	float lifetime;
	float age;
	bool exploded;

public:
	RisingParticle(const glm::vec2 & pos, const glm::vec2 & vel, const ofColor & col, float life)
		: position(pos)
		, velocity(vel)
		, color(col)
		, lifetime(life)
		, age(0)
		, exploded(false) {
	}

	void update(float dt) override {
		position += velocity * dt;
		age += dt;
		velocity.y += 9.8f * dt * 8;
		float explosionThreshold = ofGetHeight() * 0.15 + ofRandom(-30, 30);
		if (position.y <= explosionThreshold || age >= lifetime) {
			exploded = true;
		}
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, 10);
	}

	bool isDead() const override { return exploded; }
	bool shouldExplode() const override { return exploded; }
	glm::vec2 getPosition() const override { return position; }
	ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// SideParticle: Partícula que nace en los costados y cruza horizontalmente
// -------------------------------------------------
class SideParticle : public Particle {
protected:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float lifetime;
	float age;
	bool exploded;

public:
	SideParticle(const glm::vec2 & pos, const glm::vec2 & vel, const ofColor & col, float life)
		: position(pos)
		, velocity(vel)
		, color(col)
		, lifetime(life)
		, age(0)
		, exploded(false) {
	}

	void update(float dt) override {
		position += velocity * dt;
		age += dt;
		velocity.y += 9.8f * dt * 2;
		if (age >= lifetime || (position.x > ofGetWidth() * 0.45 && position.x < ofGetWidth() * 0.55)) {
			exploded = true;
		}
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, 8);
	}

	bool isDead() const override { return exploded; }
	bool shouldExplode() const override { return exploded; }
	glm::vec2 getPosition() const override { return position; }
	ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// DiagonalParticle: Partícula que sube en diagonal desde las esquinas
// -------------------------------------------------
class DiagonalParticle : public Particle {
protected:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float lifetime;
	float age;
	bool exploded;

public:
	DiagonalParticle(const glm::vec2 & pos, const glm::vec2 & vel, const ofColor & col, float life)
		: position(pos)
		, velocity(vel)
		, color(col)
		, lifetime(life)
		, age(0)
		, exploded(false) {
	}

	void update(float dt) override {
		position += velocity * dt;
		age += dt;
		velocity.y += 9.8f * dt * 3;
		float explosionThreshold = ofGetHeight() * 0.33 + ofRandom(-20, 20);
		if (position.y <= explosionThreshold || age >= lifetime) {
			exploded = true;
		}
	}

	void draw() override {
		ofSetColor(color);
		ofDrawRectangle(position.x, position.y, 12, 12);
	}

	bool isDead() const override { return exploded; }
	bool shouldExplode() const override { return exploded; }
	glm::vec2 getPosition() const override { return position; }
	ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// Clase base para explosiones: ExplosionParticle
// -------------------------------------------------
class ExplosionParticle : public Particle {
protected:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float age;
	float lifetime;
	float size;

public:
	ExplosionParticle(const glm::vec2 & pos, const glm::vec2 & vel, const ofColor & col, float life, float sz)
		: position(pos)
		, velocity(vel)
		, color(col)
		, age(0)
		, lifetime(life)
		, size(sz) {
	}

	void update(float dt) override {
		position += velocity * dt;
		age += dt;
		float alpha = ofMap(age, 0, lifetime, 255, 0, true);
		color.a = alpha;
	}

	bool isDead() const override { return age >= lifetime; }
};

// -------------------------------------------------
// CircularExplosion: Explosión en patrón circular
// -------------------------------------------------
class CircularExplosion : public ExplosionParticle {
public:
	CircularExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.2f, ofRandom(16, 32)) {
		float angle = ofRandom(0, TWO_PI);
		float speed = ofRandom(80, 200);
		velocity = glm::vec2(cos(angle), sin(angle)) * speed;
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, size);
	}
};

// -------------------------------------------------
// RandomExplosion: Explosión con direcciones aleatorias
// -------------------------------------------------
class RandomExplosion : public ExplosionParticle {
public:
	RandomExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.5f, ofRandom(16, 32)) {
		velocity = glm::vec2(ofRandom(-200, 200), ofRandom(-200, 200));
	}

	void draw() override {
		ofSetColor(color);
		ofDrawRectangle(position.x, position.y, size, size);
	}
};

// -------------------------------------------------
// StarExplosion: Explosión en forma de estrella
// -------------------------------------------------
class StarExplosion : public ExplosionParticle {
public:
	StarExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.3f, ofRandom(20, 40)) {
		float angle = ofRandom(0, TWO_PI);
		float speed = ofRandom(90, 180);
		velocity = glm::vec2(cos(angle), sin(angle)) * speed;
	}

	void draw() override {
		ofSetColor(color);
		int rays = 5;
		float outerRadius = size;
		float innerRadius = size * 0.5;
		ofPushMatrix();
		ofTranslate(position);
		for (int i = 0; i < rays; i++) {
			float theta = ofMap(i, 0, rays, 0, TWO_PI);
			float xOuter = cos(theta) * outerRadius;
			float yOuter = sin(theta) * outerRadius;
			float xInner = cos(theta + PI / rays) * innerRadius;
			float yInner = sin(theta + PI / rays) * innerRadius;
			ofDrawLine(0, 0, xOuter, yOuter);
			ofDrawLine(xOuter, yOuter, xInner, yInner);
		}
		ofPopMatrix();
	}
};
// -------------------------------------------------
// SpiralExplosion: Explosión en espiral
// -------------------------------------------------
class SpiralExplosion : public ExplosionParticle {
private:
	float angle; // ángulo actual
	float angularVel; // velocidad angular
public:
	SpiralExplosion(const glm::vec2 & pos, const ofColor & col)
		: ExplosionParticle(pos, glm::vec2(0, 0), col, 1.8f, ofRandom(10, 25)) {
		angle = ofRandom(0, TWO_PI);
		angularVel = ofRandom(4, 10); // qué tan rápido rota
		float speed = ofRandom(60, 120);
		velocity = glm::vec2(cos(angle), sin(angle)) * speed;
	}

	void update(float dt) override {
		age += dt;
		angle += angularVel * dt;

		// velocidad radial se actualiza como si girara
		float speed = glm::length(velocity);
		velocity = glm::vec2(cos(angle), sin(angle)) * speed;

		position += velocity * dt;

		// desvanecer
		float alpha = ofMap(age, 0, lifetime, 255, 0, true);
		color.a = alpha;
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, size);
	}
};

// -------------------------------------------------
// ofApp: Manejo de la escena y eventos
// -------------------------------------------------
class ofApp : public ofBaseApp {
public:
	void setup();
	void update();
	void draw();
	void mousePressed(int x, int y, int button);
	void keyPressed(int key);

	std::vector<Particle *> particles;
	~ofApp();

private:
	void createRisingParticle();
	void createSideParticle();
	void createDiagonalParticle();
};

```
ofApp.cpp
```cpp
#include "ofApp.h"

// --------------------------------------------------------------
void ofApp::setup() {
	ofSetFrameRate(60);
	ofBackground(0);
}

// --------------------------------------------------------------
void ofApp::update() {
	float dt = ofGetLastFrameTime();

	for (int i = 0; i < particles.size(); i++) {
		particles[i]->update(dt);
	}

	
	for (int i = particles.size() - 1; i >= 0; i--) {
		if (particles[i]->shouldExplode()) {
			int explosionType = (int)ofRandom(4); // 0: Circular, 1: Random, 2: Star, 3: Spiral
			int numParticles = (int)ofRandom(20, 30);
			for (int j = 0; j < numParticles; j++) {
				if (explosionType == 0) {
					particles.push_back(new CircularExplosion(particles[i]->getPosition(), particles[i]->getColor()));
				} else if (explosionType == 1) {
					particles.push_back(new RandomExplosion(particles[i]->getPosition(), particles[i]->getColor()));
				} else if (explosionType == 2) {
					particles.push_back(new StarExplosion(particles[i]->getPosition(), particles[i]->getColor()));
				} else if (explosionType == 3) {
					particles.push_back(new SpiralExplosion(particles[i]->getPosition(), particles[i]->getColor()));
				}
			}
			delete particles[i];
			particles.erase(particles.begin() + i);
		} else if (particles[i]->isDead()) {
			delete particles[i];
			particles.erase(particles.begin() + i);
		}
	}
}

// --------------------------------------------------------------
void ofApp::draw() {
	for (int i = 0; i < particles.size(); i++) {
		particles[i]->draw();
	}
}

// --------------------------------------------------------------
void ofApp::createRisingParticle() {
	float minX = ofGetWidth() * 0.35;
	float maxX = ofGetWidth() * 0.65;
	float spawnX = ofRandom(minX, maxX);
	glm::vec2 pos(spawnX, ofGetHeight());
	glm::vec2 target(ofGetWidth() / 2 + ofRandom(-300, 300), ofGetHeight() * 0.10 + ofRandom(-30, 30));
	glm::vec2 direction = glm::normalize(target - pos);
	glm::vec2 vel = direction * ofRandom(250, 350);
	ofColor col;
	col.setHsb(ofRandom(255), 220, 255);
	float lifetime = ofRandom(1.5, 3.5);
	particles.push_back(new RisingParticle(pos, vel, col, lifetime));
}

// --------------------------------------------------------------
void ofApp::createSideParticle() {
	float y = ofRandom(ofGetHeight() * 0.4, ofGetHeight() * 0.9);
	bool fromLeft = ofRandom(1.0) < 0.5;
	glm::vec2 pos(fromLeft ? 0 : ofGetWidth(), y);
	glm::vec2 vel = glm::normalize(glm::vec2(fromLeft ? 1 : -1, ofRandom(-0.3, -0.6))) * ofRandom(200, 300);
	ofColor col;
	col.setHsb(ofRandom(255), 220, 255);
	float lifetime = ofRandom(1.5, 3.0);
	particles.push_back(new SideParticle(pos, vel, col, lifetime));
}

// --------------------------------------------------------------
void ofApp::createDiagonalParticle() {
	bool fromLeft = ofRandom(1.0) < 0.5;
	glm::vec2 pos(fromLeft ? glm::vec2(0, ofGetHeight()) : glm::vec2(ofGetWidth(), ofGetHeight()));
	glm::vec2 target(ofGetWidth() / 2, ofGetHeight() * 0.2);
	glm::vec2 vel = glm::normalize(target - pos) * ofRandom(250, 350);
	ofColor col;
	col.setHsb(ofRandom(255), 200, 255);
	float lifetime = ofRandom(1.8, 3.2);
	particles.push_back(new DiagonalParticle(pos, vel, col, lifetime));
}

// --------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button) {
	createRisingParticle();
}

// --------------------------------------------------------------
void ofApp::keyPressed(int key) {
	if (key == ' ') {
		for (int i = 0; i < 1000; i++) {
			createRisingParticle();
		}
	}
	if (key == 's') {
		ofSaveScreen("screenshot_" + ofToString(ofGetFrameNum()) + ".png");
	}
	if (key == '1') {
		createSideParticle();
	}
	if (key == '2') {
		createDiagonalParticle();
	}
}

// --------------------------------------------------------------
ofApp::~ofApp() {
	for (int i = 0; i < particles.size(); i++) {
		delete particles[i];
	}
	particles.clear();
}

```
1. ¿Cómo y por qué de la implementación de cada una de las extensiones solicitadas al caso de estudio?

En el caso de estudio partimos de una clase base de partículas (Particle) y fui extendiendo su comportamiento con nuevos tipos:

RisingParticle

Cómo: se implementó como partícula inicial que asciende y, tras cierto tiempo, genera una explosión.

Por qué: simula un fuego artificial antes de explotar.

CircularExplosion, RandomExplosion, StarExplosion

Cómo: se sacan de la clase base ExplosionParticle, cada uno con su lógica propia para inicializar y actualizar las trayectorias.

Por qué: permiten ver diferentes patrones de fuegos artificiales. Cada extensión aumenta la variedad visual sin modificar el código ya existente.

SpiralExplosion (nueva)

Cómo: se implementó como una clase derivada de ExplosionParticle, en la que la posición se calcula usando un ángulo que rota con velocidad angular y un radio que aumenta con el tiempo.

Por qué: agrega un nuevo tipo de explosión.

2. ¿Cómo y por qué de la implementación de los conceptos de encapsulamiento, herencia y polimorfismo en tu código?

Encapsulamiento

Cómo: cada clase tiene atributos privados (position, velocity, age, etc.) y métodos públicos controlados (update(), draw()).

Por qué: protege el estado interno de las partículas y obliga a interactuar mediante funciones, garantizando coherencia y evitando modificaciones externas no deseadas.

Herencia

Cómo: RisingParticle y todas las explosiones derivan de Particle o de ExplosionParticle.

Por qué: se reutilizan atributos comunes (posición, velocidad, color, tiempo de vida) sin duplicar código. Cada clase solo redefine lo que cambia en su comportamiento.

Polimorfismo

Cómo: se usan punteros a la clase base Particle* para almacenar y manipular todas las partículas, sin importar si en tiempo de ejecución son Rising, Circular, Random, Star o Spiral.

Por qué: permite tratar de manera uniforme a todos los objetos, pero cada uno ejecuta su versión de update() y draw() según su tipo real (polimorfismo dinámico).

3. Explica cómo verificaste que cada una de las extensiones funciona correctamente, muestra capturas de pantalla del depurador donde evidencias lo anterior, en particular el polimorfismo en tiempo de ejecución.
Pruebas visuales

Se forzó temporalmente el explosionType en el update() para generar únicamente cada tipo de explosión (ejemplo: int explosionType = 3; // Spiral), verificando que apareciera el patrón esperado.

<img width="882" height="267" alt="image" src="https://github.com/user-attachments/assets/b23d4a12-65fa-4ec6-9d56-1c80719ed632" />

<img width="819" height="563" alt="image" src="https://github.com/user-attachments/assets/ac728d2c-2cfe-4ac1-bbea-16dbf179a4cd" />


## 4.  **Consolidación, autoevaluación y cierre:**


Criterio 1: profundidad de la indagación

Mi autoevaluación: me sitúo en el nivel [logrado] porque…formulé preguntas que no solo buscaban entender cada concepto de forma aislada, sino también establecer conexiones entre ellos. Por ejemplo, traté de comprender cómo la herencia influye en el comportamiento del polimorfismo a través de estructuras internas como la vtable, y cómo el encapsulamiento puede afectar la manera en que esas relaciones se implementan en memoria. Estas preguntas muestran que busqué ir más allá de la simple definición de los conceptos, siguiendo una línea lógica de exploración que apuntaba a entender sus mecanismos internos.
Evidencias: En mis notas, hice preguntas como:

¿Cómo se organiza en memoria una clase base y sus clases derivadas?

¿Qué papel juega la vtable en el despacho dinámico de métodos polimórficos?

¿Cómo cambia el acceso a los miembros cuando aplico encapsulamiento y cómo eso afecta el polimorfismo?

Utilicé el depurador para observar cómo se crean y almacenan los objetos en memoria al aplicar herencia, verificando qué cambia en la vtable cuando redefino métodos virtuales.

Relacioné estos hallazgos con ejemplos escritos tanto en ensamblador como en C++, comprobando la traducción de conceptos de alto nivel a bajo nivel.

Criterio 2: esfuerzo cognitivo y experimentación

Mi autoevaluación: considero que mi nivel es [logrado] porque… diseñé y ejecuté experimentos específicos para comprobar el funcionamiento de los conceptos de herencia, polimorfismo y encapsulamiento, y no me limité a ejecutar el código base. Además, utilicé el depurador para recolectar evidencia del comportamiento interno de los programas, analizando paso a paso cómo se ejecutaban y cómo cambiaban los valores en memoria al aplicar cada concepto.
Evidencias: 

Modifiqué el código original creando nuevas clases derivadas que sobrescribían métodos virtuales para observar cómo se actualizaba la vtable y cómo se resolvían las llamadas polimórficas en tiempo de ejecución.

Implementé pruebas donde comparé el acceso a atributos privados, protegidos y públicos, verificando con el depurador qué miembros eran visibles desde cada contexto y cómo esto influía en la interacción entre clases.

Criterio 3: calidad del análisis y la reflexión

Mi autoevaluación: mi nivel aquí es [Excelente] porque… mi bitácora no solo verifica el funcionamiento de los conceptos, sino que explica por qué ocurren de esa forma y cuáles son sus implicaciones en el diseño. Analicé errores para extraer aprendizajes, conecté la evidencia con la teoría y construí un modelo mental coherente que integra encapsulamiento, herencia y polimorfismo como parte de un mismo sistema.

Evidencias: 
Analicé en profundidad cómo el polimorfismo se implementa en la vtable.

Evalué errores (acceso a atributos privados) para reforzar el encapsulamiento.

Reflexioné sobre las implicaciones de diseño de la herencia.

Conecté la evidencia experimental con la teoría, mostrando comprensión crítica.




Criterio 4: apropiación y articulación de conceptos

Mi autoevaluación: demuestro mi apropiación en el nivel [Excelente] porque… logré articular los conceptos de encapsulamiento, herencia y polimorfismo como partes de un mismo sistema interdependiente dentro de la programación orientada a objetos. No solo los comprendí de forma aislada, sino que construí un modelo mental coherente que explica cómo colaboran entre sí para permitir la extensibilidad y el comportamiento dinámico del software. Además, utilicé un lenguaje propio, ejemplos originales y analogías que mostraron que dominé los conceptos a un nivel transferible.
Evidencias: 
Expliqué encapsulamiento, herencia y polimorfismo como un sistema que trabaja en conjunto.

Mostré cómo el encapsulamiento protege los datos y permite aplicar polimorfismo de forma segura.

Relacioné cómo la herencia crea jerarquías que el polimorfismo usa para el despacho dinámico.

Conecté estos conceptos con su representación en memoria y en ensamblador, demostrando dominio profundo.


En una hoja de papel o un white board digital te pediré que hagas un inventario de los conceptos de las unidades 1 a la 5. Luego construye un diagrama donde ubiques todos los conceptos tratando de agruparlos y relacionarlos entre sí.

https://sharing.clickup.com/90132495685/wb/h/2ky51fa5-573/52ae501ac2143c5

Pregúntate: ¿Qué conceptos domino bien? ¿Cuáles me cuestan más trabajo?

Domino bien la herencia, me cuesta un poco los espacios en la memoria u como identificar en donde se encuentra cada objeto o procedimiento del codigo en c++.

Pregúntate para qué pueden servirte estos conceptos.

Para realizar programas mas estructurados y tener un cococimiento mayor de donde utilizar cada procedimiento, partiendo del que se quiere conseguir con el codigo. 

¿Qué hiciste bien en esta unidad que debes continuar haciendo?

Investigar y leer bien los codigos que se nos entrergan, analizarlos y comprenderlos.

¿Qué deberías comenzar a hacer para mejorar tu proceso?

utilizar la ia para mejorar el rendimiento de mi tiempo.

Formula tu plan de acción personal para abordar aquello que te cueste más trabajo.

De ahora en adelante, leeré bien las instrucciones y los codigos, los analizare y tomare nota de las cosas importante, luego puedo preguntarle a la ia que aspectos son fundamentales y debo tener presentes para luego realizar la actividad. 

> Esta sección es OBLIGATORIA y central para tu evaluación
