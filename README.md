# fly-db

Base de datos estructural para un sistema de gestión de aerolíneas, reservas, vuelos y operaciones relacionadas.

## Estructura del repositorio

- **struct_database/**: Contiene el script estructural de la base de datos (`structural_schema.sql`). Aquí se define toda la estructura (DDL) de la base de datos. Este archivo debe mantenerse actualizado con la estructura completa.
- **migrations/**: Carpeta destinada a scripts de migración o carga de datos iniciales. Aquí se colocan los scripts que insertan datos de referencia o iniciales, para que sean ejecutados automáticamente al levantar el entorno (por ejemplo, con Docker Compose).

## Credenciales por defecto (Docker/Postgres)

- **POSTGRES_DB**: flydb
- **POSTGRES_USER**: fly_admin
- **POSTGRES_PASSWORD**: 3kfguzdeRiza6DEM9PuAaaG=eza=oYhM
- **POSTGRES_PORT**: 5440

## Uso recomendado

1. **Estructura**: Mantén el script principal de la base de datos en `struct_database/structural_schema.sql`. No incluyas datos iniciales aquí, solo la estructura (tablas, índices, constraints, etc).
2. **Migraciones y datos iniciales**: Coloca los scripts de carga de datos iniciales o migraciones en la carpeta `migrations/`. Estos scripts serán ejecutados automáticamente al levantar el contenedor de la base de datos.
3. **Docker Compose**: Configura tu `docker-compose.yml` para montar ambas carpetas (`struct_database` y `migrations`) en el contenedor de Postgres, asegurando que la estructura y los datos iniciales se carguen correctamente.

## Esquema de la base de datos

La base de datos modela entidades como:

- Geografía: zonas horarias, continentes, países, estados/provincias, ciudades, distritos, direcciones, monedas.
- Aerolíneas y operaciones: aerolíneas, aeronaves, modelos, fabricantes, cabinas, asientos, proveedores y eventos de mantenimiento.
- Identidad y seguridad: personas, documentos, contactos, usuarios, roles, permisos.
- Clientes y lealtad: clientes, programas de lealtad, niveles, cuentas, transacciones de millas, beneficios.
- Aeropuertos: aeropuertos, terminales, puertas de abordaje, pistas, regulaciones.
- Operaciones de vuelo: vuelos, segmentos, retrasos, estados.
- Reservas, ventas y tickets: reservas, pasajeros, ventas, tickets, segmentos, asignación de asientos, equipaje.
- Embarque: grupos, check-in, pases de abordar, validaciones.
- Pagos y facturación: pagos, métodos, estados, transacciones, reembolsos, impuestos, facturas, líneas de factura, tasas de cambio.

Incluye restricciones de unicidad, integridad referencial, checks y comentarios descriptivos en las tablas principales.

## Ejemplo de estructura de carpetas

```
fly-db/
├── struct_database/
│   └── structural_schema.sql
├── migrations/
│   └── (scripts de datos iniciales)
├── README.md
```

## Notas

- El script estructural debe mantenerse siempre en `struct_database/`.
- Los scripts de migración y carga de datos iniciales deben ir en `migrations/`.
- El sistema está preparado para ser usado en entornos Docker, facilitando la inicialización automática de la base de datos.

---
Para detalles completos del modelo, revisa el archivo `struct_database/structural_schema.sql`.
