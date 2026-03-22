<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

### Respuesta

### ✅ Opción 1: Devolver un valor especial que indique error
Es la técnica más simple y más usada en C.
La función devuelve un valor que no puede ser un resultado válido, y el usuario debe comprobarlo.

Por ejemplo, si la raíz cuadrada siempre es ≥ 0, podemos devolver -1 para indicar error.
```java
#include <stdio.h>
#include <math.h>

double raiz(double x) {
    if (x < 0) {
        return -1;   // valor especial indicando error
    }
    return sqrt(x);
}

int main() {
    double r = raiz(-9);

    if (r == -1) {
        printf("Error: número negativo\n");
    } else {
        printf("Resultado: %f\n", r);
    }
}
```
### ✅ Opción 2: Usar un parámetro de salida para indicar error
La función devuelve el resultado normal, pero además recibe un puntero a un entero donde escribe si hubo error.
```java
#include <stdio.h>
#include <math.h>

double raiz(double x, int *error) {
    if (x < 0) {
        *error = 1;      // indicamos error
        return 0;        // valor cualquiera, no importa
    }
    *error = 0;          // sin error
    return sqrt(x);
}

int main() {
    int error;
    double r = raiz(-9, &error);

    if (error) {
        printf("Error: número negativo\n");
    } else {
        printf("Resultado: %f\n", r);
    }
}
```


## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Respuesta

### ✔️ ¿Qué es una excepción?
Una excepción es un objeto que representa un error que ocurre durante la ejecución y que interrumpe el flujo normal del programa para que ese error pueda ser manejado en otro punto.

### ✔️ ¿Para qué las usa un programador?
Cuando implementa funciones
-Para señalar un error de forma clara y automática.

-Evita devolver valores especiales o usar parámetros extra.

Cuando llama funciones
-Para capturar y gestionar ese error sin mezclarlo con el código normal.

-Permite decidir qué hacer: mostrar mensaje, repetir, abortar…


## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### Respuesta

```java
public class Calculadora {

    public static double raiz(double x) {
        if (x < 0) {
            throw new IllegalArgumentException("El número no puede ser negativo");
        }
        return Math.sqrt(x);
    }
}
```
-Si x es negativo → lanza una excepción.

-Si es válido → devuelve la raíz.
```java
public class Main { //controlando el error
    public static void main(String[] args) {
        try {
            double r = Calculadora.raiz(-9);
            System.out.println("Resultado: " + r);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```
-try → intentamos ejecutar la operación.

-catch → capturamos la excepción y mostramos el mensaje.


## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Respuesta

### ✔️ ¿Qué es lanzar una excepción?
Es interrumpir la ejecución normal y crear un objeto de error que “salta” hacia arriba.
```java
throw new IllegalArgumentException("El número no puede ser negativo");
```
### ✔️ ¿Qué es capturar o controlar una excepción?
Es atraparla para evitar que el programa termine abruptamente y decidir qué hacer.
```java
try {
    Calculadora.raiz(-9);
} catch (IllegalArgumentException e) {
    System.out.println("Error: " + e.getMessage());
}
```
### ✔️ ¿Qué es que una excepción se propague?
Si una función no captura la excepción, esta sube automáticamente a la función que la llamó.

main → llama a → raiz
raiz lanza excepción
raiz NO la captura → sube a main
main SÍ la captura → se maneja allí

### ✔️ ¿Qué pasa con las funciones por donde pasa la excepción?
-Cada función que no la captura se aborta inmediatamente.

-No ejecuta el resto de su código.

-No se “reanuda” después.

-La ejecución continúa solo en el primer catch que la atrape.
```java 
public class Calculadora {
    public static double raiz(double x) {
        if (x < 0) {
            throw new IllegalArgumentException("El número no puede ser negativo");
        }
        return Math.sqrt(x);
    }
}
public class Main {
    public static void main(String[] args) {
        try {
            double r = Calculadora.raiz(-9);  // aquí se lanza la excepción
            System.out.println("Resultado: " + r); // esto NO se ejecuta
        } catch (IllegalArgumentException e) {
            System.out.println("Error capturado en main: " + e.getMessage());
        }
    }
}
```


## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### Respuesta

### ⭐ 1. No hace falta comprobar errores en cada función
En C, cada función debe:

-devolver un código de error,

-y la función que la llama debe comprobarlo,

-y la siguiente también…

En Java, si no capturas la excepción, sube sola.
Solo la capturas donde realmente te interesa.

### ⭐ 2. El código normal queda limpio
En C, la lógica se mezcla con:

-if (error) return -1;

-variables de error,

-comprobaciones constantes.

En Java, el código normal va en el try  
y el código de error va en el catch.
Separación total.

### ⭐ 3. Las funciones intermedias no tienen que saber del error
Si main llama a a(), que llama a b(), que llama a c():

-En C → cada una debe comprobar y reenviar el error.

-En Java → si c() lanza la excepción, sube directamente hasta main.

Las funciones intermedias se abortan y no continúan.

### ⭐ 4. No hay reanudación: el flujo es claro y seguro
Cuando una excepción sube:

-la función donde ocurrió se detiene,

-las funciones intermedias se detienen,

-solo continúa el programa en el primer catch que la capture.

Esto evita estados incoherentes y errores silenciosos.
```java
public static double raiz(double x) {
    if (x < 0) {
        throw new IllegalArgumentException("negativo");
    }
    return Math.sqrt(x);
}
try {
    double r = Calculadora.raiz(-9);
} catch (IllegalArgumentException e) {
    System.out.println("Error: " + e.getMessage());
}
```


## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### Respuesta

### ✔️ ¿Las excepciones suelen ser objetos?
Sí.
En orientación a objetos (y en Java en particular), una excepción es un objeto que contiene información sobre el error:

-tipo de error,

-mensaje,

-dónde ocurrió,

-pila de llamadas, etc.

### ✔️ ¿Qué ventajas tiene esto en términos de encapsulación?
Al ser objetos, las excepciones pueden encapsular toda la información relevante del error dentro de sí mismas.

Esto permite:

-describir el error con precisión,

-adjuntar datos adicionales,

-tener distintos tipos de errores bien diferenciados,

-tratarlos de forma específica según su clase.

Es decir: cada tipo de error puede ser una clase distinta, con su propio comportamiento.

### ✔️ ¿Podemos crear excepciones personalizadas?
Sí, totalmente.
En Java basta con crear una clase que herede de Exception o RuntimeException.
```java 
public class NumeroNegativoException extends RuntimeException {
    public NumeroNegativoException(String msg) {
        super(msg);
    }
}
if (x < 0) {
    throw new NumeroNegativoException("No se admiten números negativos");
}
```


## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Respuesta

Toda excepción en Java siempre incluye al menos:

### ⭐ 1. Un mensaje descriptivo del error
Lo que tú pasas en el constructor ("El número no puede ser negativo").
Sirve para entender qué ha fallado.

### ⭐ 2. La traza de la pila (stack trace)
Es la lista de funciones por las que pasó el programa hasta llegar al error.
Incluye:

-nombre de las funciones,

-archivo,

-número de línea.

Esto es oro puro para depurar, porque te dice exactamente dónde ocurrió el problema y cómo se llegó hasta allí.

### ✔️ Comparación con C
En C:

-tú tienes que inventarte cómo comunicar el error,

-no hay mensaje automático,

-no hay traza de llamadas,

-si quieres saber dónde falló, tienes que imprimirlo tú manualmente.

En Java:

-el objeto excepción ya encapsula toda esa información,

-y llega intacta al manejador (catch),

-sin que tengas que pasar nada a mano.


## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### Respuesta

### ✔️ ¿Se pueden tener varios catch?
Sí.
Un bloque try puede ir seguido de varios bloques catch, cada uno para un tipo distinto de excepción.

### ✔️ ¿Cuántos catch se ejecutan?
Solo uno.  
El primero cuyo tipo coincida con la excepción lanzada.

Una vez se ejecuta un catch, los demás se ignoran.
```java
try {
    double r = Calculadora.raiz(-9);
} 
catch (IllegalArgumentException e) {
    System.out.println("Error de argumento");
} 
catch (Exception e) {
    System.out.println("Otro error");
}
```


## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### Respuesta

### ✔️ ¿Cómo garantizamos que un código se ejecuta siempre?
Usamos el bloque finally.

El bloque finally se ejecuta siempre, ocurra o no ocurra una excepción, y se capture o no.
Sirve para cerrar ficheros, liberar recursos, desconectar bases de datos, etc.
```java
try {
    double r = Calculadora.raiz(-9);
    System.out.println("Resultado: " + r);
} 
catch (IllegalArgumentException e) {
    System.out.println("Error: " + e.getMessage());
} 
finally {
    System.out.println("Cerrando recursos...");
}
```
### ✔️ Ejemplo con try + finally (sin catch)
Esto es útil cuando no quieres manejar la excepción aquí, pero sí necesitas liberar recursos antes de que la excepción siga subiendo.
```java
try {
    double r = Calculadora.raiz(-9);  // lanza excepción
    System.out.println("Resultado: " + r);
} 
finally {
    System.out.println("Liberando recursos antes de propagar la excepción...");
}
```


## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta

### ✔️ ¿Puede haber finally sin catch?
Sí.
Un bloque try puede tener:

-try + catch + finally, o

-try + finally (sin catch).

### ✔️ ¿Se ejecuta siempre el finally?
Sí, siempre:

-si hay excepción,

-si no hay excepción,

-si la excepción se captura,

-si la excepción se propaga,

-incluso si hay un return dentro del try.

El finally siempre se ejecuta antes de salir del bloque.

### ✔️ ¿Y si hay un return dentro del try?
El finally se ejecuta igualmente, antes de que el método devuelva el valor.
```java
try {
    double r = Calculadora.raiz(-9);
    return;
} 
catch (IllegalArgumentException e) {
    System.out.println("Error: " + e.getMessage());
} 
finally {
    System.out.println("Cerrando recursos...");
}
//sin catch
try {
    double r = Calculadora.raiz(-9);  // lanza excepción
    return;
} 
finally {
    System.out.println("Liberando recursos...");
}
```


## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta

### Excepciones controladas (checked exceptions)
-Son excepciones que el compilador obliga a manejar.

-Deben aparecer en un try-catch o declararse con throws.

-Representan errores esperables y recuperables.

Ejemplos típicos:

-IOException

-SQLException

-FileNotFoundException

-ClassNotFoundException

### Excepciones no controladas (unchecked exceptions)
-Son las que no es obligatorio capturar.

-Heredan de RuntimeException.

-Representan errores de programación o situaciones que no se suelen recuperar.

Ejemplos típicos:

-NullPointerException

-IllegalArgumentException

-ArithmeticException

-IndexOutOfBoundsException

### ✔️ ¿Qué papel juega RuntimeException?
RuntimeException es la superclase de todas las excepciones no controladas.

-Todo lo que herede de RuntimeException no requiere try-catch.

-Se usa para errores que indican fallos del programador, no del entorno.

### ✔️ ¿Podemos crear excepciones personalizadas?
Sí.
Podemos crear:

-controladas → heredando de Exception

-no controladas → heredando de RuntimeException
```java
public class NumeroNegativoException extends RuntimeException {
    public NumeroNegativoException(String msg) {
        super(msg);
    }
}
```
### ✔️ Cuándo preferir excepciones controladas
Situaciones donde el error es esperable y el programa puede recuperarse:

-Abrir un fichero que puede no existir.

-Leer de red o base de datos (fallos externos).

-Operaciones de entrada/salida (I/O).

-Cargar una clase o recurso que puede faltar.

### ✔️ Cuándo preferir excepciones no controladas
Situaciones que indican fallos de programación:

-Pasar argumentos inválidos a un método.

-Dividir entre cero.

-Acceder fuera de los límites de un array.

-Usar un objeto nulo.


## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta

### ✔️ ¿Qué es throws?
throws es una declaración en la cabecera de un método que indica que ese método puede lanzar una excepción controlada y que no la va a capturar él mismo.
```java
public static double raiz(double x) throws Exception {
    if (x < 0) {
        throw new Exception("Número negativo");
    }
    return Math.sqrt(x);
}
```
### ✔️ ¿Para qué se usa?
Para delegar el manejo de la excepción a quien llame al método.

Es decir:
👉 “Yo no la capturo aquí; que la gestione quien me llame”.

### ✔️ ¿Por qué es alternativa a capturar una excepción controlada?
Porque en Java, si una excepción es controlada (checked), el compilador te obliga a:

-capturarla con try-catch, o

-declararla con throws.

Por eso throws es la alternativa a poner un try-catch dentro del método.

### ✔️ Mini‑ejemplo comparativo
Opción A: capturar dentro del método
```java
public static double raiz(double x) {
    try {
        if (x < 0) throw new Exception("negativo");
        return Math.sqrt(x);
    } catch (Exception e) {
        System.out.println("Error en raiz");
        return 0;
    }
}
```
Opción B: delegar con throws
```java
public static double raiz(double x) throws Exception {
    if (x < 0) throw new Exception("negativo");
    return Math.sqrt(x);
}
//main
try {
    double r = raiz(-9);
} catch (Exception e) {
    System.out.println("Error capturado en main");
}
```


## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta

### ✔️ Ejemplo de método que abre un fichero y declara que no quiere manejar la excepción
Este método:

-intenta abrir un fichero,

-no captura la excepción FileNotFoundException,

-la declara con throws para que se propague,

-pero usa finally para cerrar el recurso si se llegó a abrir.
```java
import java.io.*;

public class Lector {

    public static void leerFichero(String nombre) throws FileNotFoundException {
        FileInputStream f = null;

        try {
            f = new FileInputStream(nombre);   // puede lanzar FileNotFoundException
            System.out.println("Fichero abierto correctamente");
        }
        finally {
            System.out.println("Ejecutando finally...");
            if (f != null) {
                try { f.close(); } catch (IOException e) {}
            }
        }
    }
}
//uso desde main
public class Main {
    public static void main(String[] args) {
        try {
            Lector.leerFichero("datos.txt");
        } catch (FileNotFoundException e) {
            System.out.println("El fichero no existe");
        }
    }
}
```


## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta

### ✔️ ¿Podemos poner excepciones no controladas en throws?
Sí, se puede, pero no sirve para nada práctico.
```java
public void f() throws RuntimeException { }
```
El compilador no obliga a capturar una excepción no controlada, así que ponerla en throws no cambia nada.

### ✔️ ¿Debe el método llamador poner try-catch en ese caso?
No está obligado.  
Las excepciones no controladas no requieren try-catch.

El método llamador solo pondría un try-catch si quiere, no porque el compilador lo exija.

### ✔️ ¿Qué sentido tendría entonces poner una excepción no controlada en throws?
Prácticamente ninguno técnico.
Solo puede tener sentido como documentación:

-para avisar al programador de que ese método puede lanzar una RuntimeException,

-aunque no esté obligado a capturarla.

Pero funcionalmente, no cambia nada.


## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta

### ✔️ ¿Cuándo usar excepciones controladas?
Se usan cuando el error es esperable, externo al programa y razonablemente recuperable.

Ejemplos típicos:

-Fallos de entrada/salida (IOException).

-Fichero que no existe (FileNotFoundException).

-Problemas de red o base de datos (SQLException).

-Recursos externos que pueden fallar.

👉 La idea: el programador que llama debe decidir qué hacer, porque es un error normal del entorno.

### ✔️ ¿Cuándo usar excepciones no controladas?
Se usan cuando el error indica fallo del programador o mal uso de la API, y no tiene sentido obligar a capturarlo.

Ejemplos típicos:

-Argumentos inválidos (IllegalArgumentException).

-Índices fuera de rango (IndexOutOfBoundsException).

-Divisiones por cero (ArithmeticException).

-Objetos nulos (NullPointerException).

👉 La idea: esto no se “recupera”; hay que corregir el código.

### ✔️ ¿Existen ambas opciones en todos los lenguajes?
No.
Muchos lenguajes solo tienen excepciones no controladas (unchecked).

Ejemplos:

-Python

-JavaScript

-C++

-Ruby

-C# (técnicamente todas son unchecked)

En estos lenguajes, no existe el concepto de “excepción controlada” como en Java.

### ✔️ En los lenguajes que solo tienen una opción, ¿cuál es la habitual?
La opción habitual es la de excepciones no controladas (tipo Java RuntimeException).

¿Por qué?

-Simplifica el lenguaje.

-Evita obligar al programador a poner try-catch por todas partes.

-Se confía en que el programador capture solo lo que realmente quiere manejar.


## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta

### ✔️ ¿Tiene sentido lanzar excepciones dentro del catch?
Sí.
A veces, dentro de un catch, quieres:

-lanzar otra excepción distinta, más específica o más informativa,

-o envolver la excepción original en otra.
```java
try {
    leerFichero("datos.txt");
} catch (IOException e) {
    throw new RuntimeException("Error leyendo configuración", e);
}
```
-capturas una excepción controlada (IOException),

-lanzas una no controlada (RuntimeException) para simplificar el manejo.

### ✔️ ¿Se puede relanzar la misma excepción capturada?
Sí, totalmente.
```java
catch (IOException e) {
    System.out.println("Log del error...");
    throw e;   // relanzar la misma excepción
}
```
### ✔️ ¿Cuándo tiene sentido relanzar la misma excepción?
Cuando quieres:

⭐ 1. Registrar (log) el error, pero no manejarlo
Ejemplo: escribir en un log y dejar que otro nivel decida qué hacer.

⭐ 2. Limpiar recursos antes de que la excepción siga subiendo
Ejemplo: cerrar conexiones, liberar memoria, etc.

⭐ 3. Añadir contexto pero sin cambiar el tipo de error
Ejemplo: indicar qué parte del programa falló.

### ✔️ Ejemplo completo: lanzar otra excepción desde un catch
```java
try {
    double r = Calculadora.raiz(-9);
} 
catch (IllegalArgumentException e) {
    throw new RuntimeException("Error al calcular la raíz cuadrada", e);
}
```
-Capturas una excepción esperada.

-Lanzas una nueva excepción más general para que el nivel superior decida.

### ✔️ Ejemplo completo: relanzar la misma excepción
```java
try {
    double r = Calculadora.raiz(-9);
} 
catch (IllegalArgumentException e) {
    System.out.println("Registrando el error...");
    throw e;   // la misma excepción sigue subiendo
}
```
-Añades información (log).

-La excepción continúa propagándose.


## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta

### ✔️ ¿Qué significa que una excepción sea la causa de otra?
Significa que una excepción de alto nivel se construye envolviendo otra excepción de bajo nivel que fue la que realmente ocurrió.

La excepción de alto nivel:

-da más contexto,

-pero no pierde la información original,

-porque guarda la excepción interna como causa.
```java
throw new MiExcepcionDeAltoNivel("Mensaje", causa);
```
### ✔️ Ejemplo: capturar una excepción de bajo nivel y encapsularla en otra personalizada
Supongamos que leer un fichero falla con IOException, pero queremos lanzar una excepción más “de negocio”, por ejemplo ErrorDeConfiguracion.

Excepción personalizada:
```java
public class ErrorDeConfiguracion extends Exception {
    public ErrorDeConfiguracion(String msg, Throwable causa) {
        super(msg, causa);
    }
}
```
Código que captura y encapsula:
```java
try {
    FileInputStream f = new FileInputStream("config.txt");
} 
catch (IOException e) {
    throw new ErrorDeConfiguracion("No se pudo cargar la configuración", e);
}
```
-IOException es la causa.

-ErrorDeConfiguracion es la excepción de alto nivel que se lanza.

### ✔️ ¿Se ve la causa cuando la excepción sale por pantalla?
Sí.
Cuando una excepción tiene causa, Java imprime ambas:

-primero la excepción de alto nivel,

-luego la palabra "Caused by:",

-y después la traza completa de la excepción original.

ErrorDeConfiguracion: No se pudo cargar la configuración
    at ...
Caused by: java.io.FileNotFoundException: config.txt (No existe el archivo)
    at ...


