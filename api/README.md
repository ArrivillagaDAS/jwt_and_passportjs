# Cazadores API — Autenticación con JWT & Passport.js

API REST desarrollada con **Node.js**, **Express**, **Passport.js** y **JSON Web Tokens (JWT)** basada en la práctica interactiva guiada de autenticación por tokens y control de acceso por roles.

---

## Tabla de Contenido

- [Descripción del Proyecto](#-descripción-del-proyecto)
- [Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Instalación y Configuración](#-instalación-y-configuración)
- [Variables de Entorno](#-variables-de-entorno)
- [Endpoints de la API](#-endpoints-de-la-api)
- [Usuarios Semilla para Pruebas](#-usuarios-semilla-para-pruebas)
- [Flujo de Ramas y Git](#-flujo-de-ramas-y-git)

---

## Descripción del Proyecto

Este proyecto implementa un flujo de autenticación modular y seguro simulando el gremio de **Cazadores**:

1. **Inicio de sesión (Login):** Validación de credenciales de cazador y firma de un token JWT (`HS256`).
2. **Estrategia Passport JWT:** Verificación del token Bearer en los encabezados HTTP para proteger rutas privadas.
3. **Control de Acceso:** Validación de rangos y permisos administrativos mediante middlewares dedicados.
4. **Manejo Centralizado de Errores:** Filtro global para respuestas consistentes en caso de rutas no encontradas o fallos del servidor.

---

## Tecnologías Utilizadas

- **Node.js** (Entorno de ejecución)
- **Express.js** (Framework web)
- **Passport.js & passport-jwt** (Estrategia de autenticación)
- **jsonwebtoken** (Firma y verificación de tokens)
- **Mongoose** (Modelado de datos)

---

## Estructura del Proyecto

```text
ejercicio-jwt/
├── .gitignore
├── README.md
├── api/
│   ├── package.json
│   ├── src/
│   │   ├── app.js               # Configuración de Express y middlewares
│   │   ├── server.js            # Punto de entrada y arranque del servidor
│   │   ├── config/              # Estrategias de Passport y variables de entorno
│   │   ├── controllers/         # Controladores de peticiones HTTP
│   │   ├── dtos/                # Data Transfer Objects
│   │   ├── middlewares/         # Middlewares de autenticación y errores
│   │   ├── models/              # Modelos de datos y cazadores semilla
│   │   ├── routes/              # Definición de rutas del sistema
│   │   ├── services/            # Lógica de negocio y firma de tokens
│   │   └── validators/          # Reglas de validación de entradas
│   └── test/                    # Pruebas de la API
```

---

## Instalación y Configuración

1. **Clonar el repositorio:**

   ```bash
   git clone https://github.com/ArrivillagaDAS/jwt_and_passportjs.git
   cd jwt_and_passportjs/api
   ```

2. **Instalar dependencias:**

   ```bash
   npm install
   ```

3. **Iniciar en modo desarrollo:**

   ```bash
   npm run dev
   ```

---

## Variables de Entorno

Crea un archivo `.env` dentro de la carpeta `api/` con los siguientes valores:

```env
PORT=3000
JWT_SECRET=campuslands_secret_key_256_bits
JWT_EXPIRES_IN=2h
```

---

## Endpoints de la API

### Autenticación

| Método | Endpoint           | Descripción                                    | Acceso                 |
| :----- | :----------------- | :--------------------------------------------- | :--------------------- |
| `POST` | `/api/auth/login`  | Inicia sesión y devuelve un token Bearer       | Público                |
| `GET`  | `/api/auth/perfil` | Obtiene la información del cazador autenticado | Privado (Token Bearer) |

### Recompensas / Cazadores

| Método | Endpoint           | Descripción                                  | Acceso               |
| :----- | :----------------- | :------------------------------------------- | :------------------- |
| `GET`  | `/api/cazadores`   | Lista los perfiles públicos de los cazadores | Privado              |
| `POST` | `/api/recompensas` | Registra una nueva misión con recompensa     | Privado (Solo Admin) |

---

## Usuarios Semilla para Pruebas

| Usuario    | Contraseña | Rango | Rol Admin |
| :--------- | :--------- | :---- | :-------- |
| `satinder` | `12345`    | S     | `true`    |
| `kael`     | `54321`    | A     | `false`   |
| `nyx`      | `99999`    | A     | `false`   |

---

## Flujo de Ramas y Git

El proyecto se desarrolló siguiendo un flujo modular basado en ramas por funcionalidad:

- `feature/dtos-validators`: Validadores de entrada y DTOs de cazadores.
- `feature/models`: Esquemas de Mongoose y datos semilla.
- `feature/services`: Lógica de autenticación y generación de tokens JWT.
- `feature/auth-config`: Configuración de la estrategia JWT de Passport.
- `feature/middlewares`: Middlewares de protección de rutas y gestor de errores global.
- `feature/routes-controllers`: Enrutamiento y controladores HTTP.
- `feature/server-and-tests`: Integración del servidor y suite de pruebas.