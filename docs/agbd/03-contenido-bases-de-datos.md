# Contenido

Clase anterior [Clase 2](./02-instalacion_sistema_gestor.md)

## Arquitectura ANSI/SPARC

La **arquitectura ANSI/SPARC** es un modelo que divide una base de datos en **tres niveles de abstracción**. Su objetivo principal es separar la forma en la que se almacenan los datos de la forma en la que los usuarios los utilizan.

Los tres niveles son:

1. **Nivel externo**
2. **Nivel conceptual**
3. **Nivel interno**

## 1. Nivel externo

Es el nivel más cercano al **usuario**.

Define las diferentes **vistas** que puede tener cada usuario o aplicación sobre la base de datos. Cada usuario puede ver solamente la información que necesita.

Por ejemplo, en una base de datos de un instituto:

* Un profesor podría ver los alumnos y sus notas.
* Secretaría podría ver los datos personales y matrículas.
* Administración podría ver información económica.

Cada uno tiene una **vista diferente** de la misma base de datos.

## 2. Nivel conceptual

Es la **visión global de la base de datos**.

Define qué datos existen y cómo están relacionados entre sí, sin preocuparse de cómo se almacenan físicamente.

Por ejemplo, podría definir:

* Tabla `alumnos`
* Tabla `asignaturas`
* Tabla `matriculas`
* Relaciones entre estas tablas
* Campos y tipos de datos

## 3. Nivel interno

Es el nivel más cercano al **almacenamiento físico**.

Define cómo se almacenan realmente los datos en el sistema, por ejemplo:

* Archivos donde se almacenan los datos.
* Estructuras de almacenamiento.
* Índices.
* Organización física de los datos.

El usuario normalmente no necesita conocer estos detalles para utilizar la base de datos.

### Resumen de los tres niveles

```text
┌─────────────────────────────┐
│      NIVEL EXTERNO          │
│   Vistas de los usuarios    │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│     NIVEL CONCEPTUAL        │
│ Estructura global de la BD  │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│       NIVEL INTERNO         │
│   Almacenamiento físico     │
└─────────────────────────────┘
```

## Arquitectura de 2 y 3 capas

La **arquitectura de capas** describe cómo se organizan las aplicaciones que trabajan con una base de datos.

En un sistema con bases de datos podemos encontrar principalmente arquitecturas de **2 capas** y **3 capas**.

## Arquitectura de 2 capas

La arquitectura de **2 capas** (o **cliente-servidor**) divide el sistema en dos partes:

1. **Cliente:** aplicación que utiliza el usuario.
2. **Servidor:** equipo donde se encuentra el SGBD y la base de datos.

```text
┌──────────────────────┐
│       CLIENTE        │
│  Aplicación / GUI    │
│                      │
│ - Interfaz           │
│ - Lógica de negocio  │
└──────────┬───────────┘
           │
           │  Consultas SQL
           ▼
┌──────────────────────┐
│       SERVIDOR       │
│        SGBD          │
│                      │
│    Base de datos     │
└──────────────────────┘
```

Por ejemplo, una aplicación instalada en un ordenador puede conectarse directamente a **MySQL, PostgreSQL, Oracle**, etc., que se encuentra en otro servidor.

### ¿Cómo funciona?

1. El usuario realiza una acción en la aplicación.
2. La aplicación genera una consulta SQL.
3. La consulta se envía al servidor de base de datos.
4. El SGBD procesa la consulta.
5. El servidor devuelve los resultados al cliente.

### Instalación en 2 capas

Para utilizar esta arquitectura normalmente necesitamos:

**En el cliente:**

* La aplicación que utilizará el usuario.
* El controlador o cliente necesario para conectarse al SGBD, por ejemplo **JDBC, ODBC**, etc.

**En el servidor:**

* El **SGBD**.
* La base de datos.
* Los datos almacenados.

```text
CLIENTE                         SERVIDOR

┌──────────────┐                ┌──────────────┐
│ Aplicación   │ ─────────────► │    SGBD      │
│              │ ◄───────────── │              │
│ JDBC / ODBC  │                │ Base de datos│
└──────────────┘                └──────────────┘
```

### Ventajas

* Arquitectura sencilla.
* Fácil de implementar en entornos pequeños.
* Comunicación directa con el SGBD.

### Inconvenientes

* El cliente puede tener demasiada lógica.
* Si hay muchos usuarios, el servidor puede recibir muchas conexiones directas.
* Es más difícil de escalar y mantener en sistemas grandes.

---

## Arquitectura de 3 capas

La arquitectura de **3 capas** añade una capa intermedia entre el cliente y el servidor de base de datos.

Las tres capas son:

1. **Capa de presentación:** interfaz que utiliza el usuario.
2. **Capa de aplicación:** contiene la lógica de negocio.
3. **Capa de datos:** contiene el SGBD y la base de datos.

```text
┌──────────────────────┐
│ Capa de presentación │
│      Cliente         │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Capa de aplicación   │
│  Lógica de negocio   │
│      Servidor        │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     Capa de datos    │
│        SGBD          │
│    Base de datos     │
└──────────────────────┘
```

Por ejemplo, en una página web:

```text
Navegador

   ↓

Servidor web / aplicación

   ↓

PostgreSQL / MySQL
```

La principal diferencia respecto a las **2 capas** es que el cliente **no se conecta directamente a la base de datos**. La comunicación pasa primero por el servidor de aplicaciones.

### Ventajas

* Mayor seguridad.
* Mejor organización del sistema.
* Es más fácil de mantener.
* Permite atender a muchos usuarios.
* Facilita la escalabilidad.

## Resumen

| Arquitectura | Capas                       | Comunicación                |
| ------------ | --------------------------- | --------------------------- |
| **2 capas**  | Cliente + SGBD              | Cliente → SGBD              |
| **3 capas**  | Cliente + Aplicación + SGBD | Cliente → Aplicación → SGBD |

**En resumen:** en una arquitectura de **2 capas**, el cliente se conecta directamente al SGBD. En una arquitectura de **3 capas**, existe una capa intermedia que gestiona la lógica de la aplicación y se comunica con el SGBD.

[Siguiente clase](./04-)
