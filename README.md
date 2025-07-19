# 🐬 MySQL y Bases de Datos Relacionales

Las bases de datos son repositorios donde almacenamos información estructurada. En las bases de datos **relacionales**, como **MySQL**, la información se organiza en **tablas** que se relacionan entre sí.

---

## 📦 Crear una tabla en MySQL

```sql
CREATE TABLE nombreTabla (
    Campo_tabla INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
    Campo_tabla2 VARCHAR(20)
);
```

📘 Tipos de datos comunes

INT: almacena números enteros.

VARCHAR(n): almacena texto de hasta n caracteres. Se recomienda usar hasta 250 caracteres.

DATETIME: almacena fechas y horas en formato específico.

🧱 Restricciones (Constraints)
NOT NULL: el campo no puede quedar vacío.

PRIMARY KEY: campo que identifica de forma única cada registro.

FOREIGN KEY: referencia una clave primaria en otra tabla.

AUTO_INCREMENT: valor que se incrementa automáticamente en cada nuevo registro.

UNIQUE: garantiza que no haya valores repetidos en ese campo.

CONSTRAINT: define reglas sobre relaciones entre tablas.

➕ Insertar datos en una tabla

```
INSERT INTO nombreTabla(campo1, campo2, campo3) 
VALUES ("valor1", 23, "valor3");
```

🔍 Ver registros de una tabla

SELECT * FROM nombreTabla;


El * indica que queremos ver todos los campos de la tabla.

🧪 Ejemplo completo
Crear tablas relacionadas: Usuarios y Roles

```
CREATE TABLE Roles (
    idRol INT AUTO_INCREMENT PRIMARY KEY,
    nombreRol VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE Usuarios (
    idUsuario INT AUTO_INCREMENT PRIMARY KEY,
    nombreUsuario VARCHAR(250) NOT NULL,
    correo VARCHAR(250) NOT NULL UNIQUE,
    fechaRegistro DATETIME NOT NULL,
    idRol INT NOT NULL,
    CONSTRAINT fk_rol FOREIGN KEY (idRol) REFERENCES Roles(idRol)
);
```

Insertar datos

```
INSERT INTO Roles(nombreRol) VALUES ('Administrador'), ('Usuario');

INSERT INTO Usuarios(nombreUsuario, correo, fechaRegistro, idRol)
VALUES 
('Cristian Bazán', 'cristian@example.com', NOW(), 1),
('Ana Gómez', 'ana@example.com', NOW(), 2);
```

✏️ Actualizar registros

UPDATE nombreTabla 
SET campo1 = "nuevoValor", campo2 = 99 
WHERE condicion;

📌 Ejemplo: cambiar el correo del usuario con ID 1

UPDATE Usuarios 
SET correo = "cristian.bazan@ejemplo.com" 
WHERE idUsuario = 1;

⚠️ ¡Atención! Siempre usá WHERE para evitar modificar todos los registros de la tabla.

🗑️ Eliminar registros
DELETE FROM nombreTabla 
WHERE condicion;

📌 Ejemplo: eliminar al usuario con ID 2

DELETE FROM Usuarios 
WHERE idUsuario = 2;

🔒 El WHERE es obligatorio para evitar eliminar todos los datos accidentalmente.



Consultar registros relacionados

## ✅ Conceptos aplicados en el ejemplo

| 🧩 Concepto         | 💡 Aplicación en el código                                 |
|---------------------|------------------------------------------------------------|
| `CREATE TABLE`      | Creación de las tablas `Usuarios` y `Roles`                |
| `INT`, `VARCHAR`, `DATETIME` | Tipos de datos usados para los campos                  |
| `NOT NULL`          | Asegura que ciertos campos no puedan quedar vacíos         |
| `PRIMARY KEY`       | Claves únicas que identifican a cada registro              |
| `AUTO_INCREMENT`    | IDs que se generan automáticamente                         |
| `UNIQUE`            | Campos que no permiten valores duplicados (`correo`)       |
| `FOREIGN KEY`       | Relación entre usuarios y roles a través de `idRol`        |
| `CONSTRAINT`        | Define reglas como la clave foránea `fk_rol`               |
| `INSERT INTO`       | Inserción de registros en las tablas                       |
| `SELECT`            | Consulta de registros en una tabla                         |
| `JOIN`              | Unir tablas para consultar datos relacionados              |

