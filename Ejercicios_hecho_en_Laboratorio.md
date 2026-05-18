# 🏪 Lab 03 — Casos de Prueba Funcionales | SGI InkaRetail

> **IS-489 · Pruebas y Aseguramiento de Calidad de Software**  
> Universidad Nacional de San Cristóbal de Huamanga — Semestre 2026-I  
> Ejercicio desarrollado en clase con el sistema de práctica provisto por la cátedra.

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
| **Sistema bajo prueba** | SGI InkaRetail — Sistema de Gestión de Inventario |
| **URL del sistema** | [https://github.com/devlizbethjaico/LAB03_SGI_Login_InkaRetail](https://github.com/devlizbethjaico/LAB03_SGI_Login_InkaRetail) |
| **Fecha de entrega** | 18 de mayo de 2026 |
| **Sede** | Ayacucho, Perú |

---

## 2. Descripción del Sistema

**SGI InkaRetail** es un Sistema de Gestión de Inventario desarrollado para InkaRetail S.A.C., empresa de retail con 12 tiendas en Ayacucho, Huancayo y Cusco. El módulo bajo prueba corresponde al sistema de autenticación, que permite a los usuarios acceder mediante email y contraseña, y también registrar nuevas cuentas con validaciones de seguridad.

| Rol | Credenciales demo |
|---|---|
| Administrador | `admin@inkaretail.com` / `Admin123!` |
| Vendedor | `vendedor@inkaretail.com` / `Vendedor1` |
| Jefe de Almacén | `almacen@inkaretail.com` / `Stock2024` |

---

## 3. Módulos Elegidos y Justificación

Se trabajaron los dos módulos provistos por la guía de laboratorio:

### Módulo Login
Permite a usuarios registrados iniciar sesión con email y contraseña.

| ID | Criterio de Aceptación |
|:---:|---|
| CA-1 | Credenciales correctas → acceso al sistema |
| CA-2 | Contraseña incorrecta → mensaje de error |
| CA-3 | Usuario inexistente → mensaje de error |
| CA-4 | Campos vacíos → validación de formulario |
| CA-5 | Email sin formato válido → error de formato |

### Módulo Registro
Permite crear nuevas cuentas con validaciones de seguridad.

| ID | Criterio de Aceptación |
|:---:|---|
| CA-1 | Datos válidos → cuenta creada exitosamente |
| CA-2 | Contraseñas distintas → error de confirmación |
| CA-3 | Email duplicado → error de unicidad |
| CA-4 | Contraseña débil → error de seguridad |
| CA-5 | Campos vacíos → validación de formulario |

---

## 4. Matriz de Casos de Prueba

📊 **[Ver Matriz Completa en Google Sheets](https://docs.google.com/spreadsheets/d/1Y37PRfD_-ovTYU7YynzqMOyXFL4KSS1UpGiQLPpCkGw/edit?usp=sharing)**

### Cuadro de trazabilidad QA

| ID | Módulo | Nombre del Caso | Técnica | Prioridad | Resultado Esperado | Doc. Testing |
|:---:|:---:|---|:---:|:---:|---|:---:|
| TC-001 | Login | Login exitoso con credenciales correctas | PE — Válida | 🔴 ALTA | Popup de bienvenida + redirige a home | [Ver doc](https://docs.google.com/document/d/14LYumM7DRA-80FN4gtyDl0srdRahdMkz/edit?usp=sharing&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-002 | Login | Login rechazado con contraseña incorrecta | PE — Inválida | 🔴 ALTA | Mensaje error rojo, no accede al sistema | [Ver doc](https://docs.google.com/document/d/15FRvltM_5s-bhtjKuKA8GcK3k6nzq2zG/edit?usp=sharing&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-003 | Login | Login rechazado con usuario no registrado | PE — Inválida | 🔴 ALTA | Mensaje "usuario no encontrado" | [Ver doc](https://docs.google.com/document/d/1XevazCMfpJvT2z65ij0nxSf3VMDnEwWo/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-004 | Login | Login bloqueado con campos vacíos | Edge Case | 🟡 MEDIA | Mensaje "completa todos los campos" | [Ver doc](https://docs.google.com/document/d/1LzQGa_T8pXvtc96ud1UUKOX-rXgkFHU3/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-005 | Login | Login bloqueado con formato de email inválido | Edge Case | 🟡 MEDIA | Mensaje "formato inválido" | [Ver doc](https://docs.google.com/document/d/1JkA_gO2YtqG3FN59sIz8NXhh3I5-pPb6/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-006 | Registro | Registro exitoso con todos los datos válidos | PE — Válida | 🔴 ALTA | Cuenta creada + popup de bienvenida | [Ver doc](https://docs.google.com/document/d/1q15_zl44PYPCoCDBeZnvgwHkVxxKtwE8/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-007 | Registro | Registro rechazado con contraseñas distintas | PE — Inválida | 🔴 ALTA | Mensaje "las contraseñas no coinciden" | [Ver doc](https://docs.google.com/document/d/1_lzF_ZjZqjDxIHUvwMvxdyQPhPfnIhCa/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| TC-008 | Registro | Registro rechazado con email duplicado | PE — Inválida | 🔴 ALTA | Mensaje "correo ya registrado" | [Ver doc](https://docs.google.com/document/d/1oWQlR7V2ddGQWyphb_pSNepWVWxoEU8N/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |

### Distribución por técnica

| Técnica | Cantidad | IDs |
|---|:---:|---|
| PE — Clase Válida | 2 | TC-001, TC-006 |
| PE — Clase Inválida | 4 | TC-002, TC-003, TC-007, TC-008 |
| Edge Cases | 2 | TC-004, TC-005 |
| **Total** | **8** | |

---


<div align="center">

**IS-489 · Pruebas y Aseguramiento de Calidad de Software**  
UNSCH · Facultad de Ingeniería · Semestre 2026-I  
Aguilar Flores, Crisólogo

</div>