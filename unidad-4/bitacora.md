# Evidencias para la unidad 4

## Seek: Investigación 🔎

### 🐆Actividad 1🐆

En esta actividad vamos a analizar juntos una aplicación creativa interactiva que utiliza una lista enlazada para solucionar un reto creativo.

***ofApp.cpp:***
Donde se ejecutan los metodos de ofApp.h
```c++
pos = glm::mix(glm::vec3(pos, 0.0f), glm::vec3(target, 0.0f), 0.2);
```
 el 0.2 es la interpolacion y seria el 20%


***ofApp.h:***
Esto es lo que representa mi aplicacion; este contiene todos los atributos del ofBaseApp y los nuevos que se declaren ahi.

void setup(); inicializa las variables

void update(); actualizo mis variables

void draw(); diburjo con las variables que se estan acutializando

***main.cpp:***




## Código

Código para ofApp.h:

``` cpp
#pragma once
#include "ofMain.h"

// Nodo de la cola
struct Node {
	float x, y;
	float radius;
	ofColor color;
	float opacity;
	Node * next;

	Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
		: x(_x)
		, y(_y)
		, radius(_radius)
		, color(_color)
		, opacity(_opacity)
		, next(nullptr) {
	}
};

// Implementación manual de una cola (FIFO)
class BrushQueue {
public:
	Node * front;
	Node * rear;
	int size;
	int maxSize;

	BrushQueue(int _maxSize);
	~BrushQueue();

	void enqueue(float x, float y, float radius, ofColor color, float opacity);
	void dequeue();
	void clear();
	bool isEmpty();
};

// Constructor
BrushQueue::BrushQueue(int _maxSize)
	: front(nullptr)
	, rear(nullptr)
	, size(0)
	, maxSize(_maxSize) { }

// Destructor
BrushQueue::~BrushQueue() {
	clear();
}

// Implementa aquí `enqueue()`
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
	// TODO: crear un nuevo nodo y agregarlo al final de la cola.
	Node * newNode = new Node(x, y, radius, color, opacity);

	// Si la cola supera `maxSize`, eliminar el nodo más antiguo con `dequeue()`.
	if (isEmpty()) {
		front = rear = newNode;

	} else {
		rear->next = newNode;
		rear = newNode;
	}

	size++;

	while (size > maxSize) {
		dequeue();
	}
	
	
}

// Implementa aquí `dequeue()`
void BrushQueue::dequeue() {
	// TODO: eliminar el nodo más antiguo si la cola no está vacía.
	if (!isEmpty()) {
		Node * temp = front;
		front = front->next;
		delete temp;
		size--;

		if (front == nullptr) {
			rear = nullptr;
		}
	}
}

// Implementa aquí `clear()`
void BrushQueue::clear() {
	// TODO: eliminar todos los nodos de la cola.
	while (!isEmpty()) {
		dequeue();
	}
}

// Implementa aquí `isEmpty()`
bool BrushQueue::isEmpty() {
	// TODO: retornar si la cola está vacía.
	return front == nullptr;
}

class ofApp : public ofBaseApp {
public:
	BrushQueue strokes; // Cola de trazos
	float backgroundHue = 0;

	ofApp()
		: strokes(50) { } // Tamaño máximo de la cola

	void setup();
	void update();
	void draw();
	void keyPressed(int key);
};


```

Código para ofApp.cpp:

``` cpp
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
	ofBackground(0);
}

//--------------------------------------------------------------
void ofApp::update() {
	backgroundHue += 0.2;
	if (backgroundHue > 255) backgroundHue = 0;

	// TODO: agregar un nuevo trazo si el mouse está presionado.
	// Usa strokes.enqueue(x, y, radius, color, opacity);
	if (ofGetMousePressed(0)) {
		float radius = ofRandom(5, 15);
		ofColor color = ofColor ::fromHsb(ofRandom(0, 255), 200, 255);
		float opacity = 150;

		strokes.enqueue(ofGetMouseX(), ofGetMouseY(), radius, color, opacity);
	}
	
}

//--------------------------------------------------------------
void ofApp::draw() {
	// Fondo con gradiente dinámico
	ofColor color1, color2;
	color1.setHsb(backgroundHue, 150, 240);
	color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
	ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

	// TODO: dibujar los trazos almacenados en la cola.
	// Node* current = strokes.front;
	// Recorre los nodos desde strokes.front hasta nullptr y usa ofDrawCircle().
	Node * current = strokes.front;

	while (current != nullptr) {
		ofSetColor(current->color, current->opacity);
		ofDrawCircle(current->x, current->y, current->radius);
		current = current->next;
	}
	
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
	if (key == 'c') {
		// TODO: limpiar la cola de trazos.
		strokes.clear();
	}
	if (key == 'a') {
		// TODO: alternar entre 50 y 100 trazos.
		if (strokes.maxSize == 50) {
			strokes.maxSize = 100;
		} else {
			strokes.maxSize = 50;
		}
	} else if (key == 's') {
		// TODO: guardar el frame actual.
		ofSaveScreen("screenshot_" + ofGetTimestampString() + ".png");
	}
}


```

Código para main.cpp:
``` cpp

#include "ofMain.h"
#include "ofApp.h"

//========================================================================
int main( ){

	//Use ofGLFWWindowSettings for more options like multi-monitor fullscreen
	ofGLWindowSettings settings;
	settings.setSize(1024, 768);
	settings.windowMode = OF_WINDOW; //can also be OF_FULLSCREEN

	auto window = ofCreateWindow(settings);

	ofRunApp(window, std::make_shared<ofApp>());
	ofRunMainLoop();

}


```

## Demostración:

[Aquí está el video demostrativo de mi aplicación](url del video no listado en youtube)



