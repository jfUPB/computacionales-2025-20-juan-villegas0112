# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 01

🥸***Predice***🥸

Esta actividad va a permitir entender de una mejor manera como es la traduccion entre codigos, es decir, como pasa del c++ al ensamblador y del ensamblador al idioma maquina. 
Por otro lado, los breake points sirven para realizar vectores de prueba o ver como van fucionando las partes de codigo de forma que no involucren la operacion siguiente al break point.

🦕***Ejecuta***🦕

``` c++
int sum(int a, int b)
{
    return a + b;
}

int main()
{
    int a = 5;
    int b = 7;
    int c = sum(a, b);
    std::cout << "La suma de " << a << " y " << b << " es " << c << "\n";
}
```

- Break Point

<img width="825" height="147" alt="image" src="https://github.com/user-attachments/assets/b94da814-4d91-4a8c-a479-d0441781de93" />

- Ventada de depuracion Autos

<img width="917" height="151" alt="image" src="https://github.com/user-attachments/assets/0c583743-f290-477d-933e-5fe27a631ad5" />



🎰***Reflexiona**🎰

¿Para qué sirven los breakpoints?

Para deter el programa en un punto, esto sirve para realizar cambio o una experimentacion, haciendo que el resto dle codigo no se vea afectado.

¿Para qué se usa la ventana de depuración Autos?

Ver como todas las variables localaes se van definiendo mediante el programa se va ejecutando.

### Actividad 01

🥸***Predice***🥸
Esta actividad permitira ver como es la utilizacion de punteros dentro de un codigo en c++

🦕***Ejecuta***🦕

- al usar el cout se imprime un mensaje

```c++
#include <iostream>

using namespace std;

void swapPorValor(int a, int b)
{
    int cambio = b;
    b = a;
    a = cambio;
}

void swapPorReferencia(int& a, int& b)
{
    int cambio = b;
    b = a;
    a = cambio;
}

void swapPorPuntero(int* a, int* b)
{
    int cambio = *b;
    *b = *a;
    *a = cambio;
}

int main() {
    int a = 12;
    int b = 15;

    cout << "Valor inicial de a: " << a << endl;
    cout << "Valor inicial de b: " << b << endl;

    cout << "\nLlamando a swapPorValor..." << endl;
    swapPorValor(a, b);
    cout << "Despues de swapPorValor, valor de a, b: " << a << ", " << b << endl;

    cout << "\nLlamando a swapPorReferencia..." << endl;
    swapPorReferencia(a, b);
    cout << "Despues de swapPorReferencia, valor de a, b: " << a << ", " << b << endl;

    cout << "\nLlamando a swapPorPuntero..." << endl;
    swapPorPuntero(&a, &b);
    cout << "Despues de swapPorPuntero, valor de a, b: " << a << ", " << b << endl;

    return 0;
}
```
 ¿Por qué pasa?
Paso por (a):
La función recibe un tipo de copia del valor.
Si la copia cambia, el original no.

Paso por (b):
La función recibe un acceso directo al original.
Cualquier cambio dentro se ve afuera.

Paso por (c):
La función recibe la dirección del original.
Usando esa dirección, puede cambiarlo en su lugar real.

🎰***Reflexiona**🎰

Esta actividad permite entender de buena forma el funcionamiento de las diferentes fucniones que hey en el codigo, permitiendo ver como se pueden realizar cambios dentro de una variable de forma permanente o solo para la utilizacion momentanea.



