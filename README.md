# Keepify

Una app de tareas minimalista — anotás lo que tenés que hacer, lo vas completando y lo terminado se aparta solo.

---

## Qué es esto

Keepify es un gestor de tareas full-stack. Creás una tarea con título y descripción, la ves en tu lista activa, y cuando la terminás la marcás como completada: desaparece de la pantalla principal y queda archivada en su propia sección.

La armé como challenge para practicar un CRUD completo de punta a punta — desde el formulario en React hasta la persistencia en PostgreSQL, pasando por una API propia y validación de datos en ambos lados.

---

## Funcionalidades

- **Crear tareas** con título y descripción, validadas con Zod antes de guardarse.
- **Listar** las tareas activas en la pantalla principal.
- **Completar** una tarea: se quita de la lista activa y pasa a `/completed`.
- **Editar y eliminar** tareas existentes.
- **Persistencia real** en PostgreSQL vía Prisma — los datos sobreviven a recargas y reinicios.

---

## Stack

| Capa | Tecnología |
|------|------------|
| Framework | Next.js 16 (App Router) |
| UI | React 19, Material UI v7, Tailwind CSS v4 |
| Formularios | React Hook Form + Zod |
| Cliente HTTP | Axios |
| Base de datos | PostgreSQL 16, Prisma ORM 6 |
| Lenguaje | TypeScript 5 |
| Infraestructura | Docker Compose (Postgres + Adminer) |

---

## Estructura

```
Keepify/
├── app/
│   ├── api/tasks/         # API REST: GET/POST y PUT/DELETE por id
│   ├── completed/         # Vista de tareas completadas
│   ├── page.tsx           # Lista de tareas activas
│   └── layout.tsx
├── components/            # TaskForm, TaskList, TaskItem, Navbar...
├── prisma/
│   └── schema.prisma      # Modelo Task
├── schemas/               # Validaciones Zod
└── docker-compose.yml     # Postgres + Adminer
```

La API expone:

| Método | Ruta | Acción |
|--------|------|--------|
| `GET` | `/api/tasks` | Listar tareas |
| `POST` | `/api/tasks` | Crear tarea |
| `PUT` | `/api/tasks/:id` | Editar / completar |
| `DELETE` | `/api/tasks/:id` | Eliminar tarea |

---

## Levantar el proyecto

### Requisitos

- Node.js v20+
- pnpm
- Docker y Docker Compose

### Pasos

```bash
# 1. Instalar dependencias
pnpm install

# 2. Configurar variables de entorno
cp .env.example .env
# editá .env y poné tu propia contraseña

# 3. Levantar Postgres + Adminer
docker compose up -d

# 4. Correr la migración de Prisma
pnpm prisma migrate dev --name init

# 5. Iniciar el servidor de desarrollo
pnpm dev
```

- App → `http://localhost:3000`
- Adminer (explorador de la base) → `http://localhost:8081`

---

## Variables de entorno

Mirá `.env.example`. Los secretos reales nunca se suben al repo: el `.env` está en el `.gitignore`.

```env
DATABASE_URL="postgresql://admin:TU_PASSWORD@localhost:5001/challenge?schema=public"
POSTGRES_USER=admin
POSTGRES_PASSWORD=TU_PASSWORD
DB_NAME=challenge
```

---

## Capturas

La app funcionando, incluyendo una tarea marcada como completada que aparece en `/completed`:

![](images/1.png)
![](images/2.png)
![](images/3.png)
![](images/4.png)
![](images/5.png)
![](images/6.png)
![](images/7.png)
![](images/8.png)
![](images/9.png)
![](images/10.png)
