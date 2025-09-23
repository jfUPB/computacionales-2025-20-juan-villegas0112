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


***¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.***

