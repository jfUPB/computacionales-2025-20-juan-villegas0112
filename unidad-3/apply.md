# Unidad 3


## 🛠 Fase: Apply

### Actividad integradora de aplicación

***1. Diagnóstico del problema (análisis):***

Cada vez que se crea un Personaje, se crea reserva memoria en el heap para guardar las estadísticas (new int[3]). Esa memoria no se libera en ningun momento porque no hay un metodo contructor, generando un gasta cada vez mas grande de memoria Ram. Por otro lado hay un error en simularEncuentro() pues Al ejecutar ```Personaje copiaHeroe = heroe;```, el compilador realiza una copia identica de los atributos. Esto significa que heroe como copiaHeroe apuntan al mismo sitio de memoria en el heap.

***2. Solución y refactorización (síntesis y creación):***

``` c++
#include <string>
#include <iostream>

class Personaje {
public:
Personaje(std::string n, int vida, int ataque, int defensa)
: nombre(n), vida(vida), ataque(ataque), defensa(defensa) {
std::cout << "Constructor: nace " << nombre << std::endl;
}

void imprimir() const {
std::cout << "Personaje " << nombre
<< " [Vida: " << vida
<< ", ATK: " << ataque
<< ", DEF: " << defensa
<< "]" << std::endl;
}

const std::string& getNombre() const { return nombre; }
int getVida() const { return vida; }
int getAtaque() const { return ataque; }
int getDefensa()const { return defensa; }

void setNombre(const std::string& n) { nombre = n; }
void setVida(int v) { vida = v; }
void setAtaque(int a) { ataque = a; }
void setDefensa(int d) { defensa = d; }

private:
std::string nombre;
int vida;
int ataque;
int defensa;
};

int main() {
Personaje heroe("Aragorn", 100, 20, 15);
heroe.imprimir();
heroe.setVida(80);
std::cout << "\nle pegan\n";
heroe.imprimir();
return 0;
}
```
***3. Justificación de la Solución:***

*- Eliminación de punteros dinámicos*

Antes: new int[3] generaba fugas de memoria.

Ahora: se usan variables simples (vida, ataque, defensa).

*- Copias seguras*

Antes: dos objetos compartían el mismo puntero (estadisticas).

Ahora: cada objeto copia sus propios datos, evitando inconsistencias.

*- Lista de inicialización en el constructor*

Mejora la eficiencia al inicializar directamente las variables.


