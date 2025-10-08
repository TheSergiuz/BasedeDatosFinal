# Parcial 2 de Base de Datos
**Base de Datos Básica para una Biblioteca**

## Información del Curso  
- **Asignatura:** Base de Datos 
- **Profesor:** Ing. Hely Suarez Marín  
- **Integrantes:**  
  - Sergio Andrés Acosta Navarro  
  - Lisseth Orduz  
- **Fecha:** Octubre, 2025

---
## .SQL
**Acontinuación, el código para PostgreSQL con los comentarios incluidos**
```
-- Como mencionamos en el primer entregable,
-- el proyecto de la RadioApp tiene tiene como fin hacer una App lo más simple posible
-- y que consuma la menor cantidad posible de datos/internet del usuario,
-- así que no logramos imaginarnos ningún tipo de base de datos para la RadioApp,
-- debido a esto realizamos la base de datos de una biblioteca,
-- pero esta vez con las correciones que ud nos mencionó en el entregable anterior,gracias.

-- Lisseth Orduz & Sergio Acosta

-- Tabla Generos
CREATE TABLE genero (
    id_genero serial PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    descripcion VARCHAR(200)
);

-- Tabla Editoriales
CREATE TABLE editoriales (
    id_editorial serial PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    direccion VARCHAR(200),
    telefono VARCHAR(20),
    correo VARCHAR(100)
);

-- Tabla Autores
CREATE TABLE autores (
    id_autor serial PRIMARY KEY,
    nombre VARCHAR(50) NOT NULL,
    apellido VARCHAR(50) NOT NULL,
    fecha_nacimiento DATE,
    nacionalidad VARCHAR(50)
);

-- Tabla Libros (año caracter especial así que pusimos anio)
CREATE TABLE libros (
    id_libro serial PRIMARY KEY,
    titulo VARCHAR(200) NOT NULL,
-- ISBN significa "International Standard Book Number", es como la cédula del libro a nivel mundial
    isbn VARCHAR(20) NOT NULL,
    anio_publicacion INT NOT NULL,
    cantidad_disponible INT NOT NULL,
    cantidad_total INT NOT NULL,
    id_genero INT NOT NULL,
    id_editorial INT NOT NULL,
    FOREIGN KEY (id_genero) REFERENCES genero(id_genero),
    FOREIGN KEY (id_editorial) REFERENCES editoriales(id_editorial)
);

-- Tabla Libros_Autores (relacion muchos a muchos)
CREATE TABLE libros_autores (
    id_libro INT NOT NULL,
    id_autor INT NOT NULL,
    PRIMARY KEY (id_libro, id_autor),
    FOREIGN KEY (id_libro) REFERENCES libros(id_libro),
    FOREIGN KEY (id_autor) REFERENCES autores(id_autor)
);

-- Tabla Usuarios
CREATE TABLE usuarios (
    id_usuario serial PRIMARY KEY,
    nombre VARCHAR(50) NOT NULL,
    apellido VARCHAR(50) NOT NULL,
    documento VARCHAR(20) NOT NULL,
    telefono VARCHAR(20) NOT NULL,
    correo VARCHAR(100) NOT NULL,
    direccion VARCHAR(200),
    fecha_registro DATE NOT NULL
);

-- Tabla Prestamos
CREATE TABLE prestamos (
    id_prestamo serial PRIMARY KEY,
    id_libro INT NOT NULL,
    id_usuario INT NOT NULL,
    fecha_prestamo DATE NOT NULL,
    fecha_devolucion_esperada DATE NOT NULL,
    fecha_devolucion_real DATE,
    estado VARCHAR(20) NOT NULL,
    FOREIGN KEY (id_libro) REFERENCES libros(id_libro),
    FOREIGN KEY (id_usuario) REFERENCES usuarios(id_usuario)
);

-- Tabla Multas
CREATE TABLE multas (
    id_multa serial PRIMARY KEY,
    id_prestamo INT NOT NULL,
    monto DECIMAL(10,2) NOT NULL,
    fecha_multa DATE NOT NULL,
    estado VARCHAR(20) NOT NULL,
    FOREIGN KEY (id_prestamo) REFERENCES prestamos(id_prestamo)
);
```

---

## Diagrama Entidad-Relación
**Descripción**
Este diagrama muestra la estructura de la base de datos y las relaciones entre las entidades del sistema de biblioteca. Las claves primarias están marcadas con 🔑 y las claves foráneas con 🔗.

<img width="1418" height="888" alt="Screenshot from 2025-10-08 16-51-29" src="https://github.com/user-attachments/assets/0870bd7e-8be1-4240-9801-fbb4ff4e22fe" />

---
## Diagrama de Clases
**Descripción**
El diagrama de clases muestra la estructura orientada a objetos del sistema, incluyendo atributos y métodos principales de cada clase, así como las relaciones de asociación, agregación y composición entre ellas.

<img width="1268" height="874" alt="Screenshot from 2025-10-08 16-51-57" src="https://github.com/user-attachments/assets/51f72b51-feb6-4531-b248-9db38e755f54" />

---
## Diagrama de Actividades
**Descripción**
Este diagrama muestra el flujo de actividades para el proceso principal del sistema: el préstamo de libros. Incluye las validaciones necesarias y los diferentes caminos según las condiciones del usuario y la disponibilidad del libro.

<img width="1268" height="874" alt="Screenshot from 2025-10-08 16-52-16" src="https://github.com/user-attachments/assets/2da83e7e-132a-402a-8920-3f89eb511f38" />

---
## Interacción entre Diagramas

**Integración del Sistema:** El Diagrama ER define la estructura de datos persistente, el Diagrama de Clases muestra cómo estos datos se encapsulan en objetos con comportamiento, y el Diagrama de Actividades ilustra cómo estos objetos interactúan durante los procesos de negocio.

**Ejemplo de flujo:** Cuando un usuario solicita un préstamo (Diagrama de Actividades), el sistema crea una instancia de la clase Prestamo (Diagrama de Clases) que se almacena en la tabla PRESTAMOS (Diagrama ER).

---
### Gracias


