<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

### Respuesta

La encapsulación y la ocultación de información buscan proteger el estado interno de los objetos y controlar cómo se accede y modifica. La idea central es que un objeto debe exponer solo lo necesario y ocultar los detalles internos que no deberían manipularse directamente.

En otras palabras:

Encapsulación = agrupar datos + métodos que operan sobre esos datos.

Ocultación = decidir qué partes son visibles y cuáles quedan protegidas.

Ambas trabajan juntas para que el objeto sea una “caja negra” con una interfaz clara y segura.

-Evita errores: impide que otras partes del programa modifiquen atributos de forma incorrecta.

-Mantiene coherencia interna: el objeto controla sus propios cambios.

-Permite cambiar la implementación sin romper el código externo.

-Reduce el acoplamiento entre módulos.

-Mejora la seguridad del estado del objeto.

-Facilita el mantenimiento y la evolución del software.


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### Respuesta

La interfaz pública de un objeto o clase es el conjunto de métodos y atributos accesibles desde fuera. Es lo que otros objetos pueden ver y usar. En esencia, es la “cara visible” del objeto: aquello que ofrece al exterior para interactuar con él.

Suele incluir:

-Métodos públicos (public) que permiten operar con el objeto.

-A veces constantes o atributos públicos (aunque no es lo habitual en buen diseño).

Todo lo demás —atributos internos, métodos auxiliares, detalles de implementación— queda oculto mediante modificadores como private o protected.

La interfaz pública es lo que se expone.
La ocultación de información es lo que se protege.

Ambas ideas se complementan:

-La interfaz pública define cómo se puede usar el objeto.

-La ocultación define qué no se puede tocar directamente.

-Gracias a esta separación, puedes cambiar la implementación interna sin romper el código que usa la clase.

-Esto reduce errores, acoplamiento y dependencias innecesarias.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### Respuesta

La interfaz pública de una clase es lo que otros programadores (o tú mismo en el futuro) van a usar para interactuar con ella. Por eso debe diseñarse con muchísimo cuidado: es el “contrato” que la clase ofrece al exterior. Si ese contrato cambia, todo el código que depende de él puede romperse.

⭐ ¿Por qué hay que diseñarla con cuidado?
-Porque define cómo se usa la clase.

-Porque otros módulos, clases o programas dependerán de ella.

-Porque una interfaz mal pensada obliga a exponer detalles internos que deberían estar ocultos.

-Porque una interfaz clara y estable hace que el código sea más fácil de mantener y entender.

-Porque una interfaz pobre obliga a hacer “parches” o romper encapsulación más adelante.

⭐ ¿Es fácil cambiarla?
No.  
-Cambiar la interfaz pública suele ser costoso y arriesgado, porque:

-Obliga a modificar todo el código que la usa.

-Puede romper compatibilidad con versiones anteriores.

-Puede introducir errores en módulos que antes funcionaban.

-A veces requiere rediseñar partes enteras del sistema.

Por eso se dice que la interfaz pública debe ser estable, mínima y bien pensada desde el principio.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Respuesta

Las invariantes de clase son condiciones que siempre deben cumplirse para que un objeto sea válido. Son reglas internas que describen qué significa que un objeto esté en un estado “correcto”. Normalmente se refieren a relaciones entre atributos, rangos válidos, coherencia interna, etc.

Ejemplos típicos de invariantes:

-Un punto no puede tener coordenadas nulas si la clase lo prohíbe.

-Un intervalo debe cumplir que inicio <= fin.

-Un empleado debe tener un DNI no vacío.

-Un vector debe mantener su tamaño coherente con su array interno.

Estas invariantes deben cumplirse antes y después de cada método público.

¿Por qué la ocultación de información ayuda?
Porque si los atributos fueran públicos, cualquier parte del programa podría modificarlos libremente y romper esas invariantes.
Al ocultar los datos (private) y exponer solo métodos controlados:

-La clase puede validar cambios antes de aplicarlos.

-Se evita que código externo deje el objeto en un estado inválido.

-Las invariantes se mantienen automáticamente.

-La clase controla su propia coherencia interna.

En resumen:
Las invariantes definen cómo debe ser un objeto válido; la ocultación garantiza que nadie pueda romper esas reglas desde fuera.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### Respuesta

```java
class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    // Getters opcionales si quieres exponer lectura controlada
    public double getX() { return x; }
    public double getY() { return y; }
}
```
### ¿Cuál es la interfaz pública de esta clase?
La interfaz pública es todo lo que está declarado como public, es decir:

El constructor: public Punto(double x, double y)

El método: public double calcularDistanciaAOrigen()

(Opcionalmente) los getters si decides incluirlos

Eso es lo que otros objetos pueden usar desde fuera.
Todo lo demás queda oculto.

### ¿Qué significa public y private?
public → accesible desde cualquier parte del programa.
Es lo que forma la interfaz pública.

private → accesible solo dentro de la propia clase.
Sirve para proteger los atributos y mantener las invariantes.

En este ejemplo, x e y son privadas, así que nadie puede modificarlas directamente desde fuera. Solo se puede interactuar con ellas a través de los métodos públicos.


## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### Respuesta

### 1.A clases (pero solo a clases “top‑level”)
-Una clase de primer nivel puede ser:

    public → accesible desde cualquier paquete.

    sin modificador (package‑private) → accesible solo desde su propio paquete.

-No puede ser private si es una clase de primer nivel.

Las clases internas (clases dentro de otras clases) sí pueden ser private.

### 2.A los miembros de una clase
Es decir:

-Atributos  
(private double x;)

-Métodos  
(public double calcularDistanciaAOrigen())

-Constructores  
(public Punto(double x, double y))

-Clases internas  
(private class Nodo { ... })

Aquí sí puedes usar public, private, protected o dejarlo sin modificador.


## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Respuesta

En POO existen más tipos de visibilidad además de pública y privada. Java, por ejemplo, define cuatro niveles distintos: public, private, protected y el nivel por defecto, llamado package‑private, que se aplica cuando no se escribe ningún modificador. Cada uno controla desde dónde puede accederse a los miembros de una clase. En otros lenguajes la situación varía: C++ tiene también public, private y protected, pero sin el concepto de paquetes; C# añade niveles adicionales como internal o protected internal; Python no tiene privacidad real y se basa en convenciones; y JavaScript ha incorporado recientemente atributos privados con #, aunque históricamente todo era público. En resumen, sí existen más niveles de visibilidad, y cada lenguaje ofrece su propio sistema para controlar el acceso a los elementos de una clase.

## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Respuesta

Aquí la clave es entender que los miembros privados están ocultos para otras clases, pero no para otras instancias de la misma clase.
En Java, cualquier método de la clase puede acceder a los atributos privados de cualquier objeto de esa misma clase, no solo al suyo propio. Esto sorprende al principio, pero es totalmente legal y forma parte del modelo de visibilidad de Java.

```java 
class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    public double calcularDistanciaAPunto(Punto otro) {
        double dx = this.x - otro.x;   // Acceso legal a atributos privados de otro
        double dy = this.y - otro.y;   // También legal
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```
En este método, otro.x y otro.y son privados, pero aun así se pueden leer sin problema.
¿Por qué? Porque la visibilidad privada se aplica a nivel de clase, no a nivel de instancia.
Eso significa:

-Están ocultos para otras clases → nadie fuera de Punto puede acceder a x o y.

-No están ocultos para otras instancias de la misma clase → un Punto puede acceder a los atributos privados de otro Punto.

Esto tiene sentido porque todos los métodos de la clase forman parte de la misma “unidad de confianza”. Si Java prohibiera acceder a los privados de otra instancia, muchos métodos naturales (como comparar, copiar, calcular distancias, etc.) serían imposibles sin exponer getters innecesarios.


## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Respuesta

Los getters y setters son métodos especiales que se usan en POO para acceder y modificar atributos privados sin romper la encapsulación.

Un getter es un método que devuelve el valor de un atributo privado. Sirve para leer un dato sin exponer directamente la variable.
Un setter es un método que permite modificar un atributo privado, normalmente realizando comprobaciones o validaciones antes de aceptar el cambio.

La idea es que, como los atributos están ocultos (private), el objeto controla cómo se leen y cómo se cambian. Esto mantiene las invariantes de clase y evita estados inválidos.

```java
public double getX() { return x; }
public void setX(double x) { this.x = x; }
``` 


## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Respuesta

No, en este contexto “seguridad” no significa protección contra hackers ni nada relacionado con ciberataques.
Cuando decimos que la ocultación de información mejora la seguridad, nos referimos a una seguridad lógica, es decir, a evitar que el propio programa se rompa por errores internos.

La idea es que, si los atributos están ocultos (private), ninguna otra parte del programa puede modificarlos de forma incorrecta o dejar el objeto en un estado inválido. Esto protege las invariantes de clase y evita fallos difíciles de rastrear. Es una seguridad orientada a la robustez del software, no a la seguridad informática.

En resumen:
La ocultación de información no evita hackers; evita que tu propio código cause daños sin querer. Cuando quieras, seguimos con la 11.


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Respuesta

Un miembro de instancia es un atributo o método que pertenece a cada objeto individual. Cada instancia tiene su propia copia de esos datos. Por ejemplo, en un Punto, cada objeto tiene su propio x y y. En cambio, un miembro de clase (marcado con static) pertenece a la clase en sí, no a cada objeto. Solo existe una copia compartida por todas las instancias, como un contador de cuántos puntos se han creado.

Ambos tipos de miembros pueden ocultarse usando private. Un atributo private static está oculto igual que uno private normal: solo la propia clase puede acceder a él. La diferencia no está en la visibilidad, sino en a quién pertenece: a cada objeto o a la clase completa.


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta

Sí, tiene sentido que los constructores sean privados, aunque no es lo habitual. Un constructor privado se usa cuando no quieres que otros puedan crear objetos libremente desde fuera de la clase. Esto permite controlar completamente cómo y cuándo se crean las instancias.

El caso más típico es el patrón Singleton, donde solo puede existir un único objeto de la clase. También se usa cuando la clase ofrece métodos estáticos de creación (factory methods) en lugar de constructores públicos, o cuando quieres impedir que se creen objetos directamente y obligar a usar otros mecanismos.

En resumen, un constructor privado sirve para restringir la creación de instancias y mantener un control total sobre el proceso.


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta

En Java, los miembros de clase se indican usando la palabra clave static.
Esto hace que el atributo o método pertenezca a la clase en sí, no a cada objeto individual. Solo existe una copia compartida por todas las instancias.

Para tu ejemplo, podemos añadir a la clase Punto dos miembros de clase (static) que registren los valores máximos de x e y que se hayan asignado en todos los puntos creados hasta ahora.
```java
class Punto {
    private double x;
    private double y;

    // Miembros de clase (compartidos por todos los objetos)
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;

        // Actualizamos los máximos globales
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    public static double getMaxX() {
        return maxX;
    }

    public static double getMaxY() {
        return maxY;
    }
}
```
Respecto a la ocultación:
Sí, los miembros de clase también pueden ser privados. La visibilidad depende del modificador (private, public…), no de si el miembro es de instancia o de clase. Aquí maxX y maxY están ocultos y solo se exponen mediante getters controlados.


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Respuesta

Aquí tienes el método factoría tal como lo pide la pregunta: solo el método, en formato limpio, y sí, usando static porque un método factoría pertenece a la clase, no a un objeto concreto.

```java
public static Punto crearRedondeado(double x, double y) {
    return new Punto(Math.round(x), Math.round(y));
}
```
Este método es factoría porque crea y devuelve un Punto, pero no es un constructor.
Y sí, he usado static porque un método factoría debe poder llamarse sin necesidad de tener un objeto previo, igual que Punto.crearRedondeado(…).


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta

```java 
class Punto {
    private double[] coords = new double[2];

    public Punto(double x, double y) {
        coords[0] = x;
        coords[1] = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(coords[0] * coords[0] + coords[1] * coords[1]);
    }

    public double calcularDistanciaAPunto(Punto otro) {
        double dx = this.coords[0] - otro.coords[0];
        double dy = this.coords[1] - otro.coords[1];
        return Math.sqrt(dx * dx + dy * dy);
    }

    public double getX() { return coords[0]; }
    public double getY() { return coords[1]; }
}
```
La interfaz pública no cambia:
sigues teniendo el mismo constructor, los mismos métodos y los mismos getters.
Solo cambia la representación interna, que ahora es un array privado.

Esto demuestra perfectamente el principio de ocultación de información:
puedes cambiar cómo se almacena el estado sin afectar a quien usa la clase.


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta

Aquí la idea importante es que aunque un atributo tenga getter y setter públicos, no conviene hacerlo público.
La razón es que un atributo público expone directamente la representación interna del objeto, mientras que un getter y un setter permiten controlar cómo se accede y cómo se modifica ese atributo.

En la práctica, la convención casi universal en POO —y especialmente en Java— es que todos los atributos sean privados, incluso si van a tener getters y setters. Esto mantiene la encapsulación y permite cambiar la implementación interna sin romper el código que usa la clase. Si el atributo fuera público, cualquier cambio interno rompería a todos los clientes que lo usen directamente.

Esto está muy relacionado con las invariantes de clase, que son las condiciones que siempre deben cumplirse para que un objeto sea válido. Si el atributo es público, cualquiera puede ponerle un valor incorrecto y romper esas invariantes. En cambio, con un setter puedes validar, corregir o impedir valores que no tengan sentido, manteniendo el objeto siempre en un estado coherente.


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta

Una clase inmutable es aquella cuyo estado no puede cambiar después de ser creada.
Una vez construyes el objeto, sus atributos quedan fijados para siempre. No existen métodos que alteren ese estado interno.

Un método modificador es cualquier método que cambia el estado del objeto.
Un setter es un tipo de método modificador, pero no todos los modificadores son setters: por ejemplo, un método mover(dx, dy) que cambie x e y también modifica el estado, aunque no sea un setter tradicional.

Las clases inmutables tienen varias ventajas:
son más seguras, más fáciles de razonar, no pueden quedar en estados inconsistentes, son naturalmente thread‑safe y permiten compartir objetos sin riesgo. Por eso muchas clases de Java, como String, son inmutables.

En resumen: una clase inmutable no cambia su estado; un método modificador cambia el estado, pero no tiene por qué ser un setter; y la inmutabilidad aporta simplicidad y robustez.


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta

No, no es recomendable incluir setters siempre “por convención”.
De hecho, en diseño orientado a objetos moderno, la convención es justo la contraria:
los atributos deben ser privados y solo deben tener setter si realmente es necesario modificar ese valor desde fuera.

-Un setter abre una puerta para cambiar el estado del objeto, y eso:

-puede romper invariantes de clase

-puede dejar el objeto en un estado incoherente

-reduce la capacidad de controlar cómo se modifica el dato

-hace la clase menos robusta y más difícil de mantener

Por eso, muchos diseños actuales prefieren:

-clases inmutables (sin setters)

-o clases mutables pero con control, donde solo algunos atributos tienen setter

-o métodos modificadores más específicos (como mover(dx, dy)), en lugar de setters genéricos

En resumen:


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta

La clase String en Java es inmutable, lo que significa que una vez creada no puede cambiar su contenido interno. Cada operación que “parece” modificar una cadena en realidad crea un nuevo objeto String.

Cuando concatenas dos cadenas, por ejemplo:
```java
String s = "Hola";
s = s + " mundo";
```
lo que ocurre internamente es que se crea otro String nuevo con el contenido "Hola mundo", y la variable s pasa a apuntar a ese nuevo objeto. El anterior queda para el recolector de basura si ya no se usa.

Esto no es un problema cuando concatenas pocas veces, pero si vas a construir una cadena muy larga paso a paso (por ejemplo, dentro de un bucle), crear cientos o miles de objetos String intermedios es muy ineficiente.

En esos casos, la solución recomendada es usar:

-StringBuilder (si no necesitas sincronización)

-StringBuffer (si necesitas sincronización, menos habitual hoy)

Por ejemplo:
```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10000; i++) {
    sb.append("hola");
}
String resultado = sb.toString();
```


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### Respuesta

En POO, los objetos pueden compararse de dos maneras: por identidad o por contenido.
La identidad significa que dos referencias apuntan exactamente al mismo objeto en memoria.
El contenido significa que dos objetos distintos pueden considerarse “iguales” si sus valores internos coinciden.

En Java, el operador == compara identidad, es decir, si dos referencias apuntan al mismo objeto.
Para comparar contenido, Java utiliza el método equals.

El método equals es un método heredado de Object.
Por defecto, su comportamiento es exactamente el mismo que ==: compara identidad, no contenido.
Por eso, si quieres que dos objetos de tu clase se consideren iguales cuando tengan los mismos valores internos, debes sobrescribir equals para que compare esos valores.

En el caso de las cadenas, Java ya sobrescribe equals en la clase String, de modo que dos cadenas se consideran iguales si tienen el mismo contenido textual, aunque sean objetos distintos. Por eso, para comparar cadenas se debe usar equals, no ==, ya que == solo diría si son la misma instancia.

En resumen: los objetos se comparan por identidad con == y por contenido con equals; equals por defecto compara identidad, pero las clases suelen sobrescribirlo; y las cadenas deben compararse siempre con equals porque su contenido es lo que importa.


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta

Las clases wrapper son clases que envuelven (wrap) un tipo primitivo para poder tratarlo como un objeto. En Java, por ejemplo, cada tipo primitivo tiene su correspondiente clase wrapper: int → Integer, double → Double, boolean → Boolean, etc. Sirven para poder usar valores primitivos allí donde solo se aceptan objetos, como en colecciones (ArrayList<Integer>, por ejemplo).

El proceso de convertir un primitivo en su wrapper se llama autoboxing, y Java lo hace de forma automática. Del mismo modo, convertir un wrapper a su primitivo se llama unboxing, y también es automático. Esto permite escribir cosas como Integer x = 5; sin necesidad de crear el objeto manualmente con new Integer(5).

Las ventajas principales son que permiten usar tipos primitivos en contextos donde se requieren objetos, que pueden almacenar valores nulos (cosa que un primitivo no puede) y que proporcionan métodos útiles asociados al valor, como conversiones o utilidades.

No todos los lenguajes orientados a objetos tienen tipos primitivos separados de los objetos. Algunos, como Python, no necesitan wrappers porque todo es un objeto desde el principio. Otros, como Java o C#, sí distinguen entre primitivos y objetos, y por eso necesitan estas clases wrapper para unificarlos cuando es necesario.


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta

Un tipo de dato enumerado (o enum) es un tipo cuyos valores posibles están predefinidos y limitados. Sirve para representar un conjunto cerrado de opciones válidas, como los días de la semana, los palos de una baraja o los estados de un semáforo. En POO, los enumerados permiten expresar estas opciones de forma clara, segura y sin recurrir a números mágicos o cadenas sueltas.

En Java, un enumerado es efectivamente una clase especial, aunque con una sintaxis más compacta. Cada valor del enum es una instancia única de esa clase, creada automáticamente. Esto significa que un enum puede tener métodos, atributos, constructores privados y lógica interna, igual que cualquier otra clase, pero con la garantía de que solo existirán las instancias definidas en el propio enumerado.

La ventaja en términos de encapsulación es que un enum controla completamente cuáles son los valores válidos. No puedes inventarte uno nuevo desde fuera, ni crear instancias adicionales, ni modificar los existentes. Esto protege las invariantes del dominio: si defines enum Color { ROJO, VERDE, AZUL }, sabes que ningún código podrá crear un color “AMARILLO” por error. Además, al ser clases, los enumerados pueden encapsular comportamiento asociado a cada valor, evitando condicionales dispersos por el programa.


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

### Respuesta

Aquí tienes un enum Mes completo, con sus doce instancias, atributos privados, constructor privado y métodos para obtener:

-el número de días del mes

-el ordinal del mes en el año (1–12)
```java
public enum Mes {
    ENERO(31, 1),
    FEBRERO(28, 2),
    MARZO(31, 3),
    ABRIL(30, 4),
    MAYO(31, 5),
    JUNIO(30, 6),
    JULIO(31, 7),
    AGOSTO(31, 8),
    SEPTIEMBRE(30, 9),
    OCTUBRE(31, 10),
    NOVIEMBRE(30, 11),
    DICIEMBRE(31, 12);

    private final int dias;
    private final int ordinal;

    private Mes(int dias, int ordinal) {
        this.dias = dias;
        this.ordinal = ordinal;
    }

    public int getDias() {
        return dias;
    }

    public int getOrdinal() {
        return ordinal;
    }
}
```


## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta

```java
public boolean esDeInvierno(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == DICIEMBRE || this == ENERO || this == FEBRERO;
    } else {
        return this == JUNIO || this == JULIO || this == AGOSTO;
    }
}

public boolean esDePrimavera(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == MARZO || this == ABRIL || this == MAYO;
    } else {
        return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
    }
}

public boolean esDeVerano(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == JUNIO || this == JULIO || this == AGOSTO;
    } else {
        return this == DICIEMBRE || this == ENERO || this == FEBRERO;
    }
}

public boolean esDeOtoño(boolean enHemisferioNorte) {
    if (enHemisferioNorte) {
        return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
    } else {
        return this == MARZO || this == ABRIL || this == MAYO;
    }
}
```
