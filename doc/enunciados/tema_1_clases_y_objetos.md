<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### Las cuatro características fundamentales son la abstracción, el encapsulamiento, la herencia y el polimorfismo. La abstracción permite enfocarse en las propiedades y comportamientos esenciales de un objeto, ignorando los detalles no relevantes para el problema actual. El encapsulamiento consiste en agrupar los datos y los métodos que los manipulan, protegiendo el estado interno del objeto frente a accesos externos no deseados.

### La herencia es el mecanismo por el cual una clase nueva (clase hija) adquiere las propiedades y métodos de una clase ya existente (clase padre), facilitando la reutilización del código. Por último, el polimorfismo permite que una misma operación se comporte de manera distinta según el objeto que la realice, permitiendo tratar objetos de diferentes clases de forma uniforme si comparten una raíz común.


## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Java, C++, Python y JavaScript


## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### La programación estructurada es un paradigma que se basa en dividir el programa en bloques lógicos utilizando estructuras de control (secuencias, selecciones y ciclos) y subrutinas (funciones). En lugar de saltos arbitrarios de código, se busca un flujo lineal y legible, siendo C el ejemplo clásico de este enfoque.

### Por su parte, la programación modular da un paso más al organizar el código en unidades separadas llamadas módulos. Cada módulo agrupa funciones y datos relacionados, ocultando su implementación interna y exponiendo solo una interfaz necesaria para interactuar con el resto del sistema, lo que facilita enormemente el mantenimiento y la escalabilidad de proyectos grandes.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Un objeto se define por tres elementos clave: estado, comportamiento e identidad. El estado está representado por los datos o atributos que posee el objeto en un momento determinado (similar a los campos de un struct en C).

### El comportamiento viene definido por los métodos o funciones que el objeto puede ejecutar y que, por lo general, operan sobre su propio estado. Finalmente, la identidad es lo que diferencia a un objeto de otro, incluso si ambos tienen el mismo estado; en términos de memoria, se puede ver como la dirección única donde reside el objeto.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Una clase es una plantilla o plano que define la estructura y el comportamiento que tendrán los objetos creados a partir de ella. No es un objeto en sí, sino la definición teórica. Un objeto es la entidad concreta que se crea siguiendo ese plano, mientras que el término instancia se refiere al acto de materializar una clase; decir que un objeto es una "instancia de una clase" es técnicamente lo más preciso.

### No todos los lenguajes orientados a objetos manejan el concepto de clase. Existen lenguajes como JavaScript (en sus versiones originales) que utilizan la "herencia basada en prototipos", donde los objetos se crean clonando otros objetos en lugar de seguir una plantilla predefinida como ocurre en Java o C++.


## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### En Java, los objetos se almacenan siempre en el Heap (memoria dinámica), mientras que las variables locales y las referencias a esos objetos residen en el Stack. Esto difiere de C, donde un programador puede decidir crear una estructura tanto en el stack como en el heap manualmente mediante malloc.

### La recolección de basura (Garbage Collection) es un proceso automático del entorno de ejecución que identifica y libera la memoria de los objetos que ya no tienen ninguna referencia apuntándoles. Esto evita las fugas de memoria (memory leaks) que son tan comunes en C cuando se olvida ejecutar un free.


## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Un método es una función que está definida dentro de una clase y que opera sobre los datos de los objetos de esa clase. A diferencia de las funciones globales en C, un método siempre tiene un contexto vinculado al objeto que lo invoca.

### La sobrecarga de métodos consiste en definir varios métodos con el mismo nombre dentro de la misma clase, pero con diferentes parámetros (en cantidad o tipo). El compilador decide cuál ejecutar basándose en los argumentos proporcionados en la llamada, lo que permite ofrecer distintas formas de realizar una acción similar.


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### class Punto {
###    double x; // Atributo x
###    double y; // Atributo y
###
###    double calculaDistanciaAOrigen() {
###        return Math.sqrt(x * x + y * y);
###    }
### }

### // Ejemplo de uso
### public class Principal {
###    public static void main(String[] args) {
###        Punto miPunto = new Punto();
###        miPunto.x = 3;
###        miPunto.y = 4;
###        System.out.println("Distancia: " + miPunto.
#### calculaDistanciaAOrigen());
###    }
### }


## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### El punto de entrada en Java es el método public static void main(String[] args). La palabra clave static indica que el método pertenece a la clase y no a una instancia específica, lo que permite al sistema ejecutarlo sin haber creado primero un objeto de esa clase.

### static no se usa solo para el main; puede emplearse en variables para crear "variables de clase" compartidas por todos los objetos. Cuando se combina con final, se crean constantes, ya que final impide que el valor de una variable sea modificado una vez asignado, similar a const en C pero con matices de tiempo de ejecución.

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Java no se compila a código máquina nativo (binario del procesador), sino a un código intermedio llamado Byte-code. El comando javac Programa.java genera un archivo .class que contiene estas instrucciones. Luego, el comando java Programa lanza la Máquina Virtual de Java (JVM) para interpretar ese byte-code.

### La JVM es lo que permite la portabilidad: el mismo archivo .class puede ejecutarse en Windows, Linux o Mac, siempre que exista una JVM instalada para ese sistema. Por tanto, se dice que Java es un lenguaje tanto compilado (a byte-code) como interpretado (por la JVM).


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### class Empleado {
###    String dni;
###    String nombre;
###    String apellidos;

###    // Constructor
###    Empleado(String dni, String nombre, String apellidos) {
###        this.dni = dni;
###        this.nombre = nombre;
###        this.apellidos = apellidos;
###    }
### }


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### La referencia this es un puntero implícito que apunta al objeto actual que está ejecutando el método. Se utiliza principalmente para evitar ambigüedades cuando los nombres de los parámetros del constructor o método coinciden con los nombres de los atributos de la clase.

### En otros lenguajes como Python se denomina self, y en PHP se usa $this. En el ejemplo de la clase Punto, su uso quedaría así:

### void setCoordenadas(double x, double y) {
###    this.x = x; // 'this.x' es el atributo, 'x' es el parámetro
###    this.y = y;
### }


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### double distanciaA(Punto otroPunto) {
###    double difX = this.x - otroPunto.x;
###    double difY = this.y - otroPunto.y;
###    return Math.sqrt(difX * difX + difY * difY);
### }


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### En Java, los objetos se pasan por referencia (técnicamente es una copia del valor de la referencia). Si se modifica un atributo de un objeto Punto dentro de un método, el cambio sí afecta al objeto original fuera del método, ya que ambos apuntan al mismo lugar en la memoria.

### Sin embargo, los tipos primitivos (como int, double, boolean) se pasan por copia. Si un método recibe un int y lo modifica internamente, el valor de la variable original fuera del método permanecerá inalterado, comportándose de forma idéntica a las funciones estándar en C.


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### El método toString() se utiliza para obtener una representación en cadena de texto de un objeto. Existe en casi todos los lenguajes de alto nivel (en Python es __str__). En Java, todas las clases lo heredan automáticamente, pero suele "sobrescribirse" para que devuelva información útil en lugar de la dirección de memoria.

### @Override
### public String toString() {
###    return "Punto(x=" + x + ", y=" + y + ")";
### }


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Una clase se parece a un struct en cuanto a que ambos definen una agrupación de datos. Sin embargo, a un struct de C le falta el concepto de encapsulamiento de comportamiento: las funciones en C son externas y no "pertenecen" al dato.

### Para que un struct fuera como una clase, debería poder contener punteros a funciones internamente y gestionar niveles de visibilidad (como private o public). Además, el struct en C no tiene mecanismos nativos de herencia ni constructores automáticos.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### struct Punto {
###    double x, y;
### };

### double calculaDistanciaAOrigen(struct Punto* p) {
###    return sqrt(p->x * p->x + p->y * p->y);
### }

### Lo que en Java es miPunto.calculaDistanciaAOrigen(), en C sería calculaDistanciaAOrigen(&miPunto). El concepto de this simplemente ha pasado de ser un parámetro explícito y visible en C a ser un parámetro implícito y automático gestionado por el compilador en Java.