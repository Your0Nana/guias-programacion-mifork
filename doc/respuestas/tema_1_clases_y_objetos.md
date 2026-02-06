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

### La programación orientada a objetos se fundamenta en cuatro pilares que permiten gestionar la complejidad del software de manera más eficiente que el enfoque puramente procedimental:

### ->Abstracción: Consiste en identificar las características y comportamientos esenciales de un objeto, ignorando los detalles irrelevantes para el contexto del problema. Permite modelar entidades del mundo real mediante la creación de tipos de datos personalizados.

### ->Encapsulamiento: Es el mecanismo que agrupa los datos (atributos) y los métodos que operan sobre ellos en una única unidad (la clase), restringiendo el acceso directo a los componentes internos. Esto protege la integridad del estado del objeto frente a modificaciones externas no controladas.

### ->Herencia: Permite crear nuevas clases a partir de clases existentes, heredando sus propiedades y comportamientos. Facilita la reutilización de código y la creación de jerarquías, donde una "clase hija" especializa la funcionalidad de una "clase padre".

### ->Polimorfismo: Es la capacidad que tienen objetos de diferentes tipos de responder a un mismo mensaje o llamada de método de forma distinta. Esto permite tratar objetos de diversas clases de manera uniforme a través de una interfaz común.


## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Existen múltiples lenguajes que implementan este paradigma, cada uno con matices diferentes en su aplicación:

### ->Java: Diseñado para ser multiplataforma y estrictamente orientado a objetos (casi todo debe residir dentro de una clase). Es ampliamente utilizado en entornos corporativos y aplicaciones Android.

### ->C++: Una extensión de C que añade soporte para clases y objetos. A diferencia de Java, permite la gestión manual de memoria y el uso de punteros, manteniendo la compatibilidad con el estilo procedimental.

### ->Python: Un lenguaje de alto nivel y tipado dinámico que trata prácticamente todo como un objeto. Es muy valorado por su sintaxis limpia y su versatilidad en ciencia de datos y desarrollo web.

### ->C#: Desarrollado por Microsoft, es un lenguaje moderno y robusto muy similar a Java, optimizado para el ecosistema .NET y el desarrollo de videojuegos mediante motores como Unity.Respuesta


## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### La programación estructurada es un paradigma basado en la división de un programa en funciones o procedimientos y en el uso de estructuras de control (bucles, condicionales) que evitan el uso de saltos incondicionales (goto). En lenguajes como C, el foco reside en la lógica algorítmica y en cómo los datos fluyen a través de una jerarquía de funciones que los transforman.

### Por otro lado, la programación modular da un paso más allá al organizar el código en unidades independientes llamadas módulos (o archivos .c y .h en C). Cada módulo agrupa funciones relacionadas y oculta su implementación interna, exponiendo solo una interfaz pública. Este enfoque busca minimizar las dependencias entre distintas partes del programa, facilitando el mantenimiento y la legibilidad en proyectos de gran envergadura.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Un objeto se define por la intersección de tres conceptos fundamentales: estado, comportamiento e identidad. El estado está representado por el conjunto de valores que poseen sus atributos en un momento determinado. Por ejemplo, en un objeto Coche, el estado podría incluir la velocidad actual, la cantidad de combustible y el color.

### El comportamiento se define mediante los métodos (funciones internas) que el objeto puede ejecutar. Estos métodos suelen interactuar con el estado interno o realizar acciones externas, como acelerar() o frenar(). Finalmente, la identidad es lo que distingue a un objeto de todos los demás, incluso si tienen el mismo estado. En memoria, la identidad suele estar vinculada a la dirección única de almacenamiento del objeto.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Una clase es un molde, plantilla o "plano" que define los atributos y métodos que tendrán los objetos creados a partir de ella. No es lo mismo que un objeto; mientras la clase es la definición teórica, el objeto es la entidad real que ocupa espacio en memoria. El término instancia es prácticamente sinónimo de objeto: se dice que un objeto es una "instancia" de una clase determinada.

### Aunque la mayoría de los lenguajes (como Java, C++, C#) se basan en clases, no todos los lenguajes orientados a objetos las requieren. Existen lenguajes como JavaScript (en su concepción original) que utilizan la programación basada en prototipos, donde los objetos se crean clonando otros objetos existentes y extendiéndolos, sin necesidad de un molde de clase formal.


## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### En lenguajes como Java, los objetos se almacenan siempre en una región de memoria dinámica denominada Heap (montículo). A diferencia de C, donde el programador puede elegir crear estructuras en el Stack (pila) o en el Heap mediante malloc, en Java solo las variables de tipo primitivo y las referencias a los objetos residen en el Stack, mientras que el cuerpo del objeto siempre va al Heap.

### La recolección de basura (Garbage Collection) es un mecanismo automático encargado de liberar la memoria de los objetos que ya no tienen ninguna referencia apuntando a ellos. Esto elimina la necesidad de liberar memoria manualmente (como se haría con free en C), reduciendo drásticamente errores comunes como las fugas de memoria (memory leaks) o los punteros colgantes.


## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Un método es una función que está definida dentro de una clase y que opera sobre los datos de los objetos de dicha clase. A diferencia de las funciones globales en C, un método siempre tiene acceso implícito al estado del objeto que lo invoca, lo que permite que el comportamiento esté intrínsecamente ligado a los datos.

### La sobrecarga de métodos es la capacidad de definir múltiples métodos con el mismo nombre dentro de una misma clase, siempre que su firma (el número o tipo de parámetros) sea distinta. El compilador decide qué método ejecutar basándose en los argumentos proporcionados durante la llamada. Esto permite ofrecer diferentes formas de realizar una acción similar sin tener que inventar nombres distintos para cada variante.


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### A continuación se presenta la implementación de la clase Punto. Se utiliza la clase Math para realizar el cálculo de la raíz cuadrada y la potencia.
```Java
class Punto {
    // Atributos con visibilidad por defecto (package-private)
    double x;
    double y;

    // Método para calcular la distancia al origen (0,0)
    double calculaDistanciaAOrigen() {
        return Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2));
    }
}

// Ejemplo de uso
public class Principal {
    public static void main(String[] args) {
        Punto miPunto = new Punto(); // Instanciación
        miPunto.x = 3.0;
        miPunto.y = 4.0;
        
        double distancia = miPunto.calculaDistanciaAOrigen();
        System.out.println("La distancia al origen es: " + distancia);
    }
}
```


## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### El punto de entrada de cualquier aplicación Java es el método public static void main(String[] args). La palabra clave static indica que el miembro (método o atributo) pertenece a la clase en sí y no a una instancia específica. Por tanto, se puede invocar sin necesidad de crear un objeto previo con new. Esto es esencial para el main, ya que la Máquina Virtual debe poder ejecutarlo antes de que exista cualquier objeto.

### static no se limita al main; se usa para definir constantes compartidas o métodos de utilidad que no dependen del estado de un objeto (como Math.sqrt). Cuando se combina con final, se crean constantes de clase. Un atributo static final es una variable cuyo valor es único para toda la clase y no puede ser modificado tras su asignación inicial, similar a un #define o una constante global en C pero con tipado fuerte.

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Para compilar un programa se utiliza el comando javac NombreFichero.java, lo cual genera un archivo .class. Este archivo no contiene código máquina nativo del procesador, sino bytecode, un lenguaje intermedio de bajo nivel. Para ejecutarlo, se utiliza el comando java NombreClase, que inicia la Máquina Virtual de Java (JVM).

### Java es un lenguaje híbrido: se compila a bytecode y luego la JVM interpreta o compila "al vuelo" (JIT - Just In Time) ese bytecode a código máquina específico del sistema operativo. La Máquina Virtual actúa como una capa de abstracción que permite la portabilidad ("Escribe una vez, ejecútalo en cualquier lugar"), encargándose además de la gestión de memoria y la seguridad durante la ejecución.


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### La palabra clave new es un operador que solicita memoria en el Heap para un nuevo objeto y devuelve una referencia (una dirección de memoria gestionada) a ese espacio. Al usar new, se invoca automáticamente a un constructor, que es un método especial destinado a inicializar el estado del objeto recién creado.

### Un constructor tiene el mismo nombre que la clase y no devuelve ningún tipo, ni siquiera void. Si no se define ninguno, Java proporciona uno por defecto sin parámetros. A continuación se muestra el ejemplo solicitado para la clase Empleado:

```Java
class Empleado {
    String dni;
    String nombre;
    String apellidos;

    // Constructor para inicializar los atributos
    Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }
}
```

## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### La referencia this es un puntero implícito que apunta al objeto actual que está ejecutando el método. Se utiliza principalmente para resolver ambigüedades cuando el nombre de un parámetro de un método o constructor coincide con el nombre de un atributo de la clase. En otros lenguajes como Python se utiliza self, mientras que en C++ también se emplea this pero como un puntero real (this->atributo).

### En el caso de la clase Punto, su uso es común en el constructor o en métodos de asignación para distinguir las variables locales de los atributos de la instancia:

```Java
class Punto {
    double x;
    double y;

    void setCoordenadas(double x, double y) {
        this.x = x; // 'this.x' es el atributo, 'x' es el parámetro
        this.y = y;
    }
}
```

## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Este método recibe otro objeto de la misma clase como parámetro.

```Java
double distanciaA(Punto otro) {
    double dx = this.x - otro.x;
    double dy = this.y - otro.y;
    return Math.sqrt(Math.pow(dx, 2) + Math.pow(dy, 2));
}
```

## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### En Java, el paso de parámetros es siempre por valor. Sin embargo, existe una distinción crítica: cuando se pasa un objeto (como Punto), lo que se copia por valor es la referencia (la dirección de memoria). Por tanto, si dentro del método se modifica un atributo del objeto recibido, los cambios sí afectan al objeto original fuera del método, ya que ambos apuntan al mismo espacio en el Heap.

### Por el contrario, si se pasa un tipo primitivo como un int, se crea una copia exacta del valor numérico. Cualquier modificación realizada sobre esa variable dentro del método es local y no tiene impacto alguno sobre la variable original. En términos de C, pasar un objeto en Java es equivalente a pasar un puntero por valor: no puedes cambiar a dónde apunta el puntero original, pero sí puedes modificar el contenido de la estructura a la que apunta.

## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### El método toString() es un método heredado de la clase base Object (de la que derivan todas las clases en Java) que devuelve una representación en forma de cadena de texto del objeto. Se invoca automáticamente cuando se intenta imprimir un objeto con System.out.println() o al concatenarlo con un String. En otros lenguajes existen equivalentes, como __str__ en Python.

### Sobrescribir este método es una buena práctica para facilitar la depuración y visualización de los datos de un objeto:

```Java
@Override
public String toString() {
    return "Punto[x=" + x + ", y=" + y + "]";
}
```

## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Una clase puede verse como una evolución de un struct de C, pero con diferencias fundamentales. Un struct es puramente una agrupación pasiva de datos (variables). La clase, en cambio, es una entidad activa que une esos datos con la lógica que los manipula (métodos).

### Para que un struct fuera como una clase, le faltaría la capacidad de contener funciones internas (encapsulamiento de comportamiento), mecanismos de control de acceso (como private o public) y la capacidad de participar en jerarquías de herencia. Además, en C, la asociación entre las funciones y las estructuras es manual, mientras que en la POO es una propiedad intrínseca del lenguaje.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Para emular el comportamiento de una clase en C, se suele definir una estructura y un conjunto de funciones que reciben un puntero a dicha estructura como primer argumento. Este puntero actúa como el this manual.

```C
#include <math.h>
#include <stdio.h>

struct Punto {
    double x;
    double y;
};

// Emulación del método: se pasa el puntero 'self' explícitamente
double calculaDistanciaAOrigen(struct Punto* self) {
    return sqrt(pow(self->x, 2) + pow(self->y, 2));
}

int main() {
    struct Punto p1 = {3.0, 4.0};
    // El 'this' de Java es aquí el parámetro '&p1'
    printf("Distancia: %f", calculaDistanciaAOrigen(&p1));
    return 0;
}
```

### En este ejemplo, la "magia" de this desaparece porque en C la conexión entre los datos y la función no es automática; se debe pasar explícitamente la dirección de la estructura para que la función sepa sobre qué datos operar.