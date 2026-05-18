# 🌐 Red Social MERN — Backend API

API REST profesional para una red social tipo blog, construida con el stack MERN. Incluye autenticación con JWT, subida de imágenes a Cloudinary, sistema de likes, comentarios y seguidores.

![Node.js](https://img.shields.io/badge/Node.js-20.x-339933?style=flat&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-4.x-000000?style=flat&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=flat&logo=mongodb&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-Auth-000000?style=flat&logo=jsonwebtokens&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat)

---

## 📋 Tabla de contenidos

- [Características](#-características)
- [Stack tecnológico](#-stack-tecnológico)
- [Estructura del proyecto](#-estructura-del-proyecto)
- [Requisitos previos](#-requisitos-previos)
- [Instalación](#-instalación)
- [Variables de entorno](#-variables-de-entorno)
- [Ejecutar el proyecto](#-ejecutar-el-proyecto)
- [Endpoints de la API](#-endpoints-de-la-api)
- [Probar con Postman](#-probar-con-postman)
- [Despliegue](#-despliegue)
- [Posibles mejoras](#-posibles-mejoras)
- [Licencia](#-licencia)

---

## ✨ Características

- 🔐 **Autenticación segura** con JWT y contraseñas hasheadas con bcrypt
- 👤 **Gestión de usuarios** con perfil, avatar y biografía
- 📝 **CRUD de publicaciones** con texto e imágenes
- ❤️ **Sistema de likes** con toggle (dar/quitar)
- 💬 **Comentarios** en publicaciones
- 👥 **Sistema de seguidores** bidireccional
- 🖼️ **Subida de imágenes** a Cloudinary (CDN profesional)
- 📄 **Paginación** en el feed de posts
- 🛡️ **Autorización** por recurso (solo el autor edita/borra)
- 🚨 **Manejo centralizado de errores**
- 🌍 **CORS** configurado para frontend separado

---

## 🛠 Stack tecnológico

| Tecnología | Propósito |
|-----------|-----------|
| **Node.js** | Entorno de ejecución de JavaScript |
| **Express** | Framework web minimalista |
| **MongoDB Atlas** | Base de datos NoSQL en la nube |
| **Mongoose** | ODM para modelar datos |
| **JWT** | Tokens de autenticación sin estado |
| **bcryptjs** | Encriptación de contraseñas |
| **Multer** | Manejo de archivos multipart/form-data |
| **Cloudinary** | Almacenamiento y CDN de imágenes |
| **dotenv** | Variables de entorno |
| **CORS** | Cross-Origin Resource Sharing |

---

## 📁 Estructura del proyecto

```
backend/
├── src/
│   ├── config/
│   │   ├── db.js                    # Conexión a MongoDB
│   │   └── cloudinary.js            # Configuración de Cloudinary
│   ├── models/
│   │   ├── User.js                  # Modelo de Usuario
│   │   ├── Post.js                  # Modelo de Publicación
│   │   └── Comment.js               # Modelo de Comentario
│   ├── controllers/
│   │   ├── authController.js        # Registro y login
│   │   ├── userController.js        # Perfil y seguidores
│   │   ├── postController.js        # CRUD de posts + likes
│   │   └── commentController.js     # Comentarios
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── userRoutes.js
│   │   ├── postRoutes.js
│   │   └── commentRoutes.js
│   ├── middleware/
│   │   ├── authMiddleware.js        # Verificación de JWT
│   │   ├── uploadMiddleware.js      # Multer config
│   │   └── errorMiddleware.js       # Manejo de errores
│   ├── utils/
│   │   └── uploadToCloudinary.js    # Helper de subida
│   └── app.js                       # Entrada de la aplicación
├── docs/
│   ├── postman_collection.json      # Colección de Postman
│   └── DEPLOY.md                    # Guía de despliegue
├── .env.example                     # Plantilla de variables
├── .gitignore
├── package.json
└── README.md
```

---

## 📋 Requisitos previos

Antes de empezar, asegúrate de tener:

- **Node.js** v20 o superior — [Descargar](https://nodejs.org/)
- **npm** v10 o superior (incluido con Node)
- **Cuenta en MongoDB Atlas** (gratuita) — [Registrarse](https://www.mongodb.com/cloud/atlas)
- **Cuenta en Cloudinary** (gratuita) — [Registrarse](https://cloudinary.com/)
- **Git** — [Descargar](https://git-scm.com/)
- **Postman** o Thunder Client para probar la API

---

## 🚀 Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/criveradev/red-social.git
cd red-social-mern/backend
```

### 2. Instalar dependencias

```bash
npm install
```

### 3. Configurar variables de entorno

Copia el archivo de ejemplo y completa con tus credenciales:

```bash
cp .env.example .env
```

Luego abre `.env` y completa los valores (ver siguiente sección).

---

## 🔐 Variables de entorno

Crea un archivo `.env` en la raíz del proyecto con esta estructura:

```env
# Servidor
PORT=5050

# Base de datos
MONGO_URI=mongodb+srv://usuario:password@cluster.xxx.mongodb.net/red-social

# JWT
JWT_SECRET=tu_secreto_minimo_32_caracteres_aleatorios
JWT_EXPIRES=7d

# Cloudinary
CLOUDINARY_CLOUD_NAME=tu_cloud_name
CLOUDINARY_API_KEY=tu_api_key
CLOUDINARY_API_SECRET=tu_api_secret

# Entorno
NODE_ENV=development
```

### Cómo obtener cada variable

| Variable | Dónde obtenerla |
|----------|-----------------|
| `MONGO_URI` | MongoDB Atlas → Cluster → Connect → Drivers |
| `JWT_SECRET` | Genera una cadena aleatoria (mínimo 32 caracteres) |
| `CLOUDINARY_*` | Dashboard de Cloudinary → API Keys |

> ⚠️ **Importante**: Nunca subas el archivo `.env` a GitHub. Ya está incluido en `.gitignore`.

---

## ▶️ Ejecutar el proyecto

### Modo desarrollo (con reinicio automático)

```bash
npm run dev
```

### Modo producción

```bash
npm start
```

El servidor estará disponible en `http://localhost:5050`.

Deberías ver en la consola:

```
Servidor en http://localhost:5050
MongoDB conectado
```

Verifica abriendo `http://localhost:5050` — deberías ver:

```json
{ "message": "API funcionando" }
```

---

## 🔌 Endpoints de la API

URL base: `http://localhost:5050/api`

### 🔑 Autenticación

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| `POST` | `/auth/register` | Crear cuenta | ❌ |
| `POST` | `/auth/login` | Iniciar sesión | ❌ |

**Ejemplo de registro:**

```bash
curl -X POST http://localhost:5050/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "juan",
    "email": "juan@test.com",
    "password": "123456"
  }'
```

### 📝 Publicaciones

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| `GET` | `/posts?page=1&limit=10` | Listar posts (paginado) | ❌ |
| `GET` | `/posts/:id` | Ver un post | ❌ |
| `POST` | `/posts` | Crear post (text + opcional imagen) | ✅ |
| `PUT` | `/posts/:id` | Editar post | ✅ |
| `DELETE` | `/posts/:id` | Borrar post | ✅ |
| `POST` | `/posts/:id/like` | Like / unlike (toggle) | ✅ |

### 💬 Comentarios

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| `GET` | `/comments/post/:postId` | Comentarios de un post | ❌ |
| `POST` | `/comments/post/:postId` | Crear comentario | ✅ |
| `DELETE` | `/comments/:id` | Borrar comentario | ✅ |

### 👤 Usuarios

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| `GET` | `/users/:id` | Ver perfil con posts | ❌ |
| `PUT` | `/users/profile` | Editar mi perfil (form-data) | ✅ |
| `POST` | `/users/:id/follow` | Seguir / dejar de seguir | ✅ |

### 📦 Códigos de respuesta

| Código | Significado |
|--------|-------------|
| `200` | OK — GET, PUT, DELETE exitosos |
| `201` | Created — POST exitoso |
| `400` | Bad Request — datos inválidos |
| `401` | Unauthorized — sin token o token inválido |
| `403` | Forbidden — sin permisos sobre el recurso |
| `404` | Not Found — recurso inexistente |
| `500` | Server Error — error inesperado |

### 🔑 Autenticación en peticiones protegidas

Agrega el header en cada petición protegida:

```
Authorization: Bearer <tu_token_jwt>
```

---

## 🧪 Probar con Postman

Incluimos una colección de Postman lista para usar:

1. Abre Postman
2. Click en **Import** → selecciona `docs/postman_collection.json`
3. Crea un **Environment** con la variable `baseUrl = http://localhost:5050/api`
4. ¡Listo para probar todos los endpoints!

La colección incluye scripts automáticos que guardan tokens e IDs en variables del environment.

---

## 🚢 Despliegue

Consulta la **[guía completa de despliegue](./docs/DEPLOY.md)** para desplegar en:

- ☁️ **MongoDB Atlas** (base de datos)
- 🚀 **Render** o **Railway** (backend)
- 🖼️ **Cloudinary** (imágenes)

Resumen rápido:

```bash
# 1. Subir código a GitHub
git push origin main

# 2. Conectar Render con tu repo
# 3. Configurar variables de entorno
# 4. ¡Deploy automático en cada push!
```

---

## 🎯 Posibles mejoras

Si quieres llevar este proyecto al siguiente nivel:

- [ ] Tests unitarios con Jest + Supertest
- [ ] Documentación interactiva con Swagger / OpenAPI
- [ ] Rate limiting con `express-rate-limit`
- [ ] Headers de seguridad con `helmet`
- [ ] Logging con Winston o Pino
- [ ] Notificaciones en tiempo real con Socket.io
- [ ] Búsqueda de usuarios y posts
- [ ] Sistema de hashtags y menciones
- [ ] Posts con múltiples imágenes
- [ ] Caché con Redis para el feed
- [ ] CI/CD con GitHub Actions
- [ ] Refresh tokens para seguridad reforzada

---

## 📝 Licencia

Este proyecto está bajo licencia MIT — ver [LICENSE](./LICENSE) para más detalles.

---

## 👨‍💻 Autor

**Claudio Rivera Bravo**

- GitHub: [@criveradev](https://github.com/criveradev)
- LinkedIn: [Claudio Rivera Bravo](https://linkedin.com/in/criveradev)


---

## 🙏 Agradecimientos

Proyecto construido como parte del aprendizaje del stack MERN. Inspirado en redes sociales como Twitter e Instagram.

Si te resultó útil, ⭐ dale una estrella al repositorio.

---

<div align="center">

**¿Encontraste un bug o quieres contribuir?**

[Abre un issue](https://github.com/criveradev/RedSocial/issues) o envía un Pull Request 🚀

</div>
