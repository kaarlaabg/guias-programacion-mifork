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

### Los cuatro pilares fundamentales son la abstracción, el encapsulamiento, la herencia y el polimorfismo. La abstracción consiste en identificar las características y comportamientos esenciales de un objeto, ignorando los detalles irrelevantes para el contexto del problema; es, en esencia, la capacidad de modelar conceptos del mundo real como entidades de software.
### El encapsulamiento es el mecanismo que agrupa datos y métodos en una unidad, restringiendo el acceso directo a los componentes internos para proteger la integridad del objeto. Por otro lado, la herencia permite que una clase nueva adquiera las propiedades y métodos de una clase existente, facilitando la reutilización de código. Finalmente, el polimorfismo permite que una misma operación se comporte de manera distinta según el objeto que la ejecute, dotando al sistema de gran flexibilidad.


## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Python, C++, Java y JavaScript


## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### La programación estructurada es un paradigma que busca mejorar la claridad y calidad de un programa utilizando únicamente tres estructuras de control: secuencia, selección (if/switch) e iteración (bucles). Este enfoque elimina el uso de saltos incondicionales (como el goto), facilitando el seguimiento del flujo lógico y la depuración del código
 
### La programación modular da un paso más allá al dividir un programa en partes independientes denominadas módulos. Cada módulo agrupa funciones relacionadas y oculta su complejidad interna, interactuando con el resto del programa a través de interfaces bien definidas. Es el precursor directo de la POO, donde la principal diferencia radica en que la POO vincula estrechamente los datos con las funciones que los manipulan.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Identidad, estado y comportamiento

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Una clase es un molde para una instancia durante la ejecucion que define la estructura del estado (atributos) y el comportamiento (modulos)

## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### Respuesta

## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### definir varios metodos con el mismo nombre sin que el compilador huya. Debemos cambiar el numero o el tipo de los parametros para cuando lo invoquemos

### Ejemplo: class Calculadora {
###             int sumar (int a, int b) {
###             return a + b;
###             }
### }

###            //ALERTA: es necesario cambiar al menos alguno de los parametros. No es suficiente, ni necesario el tipo de retorno
###            double sumar (double a, double b) {
###            return a + b;
###            }

###            main () {
###            Calculadora miCalculadora = new Calculadora ();
###            int resultado = miCalculadora.sumar(3, 5);
###            double resultado2= miCalculadora.sumar(3.7, 5.4);
###         }


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### struct Punto {
### int x;
### int y;
### } 

### double calcularDistanciaAOrigen (struct Punto punto) {
### return sqrt(punto.x * punto.x + punto.y * punto.y);
### }

### int main() {
### Punto mipunto;
### mipunto.x = 5;
### mipunto.y = 6;
    
### double distancia = calcularDistanciaAOrigen(mipunto);
### }


### -------- JAVA --------
### class Punto {
### //estado, es decir, atributos
### int x;
### int y;

### //comportamiento, es decir, metodos
### double calcularDistanciaAOrigen() {
### return Math.sqrt(x * x + y * y);
### }
### }

### public class Ejercicio1 {
###    public static void main(String[] args) {
###        Punto mipunto = new Punto();
###        mipunto.x = 5;
###        mipunto.y = 6;

###        double distancia = mipunto.calcularDistanciaAOrigen();
### }
### }    

## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### Respuesta

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### Respuesta


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Respuesta


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta
