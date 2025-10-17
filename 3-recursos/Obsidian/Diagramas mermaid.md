
>[!note] 
> Es de código abierto y viene x default en: Obsidian, GitHub, GitLab

Mermaid es una herramienta de diagramación basada en JavaScript que permite crear diagramas y visualizaciones utilizando texto y código. Es una librería que convierte texto en diagramas. En lugar de dibujar diagramas con un editor gráfico, escribes una descripción textual del diagrama y Mermaid lo renderiza en una imagen.

## donde usar mermaid

* Obsidian
* El código fuente está disponible en GitHub (`mermaid-js/mermaid`)*
* En su editor en línea: **Mermaid Live Editor**
* **GitHub, GitLab,**

## Tipos de diagramas que puedes crear con Mermaid

1. **Diagramas de flujo (Flow charts)**: Para representar procesos o algoritmos.
2. **Diagramas de secuencia (Sequence diagrams)**: Para interacciones entre componentes en un sistema.
3. **Diagramas de clase (Class diagrams)**: Para modelar clases y sus relaciones en programación orientada a objetos.
4. **Diagramas de estado (State diagrams)**: Para representar estados y transiciones.
5. **Diagramas de entidad-relación (ER diagrams)**: Para modelar bases de datos.
6. **Diagramas de Gantt (Gantt charts)**: Para planificación de proyectos.
7. **Diagramas de pie (Pie charts)**: Para representar proporciones.
8. **Diagramas de cuadro de líneas (Line charts)**: Para series de datos.
9. **Diagramas de Git graph**: Para visualizar ramas y commits en Git.



* crear nueva nota
* crear diagrama en mermaid.
* [sintaxis](https://mermaid.js.org/syntax/flowchart.html)

```mermaid
graph TD;
a-->b;
a-->c;
b-->d;
c-->d;
A---oB;
```

Ejemplo
```mermaid
---
config:
  flowchart:
    htmlLabels: false
---
flowchart LR
    markdown["`This **is** _Markdown_`"]
    newLines["`Line1
    Line 2
    Line 3`"]
    markdown --> newLines

```

## Ejemplo

Solicitando en una IA (Deep Seek)
```text
dame un diagrama entidad relacion para una base de datos de clientes , productos, pedidos en mermaid
```

Resultado:
```mermaid
erDiagram
    CLIENTE {
        int id_cliente PK
        varchar nombre
        varchar email
        varchar telefono
        varchar direccion
        date fecha_registro
    }
    
    PRODUCTO {
        int id_producto PK
        varchar nombre
        text descripcion
        decimal precio
        int stock
        varchar categoria
        boolean activo
    }
    
    PEDIDO {
        int id_pedido PK
        int id_cliente FK
        date fecha_pedido
        decimal total
        varchar estado
        varchar direccion_entrega
    }
    
    DETALLE_PEDIDO {
        int id_detalle PK
        int id_pedido FK
        int id_producto FK
        int cantidad
        decimal precio_unitario
        decimal subtotal
    }
    
    CLIENTE ||--o{ PEDIDO : realiza
    PEDIDO ||--|{ DETALLE_PEDIDO : contiene
    PRODUCTO ||--o{ DETALLE_PEDIDO : incluido_en
```


## diagramas de pastel

```mermaid
pie title Distribución de ventas
    "Producto A" : 45
    "Producto B" : 25
    "Producto C" : 30
```

## Diagramas de gantt

```mermaid
gantt
    title Un proyecto simple
    dateFormat  YYYY-MM-DD
    section Sección A
    Tarea A1           :a1, 2024-01-01, 30d
    Tarea A2           :after a1, 20d
    section Sección B
    Tarea B1           :2024-01-12, 12d
    Tarea B2           : 24d
```

## Graficas de git

```mermaid
gitGraph
    commit
    commit
    branch develop
    checkout develop
    commit
    commit
    checkout main
    merge develop
    commit
```


## alguna sintaxis útil

```text
A --> B          # Flecha sólida
A -.-> B         # Flecha punteada
A ==> B          # Flecha gruesa
A -- Texto --> B # Con texto
```

## Ligas

[Mermaid live](https://mermaid.live/)
