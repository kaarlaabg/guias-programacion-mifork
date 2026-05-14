<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Composición". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación y Excepciones.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 4.1. Composición


## 1. En C, podemos crear estructuras mayores **componiendo** unas con otras, que suelen describirse como "A tiene-un/tiene-varios B". Pon un ejemplo, empleando `struct`, de una línea de puntos, donde puntos tienen dos coordenadas (`x` e `y`), y la línea esta hecha de dos puntos. Incluye una función para calcular la distancia entre puntos y otra para hallar la longitud de una línea.

### Respuesta


## 2. Ahora transforma ese ejemplo a orientación a objetos con Java, para tener un primer ejemplo de **composición** en orientación a objetos. Crea una clase `Punto`, y una clase `Linea`. La clase `Punto` debe tener un método para calcular distancia a otro `Punto` y `Linea` debe tener un método para calcular su longitud. Gracias a la ocultación de información, supera a C, garantizando que los puntos sean inmutables, al igual que la línea, que una vez creada, no queremos que se modifique de qué a qué puntos va dicha línea.  

### Respuesta


## 3. ¿Qué significa la **multiplicidad** en la composición? En el ejemplo anterior, ¿cuál es la multiplicidad entre `Linea` y `Punto`? Indícalo expresando la multiplicidad en ambas direcciones, de `Linea` a `Punto` y de `Punto` a `Linea`.

### Respuesta


## 4. ¿Qué significa composición **fuerte** y composición **débil**? ¿Qué consecuencia implica en relación al ciclo de vida de los objetos? Indica a cuál solemos referirnos como **"asociación o agregación"** y a cuál como **"composición"** propiamente.

### La composición fuerte (referida simplemente como composición) implica una relación de pertenencia vital: el objeto contenido no tiene sentido de existencia sin su contenedor. Si el objeto "padre" es destruido, los objetos "hijos" también desaparecen. Existe un control total sobre el ciclo de vida de los componentes dentro de la clase contenedora.

### Por otro lado, la composición débil (conocida como agregación o asociación) describe una relación donde los objetos tienen ciclos de vida independientes. El objeto contenido puede existir antes de que se cree el contenedor y puede seguir existiendo después de que este se destruya. Es una relación de "pertenencia" más flexible donde el contenedor solo mantiene una referencia a objetos creados externamente.


## 5. Cuando una clase usa a otra al recibirla o devolverla como parámetro en algún método, al hacer `new` dentro de un método, o al usarlas como variables locales, ¿hablamos de composición o de **"dependencia"**?

### Cuando una clase utiliza a otra únicamente de forma temporal —por ejemplo, como una variable local dentro de un método, recibiéndola como parámetro o instanciándola con new para un uso inmediato que no se almacena en un atributo—, se habla de dependencia (o uso).

### A diferencia de la composición, la dependencia no establece un vínculo estructural permanente entre los objetos. Es el tipo de relación más débil en orientación a objetos: la clase "A" necesita a la clase "B" para ejecutar una tarea específica, pero "A" no "posee" a "B" como parte de su estado.


## 6. En el ejemplo anterior de línea y punto, programa la relación entre `Linea` y `Punto` de dos formas. Una **como composición fuerte**, donde el ciclo de vida de los puntos está ligado al de Linea y otra **como composición débil**, donde no.

### Respuesta


## 7. En Java, en la composición fuerte, ¿cuando el contenedor destruye los objetos? No se observa que `Linea` destruya los `Punto` explícitamente, ¿Por qué?

### En Java, no existe una destrucción explícita de objetos como el free() de C o el delete de C++. El encargado de liberar la memoria es el Garbage Collector (Recolector de Basura). Un objeto es candidato a ser destruido cuando ya no existen referencias activas que apunten a él.

### En la composición fuerte, cuando el objeto Linea deja de ser accesible, las referencias internas a los objetos Punto también se pierden (siempre que no se hayan "fugado" fuera de la clase). Al quedar estos puntos sin ninguna referencia que los alcance, el Garbage Collector los eliminará automáticamente de la memoria en su próximo ciclo de ejecución.


## 8. Pon un ejemplo de composicion débil entre un departamento que tiene varios profesores. Implementa dos composiciones a la vez: entre el departamento y todos sus profesores y entre el departamento y su director, que es un profesor del departamento. Siempre debe haber un director en el departamento desde el inicio. Lanza excepciones si se viola la invariante. Emplea arrays primitivos de Java, estilo `Profesor[]`, con máximo 50, pero no rompas la encapsulación, no desveles que estás empleando un array, permite añadir un `Profesor` al final de la lista, y eliminar un profesor dada su posición. Da acceso a los profesores con un método para saber cuántos hay y otro para obtener un profesor por posición. El director se puede cambiar por otro profesor del departamento. Sin embargo, ten en cuenta esta invariante de clase: el director debe formar siempre parte de la lista de profesores, es decir, ten cuidado al cambiar el director o al eliminar un profesor.

### Respuesta


## 9. En Java, existen también `List`, cambia y muestra cómo sería el código anterior empleando `List` en vez de arrays primitivos. ¿Qué parte del código original te has ahorrado? Además, fíjate en el método `getProfesor(int pos)`: si en su lugar existiera un método que devolviera todos los profesores a la vez, ¿qué problema tendría devolver directamente la lista interna? ¿Cómo lo resolverías?

### Al emplear ArrayList, se ahorra toda la gestión manual del tamaño del array, el desplazamiento de elementos al eliminar y el control del índice numProfesores. La lista crece dinámicamente y ofrece métodos como add() y remove() que simplifican el código drásticamente.

### Si un método devolviera la lista interna directamente (return estaLista), se rompería la encapsulación. Cualquier usuario externo podría añadir o quitar profesores (incluyendo al director) sin pasar por las validaciones de la clase Departamento. Para resolver esto, se debe devolver una copia de la lista o, mejor aún, una vista no modificable mediante Collections.unmodifiableList(lista).


## 10. Al igual que ocurre con las excepciones en Java, que pueden encerrar causas (que son excepciones), de forma recursiva, suponen un tipo especial de composiciones, denominadas composiciones recursivas. Pon un ejemplo en Java de una `Persona`, que sea inmutable, y que tiene una madre, que es otra `Persona`. Haz un main con un ejemplo de uso con una familia de personas, desde el nieto hasta la abuela. Enumera algún otro ejemplo clásico de composiciones recursivas.

### Respuesta

## 11. ¿Qué son las relaciones de composición "bidireccionales"? ¿Qué habría que hacer para implementar este tipo de relación en el ejemplo de `Profesor` y `Departamento`?

### Una relación es bidireccional cuando ambos objetos conocen la existencia del otro. En el ejemplo de Profesor y Departamento, esto significaría que el departamento tiene una lista de profesores, y cada profesor tiene un atributo que apunta al departamento al que pertenece.

### Para implementarlo, es necesario sincronizar ambas referencias: al añadir un profesor al departamento, se debe asignar automáticamente ese departamento al atributo interno del profesor. Esto requiere cuidado para evitar bucles infinitos y asegurar que, si un profesor cambia de departamento, la información sea coherente en ambos extremos de la relación.
