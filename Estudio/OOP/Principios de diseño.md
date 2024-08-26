Representan recomendaciones generales o mejores prácticas que los desarrolladores de software deben considerar al diseñar la arquitectura del sistema con el fin de disminuir la deuda técnica

---
## Single Responsibility Principle (SRP)
El principio de Responsabilidad Única, indica que cada clase debe tener una única responsabilidad o razón para cambiar. Es decir, una clase debe encargarse de una sola tarea.

### Ejemplo 1
```java
// Clase que incumple SRP
class Report {
    public String getReportData() {
        // Obtiene datos para el reporte
        return "Datos del Reporte";
    }

    public void printReport(String report) {
        // Imprime el reporte
        System.out.println(report);
    }
}

// Corrección aplicando SRP
class ReportGenerator {
    public String getReportData() {
        return "Datos del Reporte";
    }
}

class ReportPrinter {
    public void printReport(String report) {
        System.out.println(report);
    }
}

```

### Ejemplo 2
```java
// Clase que incumple SRP
class Empleado {
	private String nombre;
	private String apellido;
	private String cargo;
	
    public double calcularSalario() {
        return salario;
    }
}

// Corrección aplicando SRP
class Empleado {
	private String nombre;
	private String apellido;
	private String cargo;
}

class CalculadoraSalario {
	private double salario;
	
    public double calcularSalario() {
        return this.salario;
    }
}
```

---
## Open Closed Principle (OCP)
Principio de Abierto/Cerrado, indica que las clases deben estar abiertas para su extensión, pero cerradas para su modificación. Esto significa que debemos poder extender el comportamiento de una clase sin modificar su código existente.

### Ejemplo 1
```java
// Ejemplo que viola el OCP
class AreaCalculator {
    public double calculateArea(Object shape) {
        if (shape instanceof Circle) {
            Circle circle = (Circle) shape;
            return Math.PI * circle.getRadius() * circle.getRadius();
        } else if (shape instanceof Rectangle) {
            Rectangle rectangle = (Rectangle) shape;
            return rectangle.getLength() * rectangle.getWidth();
        }
        return 0;
    }
}

// Corrección aplicando OCP
interface Shape {
    double calculateArea();
}

class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getRadius() {
        return radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle implements Shape {
    private double length;
    private double width;

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    @Override
    public double calculateArea() {
        return length * width;
    }
}

class AreaCalculator {
    public double calculateArea(Shape shape) {
        return shape.calculateArea();
    }
}
```

Si se desea agregar una nueva figura geométrica, por ejemplo, un triángulo, se puede crear una nueva clase que implemente la interfaz `Shape` sin modificar el código de `AreaCalculator`

### Ejemplo 2
```java
class abstract Forma {
	public calcularArea();
	public setLado();
}
```

En este caso incumple el principio dado que no todas las formas tienen un lado, algunas tienen dos, otras un radio, etc. Se tendria que remover ese metodo

---
## Liskov Substitution Principle (LSP)
Principio de Sustitución de Liskov, indica que Los objetos de una subclase deben poder reemplazar objetos de su superclase sin alterar el correcto funcionamiento del programa.

### Ejemplo 1
```java
// Ejemplo que viola el LSP
class Bird {
    public void fly() {
        System.out.println("El ave está volando");
    }
}

class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("¡Las avestruces no pueden volar!");
    }
}

// Corrección aplicando LSP
interface Bird {
    void move();
}

class FlyingBird implements Bird {
    @Override
    public void move() {
        System.out.println("El ave está volando");
    }
}

class Ostrich implements Bird {
    @Override
    public void move() {
        System.out.println("La avestruz está corriendo");
    }
}
```

En la corrección, la clase `Ostrich` no hereda de una clase que la obliga a implementar un método `fly()` no compatible con su comportamiento.

### Ejemplo 2
```java
class Rectangulo {
	public double ancho;
	public double largo;
}

class Cuadrado {
	public double lado;
	
	public Cuadrado(double lado) extends Rectangulo{
		this.lado = lado;
		this.ancho = lado;
		this.largo = lado;
	}
}
```

al implementar en el constructor de la clase hija los atributos heredados de la clase padre se cumple el principio LSP

---
## Interface Segregation Principle (ISP)
Principio de Segregación de Interfaces, los clientes no deberían estar obligados a depender de interfaces que no usan. Es mejor tener varias interfaces pequeñas y específicas que una grande y general.

### Ejemplo 1
```java
// Ejemplo que viola el ISP
interface Worker {
    void work();
    void eat();
}

class Programmer implements Worker {
    @Override
    public void work() {
        System.out.println("Programando código...");
    }

    @Override
    public void eat() {
        System.out.println("Comiendo...");
    }
}

class Robot implements Worker {
    @Override
    public void work() {
        System.out.println("Trabajando en la fábrica...");
    }

    @Override
    public void eat() {
        // Los robots no comen, pero están forzados a implementar este método
    }
}

// Corrección aplicando ISP
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Programmer implements Workable, Eatable {
    @Override
    public void work() {
        System.out.println("Programando código...");
    }

    @Override
    public void eat() {
        System.out.println("Comiendo...");
    }
}

class Robot implements Workable {
    @Override
    public void work() {
        System.out.println("Trabajando en la fábrica...");
    }
}
```

En la corrección, el `Robot` no está obligado a implementar un método `eat()` que no tiene sentido para él.

### Ejemplo 2
Las clases que implementan una interfaz no están obligadas a usar todos los métodos de la interfaz, por ejemplo, una interfaz llamada impresora con sus métodos `imprimir()`, `escanear()` y `enviarFax()` incumple este principio dado que no todas las impresoras tienen todos esos componentes, depende del fabricante y modelo.

Una forma de corregir esto es tener una `InterfazEscaner`, `InterfazImpresora` y `InterfazFax` con sus respectivos métodos para que una clase `EpsonXYZ` implemente cada una de las interfaces que corresponda

---
## Dependency Inversion Principle (DIP)
Principio de Inversión de Dependencias, los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones. Además, las abstracciones no deben depender de los detalles, sino que los detalles deben depender de las abstracciones.

### Ejemplo 1
```java
// Ejemplo que viola el DIP
class Keyboard {
    public void type() {
        System.out.println("Escribiendo...");
    }
}

class Computer {
    private Keyboard keyboard;

    public Computer() {
        this.keyboard = new Keyboard();
    }

    public void type() {
        keyboard.type();
    }
}

// Corrección aplicando DIP
interface InputDevice {
    void type();
}

class Keyboard implements InputDevice {
    @Override
    public void type() {
        System.out.println("Escribiendo...");
    }
}

class Computer {
    private InputDevice inputDevice;

    public Computer(InputDevice inputDevice) {
        this.inputDevice = inputDevice;
    }

    public void type() {
        inputDevice.type();
    }
}
```

En la corrección, la clase `Computer` depende de una abstracción (`InputDevice`) en lugar de una implementación específica (`Keyboard`). Esto facilita cambiar el dispositivo de entrada sin modificar la clase `Computer`.

