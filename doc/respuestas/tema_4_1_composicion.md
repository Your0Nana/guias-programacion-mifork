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

### En el lenguaje C, la composición se logra mediante la inclusión de una estructura dentro de otra. Esta relación se define como "un objeto de tipo A contiene a uno o varios de tipo B". Al anidar estructuras, se permite organizar los datos de manera jerárquica, facilitando la representación de entidades complejas a partir de tipos más simples.Para calcular la distancia entre dos puntos, se utiliza la fórmula de la distancia euclídea. En el caso de la longitud de la línea, esta se obtiene invocando la función de distancia pasando como argumentos los dos puntos que componen la estructura de la línea.

``` C
#include <stdio.h>
#include <math.h>

typedef struct {
    double x;
    double y;
} Punto;

typedef struct {
    Punto p1;
    Punto p2;
} Linea;

double calcularDistancia(Punto a, Punto b) {
    return sqrt(pow(b.x - a.x, 2) + pow(b.y - a.y, 2));
}

double calcularLongitud(Linea l) {
    return calcularDistancia(l.p1, l.p2);
}
```


## 2. Ahora transforma ese ejemplo a orientación a objetos con Java, para tener un primer ejemplo de **composición** en orientación a objetos. Crea una clase `Punto`, y una clase `Linea`. La clase `Punto` debe tener un método para calcular distancia a otro `Punto` y `Linea` debe tener un método para calcular su longitud. Gracias a la ocultación de información, supera a C, garantizando que los puntos sean inmutables, al igual que la línea, que una vez creada, no queremos que se modifique de qué a qué puntos va dicha línea.  

### En la orientación a objetos, la composición se representa mediante atributos de instancia que son referencias a otros objetos. A diferencia de C, Java permite proteger el estado interno mediante el uso de modificadores de acceso (private) y la omisión de métodos "setter". Para garantizar la inmutabilidad, los atributos se declaran como final, asegurando que una vez asignados en el constructor, no puedan ser modificados.

### La clase Punto encapsula sus coordenadas y ofrece un método para calcular la distancia respecto a otra instancia. La clase Linea se compone de dos objetos Punto. Al ser inmutable, cualquier intento de cambiar la trayectoria de la línea requeriría la creación de una nueva instancia, lo que evita efectos secundarios no deseados en otras partes del programa que compartan la referencia.

``` Java
public class Punto {
    private final double x;
    private final double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double distanciaA(Punto otro) {
        return Math.sqrt(Math.pow(otro.x - this.x, 2) + Math.pow(otro.y - this.y, 2));
    }
}

public class Linea {
    private final Punto p1;
    private final Punto p2;

    public Linea(Punto p1, Punto p2) {
        this.p1 = p1;
        this.p2 = p2;
    }

    public double obtenerLongitud() {
        return p1.distanciaA(p2);
    }
}
```


## 3. ¿Qué significa la **multiplicidad** en la composición? En el ejemplo anterior, ¿cuál es la multiplicidad entre `Linea` y `Punto`? Indícalo expresando la multiplicidad en ambas direcciones, de `Linea` a `Punto` y de `Punto` a `Linea`.

### La multiplicidad define el número de instancias de una clase que pueden estar asociadas a una única instancia de otra clase en un momento dado. Se expresa habitualmente mediante un rango (por ejemplo, 0..1, 1..*, o un número fijo). Este concepto es fundamental para determinar si la relación es de uno a uno, de uno a muchos o de muchos a muchos.

### En el ejemplo anterior, la multiplicidad de Linea a Punto es exactamente 2, ya que una línea está compuesta obligatoriamente por dos puntos para existir. En sentido inverso, de Punto a Linea, la multiplicidad suele ser de 0..* (cero a muchos), puesto que un punto puede existir de forma independiente sin pertenecer a ninguna línea, o puede ser el extremo de múltiples líneas distintas.


## 4. ¿Qué significa composición **fuerte** y composición **débil**? ¿Qué consecuencia implica en relación al ciclo de vida de los objetos? Indica a cuál solemos referirnos como **"asociación o agregación"** y a cuál como **"composición"** propiamente.

### La distinción entre composición fuerte y débil radica en el grado de dependencia del ciclo de vida de los objetos relacionados. En la composición fuerte (llamada simplemente "composición"), el objeto contenedor es responsable de la existencia de los objetos contenidos; si el contenedor se destruye, las partes también desaparecen. Existe una relación de propiedad absoluta.

### Por el contrario, en la composición débil (conocida como "agregación" o "asociación"), los objetos tienen ciclos de vida independientes. El objeto contenido puede existir antes de ser parte del contenedor y puede seguir existiendo después de que el contenedor sea destruido. Es una relación del tipo "pertenece a" pero sin una dependencia vital estricta.


## 5. Cuando una clase usa a otra al recibirla o devolverla como parámetro en algún método, al hacer `new` dentro de un método, o al usarlas como variables locales, ¿hablamos de composición o de **"dependencia"**?

### Se habla de "dependencia" (o relación de uso) cuando una clase utiliza a otra de forma temporal y efímera, sin que esta forme parte de su estado permanente. Esto ocurre cuando se recibe un objeto como parámetro en un método, se crea una instancia local dentro de un bloque de código o se invoca un método estático de otra clase. El objeto utilizado no es un "atributo" de la clase.

### La composición, en cambio, implica una relación estructural y duradera. En la composición, el objeto contenido es un atributo de la clase, lo que significa que el contenedor "tiene un" objeto como parte de su definición de estado. Mientras que la dependencia es una relación de comportamiento ("usa un"), la composición es una relación de estructura ("tiene un").


## 6. En el ejemplo anterior de línea y punto, programa la relación entre `Linea` y `Punto` de dos formas. Una **como composición fuerte**, donde el ciclo de vida de los puntos está ligado al de Linea y otra **como composición débil**, donde no.

### Para implementar una composición fuerte, el objeto contenedor suele instanciar sus partes internamente (en el constructor o campos). De este modo, nadie externo tiene acceso directo a esas instancias originales, y su vida está ligada a la del objeto padre.

### En la composición débil, el contenedor recibe las instancias ya creadas desde el exterior (a través del constructor o métodos). Esto permite que los mismos objetos sean compartidos por diferentes contenedores o que sobrevivan de forma independiente.

``` Java
// Composición FUERTE: La Linea crea sus propios puntos.
public class LineaFuerte {
    private final Punto p1;
    private final Punto p2;

    public LineaFuerte(double x1, double y1, double x2, double y2) {
        this.p1 = new Punto(x1, y1);
        this.p2 = new Punto(x2, y2);
    }
}

// Composición DÉBIL: La Linea recibe puntos ya existentes.
public class LineaDebil {
    private Punto p1;
    private Punto p2;

    public LineaDebil(Punto p1, Punto p2) {
        this.p1 = p1;
        this.p2 = p2;
    }
}
```


## 7. En Java, en la composición fuerte, ¿cuando el contenedor destruye los objetos? No se observa que `Linea` destruya los `Punto` explícitamente, ¿Por qué?

### En Java, a diferencia de C++, no existe una instrucción explícita como delete o free para destruir objetos. La destrucción de los objetos en una composición fuerte ocurre de forma automática gracias al Garbage Collector (Recolector de Basura). Cuando el objeto contenedor deja de ser accesible, las referencias internas que mantenía hacia sus partes también se pierden.

### Si no existen otras referencias externas a esos objetos internos (como es el caso de la composición fuerte bien encapsulada), el Garbage Collector identifica que esos objetos ya no son necesarios y libera su memoria. Por tanto, no se observa una destrucción explícita en el código porque la gestión de memoria es una tarea automatizada por la Máquina Virtual de Java (JVM).


## 8. Pon un ejemplo de composicion débil entre un departamento que tiene varios profesores. Implementa dos composiciones a la vez: entre el departamento y todos sus profesores y entre el departamento y su director, que es un profesor del departamento. Siempre debe haber un director en el departamento desde el inicio. Lanza excepciones si se viola la invariante. Emplea arrays primitivos de Java, estilo `Profesor[]`, con máximo 50, pero no rompas la encapsulación, no desveles que estás empleando un array, permite añadir un `Profesor` al final de la lista, y eliminar un profesor dada su posición. Da acceso a los profesores con un método para saber cuántos hay y otro para obtener un profesor por posición. El director se puede cambiar por otro profesor del departamento. Sin embargo, ten en cuenta esta invariante de clase: el director debe formar siempre parte de la lista de profesores, es decir, ten cuidado al cambiar el director o al eliminar un profesor.

### Se presenta una implementación donde un Departamento gestiona un conjunto de profesores. Se garantiza que el director siempre sea parte del listado y se gestionan las restricciones mediante excepciones para mantener la integridad de la estructura.

``` Java
public class Departamento {
    private String nombre;
    private Profesor[] profesores = new Profesor[50];
    private int numProfesores = 0;
    private Profesor director;

    public Departamento(String nombre, Profesor director Inicial) {
        if (directorInicial == null) throw new IllegalArgumentException("El director es obligatorio");
        this.nombre = nombre;
        this.director = directorInicial;
        agregarProfesor(directorInicial);
    }

    public void agregarProfesor(Profesor p) {
        if (numProfesores >= 50) throw new IllegalStateException("Departamento lleno");
        profesores[numProfesores++] = p;
    }

    public void eliminarProfesor(int pos) {
        if (pos < 0 || pos >= numProfesores) throw new IndexOutOfBoundsException();
        if (profesores[pos] == director) throw new IllegalStateException("No se puede eliminar al director");
        
        for (int i = pos; i < numProfesores - 1; i++) {
            profesores[i] = profesores[i + 1];
        }
        profesores[--numProfesores] = null;
    }

    public void cambiarDirector(Profesor nuevoDirector) {
        if (nuevoDirector == null) throw new IllegalArgumentException("Director nulo");
        boolean encontrado = false;
        for (int i = 0; i < numProfesores; i++) {
            if (profesores[i] == nuevoDirector) {
                encontrado = true;
                break;
            }
        }
        if (!encontrado) throw new IllegalArgumentException("El director debe ser del departamento");
        this.director = nuevoDirector;
    }

    public int getCantidad() { return numProfesores; }
    public Profesor getProfesor(int pos) { return profesores[pos]; }
}
```


## 9. En Java, existen también `List`, cambia y muestra cómo sería el código anterior empleando `List` en vez de arrays primitivos. ¿Qué parte del código original te has ahorrado? Además, fíjate en el método `getProfesor(int pos)`: si en su lugar existiera un método que devolviera todos los profesores a la vez, ¿qué problema tendría devolver directamente la lista interna? ¿Cómo lo resolverías?

### Al emplear la interfaz List (como ArrayList), se elimina la necesidad de gestionar manualmente el tamaño del array, el contador de elementos y el desplazamiento de índices al eliminar (for). La colección crece dinámicamente y ofrece métodos optimizados como add, remove y size, lo que reduce significativamente el código de infraestructura o "boilerplate".

### El problema de devolver la lista interna directamente es la fuga de encapsulación: cualquier código externo podría modificar la lista (añadir o quitar elementos) sin pasar por las reglas de validación del Departamento. Para resolverlo, se debe devolver una copia defensiva de la lista o una vista no modificable mediante Collections.unmodifiableList(lista).


## 10. Al igual que ocurre con las excepciones en Java, que pueden encerrar causas (que son excepciones), de forma recursiva, suponen un tipo especial de composiciones, denominadas composiciones recursivas. Pon un ejemplo en Java de una `Persona`, que sea inmutable, y que tiene una madre, que es otra `Persona`. Haz un main con un ejemplo de uso con una familia de personas, desde el nieto hasta la abuela. Enumera algún otro ejemplo clásico de composiciones recursivas.

### Una composición es recursiva cuando una clase contiene un atributo que es del mismo tipo que la propia clase. Esto permite crear estructuras en cadena o en forma de árbol, donde cada elemento puede tener un "padre" o un "hijo" de su misma naturaleza.

``` Java
public class Persona {
    private final String nombre;
    private final Persona madre; // Composición recursiva

    public Persona(String nombre, Persona madre) {
        this.nombre = nombre;
        this.madre = madre;
    }

    public static void main(String[] args) {
        Persona abuela = new Persona("Ana", null);
        Persona madre = new Persona("María", abuela);
        Persona nieto = new Persona("Juan", madre);
    }
}
```

### Otros ejemplos clásicos incluyen las Estructuras de Directorios (una carpeta contiene otras carpetas), los Nodos de un Árbol o las Excepciones (una excepción puede contener otra excepción como causa original).


## 11. ¿Qué son las relaciones de composición "bidireccionales"? ¿Qué habría que hacer para implementar este tipo de relación en el ejemplo de `Profesor` y `Departamento`?

### Las relaciones bidireccionales son aquellas donde ambos objetos mantienen una referencia mutua. Mientras que en una relación unidireccional solo el Departamento conoce a sus Profesores, en una bidireccional el Profesor también tiene un atributo que apunta al Departamento al que pertenece.

### Para implementar esto en el ejemplo anterior, la clase Profesor debería incluir un atributo private Departamento departamento. Al añadir un profesor al departamento mediante agregarProfesor(p), el método debería encargarse también de actualizar el estado del profesor haciendo algo como p.setDepartamento(this). Esto requiere especial cuidado para mantener la consistencia en ambos lados y evitar bucles infinitos en métodos como toString().
