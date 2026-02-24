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

### En el lenguaje C, al no existir un sistema de excepciones, el control de errores debe realizarse mediante el flujo de ejecución convencional. La función no puede "saltarse" el retorno, por lo que se debe pactar una señal entre la función y quien la llama para indicar que algo ha fallado.

### Dos opciones comunes para diseñar este control son:

### Uso de valores de retorno especiales (valores centinela): Se reserva un valor que no sea un resultado válido de la función (como un número negativo o una constante NaN) para indicar el error.

### Uso de punteros de estado: Se añade un parámetro adicional a la función (un puntero) donde se escribe el código del error, permitiendo que el retorno de la función se use exclusivamente para el resultado matemático.

```C
// Opción 1: Valor centinela
double raiz_centinela(double n) {
    if (n < 0) return -1.0; 
    return sqrt(n);
}

// Opción 2: Puntero de estado
double raiz_puntero(double n, int *error) {
    if (n < 0) {
        *error = 1; // Código de error para n negativo
        return 0;
    }
    *error = 0;
    return sqrt(n);
}
```




## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Una excepción es un evento que ocurre durante la ejecución de un programa y que interrumpe el flujo normal de las instrucciones. Se considera un objeto que encapsula información sobre un error o una condición inesperada que el método actual no sabe o no puede resolver por sí mismo.

### El objetivo de un programador al implementar funciones es separar la "lógica de negocio" (lo que debe hacer la función) de la "lógica de control de errores". Al llamar a funciones, el objetivo es delegar la gestión del fallo a un bloque especializado, evitando que el código principal se llene de estructuras if-else constantes para comprobar cada paso intermedio.


## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### En Java, se emplea la clase Calculadora para encapsular el comportamiento matemático. Si el argumento es inválido, se interrumpe la ejecución mediante el lanzamiento de una instancia de excepción.

```Java
public class Calculadora {
    public double raiz(double n) {
        if (n < 0) {
            throw new IllegalArgumentException("No se permite raíz de negativos");
        }
        return Math.sqrt(n);
    }
}

public class Principal {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();
        try {
            double res = calc.raiz(-5.0);
            System.out.println("Resultado: " + res);
        } catch (IllegalArgumentException e) {
            System.out.println("Error capturado: " + e.getMessage());
        }
    }
}
```


## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Lanzar una excepción consiste en crear un objeto de error y entregarlo al sistema de ejecución mediante la palabra throw. Controlar o capturar es el acto de interceptar ese objeto mediante un bloque catch para realizar una acción correctiva. La propagación es el proceso por el cual, si una función no captura la excepción, esta viaja hacia atrás por la pila de llamadas buscando a alguien que la gestione.

### A medida que la excepción se propaga, las funciones en la pila de llamadas finalizan de forma abrupta. No se llega a ejecutar ninguna línea de código posterior al punto donde se produjo el error o la llamada fallida. Estas funciones no se reanudan; simplemente desaparecen de la memoria (pila) como si hubieran terminado por un return forzado.

### En el ejemplo de la raíz, si el método raiz lanza la excepción, el control sale inmediatamente de raiz. Si el main no tuviera un try-catch, el main también finalizaría inmediatamente y el programa terminaría mostrando un error en la consola.


## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### La principal ventaja frente a C es la limpieza del código. En C, si una función a nivel 5 de profundidad falla, todas las funciones intermedias (nivel 4, 3, 2 y 1) deben incluir lógica para capturar ese error y devolverlo manualmente hacia arriba. Esto ensucia las firmas de las funciones y complica el mantenimiento.

### Con la propagación de Java, las funciones intermedias pueden ignorar completamente el error si no saben cómo arreglarlo. La excepción "salta" automáticamente por encima de ellas hasta encontrar un manejador competente, permitiendo que el programador se concentre solo en el flujo donde realmente se puede solucionar el problema.


## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### En Java, las excepciones son objetos que pertenecen a una jerarquía de clases. Al ser objetos, se benefician de la encapsulación, permitiendo agrupar no solo un mensaje de error, sino también datos contextuales del momento del fallo. Esto permite que el manejador reciba una entidad rica en información en lugar de un simple número entero.

### Es posible y recomendable crear excepciones personalizadas mediante la herencia. Al crear una clase que hereda de Exception o RuntimeException, se dota al sistema de nombres de error específicos para el dominio del problema (por ejemplo, SaldoInsuficienteException), lo que hace el código mucho más legible y profesional.


## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Comparado con los códigos de error de C, un objeto excepción en Java transporta tres elementos críticos:

#### El tipo de la excepción: El nombre de la clase (identifica qué ocurrió).

#### El mensaje descriptivo: Una cadena de texto con detalles para el humano.

#### La traza de la pila (Stack Trace): Un historial detallado de los archivos y líneas de código por los que ha pasado la ejecución antes de fallar.

### Esta información es fundamental para el diagnóstico, ya que permite saber exactamente el "camino" que tomó el programa antes del colapso, algo que en C requeriría herramientas externas de depuración.


## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### En Java, un bloque try puede ir seguido de múltiples bloques catch. Esto permite definir diferentes estrategias de recuperación según el tipo de error ocurrido (por ejemplo, un tratamiento para errores de red y otro para errores de formato de datos).

### Sin embargo, solo se ejecuta un bloque catch: el primero que coincida con el tipo de la excepción lanzada o con una de sus clases padre. Por esta razón, se deben colocar las excepciones más específicas (hijas) arriba y las más genéricas (padres, como Exception) abajo.


## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### El bloque finally se utiliza para garantizar la ejecución de código de limpieza, como cerrar ficheros o liberar conexiones, independientemente de si el bloque try terminó con éxito o si se lanzó una excepción. Es la red de seguridad para evitar fugas de memoria o recursos bloqueados.

```Java
// Ejemplo con catch y finally
try {
    abrirFichero();
    leerDatos();
} catch (IOException e) {
    System.out.println("Error de lectura");
} finally {
    cerrarFichero(); // Se ejecuta siempre
}

// Ejemplo sin catch (solo para limpieza y propagar)
try {
    conectarBaseDatos();
    realizarConsulta();
} finally {
    desconectar(); // Se ejecuta y luego la excepción sigue propagándose
}
```


## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### El bloque finally es opcional si hay un catch, pero puede existir perfectamente sin él (formato try-finally). Su característica principal es que se ejecuta siempre, incluso si ocurre una excepción no capturada.

### Un detalle importante es que si dentro del try hay una sentencia return, el bloque finally se ejecutará justo después del return pero antes de que el control vuelva realmente al llamador. El sistema garantiza que nada interrumpa esta limpieza.


## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Las excepciones controladas (Checked) son aquellas que el compilador obliga a capturar o declarar. Representan condiciones externas de las que el programa debería poder recuperarse. Las no controladas (Unchecked) heredan de RuntimeException y suelen representar errores de lógica del programador.

| **Tipo** | Ejemplo | Cuándo usar |
|----------|-------------|----------|
| **Controlada** | IOException | Fallos de red, ficheros inexistentes, base de datos caída. |
| **No controlada** | NullPointerException | Parámetros nulos, índices fuera de rango, errores de lógica. |


## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### La palabra clave throws se utiliza en la firma de un método para declarar que dicho método puede lanzar ciertas excepciones. Es un aviso para el programador que use ese método, indicándole que debe estar preparado para gestionar esos errores.

### Se considera la alternativa a capturar la excepción porque, en lugar de resolver el problema localmente, el método admite que no puede manejarlo y permite que la excepción se propague hacia arriba en la pila de llamadas.


## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### En este ejemplo, el método leerConfiguracion se desentiende de la gestión del error de apertura, pero asegura que cualquier intento de apertura se limpie.

```Java
public void leerConfiguracion(String ruta) throws FileNotFoundException {
    FileReader fr = new FileReader(ruta);
    try {
        // Procesamiento del fichero
    } finally {
        // El cierre debería ir aquí (simplificado para el ejemplo)
        System.out.println("Cerrando recursos...");
    }
}
```


## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### REs técnicamente posible incluir excepciones no controladas (como NullPointerException) en el throws, pero el compilador no lo exige. El método llamador no estará obligado a poner un try-catch aunque se declaren.

### El único sentido de hacer esto es puramente documentativo. Sirve para advertir de forma explícita al usuario de la función que, bajo ciertas circunstancias, ese error podría ocurrir, aunque lo ideal sería evitar que ocurran mediante una programación defensiva.


## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Se recomienda usar excepciones controladas para errores que son ajenos al control del programador (entorno, red, usuario). Se deben evitar para errores que el programador puede prevenir con un simple if (como comprobar si un puntero es nulo).

### No todos los lenguajes tienen ambos tipos. En C++ o Python, todas las excepciones son "no controladas" (el compilador no te obliga a nada). En los lenguajes donde solo existe una opción, la más habitual es el modelo de excepciones no controladas, ya que hace el código menos verboso y más flexible.


## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Es una práctica común lanzar excepciones dentro de un catch. Se puede relanzar la misma excepción si solo se quería hacer una anotación en el log pero se desea que el error siga subiendo. También se puede lanzar una excepción diferente, a menudo de mayor nivel de abstracción.

```Java
// Caso 1: Relanzar
catch (IOException e) {
    log.error("Fallo de IO");
    throw e; 
}

// Caso 2: Lanzar una nueva (encapsulación)
catch (SQLException e) {
    throw new ErrorDeAccesoDatosException("No se pudo conectar");
}
```


## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Una excepción es la causa de otra cuando un error de bajo nivel (técnico) provoca un error de alto nivel (negocio). Esto permite mantener la abstracción sin perder la pista de qué originó realmente el problema.

```Java
try {
    abrirArchivoProtegido();
} catch (SecurityException e) {
    // La SecurityException es la "causa" de mi nueva excepción
    throw new AccesoDenegadoException("No tienes permisos", e);
}
```

### Cuando una excepción con causa sale por pantalla, el sistema muestra la cadena completa. Primero aparece la excepción principal y debajo un encabezado "Caused by:" con el error original, lo cual es extremadamente útil para el programador.