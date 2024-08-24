Representan recomendaciones generales o mejores prácticas que los desarrolladores de software deben considerar al diseñar la arquitectura del sistema con el fin de disminuir la deuda técnica

---
## Single Responsibility Principle
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
## Open Closed Principle
Principio de Abierto/Cerrado, indica que las clases deben estar abiertas para su extensión, pero cerradas para su modificación. Esto significa que debemos poder extender el comportamiento de una clase sin modificar su código existente.

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

## Liskov Substitution Principle


---
## Interface Segregation Principle


---
## Dependency Inversion Principle

