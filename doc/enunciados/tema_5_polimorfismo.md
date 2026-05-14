<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Polimorfismo". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación, Excepciones, Composición y Herencia.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 5. Polimorfismo

## 1. Brevemente, ¿qué es el **"polimorfismo"** y para qué sirve en programación orientada a objetos? ¿qué es la **"sobreescritura"** de métodos?

### El polimorfismo es la capacidad que tienen los objetos de diferentes clases de responder de manera distinta a un mismo mensaje (o llamada a un método). Etimológicamente significa "muchas formas", y en programación orientada a objetos permite tratar a objetos de distintas subclases de manera uniforme a través de una referencia de su superclase, delegando en cada objeto la ejecución de su comportamiento específico. Esto es fundamental para reducir la dependencia entre el código que usa los objetos y las clases concretas.

### La sobreescritura (overriding) es la herramienta técnica que hace posible el polimorfismo. Consiste en volver a definir en una subclase un método que ya existía en la superclase, manteniendo la misma firma (nombre, parámetros y retorno). Al sobreescribir, la subclase proporciona una implementación propia que anula o especializa la versión de la clase padre para ese tipo de objeto en particular.


## 2. ¿En qué consiste la **"ligadura dinámica"** o **"enlace tardío"**? ¿qué relación tiene con el polimorfismo? ¿hay que indicarlos explícitamente al programar o depende esto del lenguaje? Compara C++ y Java. Indicalo después también para Python.

### La ligadura dinámica es el mecanismo por el cual el entorno de ejecución decide qué implementación de un método debe ejecutarse justo en el momento de la llamada, basándose en el tipo real del objeto al que apunta la referencia, y no en el tipo de la referencia misma. Si se tiene una referencia de tipo Soldado que apunta a un Artillero, al llamar a un método sobreescrito, la ligadura dinámica garantiza que se ejecute el código de Artillero.

### En C++, por defecto la ligadura es estática (en tiempo de compilación). Para habilitar el polimorfismo, se debe indicar explícitamente mediante la palabra clave virtual en la función de la clase base. En Java, por el contrario, la ligadura dinámica es el comportamiento por defecto para todos los métodos no estáticos y no privados; no es necesario indicarlo. En Python, al ser un lenguaje puramente dinámico, el polimorfismo es inherente y no requiere ninguna declaración especial, permitiendo incluso lo que se conoce como "duck typing".


## 3. Pon un ejemplo sencillo en Java, de un `Soldado`, con un método `saluda`, con dos subclases: `Zapador` y `Artillero`, donde `Zapador` sobreescribe el método `saludar`, sustituyendo por completo su comportamiento. Ilustra el funcionamiento del polimorfismo creando un array de `Soldados` de dos tipos y luego recorriéndolo empleando referencias de tipo `Soldado` y llamando a `saludar`.

### Respuesta


## 4. Si sobreescribo un método, ¿puedo invocar el método base para trabajar a partir de su resultado? Haz que zapador cambie ligeramente la forma de saludar, que salude de forma normal, tal cual hace el soldado base, pero que además añada un "ZAPADOR A SUS ORDENES" ¿qué palabra clave del lenguaje has usado para invocar al método de la clase base?

### Cuando se sobreescibe un método, es habitual querer aprovechar la lógica que ya existía en la clase base en lugar de sustituirla por completo. Para invocar la versión del método de la superclase desde dentro de la subclase, se utiliza la palabra clave super. Esto permite extender el comportamiento en lugar de simplemente reemplazarlo, manteniendo la coherencia de la jerarquía.


## 5. Al sobreescribir un método en Java, ¿qué restricciones existen sobre los tipos de los parámetros y el tipo de retorno? ¿Qué diferencia hay entre sobreescritura (*overriding*) y sobrecarga (*overloading*)? ¿Para qué sirve la anotación `@Override` y por qué es recomendable usarla siempre?

### En Java, para que un método sea una sobreescritura válida, debe mantener exactamente la misma lista de parámetros y un tipo de retorno compatible (igual o un subtipo, conocido como retorno covariante). La sobrecarga (overloading), a diferencia de la sobreescritura, ocurre cuando se crean varios métodos con el mismo nombre pero con distinta lista de parámetros en la misma clase. Mientras la sobreescritura se resuelve en tiempo de ejecución (polimorfismo), la sobrecarga se resuelve en tiempo de compilación.

### La anotación @Override se utiliza para informar al compilador de que la intención es sobreescibir un método de la superclase. Es altamente recomendable porque, si se comete un error tipográfico en el nombre o en los parámetros, el compilador lanzará un error en lugar de crear un método nuevo por error (que sería una sobrecarga accidental).


## 6. Entonces, cuando se estudia Java, ¿se emplea el polimorfismo desde el principio? Por ejemplo, sobreescribiendo `toString` o sobreescribiendo `equals`, ¿ya estoy usando polimorfismo?

### Efectivamente, el polimorfismo se utiliza en Java desde los primeros pasos, incluso de forma inconsciente. Como todas las clases en Java heredan de la clase Object, cualquier clase tiene acceso a métodos como toString() o equals(). Al redefinir estos métodos en una clase propia para que devuelvan una representación textual coherente o para comparar atributos específicos, se está practicando la sobreescritura.

### Cuando se utiliza un objeto en un contexto que requiere una cadena de texto (como System.out.println(objeto)), Java llama internamente al método toString(). Gracias al polimorfismo, si la clase ha sobreescrito ese método, se ejecutará su versión personalizada, demostrando que el polimorfismo es la base sobre la cual se construye gran parte del comportamiento de la API estándar de Java.


## 7. ¿Qué es una **"clase abstracta"**? ¿Qué es un **"método abstracto"**? ¿Puedo crear instancias de una clase abstracta? Pongamos un ejemplo en Java: Redefinamos `Soldado`, hagamos que, además del método `saluda` que ya tenía, tenga un método `atacar`, que sea abstracto y que cada tipo de soldado haga su acción cuando se le pida atacar. ¿Donde debemos poner `abstract`?

### Una clase abstracta es una clase que no se puede instanciar (no se puede hacer new de ella) y que sirve exclusivamente como molde o base para otras subclases. Se utiliza para representar conceptos genéricos que no tienen una existencia concreta por sí mismos. Un método abstracto es aquel que se declara en la clase base pero no tiene implementación (no tiene cuerpo); es una "promesa" de que todas las subclases tendrán ese método.

### Si una clase contiene al menos un método abstracto, la clase obligatoriamente debe ser declarada como abstracta. La palabra clave abstract se coloca tanto en la firma de la clase como en la del método. Esto obliga a las subclases a proporcionar una implementación real para ese método si quieren dejar de ser abstractas.


## 8. ¿Qué efecto tiene la palabra clave `final` sobre métodos y clases en Java? ¿Cómo se relaciona con el polimorfismo? ¿Conoces algún ejemplo de clase `final` en la propia API estándar de Java?

### La palabra clave final actúa como el opuesto directo del polimorfismo. Si se aplica a un método, impide que las subclases puedan sobreescribirlo, asegurando que el comportamiento definido sea inalterable. Si se aplica a una clase, impide que se puedan crear subclases de ella, "cerrando" la jerarquía de herencia.

### Esto se utiliza por seguridad o eficiencia, cuando se quiere garantizar que nadie cambie la lógica de una clase crítica. Un ejemplo clásico en la API de Java es la clase String. Al ser final, se garantiza que el comportamiento de las cadenas de texto sea siempre el mismo y no pueda ser alterado por terceros, lo cual es vital para la seguridad y el manejo de memoria del lenguaje.


## 9. En Java, qué son las **"interfaces"**? ¿Son como clases abstractas? ¿Una clase puede implementar más de una interfaz?

### Las interfaces son contratos que definen un conjunto de métodos que una clase debe implementar, pero no especifican cómo. A diferencia de las clases abstractas (que pueden tener atributos y métodos con código), las interfaces tradicionalmente solo contenían firmas de métodos públicos y constantes. Son tipos puramente abstractos que definen "lo que un objeto puede hacer" más que "lo que un objeto es".

### Una diferencia fundamental es que, mientras Java solo permite heredar de una clase (extends), permite que una clase implemente múltiples interfaces (implements). Esto permite que un objeto tenga múltiples comportamientos o "roles" independientes de su jerarquía de herencia, facilitando un diseño mucho más flexible y desacoplado que la herencia tradicional.


## 10. Vamos a poner un ejemplo nuevo con polimorfismo. Queremos implementar una clase `Punto`, con un método `calcularDistanciaA`, que permite calcular la distancia a otro `Punto`. Sin embargo, como queremos trabajar con puntos 2D y 3D, haz que ese método sea abstracto y haya dos implementaciones de ese cálculo de distancia. Emplea `instanceof` y *downcasting* para verificar que se recibe un punto compatible y poder calcular correctamente la distancia siempre entre puntos del mismo subtipo. Aprovecha este diseño para crear ahora una clase `Linea`, que acepta `Punto`, sin saber de qué tipo es, y es capaz de dar su longitud independientemente de las dimensiones de sus puntos (las cuales desconoce).

### Respuesta


## 11. ¿Qué es la **"herencia de interfaces"** en Java? ¿Existe **"herencia múltiple de interfaces"**? Pon un ejemplo de una interfaz `Fichero` que tenga un método para leer su contenido en forma de `String` y luego dicha interfaz sea extendida por otra que sea `FicheroEscribible` que permita enviar contenido e incluso eliminar el fichero.

### Respuesta
