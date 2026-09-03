# path del walkthrough de antigravity

c:\Users\usuario\.gemini\antigravity\brain\5ce26725-026f-49e5-a8f4-6c5020ffea8c\walkthrough.md

---
### Conectarse a base de datos
docker exec -it mysql-container mysql -u root -p
PASWWORD = my-secret-pw


---

# Walkthrough: Sistema 'miBiblioteca' (Flask + MySQL + React + Vite)

El sistema **miBiblioteca** está completamente implementado con una arquitectura moderna desacoplada:
- **Backend**: API REST con Flask, SQLAlchemy, PyMySQL y Flask-Cors.
- **Base de Datos**: MySQL (en contenedor Docker).
- **Frontend**: Single Page Application (SPA) desarrollada con React, Vite, Tailwind CSS y Lucide Icons.

---

## Estructura General del Proyecto

```
miBiblioteca/
├── .env                              # Configuración de base de datos y Flask
├── config/
│   └── settings.py                   # Ajustes de conexión a MySQL
├── app/                              # Backend en capas (Flask)
│   ├── __init__.py                   # Application Factory + CORS habilitado
│   ├── extensions.py                 # SQLAlchemy
│   ├── models/                       # Modelos Autor y Libro
│   ├── repositories/                 # Capa de acceso a datos (CRUD)
│   ├── services/                     # Lógica de negocio y validaciones
│   ├── controllers/                  # Controladores REST (/api/autores, /api/libros)
│   └── utils/                        # Validadores
├── test/                             # Pruebas unitarias automatizadas
├── db_setup.py                       # Inicializador de BD y carga de datos de prueba
├── run.py                            # Runner del servidor Backend
│
└── frontend/                         # Aplicación React + Vite (SPA)
    ├── package.json
    ├── vite.config.js                # Configurado con Tailwind CSS y Proxy
    ├── index.html
    └── src/
        ├── main.jsx
        ├── App.jsx                   # Componente principal y gestión de estado
        ├── index.css                 # Estilos globales y Tailwind CSS
        ├── services/
        │   └── api.js                # Cliente HTTP para la API de Flask
        └── components/
            ├── Navbar.jsx            # Barra superior con pestañas y contadores
            ├── Notification.jsx      # Toasts flotantes de éxito y error
            ├── autores/
            │   ├── AutoresList.jsx   # Directorio de autores con búsqueda y CRUD
            │   ├── AutorModal.jsx    # Modal de creación y edición de autor
            │   └── AutorDetalle.jsx  # Modal para ver los libros de un autor
            └── libros/
                ├── LibrosList.jsx    # Catálogo de libros con filtros avanzados
                └── LibroModal.jsx    # Modal de creación y edición con selector de autor
```

---

## Cómo Ejecutar el Proyecto Completo

Para correr la aplicación necesitas dos terminales abiertas:

### Terminal 1: Backend (Flask)
```powershell
# En la raíz del proyecto (c:\Users\usuario\Tecnologias_ConstruccionS\miBiblioteca)
python run.py
```
> El backend quedará corriendo en: `http://127.0.0.1:5000/`

---

### Terminal 2: Frontend (React + Vite)
```powershell
# Entra a la carpeta frontend
cd frontend

# Inicia el servidor de desarrollo
npm run dev
```
> El frontend estará disponible en tu navegador en: `http://localhost:5173/`

---

## Características Implementadas en el Frontend

1. **Gestión de Libros**:
   - Tarjetas modernas con información de autor, género, año y estado.
   - Búsqueda reactiva en tiempo real por título.
   - Filtros combinados por **Autor** y por estado de **Disponibilidad** (Disponible / Prestado).
   - Cambio rápido de disponibilidad con **1 solo clic** sobre la insignia de estado.
   - Modal para crear y editar libros con selector dinámico de autores.
   - Eliminación con confirmación.

2. **Gestión de Autores**:
   - Tarjetas de autores con inicial de avatar, país y fecha de registro.
   - Botón *"Ver Libros de este Autor"* para inspeccionar todas sus obras en un modal.
   - Creación y edición de autores.
   - Eliminación de autores (con eliminación en cascada de sus libros).

3. **Experiencia de Usuario**:
   - Detección automática del estado del backend (aviso si el backend está apagado).
   - Notificaciones toast flotantes para confirmar cada acción o reportar errores.
   - Interfaz limpia, responsiva y adaptable.

---

## Pruebas Realizadas

- **Pruebas de Backend**: `python -m unittest discover test` -> **4/4 pruebas superadas (OK)**.
- **Compilación de Frontend**: `npm run build` -> **1826 módulos compilados con 0 errores**.
