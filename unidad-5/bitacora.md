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
Porque hace que el atributo nombre sea privado y queno se tenga un acceso directo, pero luego en el metodo Nombre permite mediante un proceso de get set que se pueda leer y modificar de forma protegida dentro de las clases que hereden a esta.


¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?

Ademas de prevenir errores, esto hace como ya lo habia mencionado que solo la clase Figura tenga acceso directo para cmabiar el atributo nombre, esto permite que haya un constructor para las clases que herenden este metodo y que el nombre no tenga un valor no deseado.

**Herencia:**

¿Cómo se evidencia la herencia en la clase Circulo?

```c++
public class Circulo : Figura
```
Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?

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

Esto sucede porque el bucle for eache, por mas que contanga la variable fig que es de tipo Figura, este debe analizar que figura debe genenrar para poder realizar el metodo de dibujar correspondiente a cada una de las clases establecidas que cuentan con la eherencia de Figura.





***Parte 3: hipótesis sobre la implementación***

Esta es la parte más importante. Imagina que eres un diseñador de lenguajes de programación. Tienes que decidir cómo implementar estos conceptos en la memoria y en el procesador. No hay respuestas incorrectas, solo ideas. Dibuja si te ayuda.



Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?

En memoria, un objeto Rectangulo es un bloque que contiene primero los datos que se heredan de Figura y luego los propios que serian Base y Altura.

El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.




La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?



***Parte 4: y tu autoevaluación y primeras preguntas***

Has completado el diagnóstico. Ahora, reflexiona sobre tu propia experiencia y basado en esto te propongo dos caminos:

Formula la primer pregunta que comenzarás a investigar. Este será el punto de partida para tu “ruta de exploración personal”. Tu vas definiendo tus propiuas actividades.
Si prefieres la “ruta guiada” adelante. Comienza con la actividad 2.



## 2.  **La pregunta inicial**

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
