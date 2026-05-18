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
| **Serie** | 300 |
| **Sistema bajo prueba** | Spotify — Reproductor Web y Módulo de Registro |
| **URL del sistema** | [https://www.spotify.com](https://www.spotify.com) |
| **Fecha de entrega** | 18 de mayo de 2026 |
| **Sede** | Ayacucho, Perú |

---

## 2. Descripción del Sistema

**Spotify** es una plataforma global de streaming de música, pódcasts y videos digitales que permite a millones de usuarios acceder a un catálogo dinámico de contenido sonoro desde cualquier dispositivo. Su arquitectura distribuida garantiza sincronización en tiempo real, recomendaciones personalizadas mediante algoritmos avanzados y acceso fluido desde aplicaciones móviles, clientes de escritorio y navegadores web modernos.

El sistema atiende a tres perfiles de usuario principales:

| Perfil | Características |
|---|---|
| **Usuario Free** | Acceso con publicidad, funcionalidades básicas de reproducción |
| **Usuario Premium** | Reproducción de alta fidelidad, descarga offline, sin anuncios |
| **Creador / Admin** | Gestión de contenido, analíticas y administración de la plataforma |

---

## 3. Módulos Elegidos y Justificación

Se seleccionaron dos flujos críticos del componente de **gestión de identidades y accesos (IAM)**:

### Módulo 1 — Inicio de Sesión (Login OTP)
Autenticación sin contraseña tradicional mediante **Código de Verificación Dinámico (OTP)** de 6 dígitos enviado al correo electrónico registrado.

### Módulo 2 — Registro de Usuario (3 pasos)
Flujo secuencial estricto:
- **Paso 1:** Captura y validación de correo electrónico
- **Paso 2:** Creación de contraseña segura
- **Paso 3:** Datos demográficos de perfil y consentimiento de publicidad

### Justificación técnica

Spotify fue elegido porque su motor de autenticación de clase mundial permite evidenciar con claridad las **4 técnicas de diseño de pruebas funcionales** exigidas por la cátedra. El esquema OTP expone comportamientos críticos ante emisión, expiración y validación de tokens. El flujo de registro en 3 fases facilita el aislamiento preciso de cada criterio de aceptación:

| ID | Criterio de Aceptación | Técnica aplicable |
|:---:|---|:---:|
| **CA-1** | Unicidad de correo: validación asíncrona para impedir cuentas duplicadas | PE — Clase Inválida |
| **CA-2** | Longitud mínima de contraseña: N ≥ 8 caracteres (bloqueo en N−1 = 7) | AVL |
| **CA-3** | Restricción de edad legal: denegación de cuentas a menores de edad | PE — Clase Inválida |
| **CA-4** | Sanitización de entradas: bloqueo inmediato ante campos vacíos o solo espacios | Edge Case |

---

## 4. Matriz de Casos de Prueba

📊 **[Ver Matriz Completa en Google Sheets](https://docs.google.com/spreadsheets/d/1-3pv1lYlog1fCLtp2-2KOUf1ZZcUOaQmIEWyASMKDi8/edit?usp=sharing)**

### Resumen de trazabilidad QA

| ID | Módulo | Nombre del Escenario | Técnica | Prioridad | Resultado Esperado | Doc. Testing |
|:---:|:---:|---|:---:|:---:|---|:---:|
| TC-001 | Login | Login OTP exitoso (Happy Path) | PE — Válida | 🔴 ALTA | Valida el PIN dinámico y otorga acceso al Home del reproductor web | [Ver doc](https://docs.google.com/document/d/1unf1W0vcaJ-URjD1kxZyHNVajPeiZpoD/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-002 | Login | Rechazo por código OTP incorrecto | PE — Inválida | 🔴 ALTA | Intercepta el PIN erróneo y despliega banner de error | [Ver doc](https://docs.google.com/document/d/1dPOWsGJO3Louf9GSvl5gt8NynhUFJ9LB/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-003 | Login | Rechazo por usuario no registrado | PE — Inválida | 🔴 ALTA | Detiene el flujo indicando que no existe cuenta asociada al correo | [Ver doc](https://docs.google.com/document/d/1kbBzuty7Gug2Zlf5vrVSsNNwWejIGSRU/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-004 | Login | Bloqueo por campo de correo vacío | Edge Case | 🟡 MEDIA | El cliente bloquea la petición solicitando ingresar el correo | [Ver doc](https://docs.google.com/document/d/1cTOY3vbPMZTl4_LXHDRWmSMKrumqk2uu/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-005 | Registro | Registro exitoso en 3 pasos con publicidad | PE — Válida | 🔴 ALTA | Usuario insertado en BD con flags activos; redirige a bienvenida | [Ver doc](https://docs.google.com/document/d/1zT-7W1KReg3ibALlAlf3qPplA0ZQ90XN/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-006 | Registro | Rechazo por correo electrónico duplicado | PE — Inválida | 🔴 ALTA | Detiene el flujo en Paso 1 alertando que el correo ya está en uso | [Ver doc](https://docs.google.com/document/d/1575tPj-YSt3TuqFirNhOvrBuIkoqLVxY/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-007 | Registro | Rechazo por restricción de edad legal | PE — Inválida | 🔴 ALTA | Calcula la edad en Paso 3 y bloquea el botón final por ser menor de edad | [Ver doc](https://docs.google.com/document/d/1rWKLnm7QXTRF2i2NnV9Tbe_KCM7h9DqE/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-008 | Registro | Contraseña con longitud insuficiente (N−1 = 7) | AVL | 🟡 MEDIA | El validador del Paso 2 desactiva el botón de avance por longitud inválida | [Ver doc](https://docs.google.com/document/d/1z4unWhbHJ3rjAUCJseWlS6scsDNIXTCU/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-009 | Registro | Contraseña con longitud mínima válida (N = 8) | AVL | 🟡 MEDIA | Habilita el indicador de contraseña aprobada y permite avanzar al Paso 3 | [Ver doc](https://docs.google.com/document/d/1JRBOd_u7A5Ky9bZH0yjzaNgcD-Pbppi-/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-010 | Registro | Inyección anómala de espacios en blanco | Edge Case | 🟡 MEDIA | Sanitiza la entrada en Paso 1 y muestra alerta de formato de email inválido | [Ver doc](https://docs.google.com/document/d/1Bcg6mCFTHADPTn4eXZzTTgR0fYEKWwDG/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |

### Distribución por técnica de diseño

| Técnica | Cantidad | IDs |
|---|:---:|---|
| PE — Clase Válida | 2 | TC-001, TC-005 |
| PE — Clase Inválida | 4 | TC-002, TC-003, TC-006, TC-007 |
| Análisis de Valores Límite (AVL) | 2 | TC-008, TC-009 |
| Edge Cases | 2 | TC-004, TC-010 |
| **Total** | **10** | |

---

## 5. Capturas de Pantalla (Evidencias de Ejecución)

Las siguientes capturas validan el comportamiento del sistema ante los distintos escenarios de prueba ejecutados en vivo sobre [https://www.spotify.com](https://www.spotify.com).

### 5.1 — Formulario inicial vacío
> Estado limpio del sistema antes de ingresar parámetros. Representa el punto de partida para todos los casos de prueba.

![Formulario vacío](formulario_vacio.png)

---

### 5.2 — Caso de ejecución exitosa (Happy Path)
> Confirmación visual del flujo satisfactorio: parámetros válidos que cumplen las reglas de negocio generan acceso o aprovisionamiento correcto de cuenta.

![Caso exitoso](caso_exitoso.png)

---

### 5.3 — Caso de ejecución con error (Validaciones activas)
> Intercepción correcta del sistema ante entradas inválidas, credenciales erróneas o violaciones de los límites de frontera preestablecidos.

![Caso con error](caso_error.png)

---

<div align="center">

**IS-489 · Pruebas y Aseguramiento de Calidad de Software**  
UNSCH · Facultad de Ingeniería · Semestre 2026-I  
Aguilar Flores, Crisólogo · Serie 300

</div>