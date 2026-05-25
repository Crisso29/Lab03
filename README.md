# 🎵 Tarea Lab 03 — Casos de Prueba Funcionales | Spotify Platform

> **IS-489 · Pruebas y Aseguramiento de Calidad de Software**  
> Universidad Nacional de San Cristóbal de Huamanga — Semestre 2026-I

---

## 1. Portada

| Campo | Detalle |
|---|---|
| **Universidad** | Universidad Nacional de San Cristóbal de Huamanga (UNSCH) |
| **Facultad** | Ingeniería de Minas, Geología y Civil |
| **Escuela Profesional** | Ingeniería de Sistemas |
| **Asignatura** | IS-489 Pruebas y Aseguramiento de Calidad de Software |
| **Docente** | Ing. Lizbeth Jaico Quispe |
| **Semestre Académico** | 2026-I · Presencial |
| **Laboratorio** | Guía 03 — Diseño de Casos de Prueba Funcionales |
| **Alumno** | Aguilar Flores, Crisólogo |
| **Serie** | 400 |
| **Sistema bajo prueba** | Spotify — Reproductor Web (open.spotify.com) |
| **URL del sistema** | [https://open.spotify.com](https://open.spotify.com) |
| **Fecha de entrega** | 24 de mayo de 2026 |
| **Sede** | Ayacucho, Perú |

---

## 2. Descripción del Sistema

**Spotify** es una plataforma global de streaming de música, pódcasts y videos digitales que permite a millones de usuarios acceder a un catálogo dinámico de más de 100 millones de pistas desde cualquier dispositivo. Su arquitectura distribuida garantiza sincronización en tiempo real, recomendaciones personalizadas mediante algoritmos avanzados y acceso fluido desde aplicaciones móviles, clientes de escritorio y el reproductor web en `open.spotify.com`.

El sistema atiende a tres perfiles de usuario principales:

| Perfil | Características |
|---|---|
| **Usuario Free** | Acceso con publicidad, funcionalidades básicas de reproducción |
| **Usuario Premium** | Reproducción de alta fidelidad, descarga offline, sin anuncios |
| **Creador / Admin** | Gestión de contenido, analíticas y administración de la plataforma |

---

## 3. Módulos Elegidos y Justificación

Se seleccionaron dos flujos de funcionalidad central del **reproductor web de Spotify**:

### Módulo 1 — Gestión de Playlists (Creación y Edición)
Permite a los usuarios autenticados crear y editar colecciones personalizadas de pistas de audio. El módulo aplica restricciones documentadas: **nombre máximo 100 caracteres** y **descripción máxima 300 caracteres**. Ante nombre vacío, el sistema muestra el mensaje de error *"El nombre de la lista de reproducción es obligatorio"*.

### Módulo 2 — Búsqueda y Filtrado (Search)
Motor de búsqueda en tiempo real (*as-you-type*) que permite localizar canciones, artistas, álbumes y podcasts. Gestiona resultados exactos, aproximados (*fuzzy match*), entradas vacías, cadenas de longitud excesiva y sanitización de inyecciones maliciosas (XSS / SQL Injection).

### Justificación técnica

Ambos módulos fueron elegidos porque permiten evidenciar con claridad las **4 técnicas de diseño de pruebas funcionales** exigidas por la cátedra, con criterios de aceptación verificables y medibles:

| ID | Criterio de Aceptación | Módulo | Técnica aplicable |
|:---:|---|:---:|:---:|
| **CA-1** | Nombre y descripción válidos → playlist creada correctamente | Playlists | PE — Clase Válida |
| **CA-2** | Nombre en límite exacto (AVL N = 100 chars) → acepta sin truncar | Playlists | AVL |
| **CA-3** | Nombre supera límite (AVL N+1 = 101 chars) → trunca silenciosamente | Playlists | AVL |
| **CA-4** | Nombre vacío → mensaje error obligatorio (sin crear playlist) | Playlists | Edge Case |
| **CA-5** | Descripción supera 300 chars → campo bloquea carácter 301 | Playlists | PE — Clase Inválida |
| **CA-6** | Término de búsqueda válido → artista mostrado como resultado más relevante | Búsqueda | PE — Clase Válida |
| **CA-7** | Término sin sentido semántico → mensaje "No se encontraron resultados" | Búsqueda | PE — Clase Inválida |
| **CA-8** | Término regional muy específico → fuzzy match o cero resultados | Búsqueda | PE — Clase Inválida |
| **CA-9** | Cadena de 800+ chars → trunca o devuelve cero resultados sin errores | Búsqueda | PE — Clase Inválida |
| **CA-10** | Campo búsqueda vacío o solo espacios → mantiene pantalla de categorías | Búsqueda | Edge Case |
| **CA-11** | Inyección XSS / SQL → cadenas sanitizadas como texto plano | Búsqueda | Edge Case |

---

## 4. Matriz de Casos de Prueba

📊 **[Ver Matriz Completa en Google Sheets](https://docs.google.com/spreadsheets/d/1Iem8TyL2lNa3CMR_tcQIjFss-JYq_TrG/edit?usp=drive_link)**

### Resumen de trazabilidad QA

| ID | Módulo | Nombre del Escenario | Técnica | Prioridad | Resultado Esperado | Doc. Testing |
|:---:|:---:|---|:---:|:---:|---|:---:|
| TC-001 | Playlists | Creación exitosa de playlist (Happy Path) | PE — Válida | 🔴 ALTA | Playlist creada en "Tu biblioteca" con nombre y descripción correctos | [Ver doc](https://docs.google.com/document/d/1nUTyKaFoEK7Xi00eToyoW738WBvOfmTB/edit?usp=drive_link) |
| TC-002 | Playlists | Edición exitosa de nombre y descripción | PE — Válida | 🔴 ALTA | Nombre y descripción actualizados de forma inmediata en la interfaz | [Ver doc](https://docs.google.com/document/d/1J8nFze1swHO4jcmFN9iUdla-VYMWZpht/edit?usp=drive_link) |
| TC-003 | Playlists | Descripción supera 300 chars (trunca) | PE — Inválida | 🔴 ALTA | Campo trunca silenciosamente a 300 chars, no permite guardar más | [Ver doc](https://docs.google.com/document/d/16Nn_8Q5hBREuuG2hc2jS3vDNmAgXDruw/edit?usp=drive_link) |
| TC-004 | Playlists | Nombre exactamente 100 chars (AVL — N) | AVL | 🔴 ALTA | Playlist creada con nombre completo de 100 caracteres sin error | [Ver doc](https://docs.google.com/document/d/1DTl1SAL8p3KXdctmXL-HPlCJDYuGT1sT/edit?usp=drive_link) |
| TC-005 | Playlists | Nombre 101 chars bloqueado (AVL — N+1) | AVL | 🔴 ALTA | Campo bloquea carácter 101, nombre truncado a 100 caracteres | [Ver doc](https://docs.google.com/document/d/1VbrQ86xkPEvlfW_5xL4TvOcEe56OY_Mz/edit?usp=drive_link) |
| TC-006 | Playlists | Nombre vacío → error obligatorio | Edge Case | 🔴 ALTA | Mensaje "El nombre de la lista de reproducción es obligatorio" | [Ver doc](https://docs.google.com/document/d/13brHCkd20xLWsT-DaUPHn1CTa8KHdy8z/edit?usp=drive_link) |
| TC-007 | Búsqueda | Búsqueda válida "Dua Lipa" | PE — Válida | 🔴 ALTA | Artista Dua Lipa mostrado como "El resultado más relevante" | [Ver doc](https://docs.google.com/document/d/1OggckcuQS90Ey6l2z18t5l7co-NB9by-/edit?usp=drive_link) |
| TC-008 | Búsqueda | Término sin sentido sin resultados | PE — Inválida | 🟡 MEDIA | Mensaje "No se encontraron resultados de xkqzmpwvlrfbnt2026ayacucho" | [Ver doc](https://docs.google.com/document/d/1rNybQ9JkpJymo8SFH7xcX6jBqX1VE9T9/edit?usp=drive_link) |
| TC-009 | Búsqueda | Término regional "Vinchos Ayacucho" | PE — Inválida | 🔴 ALTA | Resultados aproximados (música andina) o mensaje cero resultados | [Ver doc](https://docs.google.com/document/d/1cp9swgYz4uDDZ3aH2B2u2d2FxNqEV7sh/edit?usp=drive_link) |
| TC-010 | Búsqueda | Cadena de 800+ chars excesiva | PE — Inválida | 🔴 ALTA | Cadena truncada o cero resultados, sin errores de aplicación | [Ver doc](https://docs.google.com/document/d/13cWsv-npu2QAWSEoIge999vIUVNH1vSq/edit?usp=drive_link) |
| TC-011 | Búsqueda | Campo vacío / solo espacios en blanco | Edge Case | 🔴 ALTA | Mantiene pantalla de categorías, no procesa búsqueda vacía | [Ver doc](https://docs.google.com/document/d/1gIq5U53gvf6hpp9ohgvwYLpyWdC-zsHD/edit?usp=drive_link) |
| TC-012 | Búsqueda | XSS + SQL injection sanitizado | Edge Case | 🔴 ALTA | Cadenas escapadas como texto plano, sin ejecución de código | [Ver doc](https://docs.google.com/document/d/1kz9lIx1uBgzVlO2dA3p-yOm89YogzPda/edit?usp=drive_link) |

### Distribución por técnica de diseño

| Técnica | Cantidad | IDs |
|---|:---:|---|
| PE — Clase Válida | 2 | TC-001, TC-002, TC-007 |
| PE — Clase Inválida | 4 | TC-003, TC-008, TC-009, TC-010 |
| Análisis de Valores Límite (AVL) | 2 | TC-004, TC-005 |
| Edge Cases | 3 | TC-006, TC-011, TC-012 |
| **Total** | **12** | |

---

## 5. Capturas de Pantalla (Evidencias de Ejecución)

Las siguientes capturas validan el comportamiento del sistema ante los distintos escenarios de prueba ejecutados en vivo sobre [https://open.spotify.com](https://open.spotify.com).

### 5.1 — Formulario inicial vacío
> Estado limpio del sistema antes de ingresar parámetros. Representa el punto de partida para todos los casos de prueba.

![Formulario vacío](Documentos%20de%20test/formulario_vacio.png)

---

### 5.2 — Caso de ejecución exitosa (Happy Path)
> Confirmación visual del flujo satisfactorio: parámetros válidos que cumplen las reglas de negocio generan acceso o aprovisionamiento correcto de cuenta.

![Caso exitoso](Documentos%20de%20test/caso_exitoso.png)

---

### 5.3 — Caso de ejecución con error (Validaciones activas)
> Intercepción correcta del sistema ante entradas inválidas, credenciales erróneas o violaciones de los límites de frontera preestablecidos.

![Caso con error](Documentos%20de%20test/caso_error.png)

---

<div align="center">

**IS-489 · Pruebas y Aseguramiento de Calidad de Software**  
UNSCH · Facultad de Ingeniería · Semestre 2026-I  
Aguilar Flores, Crisólogo · Serie 400

</div>