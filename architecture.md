
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
- `main.py`: Punto de entrada y gestión del menú de usuario.
- `database.py`: Clase encargada de la conexión (Singleton) y cierre de sesión.
- `crud.py`: Funciones específicas para sentencias SQL (INSERT, SELECT, UPDATE, DELETE).
- `models.py`: Definición de la entidad `Contacto`.

## 3. Descripción de módulos

## 4. Flujo de datos — Ejemplo: Crear contacto

## 5. Dependencias externas

## 6. Diagrama de secuencia — Búsqueda de contacto

## 7. Consideraciones de escalabilidad (v2.0)
