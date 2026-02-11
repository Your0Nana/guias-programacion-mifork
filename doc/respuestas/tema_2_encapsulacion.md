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

### La encapsulación busca agrupar en una misma entidad (la clase) tanto los datos (atributos) como las operaciones que actúan sobre ellos (métodos). Se pretende que el objeto sea una unidad autónoma y coherente, evitando que la lógica esté dispersa como ocurre en la programación procedimental pura, donde las funciones y las estructuras de datos suelen estar separadas.

### Por su parte, la ocultación de información es un principio que busca restringir el acceso directo a los componentes internos de un objeto. Se intenta que los detalles de implementación permanezcan invisibles para el "mundo exterior", permitiendo que solo se interactúe con el objeto a través de mecanismos controlados.

### Entre las ventajas de la ocultación destacan:

### ->Mantenibilidad: Se puede cambiar la implementación interna (por ejemplo, cambiar un tipo de dato) sin afectar a quienes usan la clase.

### ->Integridad: Se evita que el estado del objeto sea modificado de forma arbitraria o errónea por código externo.

### ->Reducción de la complejidad: El usuario de la clase solo necesita saber qué hace el objeto, no cómo lo hace.


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### La interfaz pública representa el conjunto de métodos y constantes que una clase expone al exterior. Es, en esencia, el "contrato" o la lista de servicios que el objeto promete realizar para otros componentes del sistema. En C, esto sería comparable a lo que se declara en un archivo de cabecera .h.

### Esta interfaz se relaciona directamente con la ocultación de información porque actúa como un filtro. Mientras que los detalles complejos y los datos sensibles se mantienen privados, la interfaz pública ofrece una vía de comunicación simplificada y segura. Se garantiza que, mientras la interfaz no cambie, el código que utiliza el objeto seguirá funcionando correctamente aunque el interior de la clase sea totalmente reescrito.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### El diseño de la interfaz pública es crítico porque determina cómo interactuarán el resto de los módulos con la clase. Una vez que una clase está siendo utilizada en un proyecto (o por terceros), cualquier cambio en su interfaz pública (como cambiar el nombre de un método o sus parámetros) obliga a modificar todo el código que la utiliza, lo que puede generar errores en cadena.

### Por el contrario, cambiar la implementación interna es sencillo siempre que la interfaz permanezca intacta. Por ello, se recomienda que la interfaz sea lo más pequeña y estable posible (principio de mínimo privilegio), exponiendo únicamente lo estrictamente necesario para cumplir con la funcionalidad requerida.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Una invariante de clase es una condición o regla que debe ser siempre verdadera para cualquier objeto de esa clase durante toda su vida. Por ejemplo, en una clase Fecha, una invariante sería que el mes siempre esté entre 1 y 12. Si estos datos fueran públicos, cualquier parte del programa podría asignar un valor erróneo (como 15) al mes.

### La ocultación de información ayuda a preservar estas invariantes al marcar los atributos como privados. Al obligar a que cualquier modificación pase por métodos controlados (como un "setter"), se puede incluir lógica de validación que impida que el objeto entre en un estado inconsistente o inválido, asegurando que las reglas de negocio se cumplan siempre.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### En este ejemplo, se utilizan los modificadores de acceso para proteger los datos internos.

```Java
public class Punto {
    // Atributos privados: no accesibles desde fuera de la clase
    private double x;
    private double y;

    // Constructor público
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    // Interfaz pública: métodos accesibles por otros
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
```
### La interfaz pública de esta clase está compuesta por el constructor Punto(double, double) y el método calcularDistanciaAOrigen(). El modificador private indica que el miembro solo es visible dentro de la propia clase, mientras que public permite el acceso desde cualquier otra parte del programa.


## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### Los modificadores de acceso se aplican a los miembros de la clase, que incluyen los atributos (variables de instancia o de clase) y los métodos (incluyendo los constructores). Su uso es fundamental para definir el nivel de encapsulamiento de cada componente.

### También se pueden aplicar a las propias clases (aunque con ciertas restricciones, como que solo puede haber una clase pública por archivo). No se pueden aplicar a variables locales dentro de un método, ya que estas tienen su propio ámbito limitado y desaparecen al finalizar la ejecución de la función.


## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Además de public y private, Java ofrece dos niveles más:

### ->Default (Package-private): No se usa ninguna palabra clave. El miembro es visible solo para clases dentro del mismo paquete (carpeta).

### ->Protected: El miembro es visible para clases del mismo paquete y para clases hijas (herencia), incluso si están en paquetes distintos.

### En otros lenguajes, la gestión cambia. En C++, se definen bloques mediante etiquetas (public:, private:). En Python, la ocultación es puramente convencional: se añade un guion bajo (_) al inicio del nombre para indicar que es privado, pero el lenguaje no impide técnicamente el acceso, apelando a la responsabilidad del programador.


## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### En POO, los miembros privados están ocultos para otras clases, pero son visibles para otras instancias de la misma clase. Esto significa que un objeto de tipo Punto puede acceder directamente a los atributos privados de otro objeto Punto si este se le pasa como parámetro.

```Java
public double calcularDistanciaAPunto(Punto otro) {
    // Se accede directamente a 'otro.x' aunque sea privado
    double dx = this.x - otro.x; 
    double dy = this.y - otro.y;
    return Math.sqrt(dx * dx + dy * dy);
}
```
### Esto se permite porque la visibilidad se define a nivel de clase, no de objeto. Dado que el código está escrito dentro de la clase Punto, tiene "permiso" para conocer la estructura interna de cualquier instancia de dicha clase.

## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Los getters (accesores) y setters (mutadores) son métodos públicos diseñados para leer y modificar, respectivamente, el valor de un atributo privado. Por convención, en Java se nombran como getAtributo() y setAtributo(valor).

### El objetivo no es simplemente dar acceso, sino proporcionar un punto de control. Un getter puede devolver una copia para evitar modificaciones accidentales, y un setter puede validar que el nuevo valor sea correcto antes de asignarlo, protegiendo así la lógica interna de la clase.


## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Cuando se habla de "seguridad" en el contexto de la ocultación, no se refiere a seguridad contra ataques informáticos externos (hacking), sino a seguridad en el diseño del software. Es una protección contra errores de programación accidentales.

### Se busca evitar que un programador, por desconocimiento o descuido, altere una variable interna que deje al objeto en un estado corrupto. Es un mecanismo para garantizar la robustez del sistema y asegurar que los componentes interactúen únicamente de la forma prevista por el diseñador de la clase.


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Un miembro de instancia (sin static) pertenece a cada objeto individual; cada Punto tiene sus propias coordenadas x e y. Un miembro de clase (con static) pertenece a la clase en su conjunto y es compartido por todas las instancias.

### Los miembros de clase también se pueden (y suelen) ocultar. Un atributo static private puede ser útil para llevar un contador interno de objetos creados o almacenar una configuración compartida que no debe ser alterada desde el exterior sin supervisión.


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Sí, tiene mucho sentido en varios patrones de diseño. Un constructor privado impide que se puedan crear instancias de la clase desde fuera mediante el operador new. Esto se utiliza, por ejemplo, en clases de utilidad que solo contienen métodos estáticos (como Math) para evitar que alguien cree objetos innecesarios.

### También es fundamental en el patrón Singleton, donde se garantiza que solo exista una única instancia de la clase en todo el programa, o en el uso de métodos factoría, donde la propia clase controla cómo y cuándo se crean sus objetos.


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Para definir miembros de clase se utiliza la palabra clave static. En el ejemplo del Punto, se usarán para rastrear los valores máximos de coordenadas vistos hasta ahora.

```Java
public class Punto {
    private double x, y;
    // Miembros de clase (compartidos)
    private static double maxX = 0;
    private static double maxY = 0;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
        // Actualización de los valores máximos de la clase
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    public static double getMaxX() { return maxX; }
    public static double getMaxY() { return maxY; }
}
```


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Un método factoría es un método estático que devuelve una instancia de la clase. Al ser estático, se puede invocar sin tener aún el objeto creado.

```Java
public static Punto crearPuntoRedondeado(double x, double y) {
    // Se usa Math.round para redondear y se llama al constructor
    return new Punto(Math.round(x), Math.round(y));
}
```
### Se ha usado static porque el método debe ser accesible a través de la clase (Punto.crearPuntoRedondeado(...)) antes de que la instancia en sí exista


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Se puede cambiar la estructura de datos interna (de dos variables a un array) sin que el usuario de la clase lo note, manteniendo la misma interfaz pública.

```Java
public class Punto {
    private double[] coords = new double[2]; // x está en [0], y en [1]

    public Punto(double x, double y) {
        this.coords[0] = x;
        this.coords[1] = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(coords[0] * coords[0] + coords[1] * coords[1]);
    }
}
```


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Aunque un atributo tenga un getter y un setter públicos, sigue siendo preferible mantenerlo privado. Si en el futuro se desea añadir una validación o si el dato debe derivarse de otro valor en lugar de almacenarse, solo se tendría que modificar el método. Si el atributo fuera público, el cambio rompería todo el código externo.

### La convención habitual es que todos los atributos sean privados. Esto refuerza las invariantes de clase, asegurando que el estado interno sea siempre gestionado por la lógica de la clase y nunca por agentes externos impredecibles.


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Una clase es inmutable si su estado no puede cambiar una vez que el objeto ha sido creado (por ejemplo, la clase String en Java). Un método modificador es aquel que altera el estado del objeto. No siempre es un setter; puede ser cualquier método que realice una operación que cambie un valor interno (como acelerar()).

### Las ventajas de la inmutabilidad incluyen:

### ->Simplicidad: Los objetos son más fáciles de entender y predecir.

### ->Seguridad en hilos (Thread-safety): No hay riesgo de que varios procesos cambien el objeto a la vez.

### ->Seguridad en el uso: Pueden compartirse libremente sin miedo a que alguien los modifique por error.


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### No es recomendable incluirlos por defecto. De hecho, la tendencia moderna es favorecer la inmutabilidad siempre que sea posible. Si un objeto no necesita cambiar tras su creación, es mejor no proporcionar métodos que permitan su modificación.

### Incluir setters "por si acaso" debilita el encapsulamiento y expone innecesariamente el estado interno, lo que a menudo conduce a diseños de software más frágiles y difíciles de depurar.


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### La clase String en Java es inmutable. Al concatenar dos cadenas (usando +), no se modifica ninguna de las cadenas originales, sino que se crea un objeto String totalmente nuevo en memoria que contiene el resultado.

### Si se requiere realizar muchas concatenaciones en un bucle, este comportamiento es muy ineficiente. En esos casos, se debe emplear la clase StringBuilder, que sí es mutable y permite construir cadenas paso a paso de forma mucho más rápida y con menor consumo de memoria.


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### En Java, el operador == compara la identidad (si ambas referencias apuntan a la misma dirección de memoria). Para comparar el contenido (si dos objetos son "lógicamente iguales"), se debe usar el método .equals().

### Por defecto, el método .equals() heredado de Object se comporta igual que ==. Las clases como String o Punto deben sobrescribir este método para definir qué significa que dos instancias sean iguales (por ejemplo, que sus coordenadas coincidan). Por tanto, las cadenas en Java siempre se comparan con .equals().


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Las clases Wrapper (envoltorios) son clases que representan tipos primitivos como si fueran objetos (ej. Integer para int, Double para double). Esto es necesario porque algunas estructuras de Java, como las colecciones (ArrayList), solo pueden almacenar objetos, no tipos primitivos.

### En Java moderno, el proceso es automático mediante el autoboxing y unboxing. La ventaja es que permiten tratar a los tipos básicos con la potencia de los objetos, proporcionando además métodos de utilidad para conversiones (como Integer.parseInt()). No todos los lenguajes los necesitan; en Python o Ruby, por ejemplo, hasta los números básicos son ya objetos de por sí.


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Un enumerado es un tipo de dato que permite definir un conjunto fijo de constantes con nombre. En Java, los enum son mucho más potentes que en C; no son simples enteros, sino clases especiales que pueden tener atributos, constructores y métodos.

### En términos de encapsulación, los enumerados son excelentes porque limitan los valores posibles a un conjunto predefinido, evitando que se pasen valores inválidos. Además, al ser clases, permiten encapsular lógica relacionada directamente con esas constantes dentro de la propia definición del enumerado.


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

```Java
public enum Mes {
    // Instancias del enumerado con sus valores para el constructor
    ENERO(1, 31), FEBRERO(2, 28), MARZO(3, 31), ABRIL(4, 30),
    MAYO(5, 31), JUNIO(6, 30), JULIO(7, 31), AGOSTO(8, 31),
    SEPTIEMBRE(9, 30), OCTUBRE(10, 31), NOVIEMBRE(11, 30), DICIEMBRE(12, 31);

    // Atributos privados
    private final int ordinal;
    private final int numDias;

    // Constructor del enumerado (siempre es privado por defecto)
    Mes(int ordinal, int numDias) {
        this.ordinal = ordinal;
        this.numDias = numDias;
    }

    // Método para obtener el número de días
    public int getNumDias() {
        return this.numDias;
    }

    // Método para obtener el ordinal (1-12)
    public int getOrdinal() {
        return this.ordinal;
    }
}
```


## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

```Java
public enum Mes {
    ENERO(1, 31), FEBRERO(2, 28), MARZO(3, 31), ABRIL(4, 30),
    MAYO(5, 31), JUNIO(6, 30), JULIO(7, 31), AGOSTO(8, 31),
    SEPTIEMBRE(9, 30), OCTUBRE(10, 31), NOVIEMBRE(11, 30), DICIEMBRE(12, 31);

    private final int ordinal;
    private final int numDias;

    Mes(int ordinal, int numDias) {
        this.ordinal = ordinal;
        this.numDias = numDias;
    }

    public int getNumDias() { return numDias; }
    public int getOrdinal() { return ordinal; }

    // --- Métodos de estaciones ---

    public boolean esDeInvierno(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == DICIEMBRE || this == ENERO || this == FEBRERO;
        }
        return this == JUNIO || this == JULIO || this == AGOSTO;
    }

    public boolean esDePrimavera(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == MARZO || this == ABRIL || this == MAYO;
        }
        return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
    }

    public boolean esDeVerano(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == JUNIO || this == JULIO || this == AGOSTO;
        }
        return this == DICIEMBRE || this == ENERO || this == FEBRERO;
    }

    public boolean esDeOtono(boolean enHemisferioNorte) {
        if (enHemisferioNorte) {
            return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
        }
        return this == MARZO || this == ABRIL || this == MAYO;
    }
}
```