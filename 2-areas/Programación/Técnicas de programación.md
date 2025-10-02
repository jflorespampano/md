
## principios SOLID y arquitectura

Los principios SOLID son **5 reglas de diseño** que hacen que el código sea más mantenible, escalable y comprensible. Fueron popularizados por Robert C. Martin (Uncle Bob).
Cada letra representa un principio:

| Letra | Principio                 | Concepto Clave                                    |
| ----- | ------------------------- | ------------------------------------------------- |
| **S** | **Single Responsibility** | Una clase, una responsabilidad                    |
| **O** | **Open/Closed**           | Abierto para extensión, cerrado para modificación |
| **L** | **Liskov Substitution**   | Los hijos deben poder reemplazar a los padres     |
| **I** | **Interface Segregation** | Interfaces pequeñas y específicas                 |
| **D** | **Dependency Inversion**  | Depender de abstracciones, no de implementaciones |

### **Single Responsibility Principle (SRP)**

Una clase debe tener una sola responsabilidad
```js
// ❌ Una clase con múltiples responsabilidades
class UserManager {
  createUser() { /* ... */ }
  sendEmail() { /* ... */ }
  generateReport() { /* ... */ }
  validateData() { /* ... */ }
}

// ✅ Clases con responsabilidad única
class UserCreator { createUser() {} }
class EmailSender { sendEmail() {} }
class ReportGenerator { generateReport() {} }
class DataValidator { validateData() {} }
```

### **Interface Segregation Principle (ISP)**

**"Muchas interfaces específicas son mejores que una interfaz general"**

```js
// En typscript
// ❌ VIOLACIÓN del ISP
interface Trabajador {
  trabajar(): void;
  comer(): void;
  dormir(): void;
  programar(): void;
  disenar(): void;
  vender(): void;
}

class Programador implements Trabajador {
  programar() { /* Sí hace esto */ }
  trabajar() { /* Sí hace esto */ }
  comer() { /* Sí hace esto */ }
  dormir() { /* Sí hace esto */ }
  disenar() { /* ❌ No debería hacer esto */ }
  vender() { /* ❌ No debería hacer esto */ }
}

// ✅ CUMPLIENDO el ISP
interface SerHumano {
  trabajar(): void;
  comer(): void;
  dormir(): void;
}

interface Programador {
  programar(): void;
}

interface Diseniador {
  disenar(): void;
}

interface Vendedor {
  vender(): void;
}

class Desarrollador implements SerHumano, Programador {
  trabajar() { /* Implementación */ }
  comer() { /* Implementación */ }
  dormir() { /* Implementación */ }
  programar() { /* Implementación */ }
}
```

### **Dependency Injection**

```js
// ❌ Acoplado fuertemente
class UserService {
  constructor() {
    this.database = new MySQLDatabase(); // Dependencia concreta
  }
}

// ✅ Desacoplado con inyección
class UserService {
  constructor(database) { // Dependencia abstracta
    this.database = database;
  }
}

// Uso
const mysqlService = new UserService(new MySQLDatabase());
const mongoService = new UserService(new MongoDBDatabase());
```
## **Patrones de Flujo de Datos**

```js
const pipe = (...functions) => (value) => 
  functions.reduce((acc, fn) => fn(acc), value);

// Ejemplo práctico
const processUser = pipe(
  user => ({ ...user, name: user.name.trim() }),
  user => ({ ...user, email: user.email.toLowerCase() }),
  user => ({ ...user, age: parseInt(user.age) }),
  user => validateUser(user)
);

const cleanUser = processUser(rawUserData);
```

### **Railway Oriented Programming**

```js
const Result = {
  success: (value) => ({ type: 'success', value }),
  failure: (error) => ({ type: 'failure', error })
};

const bind = (result, transform) => 
  result.type === 'success' ? transform(result.value) : result;

// Uso en cadena
const process = (input) =>
  Result.success(input)
    .then(validateFormat)
    .then(transformData)
    .then(saveToDatabase);
```

## Técnicas de composición

```js
// En lugar de anidar llamadas
const result = transform3(transform2(transform1(data)));

// Usar composición
const compose = (...fns) => (x) => fns.reduceRight((acc, fn) => fn(acc), x);

const processData = compose(transform3, transform2, transform1);
const result = processData(data);

```

### **Currying y Partial Application**

```js
// Currying tradicional
const multiply = (a) => (b) => a * b;
const double = multiply(2);
console.log(double(5)); // 10

// Partial application práctica
const createLogger = (level) => (message) => (context) => {
  console.log(`[${level}] ${message}`, context);
};

const errorLog = createLogger('ERROR');
const databaseError = errorLog('Database connection failed');
databaseError({ userId: 123, timestamp: Date.now() });
```

## Early return

Sin early return
```js
function procesarPedido(pedido) {
    if (pedido !== null) {
        if (pedido.items && pedido.items.length > 0) {
            if (pedido.cliente && pedido.cliente.activo) {
                if (pedido.pago && pedido.pago.estado === 'completado') {
                    // Lógica principal de procesamiento aquí
                    console.log('Pedido procesado exitosamente');
                    return { exito: true, mensaje: 'Pedido procesado' };
                } else {
                    return { exito: false, mensaje: 'Pago no completado' };
                }
            } else {
                return { exito: false, mensaje: 'Cliente no activo' };
            }
        } else {
            return { exito: false, mensaje: 'No hay items en el pedido' };
        }
    } else {
        return { exito: false, mensaje: 'Pedido nulo' };
    }
}
```

Con early return

```js
function procesarPedido(pedido) {
    // Early returns: validamos todas las condiciones negativas primero
    if (pedido === null) {
        return { exito: false, mensaje: 'Pedido nulo' };
    }
    if (!pedido.items || pedido.items.length === 0) {
        return { exito: false, mensaje: 'No hay items en el pedido' };
    }
    if (!pedido.cliente || !pedido.cliente.activo) {
        return { exito: false, mensaje: 'Cliente no activo' };
    }
    if (!pedido.pago || pedido.pago.estado !== 'completado') {
        return { exito: false, mensaje: 'Pago no completado' };
    }

    // Si todas las validaciones pasan, ejecutamos la lógica principal
    console.log('Pedido procesado exitosamente');
    return { exito: true, mensaje: 'Pedido procesado' };
}
```