<div id="top" style="margin: 0; padding:0"></div>

# Principios S.O.L.I.D.
`SOLID` es un conjunto de principios de programación orientada a objetos que tiene como objetivo crear software escalable, mantenible y flexible. Estos principios guían a los desarrolladores en el diseño de código limpio y eficiente. Exploremos cada principio SOLID con ejemplos en JavaScript y Node.js.

- [Principios S.O.L.I.D.](#principios-solid)
  - [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
  - [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
  - [Liskov's Substitution Principle (LSP)](#liskovs-substitution-principle-lsp)
  - [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
  - [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)
  - [Conclusión](#conclusión)

## Single Responsibility Principle (SRP)
En español `Principio de Responsabilidad Única`, establece que una clase debe tener sólo una razón para cambiar. En otras palabras, debería tener una sola responsabilidad. Consideremos un ejemplo sencillo:
```js
// Sin SRP
class User {
  constructor(name) {
    this.name = name;
  }

  saveToDatabase() {
    // Guardar usuario en la base de datos
  }

  sendEmail() {
    // Enviar correo electrónico de bienvenida al usuario
  }
}

// Con SRP
class User {
  constructor(name) {
    this.name = name;
  }
}

class UserRepository {
  saveToDatabase(user) {
    // Guardar usuario en la base de datos
  }
}

class EmailService {
  sendWelcomeEmail(user) {
    // Enviar correo electrónico de bienvenida al usuario
  }
}
```
Al separar las preocupaciones, cada clase ahora tiene una única responsabilidad: administrar los datos del usuario, guardarlos en la base de datos y enviar correos electrónicos.
<p align="right">(<a href="#top">Back to top</a>)</p>

## Open/Closed Principle (OCP)
En español `Principio abierto/cerrado`, establece que las entidades de software deben estar abiertas a la extensión pero cerradas a la modificación. Esto fomenta el uso de abstracciones e interfaces. He aquí un ejemplo:
```js
// Sin OCP
class Square {
  constructor(side) {
    this.side = side;
  }
}

class AreaCalculator {
  calculateSquareArea(square) {
    return square.side * square.side;
  }
}

// Con OCP
class Shape {
  calculateArea() {}
}

class Square extends Shape {
  constructor(side) {
    super();
    this.side = side;
  }

  calculateArea() {
    return this.side * this.side;
  }
}

class Circle extends Shape {
  constructor(radius) {
    super();
    this.radius = radius;
  }

  calculateArea() {
    return Math.PI * this.radius * this.radius;
  }
}
```
Ahora puedes agregar fácilmente nuevas formas sin modificar la clase `AreaCalculator`.
<p align="right">(<a href="#top">Back to top</a>)</p>

## Liskov's Substitution Principle (LSP)
En español `Principio de Sustitución de Liskov`, establece que los objetos de una superclase deben ser reemplazables por objetos de una subclase sin afectar la corrección del programa. Considere el siguiente ejemplo:
```js
// Sin LSP
class Bird {
  fly() {
    // Lógica de vuelo
  }
}

class Penguin extends Bird {
  // Los pingüinos no pueden volar 
  fly() {
    throw new Error('Penguins cannot fly');
  }
}

// Con LSP
class Bird {
  move() {}
}

class FlyingBird extends Bird {
  fly() {
    // Lógica de vuelo
  }
}

class Penguin extends Bird {
  // Los pingüinos no pueden volar 
  move() {}
}
```
Al adherirse a LSP, se asegura de que las subclases se puedan usar indistintamente con su clase base.
<p align="right">(<a href="#top">Back to top</a>)</p>

## Interface Segregation Principle (ISP)
En español `Principio de Segregación de Interfaces`, establece que no se debe obligar a una clase a implementar interfaces que no utiliza. En JavaScript no existen interfaces estrictas, pero podemos crear estructuras similares:
```js
// Sin ISP
class Worker {
  work() {
    // Lógica de trabajo
  }

  eat() {
    // Lógica comer
  }
}

// Con ISP
class Workable {
  work() {}
}

class Eatable {
  eat() {}
}

class Worker implements Workable, Eatable {
  work() {
    // Lógica de trabajo
  }

  eat() {
    // Lógica comer
  }
}
```
Al dividir las interfaces en otras más pequeñas, las clases pueden implementar sólo lo que necesitan.
<p align="right">(<a href="#top">Back to top</a>)</p>

## Dependency Inversion Principle (DIP)
En español `Principio de Inversión de Dependencia`, establece que los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deberían depender de abstracciones. Considere este ejemplo:
```js
// Sin DIP
class LightBulb {
  turnOn() {
    // Activar la lógica
  }

  turnOff() {
    // Desactivar la lógica
  }
}

class Switch {
  constructor(bulb) {
    this.bulb = bulb;
  }

  operate() {
    // Opere la bombilla 
    if (/* alguna condición */) {
      this.bulb.turnOn();
    } else {
      this.bulb.turnOff();
    }
  }
}

// Con DIP
class Switchable {
  turnOn() {}

  turnOff() {}
}

class LightBulb implements Switchable {
  turnOn() {
    // Activar la lógica
  }

  turnOff() {
    // Desactivar la lógica
  }
}

class Switch {
  constructor(device) {
    this.device = device;
  }

  operate() {
    // Operar el dispositivo
    if (/* alguna condición */) {
      this.device.turnOn();
    } else {
      this.device.turnOff();
    }
  }
}
```
Ahora, la clase `Switch` depende de una abstracción (`Switchable`) en lugar de una implementación concreta.
<p align="right">(<a href="#top">Back to top</a>)</p>

## Conclusión
En conclusión, la aplicación de principios `SOLID` en JavaScript y Node.js conduce a un código más modular, escalable y mantenible. Al comprender e implementar estos principios, los desarrolladores pueden crear arquitecturas de software sólidas y flexibles.
<p align="right">(<a href="#top">Back to top</a>)</p>
