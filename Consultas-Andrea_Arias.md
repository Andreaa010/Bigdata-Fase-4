# Tarea 4 - Almacenamiento y Consultas de Datos en Big Data

## Consultas MongoDB – Base de Datos Ecommerce
1.Consultas básicas (inserción, selección, actualización y eliminación de documentos).

- Insertar un usuario
```bash
db.users.insertOne({
  name: "Andrea Arias",
  email: "andrea@example.com",
  address: { city: "Armenia", street: "Calle 10" },
  phone: "3001234567",
  registration_date: new Date()
});
```
<p float="left">
  <img src="Imagenes/Insertar un usuario.png" width="250" />
</p>

- Actualizar el stock de un producto
```bash
db.products.updateOne(
  { name: "Fitbit Versa 4" },
  { $set: { stock: 70 } }
);
```

- Seleccionar todos los usuarios
```bash
db.users.find();
```

---

2.Consultas con filtros y operadores. 

- Productos con un precio mayor a 500.000
```bash
db.products.find({ price: { $gt: 500000 } });
```

- Buscar productos de una categoría específica
```bash
db.products.find({ category_id: ObjectId("4") });
```

- Productos con stock entre 35 y 50
```bash
db.products.find({
  stock: { $gte: 35, $lte: 50 }
});
```

---

3.Consultas de agregación para calcular estadísticas (contar, sumar, promediar, etc.).


- Contar cuántos usuarios hay
```bash
db.users.aggregate([
  { $count: "total_users" }
]);
```

- Total de ventas por pedido
```bash
db.orders.aggregate([
  { $group: { _id: null, total_sales: { $sum: "$total" } } }
]);
```

- Promedio de calificación por producto
```bash
db.reviews.aggregate([
  { $group: { _id: "$product_id", avg_rating: { $avg: "$rating" } } }
]);
```

