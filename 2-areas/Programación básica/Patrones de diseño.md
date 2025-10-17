Los **patrones de código** (también conocidos como **patrones de diseño**) son soluciones probadas y reutilizables a problemas comunes en el desarrollo de software. Son como "planos" que puedes seguir para resolver problemas específicos de manera eficiente.
###  **Patrones Creacionales**

Gestionan la creación de objetos, proporcionando mecanismos flexibles de instanciación.

| Patrón        | Problema que resuelve                              | Ejemplo práctico            |
| ------------- | -------------------------------------------------- | --------------------------- |
| **Singleton** | Garantiza una única instancia                      | Conexión a base de datos    |
| **Factory**   | Creación de objetos sin especificar clase concreta | Sistema de notificaciones   |
| **Builder**   | Construcción de objetos complejos paso a paso      | Configuración de servidores |
### **Patrones Estructurales**

Se enfocan en cómo se componen las clases y objetos para formar estructuras más grandes.

|Patrón|Problema que resuelve|Ejemplo práctico|
|---|---|---|
|**Adapter**|Interface incompatible entre sistemas|Conexión con APIs externas|
|**Decorator**|Añadir funcionalidad sin modificar la clase base|Sistema de logging extendido|
|**Facade**|Simplificar interfaces complejas|Cliente para servicios web|
### **Patrones de Comportamiento**

Gestionan la comunicación y asignación de responsabilidades entre objetos.

|Patrón|Problema que resuelve|Ejemplo práctico|
|---|---|---|
|**Observer**|Notificar cambios a múltiples objetos|Sistema de eventos|
|**Strategy**|Intercambiar algoritmos en tiempo de ejecución|Sistemas de pago|
|**Command**|Encapsular peticiones como objetos|Sistema de undo/redo|
## Ejemplos

### Patrón singleton

>[!note] Singleton
>El patrón Singleton asegura que una clase tenga una única instancia y proporciona un punto de acceso global a ella.

```js
class Singleton {
  constructor() {
    if (Singleton.instance) {
      return Singleton.instance;
    }
    Singleton.instance = this;
    return this;
  }

  // Métodos de la clase
  someMethod() {
    console.log("Método del Singleton");
  }
}

// Uso:
const instance1 = new Singleton();
const instance2 = new Singleton();

console.log(instance1 === instance2); // true, son la misma instancia
```

Ejemplo práctico:

```js
class DatabaseConnection {
  constructor() {
    if (DatabaseConnection.instance) {
      return DatabaseConnection.instance;
    }
    this.connection = this.createConnection();
    DatabaseConnection.instance = this;
  }

  createConnection() {
    // Lógica de conexión
    return { connect: () => console.log('Conectado') };
  }
}

// Uso - siempre devuelve la misma instancia
const db1 = new DatabaseConnection();
const db2 = new DatabaseConnection();
console.log(db1 === db2); // true
```
### Patrón observer

>[!note] Observer
>El patrón Observer define una dependencia uno-a-muchos entre objetos, de modo que cuando un objeto cambia de estado, todos sus dependientes son notificados.

```js
// Sujeto (Subject)
class Subject {
  constructor() {
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter(obs => obs !== observer);
  }

  notify(data) {
    this.observers.forEach(observer => observer.update(data));
  }
}

// Observador (Observer)
class Observer {
  constructor(name) {
    this.name = name;
  }

  update(data) {
    console.log(`${this.name} recibió: ${data}`);
  }
}

// Uso:
const subject = new Subject();

const observer1 = new Observer("Observador 1");
const observer2 = new Observer("Observador 2");

subject.subscribe(observer1);
subject.subscribe(observer2);

subject.notify("¡Hola observadores!");
// Output:
// Observador 1 recibió: ¡Hola observadores!
// Observador 2 recibió: ¡Hola observadores!
```

## Ejemplos

Patrón factory

```js
class NotificationFactory {
  createNotification(type) {
    switch(type) {
      case 'email':
        return new EmailNotification();
      case 'sms':
        return new SMSNotification();
      case 'push':
        return new PushNotification();
      default:
        throw new Error('Tipo no soportado');
    }
  }
}

// Uso
const factory = new NotificationFactory();
const notification = factory.createNotification('email');
```

Patrón observer

```js
class EventObserver {
  constructor() {
    this.observers = [];
  }

  subscribe(fn) {
    this.observers.push(fn);
  }

  unsubscribe(fn) {
    this.observers = this.observers.filter(subscriber => subscriber !== fn);
  }

  broadcast(data) {
    this.observers.forEach(subscriber => subscriber(data));
  }
}

// Uso
const observer = new EventObserver();
observer.subscribe(data => console.log('Observer 1:', data));
observer.broadcast('¡Hola observadores!');
```

### Beneficios de usar patrones:

- Código más mantenible
- Soluciones probadas
- Comunicación eficiente entre desarrolladores
- Reducción de errores comunes
- Escalabilidad del código
    
### Cuándo NO usarlos:

- Problemas simples** que no requieren complejidad
- Cuando añaden sobre-ingeniería
- Sin entender completamente el problema
    

## **Comparación: Con vs Sin Patrones**

|Aspecto|Sin Patrones|Con Patrones|
|---|---|---|
|**Mantenibilidad**|Difícil de modificar|Fácil de extender|
|**Legibilidad**|Depende del desarrollador|Estructura consistente|
|**Reutilización**|Código duplicado|Componentes reutilizables|
|**Colaboración**|Dificulta el trabajo en equipo|Lenguaje común|
