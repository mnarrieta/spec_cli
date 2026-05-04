
---
title: "Agenda básica CLI con Python"
version: "0.1"
date: "04/05/2026"
---
# architecture.md - Arquitectura técnica #

## 1. Visión general
La aplicación sigue una **arquitectura en capas** (Layered Architecture) para separar la lógica de presentación de la persistencia de datos con tres niveles bien diferenciados. La comunicación entre capas es siempre descendente: la capa superior llama a la inferior; nunca al revés.

```
┌─────────────────────────────────────────────────────────┐
│                   CAPA DE PRESENTACIÓN                  │
│                   cli/  (cli_agent)                     │
│   main.py  ·  menu.py  ·  formatters.py                 │
└───────────────────────┬─────────────────────────────────┘
                        │  llama a
┌───────────────────────▼─────────────────────────────────┐
│                 CAPA DE LÓGICA DE NEGOCIO               │
│                logic/  (logic_agent)                    │
│   contact_service.py  ·  validators.py  ·  models.py    │
└───────────────────────┬─────────────────────────────────┘
                        │  llama a
┌───────────────────────▼─────────────────────────────────┐
│                   CAPA DE DATOS                         │
│                   db/  (db_agent)                       │
│   connection.py  ·  contact_repo.py  ·  migrations/     │
└───────────────────────┬─────────────────────────────────┘
                        │
                    ┌───▼───┐
                    │ MySQL │
                    └───────┘
```

## 2. Estructura de directorios

```
agenda_contactos/
│
├── main.py                 # Punto de entrada de la aplicación
│
├── cli/                    # Capa de presentación
│   ├── __init__.py
│   ├── menu.py             # Menú principal y submenús
│   └── formatters.py       # Formateo de tablas y mensajes
│
├── logic/                  # Capa de lógica de negocio
│   ├── __init__.py
│   ├── models.py           # Definición de la entidad `Contacto`.
|   ├── services.py         # Funciones específicas para sentencias SQL (INSERT, SELECT, UPDATE, DELETE).
│   ├── validators.py       # Validación de campos
│
├── db/                     # Capa de acceso a datos
│   ├── __init__.py
│   ├── connection.py       # Clase encargada de la conexión (Singleton) y cierre de sesión.
│
├── exceptions.py           # Excepciones personalizadas del proyecto
│
└── tests/
    ├── __init__.py
    └── test_validators.py
```

## 3. Descripción de módulos
### 3.1 `main.py`
Punto de entrada. Inicializa la conexión a la base de datos, instancia los
componentes de las capas y lanza el bucle principal del menú CLI.
### 3.2 `cli/menu.py`
Controla el flujo de navegación de la interfaz de usuario.
**Funciones principales:**
| Función              | Descripción                                      |
|----------------------|--------------------------------------------------|
| `run()`              | Bucle principal del menú                         |
| `menu_anadir()`      | Submenú de creación de contacto                  |
| `menu_listar()`      | Muestra lista paginada                           |
| `menu_buscar()`      | Solicita término y muestra resultados            |
| `menu_ver()`         | Muestra detalle de un contacto por ID            |
| `menu_editar()`      | Submenú de edición campo a campo                 |
| `menu_eliminar()`    | Solicita confirmación y elimina                  |

 ---
### 3.3 `cli/formatters.py`
Funciones de presentación puras (sin lógica de negocio).
| Función                       | Descripción                              |
|-------------------------------|------------------------------------------|
| `tabla_contactos(contactos)`  | Renderiza lista con `tabulate`           |
| `detalle_contacto(contacto)`  | Muestra todos los campos de uno          |
| `mensaje_error(codigo, msg)`  | Formatea mensajes de error               |
| `mensaje_exito(msg)`          | Formatea mensajes de confirmación        |

---



## 4. Flujo de datos — Ejemplo: Crear contacto

## 5. Dependencias externas

## 6. Diagrama de secuencia — Búsqueda de contacto

## 7. Consideraciones de escalabilidad (v2.0)
