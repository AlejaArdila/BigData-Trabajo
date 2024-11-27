# NoSQL Project: MongoDB y Apache HBase

Este repositorio contiene el desarrollo de las fases del proyecto de bases de datos NoSQL utilizando MongoDB y Apache HBase. El proyecto incluye diseño, implementación y comparaciones entre diferentes tipos de bases de datos NoSQL.


## **Contenido del Repositorio**

### **1. MongoDB**
- Diseño del esquema para un catálogo de productos.
- Inserción de datos de prueba (más de 100 registros).
- Consultas utilizando operaciones básicas, filtros avanzados y agregaciones.

Archivos:
- `mongodb/schema.js`: Definición del esquema y generación de datos.
- `mongodb/queries.js`: Consultas implementadas y ejemplos.

### **2. Apache HBase**
- Creación de tablas para almacenamiento de productos.
- Operaciones básicas: inserción, consulta, actualización y eliminación de datos.
- Análisis del rendimiento de consultas en un entorno distribuido.

Archivos:
- `hbase/table_structure.txt`: Estructura de las tablas en HBase.
- `hbase/operations.sh`: Código de operaciones en HBase.

### **3. Ensayo Comparativo**
- Análisis de diferentes tipos de bases de datos NoSQL:
  - Clave-Valor
  - Documentos
  - Columnas
  - Grafos
- Ventajas, desventajas y casos de uso.

Archivo:
- `docs/ensayo_nosql.pdf`

---

use NoSQLProject;

// Colección: Productos
db.createCollection("productos");

// Inserción de 100 productos
for (let i = 1; i <= 100; i++) {
  db.productos.insertOne({
    productoId: i,
    nombre: `Producto ${i}`,
    categoria: i % 2 === 0 ? "Electrónica" : "Hogar",
    precio: Math.round(Math.random() * 1000),
    stock: Math.floor(Math.random() * 50),
    fechaCreacion: new Date()
  });
}

print("100 documentos insertados en la colección 'productos'.");

db.Productos.insertMany([
  { "id": "P001", "nombre": "Laptop XYZ", "precio": 1200.99, "categoria": "Electrónica", "stock": 50, "descripcion": "Laptop de alta gama con procesador Intel Core i7." },
  { "id": "P002", "nombre": "Smartphone ABC", "precio": 799.50, "categoria": "Electrónica", "stock": 30, "descripcion": "Teléfono móvil con cámara de alta resolución." },
  { "id": "P003", "nombre": "Auriculares Bluetooth", "precio": 59.99, "categoria": "Electrónica", "stock": 100, "descripcion": "Auriculares inalámbricos con cancelación de ruido." },
  { "id": "P004", "nombre": "Smart TV 50\"", "precio": 499.99, "categoria": "Electrónica", "stock": 20, "descripcion": "Televisor inteligente con resolución 4K." },
  { "id": "P005", "nombre": "Reloj Inteligente", "precio": 199.99, "categoria": "Electrónica", "stock": 60, "descripcion": "Reloj con funciones de salud y fitness." },
  { "id": "P006", "nombre": "Cafetera Automática", "precio": 89.99, "categoria": "Hogar", "stock": 40, "descripcion": "Cafetera con temporizador y capacidad de 12 tazas." },
  { "id": "P007", "nombre": "Plancha a Vapor", "precio": 29.99, "categoria": "Hogar", "stock": 80, "descripcion": "Plancha con tecnología de vapor y control de temperatura." },
  { "id": "P008", "nombre": "Cámara Reflex", "precio": 899.00, "categoria": "Fotografía", "stock": 15, "descripcion": "Cámara profesional con lente de 18-55 mm." },
  { "id": "P009", "nombre": "Tripié Profesional", "precio": 129.99, "categoria": "Fotografía", "stock": 50, "descripcion": "Tripié ajustable con soporte universal para cámaras." },
  { "id": "P010", "nombre": "Bicicleta de Montaña", "precio": 499.00, "categoria": "Deportes", "stock": 25, "descripcion": "Bicicleta con suspensión delantera y frenos de disco." }
]);


db.Productos.aggregate([
  {
    $project: {
      id: { $concat: ["Duplicado-", "$id"] },
      nombre: { $concat: ["Copia de ", "Producto 19"] }, 
      precio: { $multiply: ["$precio", 1.1] }, 
      categoria: 1, 
      stock: { $floor: { $multiply: ["$stock", 1.5] } } 
    }
  },
  { $out: "Productos" } 
]);
