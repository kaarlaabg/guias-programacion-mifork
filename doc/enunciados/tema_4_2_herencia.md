<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Herencia". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación, Excepciones y Composición.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 4.2. Herencia

## 1. En orientación a objetos, ¿qué es la **herencia** y su relación con "A es-un B"?. Explica las dos implicaciones principales: (1) **compatibilidad de tipos** y (2) **herencia de estado y comportamiento**. Pon un ejemplo en Java muy sencillo, donde un `Soldado` tiene un `nombre` (privado) y un método `saludar()` que muestra su nombre. Hay dos subtipos: un `Artillero`, que es capaz de disparar cohetes y un `Zapador` que pone minas, ambos heredan el atributo nombre y la capacidad de saludar. Además, y de forma específica, el artillero tiene un número de cohetes y el zapador un número de minas, accesibles mediante "getters" específicos. Respecto a la compatibilidad de tipos, aprovechémosla: crea un array de `Soldado`, mete varios de distinto tipo (son todos compatibles con `Soldado`). Recórrela y que todos te saluden.

### La herencia es un mecanismo de programación orientada a objetos que permite crear nuevas clases a partir de clases existentes. Se basa en la relación semántica "es-un": un Artillero es un Soldado. Esto implica que la subclase (hija) es una especialización de la superclase (padre), adquiriendo de forma automática sus características y capacidades.

### Esta relación tiene dos implicaciones fundamentales. Primero, la herencia de estado y comportamiento, donde la subclase recibe los atributos y métodos de la superclase, evitando la duplicación de código. Segundo, la compatibilidad de tipos, que permite tratar a un objeto de la subclase como si fuera del tipo de la superclase. Esto facilita el polimorfismo, permitiendo que un array de tipo general almacene objetos específicos.


## 2. Al crear los soldados concretos, ¿cuántos constructores se ejecutan y en qué orden? ¿Qué significa `super` dentro de un constructor? Si la clase base no tiene visible el constructor sin parámetros, ¿debo llamar a `super` siempre? 

### Cuando se instancia una subclase, se produce una cadena de llamadas a los constructores. Siempre se ejecuta primero el constructor de la superclase y luego el de la subclase. Esto garantiza que la parte del objeto que corresponde a la jerarquía superior esté correctamente inicializada antes de añadir las particularidades de la clase hija. Es un proceso recursivo que sube hasta la cima de la jerarquía.

### La palabra reservada super se utiliza dentro de un constructor para invocar explícitamente a un constructor específico de la superclase. Si la clase base no tiene un constructor sin parámetros (constructor por defecto), es obligatorio llamar a super en la primera línea del constructor de la subclase, pasando los argumentos necesarios. De lo contrario, Java intentaría llamar a un constructor vacío inexistente y el código no compilaría.

## 3. Respecto a los objetos de subclases en memoria, los atributos privados de la superclase, ¿forman parte de una instancia de la subclase en memoria? En caso afirmativo ¿implica que se puedan usar desde el código de la subclase? Explícalo con el ejemplo de `Soldado` y alguna de sus subclases.

### En la memoria, una instancia de una subclase es un bloque único que contiene todos los atributos definidos en su jerarquía, incluidos los privados de la superclase. Aunque el Zapador no pueda ver directamente el atributo nombre del Soldado por ser private, dicho dato reside físicamente dentro del objeto Zapador. Es una estructura única, similar a como en C una struct anidada contiene los campos de la estructura interna.

### Sin embargo, que el atributo exista en memoria no significa que sea accesible desde el código de la subclase. La encapsulación sigue vigente: la subclase no puede modificar ni leer directamente los campos privados de su padre. Para interactuar con ellos, debe utilizar los métodos públicos o protegidos que la superclase proporcione (como el constructor o un "getter"). Esto protege la integridad de los datos definidos en la clase base.

## 4. ¿Qué implica en términos de **extensibilidad** de código el hecho de que sean compatibles a nivel de tipos? Ilustra esto añadiendo un nuevo tipo de `Soldado` y demostrando que el código para pedir el saludo a todos los soldados no se modifica.

### La compatibilidad de tipos es un pilar de la extensibilidad. Permite escribir código que trabaje con la superclase (el tipo más general) y que este siga funcionando sin cambios cuando se añaden nuevas subclases en el futuro. El sistema se vuelve "abierto a la extensión pero cerrado a la modificación", un principio fundamental en el diseño de software robusto.

### Si se añade un Medico, el código que recorre el array de Soldado para pedir saludos no necesita ser tocado. El nuevo objeto es, por definición, un Soldado, por lo que el método saludar() está garantizado.


## 5. En Java, cuando trabajo con referencias y herencia. ¿Puedo tener una referencia del supertipo que apunte a objetos reales de un subtipo? ¿Puedo invocar con la referencia del supertipo a métodos públicos del subtipo? ¿En qué consiste el **"upcasting"** y el **"downcasting"**? ¿Qué es el `instanceof`? Pon un ejemplo de recorrido de un array de `Soldado`, comprobando que, si el objeto real es un `Artillero`, solicite el número de cohetes que tiene y los imprima.

### Es perfectamente posible que una referencia de supertipo (Soldado) apunte a un objeto de subtipo (Artillero). A esto se le llama upcasting y es automático y seguro. Sin embargo, a través de esa referencia solo se pueden invocar métodos definidos en Soldado. Para acceder a los métodos específicos de Artillero (como getCohetes()), se debe realizar un downcasting, que es una conversión explícita de tipo.

### El operador instanceof se utiliza para verificar de forma segura si un objeto pertenece a una clase determinada antes de intentar el downcasting. Esto evita errores en tiempo de ejecución (excepciones de cast). En el ejemplo, se recorre el array y se extrae información específica solo si el soldado resulta ser un artillero.


## 6. Respecto a la ocultación de información y herencia, ¿qué significa acceso **"protegido"** de métodos y/o atributos? ¿Cómo se implementa en Java? Pon un ejemplo de uso de en la clase `Soldado` para que su nombre sea protegido y pueda usarse en el método de poner bombas del `Zapador`.

### El modificador de acceso protected es un nivel intermedio entre public y private. Un miembro (atributo o método) declarado como protegido es accesible para la propia clase, para todas sus subclases (independientemente del paquete donde estén) y para otras clases dentro del mismo paquete. Es una forma de "abrir" la cápsula solo a la familia de clases relacionadas.

### Se implementa en Java mediante la palabra protected. En el caso del Zapador, si el nombre del Soldado fuera protegido, el zapador podría concatenar ese nombre directamente en sus mensajes específicos sin necesidad de usar un método intermedio, facilitando la integración interna de la jerarquía.


## 7. En los lenguajes orientados a objetos ¿hay una **clase base** para todos los objetos? ¿Ocurre en todos los lenguajes? ¿Qué ocurre en Java?

### En Java, existe una clase base para absolutamente todos los objetos: la clase Object. Cualquier clase que se defina, si no indica explícitamente que hereda de otra mediante extends, hereda automáticamente de Object. Esto garantiza que todos los objetos en Java compartan comportamientos mínimos, como la capacidad de compararse (equals()) o de convertirse a texto (toString()).

### Esta característica no ocurre en todos los lenguajes. En C++, por ejemplo, no existe una raíz única obligatoria; se pueden crear múltiples jerarquías de clases totalmente independientes entre sí. Java optó por un modelo de raíz única para simplificar la gestión de memoria y permitir que estructuras de datos generales puedan almacenar cualquier tipo de objeto.


## 8. ¿Qué es la **"herencia múltiple"**? ¿Existe en Java herencia múltiple?

### La herencia múltiple es la capacidad de una clase de heredar de más de una superclase simultáneamente (por ejemplo, que una ClaseC herede de ClaseA y ClaseB). Esto puede generar conflictos de ambigüedad si ambas superclases tienen métodos con el mismo nombre pero distinto comportamiento (el conocido "problema del diamante").

### En Java no existe la herencia múltiple de clases. Una clase solo puede tener una única madre directa (extends). Java evita así las complejidades y errores derivados de la ambigüedad. Para lograr objetivos similares de polimorfismo múltiple sin los riesgos de la herencia, Java utiliza las "Interfaces", que se estudian en temas posteriores.


## 9. Las excepciones en los lenguajes orientados a objetos son objetos. Por tanto, se pueden crear excepciones personalizadas. Pon un ejemplo en Java de una excepción personalizada (`UsuarioNoEncontradoException`), que sea *no controlada* y que además este compuesto con un `Usuario`, para saber qué `Usuario` dio el problema. Permite además que se pueda incluir la causa, es decir, sobrecarga el constructor para tener una versión que permita añadir la causa subyacente. 

### Puesto que las excepciones son objetos, se pueden extender para llevar información contextual. Para crear una excepción no controlada, se debe heredar de RuntimeException. Al incluir un objeto Usuario por composición dentro de la excepción, se facilita la depuración al saber exactamente quién causó el error.

### Es una buena práctica incluir un constructor que acepte la "causa" (otra excepción), lo cual permite el encadenamiento de excepciones. Esto es útil cuando una excepción de bajo nivel (como un error de base de datos) provoca nuestra excepción de negocio (UsuarioNoEncontradoException).


## 10. Herencia vs. Composición. Se dice que no se debe emplear herencia simplemente por reutilizar código, es decir, que si quiero reutilizar código simplemente, no debo pensar en herencia como primera opción ¿por qué?

### No se debe usar la herencia solo para reutilizar código porque esto crea un acoplamiento extremadamente fuerte. Si la clase A hereda de B solo para usar una función de cálculo, A queda ligada de por vida a toda la estructura de B, incluso a las partes que no necesita. La herencia debe reflejar una relación de naturaleza conceptual ("es-un"), no una conveniencia técnica.

### Cuando se hereda por error, se exponen métodos de la superclase que quizás no tengan sentido en la subclase, violando el principio de diseño de interfaces limpias. Si solo se desea usar una funcionalidad, es preferible que la clase "tenga" una instancia de la otra (composición) y delegue el trabajo en ella.


## 11. Herencia vs. Composición. Se dice que se debe *"favorecer la composición frente a la herencia"*, ¿por qué?

### El principio de "favorecer la composición frente a la herencia" se basa en que la composición es mucho más flexible y menos arriesgada. La composición permite cambiar el comportamiento en tiempo de ejecución (podemos cambiar el objeto contenido por otro), mientras que la herencia es estática y se decide en tiempo de compilación.

### Además, la composición facilita las pruebas unitarias y el mantenimiento, ya que las clases permanecen independientes y solo se comunican a través de interfaces bien definidas. La herencia suele crear jerarquías rígidas y profundas que son muy difíciles de modificar cuando los requisitos del sistema cambian.


## 12. Herencia vs. Composición. Se dice que la *"herencia rompe la encapsulación"*, ¿a qué se refiere esto?

### Se dice que la herencia rompe la encapsulación porque la subclase depende de los detalles de implementación de la superclase. Si un programador cambia el funcionamiento interno de un método en la superclase, puede romper accidentalmente el comportamiento de todas las subclases que dependen de él o que lo sobrescriben, a pesar de que la interfaz pública no haya cambiado.

### Este fenómeno se conoce como el "problema de la fragilidad de la clase base". A diferencia de la composición, donde la relación ocurre estrictamente a través de métodos públicos, en la herencia la frontera entre lo que es interno y lo que es externo se difumina, haciendo que el mantenimiento sea más peligroso.


## 13. Pongamos un ejemplo de dos alternativas para lo mismo. Tenemos un `Estudiante` y un `Trabajador`, ambos tienen datos en común: el DNI y el nombre. Modelemos esto de dos formas: uno por herencia, con una superclase `Persona`, y otro con composición, con una clase `DatosPersonales`. Se debe recibir una instancia de `DatosPersonales` en el constructor de la clase `Estudiante` y `Trabajador`.

### En el modelo de herencia, tanto Estudiante como Trabajador son tipos de Persona. El estado común reside arriba. En el modelo de composición, ambos objetos contienen una referencia a una clase externa que almacena sus datos, permitiendo incluso que un objeto cambie de rol más fácilmente.

### La opción de composición permitiría, por ejemplo, que un Estudiante y un Trabajador compartan la misma instancia física de DatosPersonales, evitando duplicidad de información si una persona cumple ambos roles.
