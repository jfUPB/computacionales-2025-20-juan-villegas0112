# Bitácora de aprendizaje de la unidad 6

## Actividad 01

🧐🧪✍️ Reporte

***¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.***

En la aplicacion se puede interactuar con las teclas: s, a, r y n.
- s para detener el movimiento de las particulas
- a para atraerlas al puntero del mouse
- r para alejaralas del puntero
- n para que vuelvan a la normalidad

***¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?***

Se ven diferentes tamaños y colores, cada particula tiene un movimiento diferente, con diferentes veocidades y direcciones. 


***Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.***

"a"

<img width="626" height="500" alt="image" src="https://github.com/user-attachments/assets/b5359d21-16b2-4dc1-ae6c-94af7f4c05cf" />

"r"

<img width="648" height="617" alt="image" src="https://github.com/user-attachments/assets/275bfdc3-c133-4c91-ba9c-fded7ffb761f" />

"s"
<img width="1017" height="756" alt="image" src="https://github.com/user-attachments/assets/51de3ef3-adff-42eb-b7e9-1b35c853ba01" />

"n"

<img width="538" height="550" alt="image" src="https://github.com/user-attachments/assets/22a62c1c-1651-4af6-bab4-dccaf20c56d9" />


***¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.***

Cada que yo presiono una tecla se cambia el estado de la aplicacion, y este estado le avisa a las particulas que comportamiento deben de seguir con respecto a la tecla presionada.


## Actividad 02

🧐🧪✍️ Reporte

***Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?***

El propósito del patrón Observer es crear una relación de dependencia entre objetos, en la cual uno (el sujeto) puede avisarle automáticamente a muchos otros (los observadores) cuando ocurre un cambio o evento. Este patrón es muy útil cuando se quiere mantener el acoplamiento bajo entre los componentes, haciendo que cada uno evolucione de forma independiente.

***Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.***

<img width="435" height="560" alt="image" src="https://github.com/user-attachments/assets/fcbbf165-9823-4052-a0fb-bb7391bee69b" />


***Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.***

<img width="824" height="508" alt="image" src="https://github.com/user-attachments/assets/d7382777-7fdc-4901-a737-974be17ae12e" />

***¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.***

- Menos dependencia: ofApp solo envía un aviso y cada partícula decide cómo reaccionar, sin que la aplicación tenga que saber los detalles de cada una.

- Más fácil de ampliar: si se quieren agregar nuevos tipos de partículas o comportamientos, no hay que cambiar el código de ofApp, solo la nueva partícula.

- Código más claro y ordenado: el programa se entiende y se mantiene mejor porque cada parte cumple su función sin mezclarse demasiado con las otras.

- Escala mejor: se pueden tener muchas partículas sin que la lógica central se vuelva complicada.

## Actividad 03

🧐🧪✍️ Reporte

***Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?***

- El propósito del patrón Factory Method (o en este caso, un Simple Factory) es hacer más fácil y ordenada la creación de objetos. En lugar de tener el código de creación repartido por toda la aplicación, se centraliza en   una clase o método que se encarga de fabricar esos objetos.

  El problema principal que resuelve es que el programa no tenga que saber los detalles de cómo se construye cada objeto específico. Así, si más adelante se quieren agregar nuevos tipos (como diferentes partículas en        nuestro caso), no toca modificar en muchos lados, solo en la “fábrica”. Esto ayuda a que el código sea más claro, menos repetitivo y más fácil de mantener.


***¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir nuevos tipos de partículas en el futuro.***

- Usar ParticleFactory en ofApp::setup tiene varias ventajas frente a crear y configurar las partículas directamente en ese método. Primero, ayuda a mantener el código organizado: ofApp se encarga solo de manejar la         aplicación y no de los detalles de cómo se construyen las partículas (esto va en línea con el principio de responsabilidad única). Segundo, mejora la legibilidad, porque en setup solo se ve que se crean partículas, sin    toda la lógica de inicialización repetida una y otra vez. Y tercero, facilita mucho agregar nuevos tipos de partículas en el futuro: basta con añadir la lógica en la fábrica, sin tener que tocar el código de ofApp,        manteniendo todo más limpio y fácil de mantener.

***Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?***

1. Ir a la clase ParticleFactory y dentro del método createParticle, agregar un nuevo bloque ```else if (type == "black_hole").```

   Ahí configuraría el tamaño grande (por ejemplo entre 10 y 15), el color negro (ofColor(0,0,0)) y le pondría una velocidad muy lenta.

2. No necesito modificar ofApp::setup, salvo que quiera usar este nuevo tipo allí.

   ofApp::setup seguiría igual de limpio, solo tendría que llamarlo así:

   ```c++
   Particle* p = ParticleFactory::createParticle("black_hole");
   ```


   Toda la lógica de cómo se configura esta partícula está encapsulada en la fábrica.


***El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?.***

- Ventajas de que createParticle sea estático

  Acceso directo: se puede llamar sin crear un objeto ParticleFactory (ej: ParticleFactory::createParticle("rising")), lo que simplifica el uso.

  Menos memoria: no se necesita instanciar la fábrica si no tiene atributos que mantener.

  Comodidad: es práctico cuando la fábrica solo contiene lógica para crear objetos y no necesita guardar estado interno.

- Desventajas

  Menos flexibilidad: no puedes tener diferentes fábricas con comportamientos distintos (ej: una fábrica que cree partículas rápidas y otra lentas).

  Difícil de extender: si quisieras que la fábrica tuviera configuraciones internas (colores, tamaños, reglas), con métodos estáticos no puedes, porque no hay un objeto que mantenga ese estado.

  Dificulta pruebas unitarias: testear métodos estáticos es menos flexible que instanciar fábricas diferentes en pruebas.


## Actividad 04

🧐🧪✍️ Reporte

***Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?***

- El propósito del patrón State es permitir que un objeto cambie su comportamiento de manera dinámica según el estado en el que se encuentre, sin necesidad de usar muchos if/else o switch en el código. En vez de eso, cada estado se encapsula en una clase independiente, lo que hace que el diseño sea más claro, flexible y fácil de mantener.

- Cuándo es útil aplicarlo:

     Cuando un objeto tiene varios estados internos y su comportamiento depende de esos estados.

     Cuando el código comienza a llenarse de condiciones (if/else o switch) que verifican el estado actual para decidir qué hacer.

     Cuando se necesita cambiar el comportamiento de un objeto en tiempo de ejecución, sin modificar la lógica principal.


***Dibuja un diagrama de estados simple para la clase Particle. Muestra los diferentes estados (Normal, Attract, Repel, Stop) como nodos y las transiciones entre ellos como flechas etiquetadas con el evento que las causa (p. ej., la tecla presionada: ‘n’, ‘a’, ‘r’, ‘s’).***

<img width="599" height="539" alt="image" src="https://github.com/user-attachments/assets/c8a39179-7eba-48b2-89b7-6fa05c2697fc" />


***Describe las ventajas de usar el patrón State en Particle en lugar de tener un miembro std::string estadoActual y usar un gran if/else if/else o switch dentro de Particle::update() para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).***

- Cohesión 🧩

   Cada estado (NormalState, AttractState, etc.) tiene su propio comportamiento en su propia clase.

   Esto evita que Particle tenga demasiado código mezclado y difícil de leer.

   Así, cada clase se enfoca en una sola responsabilidad (SRP: Single Responsibility Principle).

- Extensibilidad 🚀

   Si quiero agregar un nuevo estado (ejemplo: BounceState), solo creo una nueva clase que herede de State y defina update().

   No necesito tocar la lógica de los otros estados ni llenar Particle::update() con más if/else.

- Principio Abierto/Cerrado (OCP) 📖

   La clase Particle está cerrada a modificaciones pero abierta a extensiones.

   En vez de modificar Particle cada vez que aparece un nuevo estado, solo extiendo con una nueva clase de estado.

   Esto reduce el riesgo de dañar código ya probado.

- Mantenimiento más fácil 🔧

   El código con un switch gigante se vuelve difícil de leer y mantener.

   Con el patrón State, si hay un bug en el comportamiento de un estado, sé exactamente dónde buscar: en su clase correspondiente.

- Polimorfismo limpio 🎭

   Particle no necesita saber cómo se actualiza cada estado.

   Solo llama state->update(this) y delega el comportamiento dinámicamente.

***¿Qué responsabilidad tienen los métodos onEnter y onExit en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en todos los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en onEnter para AttractState o en onExit para StopState?***

En el patrón State, los métodos onEnter y onExit sirven para ejecutar código cuando una partícula entra o sale de un estado.

```onEnter(Particle * p)```: se corre al activar un nuevo estado, justo después de hacer el cambio.

```onExit(Particle * p)```: se corre antes de dejar un estado, útil para limpiar, reiniciar o guardar datos.

De esta forma, el comportamiento no se limita solo a lo que pasa en update(), sino también a las transiciones entre estados.

Ejemplos

```En AttractState::onEnter()```
Podría cambiar el color de la partícula para indicar visualmente que está siendo atraída por el mouse.
```c++
void AttractState::onEnter(Particle * particle) {
    particle->color = ofColor(255, 100, 100); // rojo suave
}
```

Así el usuario ve un feedback inmediato de que las partículas cambiaron de comportamiento.

```En StopState::onExit()```
Podría restaurar la velocidad de la partícula a un valor aleatorio para que, cuando salga de “Stop” (y vuelva a “Normal” o “Attract”), no quede estática.
```c++
void StopState::onExit(Particle * particle) {
    if (particle->velocity.lengthSquared() < 1e-4f) {
        particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
    }
}
```

De esta forma, al salir de “Stop”, la partícula recupera un movimiento inicial.

## Actividad 05

🧐🧪✍️ Reporte

<img width="1021" height="764" alt="image" src="https://github.com/user-attachments/assets/2defc762-df82-480d-b47b-6a1d9cb460b3" />


***El código fuente completo de tu proyecto openFrameworks.***

**OfApp.cpp**

```c++
#include "ofApp.h"
#include <algorithm>


void Subject::addObserver(Observer * observer) {
	if (!observer) return;
	if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
		observers.push_back(observer);
	}
}

void Subject::removeObserver(Observer * observer) {
	if (!observer) return;
	observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}

void Subject::notify(const std::string & event) {
	for (Observer * observer : observers) {
		observer->onNotify(event);
	}
}

Particle::Particle()
	: state(nullptr) {
	position = ofVec2f(ofRandomWidth(), ofRandomHeight());
	velocity = ofVec2f(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
	size = ofRandom(2.0f, 5.0f);
	color = ofColor(255);

	state = new NormalState();
	state->onEnter(this);
}

Particle::~Particle() {
	if (state) {
		state->onExit(this);
		delete state;
		state = nullptr;
	}
}

void Particle::setState(State * newState) {
	if (state) {
		state->onExit(this);
		delete state;
	}
	state = newState;
	if (state) {
		state->onEnter(this);
	}
}

void Particle::update() {
	if (state) {
		state->update(this);
	}
	keepInsideWindow();
}

void Particle::draw() {
	ofPushStyle();
	ofSetColor(color);
	ofDrawCircle(position, size);
	ofPopStyle();
}

void Particle::onNotify(const std::string & event) {
	if (event == "attract") {
		setState(new AttractState());
	} else if (event == "repel") {
		setState(new RepelState());
	} else if (event == "stop") {
		setState(new StopState());
	} else if (event == "normal") {
		setState(new NormalState());
	}
}

void Particle::keepInsideWindow() {
	const float W = static_cast<float>(ofGetWidth());
	const float H = static_cast<float>(ofGetHeight());

	if (position.x < 0.0f) {
		position.x = 0.0f;
		velocity.x *= -1.0f;
	} else if (position.x > W) {
		position.x = W;
		velocity.x *= -1.0f;
	}
	if (position.y < 0.0f) {
		position.y = 0.0f;
		velocity.y *= -1.0f;
	} else if (position.y > H) {
		position.y = H;
		velocity.y *= -1.0f;
	}
}


void NormalState::onEnter(Particle * particle) {
	particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
}

void NormalState::update(Particle * particle) {
	particle->position += particle->velocity;
}

static void steer(Particle * particle, const ofVec2f & toward, float accel, float vmax, float posScale) {
	ofVec2f dir = toward - particle->position;
	float len = dir.length();
	if (len > 1e-6f) {
		dir /= len;
		particle->velocity += dir * accel;
	}
	particle->velocity.limit(vmax);
	particle->position += particle->velocity * posScale;
}

void AttractState::update(Particle * particle) {
	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	steer(particle, mouse, /*accel*/ 0.05f, /*vmax*/ 3.0f, /*posScale*/ 0.2f);
}

void RepelState::update(Particle * particle) {
	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	ofVec2f away = particle->position - mouse;
	float len = away.length();
	if (len > 1e-6f) {
		away /= len;
		particle->velocity += away * 0.05f;
	}
	particle->velocity.limit(3.0f);
	particle->position += particle->velocity * 0.2f;
}

void StopState::update(Particle * particle) {
	particle->velocity *= 0.80f;
	if (particle->velocity.lengthSquared() < 1e-4f) {
		particle->velocity.set(0.0f, 0.0f);
	}
	particle->position += particle->velocity;
}


Particle * ParticleFactory::createParticle(const std::string & type) {
	Particle * particle = new Particle();

	if (type == "star") {
		particle->size = ofRandom(2.0f, 4.0f);
		particle->color = ofColor(255, 0, 0);
	} else if (type == "shooting_star") {
		particle->size = ofRandom(3.0f, 6.0f);
		particle->color = ofColor(0, 255, 0);
		particle->velocity *= 3.0f;
	} else if (type == "planet") {
		particle->size = ofRandom(5.0f, 8.0f);
		particle->color = ofColor(0, 0, 255);
	} else if (type == "comet") { // nuevo tipo
		particle->size = ofRandom(20.0f, 40.0f);
		particle->color = ofColor(255, 182, 193);
		particle->velocity *= 2.0f; 
	}
	return particle;
}


ofApp::~ofApp() {
	for (Particle * p : particles) {
		removeObserver(p);
		delete p;
	}
	particles.clear();
}

void ofApp::setup() {
	ofBackground(0);
	particles.reserve(100 + 5 + 10 + 3);

	for (int i = 0; i < 100; ++i) {
		Particle * p = ParticleFactory::createParticle("star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 5; ++i) {
		Particle * p = ParticleFactory::createParticle("shooting_star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 10; ++i) {
		Particle * p = ParticleFactory::createParticle("planet");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 3; ++i) { // cometa
		Particle * p = ParticleFactory::createParticle("comet");
		particles.push_back(p);
		addObserver(p);
	}
}

void ofApp::update() {
	for (Particle * p : particles) {
		p->update();
	}
}

void ofApp::draw() {
	for (Particle * p : particles) {
		p->draw();
	}
}

void ofApp::keyPressed(int key) {
	switch (key) {
	case 's':
		notify("stop");
		break;
	case 'a':
		notify("attract");
		break;
	case 'r':
		notify("repel");
		break;
	case 'n':
		notify("normal");
		break;
	default:
		break;
	}
}


```

**OfApp.h**

```c++
#pragma once

#include "ofMain.h"
#include <string>
#include <vector>

class Observer {
public:
	virtual ~Observer() = default;
	virtual void onNotify(const std::string & event) = 0;
};

class Subject {
public:
	void addObserver(Observer * observer);
	void removeObserver(Observer * observer);

protected:
	void notify(const std::string & event);

private:
	std::vector<Observer *> observers;
};

class Particle;

class State {
public:
	virtual ~State() = default;
	virtual void update(Particle * particle) = 0;
	virtual void onEnter(Particle * particle) { }
	virtual void onExit(Particle * particle) { }
};

class Particle : public Observer {
public:
	Particle();
	~Particle() override;

	Particle(const Particle &) = delete;
	Particle & operator=(const Particle &) = delete;

	void update();
	void draw();
	void onNotify(const std::string & event) override;

	void setState(State * newState);

	ofVec2f position;
	ofVec2f velocity;
	float size;
	ofColor color;

private:
	void keepInsideWindow();
	State * state;
};

class NormalState : public State {
public:
	void update(Particle * particle) override;
	void onEnter(Particle * particle) override;
};

class AttractState : public State {
public:
	void update(Particle * particle) override;
};

class RepelState : public State {
public:
	void update(Particle * particle) override;
};

class StopState : public State {
public:
	void update(Particle * particle) override;
};

class ParticleFactory {
public:
	static Particle * createParticle(const std::string & type);
};

class ofApp : public ofBaseApp, public Subject {
public:
	~ofApp() override;
	void setup() override;
	void update() override;
	void draw() override;
	void keyPressed(int key) override;

private:
	std::vector<Particle *> particles;
};


```

***Explica cómo usaste el patrón Factory para esta nueva partícula.***

Se usa el patrón Factory para crear el nuevo tipo de partícula “comet” (grande, rosada y rápida) sin tener que reescribir código en ofApp. Esto hace que el diseño sea modular, fácil de mantener y de extender.

***Describe cómo implementaste el patrón Observer para esta nueva partícula.***

El patrón Observer está implementado en el código con las clases Subject  y Observer.

ofApp hereda de Subject, entonces es el emisor de eventos.

Cada Particle hereda de Observer, entonces es un observador que reacciona cuando ofApp envía una notificación.

***Explica cómo aplicaste el patrón State a esta nueva partícula.***

El patrón State se aplicó al cometa de forma natural y sin cambios extra, porque este nuevo tipo de partícula hereda todo el sistema de estados ya existente. Lo único que cambió fue su configuración inicial, pero su comportamiento dinámico sigue controlado por las mismas clases de estado.


## Autoevaluacion 

5: realicé las 5 actividades completas y la autoevaluación.

Durante esta unidad, realicé todas las actividades, lo que me permitio aprender de los elemetros tarabajados en esta, por ultimo realicé el apply que es como la reunion de todo lo que se debia aprender durante esta unidad, lo hice correctamente y ademas con las evidencias necesarias, esto tambien lo hice en las otras actividades, evidencie todo lo que era requerido y utilice la informacion suministrada para hacer todos los ejercicios de una buena manera. 
