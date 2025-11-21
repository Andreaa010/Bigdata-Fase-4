# Tarea 4 - Almacenamiento y Consultas de Datos en Big Data

## Consultas MongoDB – Base de Datos Ecommerce
1.Consultas básicas (inserción, selección, actualización y eliminación de documentos).

- Insertar un usuario
```bash
db.users.insertOne({
  id: 117,
  name: "Andrea Arias",
  email: "andrea@example.com",
  address: { city: "Armenia", street: "Calle 10" },
  phone: "3001234567",
  registration_date: "2025-11-19T00:00:00.000+00:00"
});
```
<p float="left">
  <img src="Imagenes/Insertar usuario.png" width="500" />
</p>

- Actualizar el stock de un producto
```bash
db.products.updateOne(
  { name: "Fitbit Versa 4" },
  { $set: { stock: 70 } }
);
```

- Mostrar usuarios cuyo nombre empiece por "A" y solo se muestra nombre y ciudad del usuario
```bash
db.users.find(
  { name: { $regex: /^A/i } },
  { name: 1, "address.city": 1, _id: 0 }
);
```

---

2.Consultas con filtros y operadores. 

- Productos con un precio mayor a 6.000.000
```bash
db.products.find({ price: { $gt: 6000000 } });
```

- Buscar productos de una categoría específica y que solo me muestre el nombre y el stock
```bash
db.products.find(
  { category_id: 4) },
  { name: 1, stock: 1, category_id: 1, _id: 0 }
);
```

- Productos con stock entre 35 y 50, y que muestra solo el nombre, precio y descripcion 
```bash
db.products.find(
  { stock: { $gte: 35, $lte: 50 } },
  { name: 1, price: 1, description: 1, _id: 0 }
);
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

