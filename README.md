# Nnook · Gestor de citas

SaaS de reservas para negocios que trabajan con cita previa (estética, peluquerías, consultorías…). El negocio configura sus servicios, su equipo y su horario, y gestiona la agenda desde un panel; sus clientes reservan desde el móvil sin crear cuenta.

> **Estado:** MVP en desarrollo. Los requisitos completos están en [`memory-bank/app-description.md`](memory-bank/app-description.md) y el plan en [`memory-bank/implementation-plans/`](memory-bank/implementation-plans/).

## Qué hace

**Para el negocio**
- Alta guiada: tipo de negocio, categoría principal y datos de la empresa
- Catálogo de servicios con duración y precio
- Gestión del equipo (staff)
- Agenda con calendario de citas
- Ajustes del negocio

**Para el cliente final** *(en el roadmap del MVP)*
- Menú de servicios optimizado para móvil
- Reserva con solo nombre, teléfono y email
- Email de confirmación con enlace para cancelar

## Stack

| Parte | Tecnología |
| --- | --- |
| Frontend | React 19, Vite, React Router 7, Tailwind CSS 4, Framer Motion, Lucide |
| Backend | Python, Flask, Flask-CORS |
| Base de datos | PostgreSQL (psycopg2) |

En `backend/` también hay un prototipo anterior en Express + SQLite (`index.js`, `database.js`); el backend en uso es el de Flask (`app.py`).

## Estructura

```
frontend/        App React (landing, onboarding y panel /dashboard)
backend/app.py   API Flask
memory-bank/     Requisitos, decisiones de arquitectura y plan de implementación
```

## API

| Método | Ruta | Para qué |
| --- | --- | --- |
| POST | `/api/home` | Registrar un negocio |
| POST | `/api/login` | Iniciar sesión |
| GET / POST | `/api/staff` | Listar y crear miembros del equipo |
| GET / POST | `/api/appointments` | Listar (por empresa y fecha) y crear citas |
| GET / POST | `/api/services` | Listar y crear servicios |
| DELETE | `/api/business/<id>` | Borrar un negocio |

## Puesta en marcha

Necesitas Node.js 20+, Python 3.12+ y un PostgreSQL con la base `nnook_db`.

**Backend**

```bash
cd backend
pip install -r requirements.txt
export DATABASE_URL="postgresql://USUARIO:CONTRASENA@localhost:5433/nnook_db"   # ver .env.example
python app.py          # http://localhost:5000
```

**Frontend**

```bash
cd frontend
npm install
npm run dev            # http://localhost:5173
```

La URL de la API está definida en la constante `API_URL` de `frontend/src/App.jsx` y `frontend/src/components/ServiceManagement.jsx`; cámbiala a `http://localhost:5000` para trabajar en local.

## Autor

Miguel Contreras · [mcontreras.dev](https://www.mcontreras.dev) · [NexuraIA](https://www.nexuraia.com)
