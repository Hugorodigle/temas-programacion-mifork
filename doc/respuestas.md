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

### Respuesta

La primera característica fundamental es la abstracción, que consiste en centrarse únicamente en los aspectos esenciales de un objeto, ignorando los detalles irrelevantes. En Java, esto se refleja en la capacidad de definir clases que representan conceptos del mundo real mediante atributos y métodos, sin necesidad de mostrar cómo están implementados internamente. La abstracción permite trabajar con ideas complejas de forma más simple y manejable.

Otra característica clave es el encapsulamiento, que agrupa datos y funciones relacionadas dentro de una misma entidad: la clase. Además, controla el acceso a esos datos mediante modificadores como private o public. Esto evita que el estado interno de un objeto pueda ser modificado de forma incorrecta desde fuera, algo que en C se suele gestionar manualmente. El encapsulamiento mejora la seguridad y la robustez del código.

La tercera característica es la herencia, que permite crear nuevas clases basadas en otras ya existentes. Gracias a ella, una clase puede reutilizar atributos y métodos de otra, evitando duplicación de código y facilitando la organización jerárquica. En Java, la herencia se expresa con la palabra clave extends. Este mecanismo permite construir sistemas más extensibles y coherentes.

Finalmente, el polimorfismo permite que un mismo método pueda comportarse de distintas formas según el objeto que lo utilice. Esto hace posible escribir código más flexible y genérico, ya que una referencia puede apuntar a objetos de diferentes clases relacionadas. En Java, el polimorfismo se manifiesta tanto en la sobrecarga de métodos como en la sobrescritura, permitiendo adaptar el comportamiento sin cambiar la estructura general del programa.


## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Respuesta

Uno de los lenguajes más representativos de la programación orientada a objetos es Java, ampliamente utilizado en desarrollo empresarial, aplicaciones Android y sistemas de gran escala. Su diseño se basa fuertemente en los principios de la POO, lo que lo convierte en un ejemplo clásico para aprender este paradigma desde cero.

Otro lenguaje muy extendido es C++, que combina programación estructurada con orientación a objetos. Aunque permite trabajar sin clases, incorpora herencia, polimorfismo y encapsulamiento, lo que lo hace adecuado para proyectos donde se requiere control de bajo nivel junto con abstracción.

También destaca Python, que adopta un enfoque flexible hacia la POO. En este lenguaje, todo es un objeto, lo que facilita la comprensión del paradigma. Su sintaxis sencilla y su ecosistema lo han convertido en una opción popular tanto en educación como en desarrollo profesional.

Finalmente, C# es un lenguaje moderno diseñado por Microsoft que sigue de forma muy clara los principios de la orientación a objetos. Se utiliza en aplicaciones de escritorio, videojuegos con Unity y servicios web, y ofrece una estructura muy similar a Java, lo que facilita el aprendizaje entre ambos.


## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Respuesta

La programación en ensamblador trabaja directamente con instrucciones simples que actúan sobre registros y memoria. El flujo del programa depende de saltos arbitrarios, lo que permite mover la ejecución a cualquier punto del código. Este estilo ofrece control total del hardware, pero genera programas difíciles de leer y mantener debido a la ausencia de una estructura clara.

La programación estructurada aparece para evitar ese caos de saltos. Se basa en tres bloques fundamentales: secuencia, bifurcación (if, switch) e iteración (while, for). Al eliminar el salto arbitrario, el código sigue un flujo más ordenado y predecible, lo que facilita la comprensión y reduce errores. Este paradigma introduce disciplina y claridad en la construcción de algoritmos.

La programación modular da un paso más al dividir el programa en módulos independientes, cada uno con una responsabilidad concreta. Estos módulos pueden organizarse como librerías, paquetes o interfaces, según el lenguaje. Su objetivo es encapsular la implementación y permitir reutilizar código, reduciendo la complejidad global y mejorando el mantenimiento.

Esta evolución —de ensamblador a estructurada y luego a modular— muestra una tendencia hacia programas más organizados y fáciles de gestionar. La POO continúa esta línea al introducir clases y objetos, que permiten modelar sistemas complejos de forma más natural y coherente.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Respuesta

Un objeto se define primero por su estado, que está formado por los datos que almacena en sus atributos. Este estado representa la información que caracteriza al objeto en un momento dado, igual que una estructura en C pero con mayor control y encapsulación.

El segundo elemento es el comportamiento, que corresponde a los métodos que puede ejecutar. Estos métodos determinan qué acciones realiza el objeto y cómo interactúa con otros, permitiendo modificar su estado o consultar información interna de forma controlada.

El tercer elemento es la identidad, que permite distinguir un objeto de otro aunque tengan el mismo estado y comportamiento. En Java, cada objeto ocupa una posición única en memoria, lo que garantiza que dos instancias iguales sigan siendo entidades distintas dentro del programa.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta

Una clase es una plantilla que describe cómo serán los objetos: define qué atributos tendrán y qué métodos podrán ejecutar. No contiene datos reales, sino la estructura y el comportamiento común que compartirán todas sus instancias. Es, por así decirlo, el “molde” a partir del cual se crean objetos concretos.

Un objeto no es lo mismo que una clase. El objeto es la materialización de esa clase en memoria: tiene valores propios en sus atributos y puede ejecutar los métodos definidos en la clase. Cada objeto puede tener un estado distinto, aunque provenga del mismo molde.

El término instancia se usa para referirse a un objeto concreto creado a partir de una clase. Instanciar significa reservar memoria y construir un objeto real siguiendo la definición de la clase. En Java, esto se hace con new, que crea una instancia independiente de las demás.

No todos los lenguajes orientados a objetos utilizan el concepto de clase. Algunos, como JavaScript, se basan en prototipos, donde los objetos se crean a partir de otros objetos sin necesidad de una clase formal. Aun así, la mayoría de lenguajes populares sí emplean clases como base de su modelo de objetos.

```java
class Punto{
    int x; // Atributos
    int y;

    double calcularDistancia(){ // Método
        return sqrt(x*x+y*y);
    }
}
class Ejercicio1{
    public static void main(String[] args){
        Punto miPunto = new Punto();
        miPunto.x=5;
        miPunto.y=3;
        double resultado = miPunto.calcularDistancia(miPunto.x, miPunto.y);
    }
}
```


## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### Respuesta

En la mayoría de lenguajes orientados a objetos modernos, los objetos se almacenan en memoria dinámica, normalmente en el heap. Cuando se crea un objeto, el lenguaje reserva espacio en esa zona y devuelve una referencia para poder usarlo. Esto permite que los objetos tengan un ciclo de vida flexible y no dependan del ámbito donde se declaran, a diferencia de las variables locales que van a la pila.

No todos los lenguajes gestionan la memoria igual. En C++, por ejemplo, el programador decide si un objeto va en la pila o en el heap, y debe liberarlo manualmente cuando ya no se necesita. En Java o Python, en cambio, todos los objetos se crean en el heap y el programador no se encarga de liberarlos. Cada lenguaje adopta un modelo distinto según su filosofía y nivel de abstracción.

La recolección de basura (garbage collection) es un mecanismo automático que libera la memoria ocupada por objetos que ya no están en uso. El sistema detecta cuándo un objeto ha dejado de ser accesible y recupera su espacio sin intervención del programador. Esto reduce errores típicos como fugas de memoria o accesos a memoria liberada, aunque implica que el control sobre el momento exacto de liberación no es directo.


## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Respuesta

Un método es una función definida dentro de una clase que describe una acción que los objetos pueden realizar. Representa el comportamiento del objeto y suele operar sobre su estado interno. En Java, los métodos permiten organizar la lógica asociada a cada clase y controlar cómo interactúan los objetos entre sí.

La sobrecarga de métodos consiste en definir varios métodos con el mismo nombre dentro de una clase, pero con distintos parámetros (ya sea en número, tipo o ambos). El compilador decide cuál usar según los argumentos que se pasen en la llamada. Esto permite ofrecer varias formas de realizar una misma acción sin cambiar el nombre del método, facilitando la legibilidad y la flexibilidad del código.

La sobrecarga no modifica el comportamiento de un método existente, sino que crea versiones alternativas del mismo. Es una forma de polimorfismo en tiempo de compilación, muy útil para simplificar interfaces y evitar nombres innecesariamente diferentes para operaciones relacionadas.


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### Respuesta

Una clase mínima en Java define sus atributos y los métodos que operan sobre ellos. En este caso, Punto tendrá dos atributos con visibilidad por defecto (int x, int y) y un método que calcule la distancia al origen usando la fórmula 
sqrt(x^2+y^2)
. El método puede devolver un double y usar Math.sqrt.

El ejemplo de uso consiste en crear una instancia de Punto, asignar valores a x e y, y llamar al método para obtener la distancia. Esto permite ver claramente la diferencia entre clase (molde) y objeto (instancia real en memoria).


## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### Respuesta

En Java, el punto de entrada de cualquier programa es el método main, cuya firma estándar es public static void main(String[] args). Es el primer método que la JVM ejecuta y actúa como inicio del programa, igual que main() en C, pero siempre dentro de una clase.

La palabra clave static indica que un método o atributo pertenece a la clase, no a un objeto concreto. Esto permite llamar a main sin crear una instancia, ya que la JVM no puede construir objetos antes de saber dónde empezar. No se usa solo en main: también sirve para definir métodos utilitarios, constantes o atributos compartidos entre todas las instancias.

Cuando static se combina con final, se obtiene un valor constante asociado a la clase. En Java, esto se usa para definir constantes globales, normalmente en mayúsculas, como static final double PI = 3.14159;. El modificador final impide que el valor cambie, y static evita que cada objeto tenga su propia copia, optimizando memoria y claridad.

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta

Para compilar un archivo Java desde la línea de comandos se usa javac NombreArchivo.java, lo que genera uno o varios ficheros .class. Para ejecutarlo, se emplea java NombreClase, sin la extensión. Por ejemplo: javac Main.java seguido de java Main. Es un proceso muy similar al de C, pero con una separación clara entre compilación y ejecución dentro del ecosistema Java.

Java es un lenguaje compilado e interpretado a la vez. Primero se compila a un formato intermedio llamado bytecode, que no es código máquina real. Ese bytecode se almacena en los ficheros .class y es independiente del sistema operativo. Esto permite que el mismo programa funcione en cualquier plataforma sin recompilar.

La máquina virtual de Java (JVM) es el componente encargado de ejecutar ese bytecode. Actúa como una capa intermedia entre el programa y el sistema operativo, interpretando o compilando dinámicamente las instrucciones. Gracias a la JVM, Java consigue portabilidad, seguridad y gestión automática de memoria.

El bytecode es el conjunto de instrucciones que entiende la JVM. No es legible para humanos, pero es mucho más compacto y portable que el código fuente. Los ficheros .class contienen precisamente ese bytecode, y son los que la JVM carga y ejecuta cuando se lanza un programa Java.


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta

La palabra clave new sirve para crear un objeto en Java. Al usarla, la JVM reserva memoria en el heap y devuelve una referencia al nuevo objeto. Es el equivalente a “instanciar” una clase, es decir, convertir el molde (la clase) en un objeto real con su propio estado.

Un constructor es un método especial que se ejecuta automáticamente al crear un objeto con new. Su función es inicializar los atributos del objeto y dejarlo listo para usarse. No tiene tipo de retorno y su nombre coincide exactamente con el de la clase. Si no se define ninguno, Java crea uno por defecto sin parámetros.

``` java
class Empleado {
    String dni;
    String nombre;
    String apellidos;

    Empleado(String d, String n, String a) {
        dni = d;
        nombre = n;
        apellidos = a;
    }
}

```


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta

La referencia this apunta al objeto actual, es decir, a la instancia sobre la que se está ejecutando un método. Se usa para distinguir entre atributos del objeto y parámetros con el mismo nombre, o simplemente para dejar claro que se accede al estado interno del objeto.

No todos los lenguajes la llaman igual, aunque casi todos tienen un mecanismo equivalente. En Java y C++ se llama this, en Python es self, en JavaScript es this pero con un comportamiento más dinámico, y en otros lenguajes puede variar.

``` java
class Punto {
    int x;
    int y;

    Punto(int x, int y) {
        this.x = x;  // "this.x" es el atributo, "x" es el parámetro
        this.y = y;
    }

    double calculaDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }
}
```


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta

```java
class Punto {
    int x;
    int y;

    Punto(int x, int y) {
        this.x = x;
        this.y = y;
    }

    double calculaDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }

    double distanciaA(Punto p) {
        int dx = this.x - p.x;
        int dy = this.y - p.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### Respuesta

En Java, cuando se pasa un objeto como parámetro (por ejemplo, un Punto), lo que se pasa es una copia de la referencia, no una copia del objeto. Esto significa que ambos —el parámetro dentro del método y la variable original— apuntan al mismo objeto en memoria. Por tanto, si dentro del método se modifica un atributo del Punto, el cambio sí afecta al objeto original fuera del método.

Sin embargo, si se pasa un tipo primitivo como int, el comportamiento es distinto: se pasa una copia del valor, no una referencia. Si el método modifica ese entero, el cambio no afecta a la variable original, porque el método trabaja con su propia copia local.

En resumen:

Objetos → copia de la referencia → cambios visibles fuera.

Primitivos → copia del valor → cambios NO visibles fuera.


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta

El método toString() sirve para obtener una representación en texto de un objeto. Es muy útil para depuración, impresión por consola o para mostrar el estado interno de forma legible. Todas las clases en Java lo heredan de Object, pero normalmente se sobrescribe para personalizar el resultado.

Muchos lenguajes tienen un mecanismo equivalente: en Python es __str__, en C++ se suele sobrecargar operator<<, en JavaScript se usa toString() también, aunque con un comportamiento más flexible.

```java
class Punto {
    int x;
    int y;

    Punto(int x, int y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public String toString() {
        return "Punto(" + x + ", " + y + ")";
    }
}
```


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?

### Respuesta

Un struct en C se parece a una clase en el sentido de que ambos agrupan datos bajo un mismo tipo. En ambos casos, las variables de ese tipo contienen un conjunto de campos que representan el estado de una entidad. Hasta aquí, la analogía funciona bastante bien.

Sin embargo, a un struct le falta lo esencial para comportarse como una clase: no puede tener métodos asociados, no tiene encapsulación, ni constructores, ni visibilidad, ni comportamiento ligado al tipo. En C, un struct solo agrupa datos; en una clase, además de datos, se define el comportamiento y las reglas de uso del objeto.

Por tanto, las variables de un struct no son “instancias” en el sentido de la POO. Son simplemente bloques de memoria con campos. Para que un struct fuese equivalente a una clase, necesitaría:

Métodos asociados al tipo.

Constructores para inicializar.

Encapsulación (visibilidad: private, public).

Comportamiento integrado, no funciones externas.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta

En C, un struct solo puede almacenar datos, no métodos. Para “emular” una clase, se define un struct para el estado y funciones externas que reciben un puntero al struct para operar sobre él. Ese puntero actúa como el equivalente manual de this.

Como C no tiene this, simplemente se pasa el objeto como parámetro. Si quieres modificarlo, pasas un puntero; si solo quieres leerlo, puedes pasar una copia o un puntero constante.

```java
#include <math.h>

typedef struct {
    int x;
    int y;
} Punto;

double calculaDistanciaAOrigen(Punto* p) {
    return sqrt(p->x * p->x + p->y * p->y);
}

#include <stdio.h>

int main() {
    Punto p = {3, 4};
    double d = calculaDistanciaAOrigen(&p);
    printf("Distancia al origen: %f\n", d);
    return 0;
}
```
