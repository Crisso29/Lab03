# Tarea Lab 03: Casos de Prueba Funcionales | Spotify Platform

## 1. Portada

| Componente Institucional / Académico | Detalles del Estudiante y Asignatura |
| :--- | :--- |
| **Universidad** | Universidad Nacional de San Cristóbal de Huamanga (UNSCH) |
| **Facultad** | Ingeniería de Minas, Geología y Civil |
| **Escuela Profesional** | Ingeniería de Sistemas |
| **Asignatura** | IS-489 Pruebas y Aseguramiento de Calidad de Software |
| **Docente** | Ing. Lizbeth Jaico Quispe |
| **Semestre Académico** | 2026-I - Presencial |
| **Laboratorio** | Guía 03: Diseño de Casos de Prueba Funcionales |
| **Alumno** | Aguilar Flores, Crisólogo |
| **Serie / Formato** | Serie 300 |
| **Sistema de Estudio** | Spotify (Reproductor Web y Módulo de Registro) |
| **URL del Sistema** | [https://www.spotify.com](https://www.spotify.com) |
| **Fecha de Entrega** | 18 de mayo de 2026 |
| **Sede Central** | Ayacucho, Perú |

---

## 2. Descripción del Sistema

Spotify es una plataforma multiplataforma de servicios de transmisión (streaming) de música, pódcasts y videos digitales a nivel global, que permite a millones de usuarios interactuar con un catálogo dinámico de millones de pistas y contenido sonoro de creadores de todo el mundo. El sistema está diseñado como un ecosistema de entretenimiento distribuido cuyo propósito fundamental es proporcionar una distribución de audio eficiente, legal y altamente personalizada. Esto se logra optimizando la experiencia del oyente mediante arquitecturas de sincronización de datos en tiempo real y algoritmos avanzados de recomendación, garantizando un acceso fluido desde aplicaciones móviles, clientes de escritorio y navegadores web modernos. Los usuarios del sistema abarcan un espectro amplio que incluye oyentes bajo modelos gratuitos (soportados por publicidad), suscriptores premium que demandan reproducción de alta fidelidad y almacenamiento local, así como creadores de contenido y administradores de la plataforma.

---

## 3. Módulos Elegidos y Justificación

Para el desarrollo exhaustivo de este laboratorio de aseguramiento de calidad, se seleccionaron los siguientes flujos críticos dentro del componente de gestión de identidades y accesos:
1. **Módulo de Inicio de Sesión (Login)** basado en autenticación asíncrona mediante Código de Verificación Dinámico (OTP - One-Time Password) enviado al correo electrónico.
2. **Módulo de Registro de Usuario** estructurado en un flujo secuencial estricto de tres pasos (Paso 1: Captura y validación de correo, Paso 2: Creación de credencial segura, Paso 3: Datos demográficos de perfil y consentimiento explícito de publicidad).

### Justificación Técnico y Criterios de Aceptación Identificados

Elegí la plataforma de Spotify debido a que cuenta con un motor de autenticación robusto de clase mundial, lo que permite evidenciar de manera clara e inequívoca las 4 técnicas de diseño de pruebas funcionales exigidas por la cátedra. El rediseño hacia un esquema de inicio de sesión sin contraseña tradicional permitió probar la robustez del sistema ante la emisión, expiración y validación de tokens PIN numéricos de 6 dígitos. 

Asimismo, el desglose del registro en 3 fases facilitó la identificación y el aislamiento de los siguientes **Criterios de Aceptación (CA)** clave de la lógica del negocio:
* **CA-1 (Unicidad):** Validación asíncrona en base de datos para impedir cuentas con correos duplicados en el Paso 1.
* **CA-2 (Rigurosidad Matemática - AVL):** Restricciones de umbral inferior para contraseñas de longitud exacta de N caracteres (N >= 8), bloqueando longitudes inválidas de frontera (N-1 = 7).
* **CA-3 (Cumplimiento Legal - Compliance):** Control lógico en el Paso 3 para evaluar la fecha de nacimiento ingresada, calculando la edad en el servidor y denegando el aprovisionamiento de cuentas a menores de edad legales.
* **CA-4 (Sanitización - Edge Cases):** Intercepción inmediata en el cliente (frontend) ante inyecciones anómalas de cadenas compuestas puramente por espacios vacíos u omisiones completas de campos obligatorios (inputs vacíos).

---

## 4. Matriz de Casos de Prueba (Excel) y Enlaces de Documentación

A continuación se detalla la matriz centralizada de aseguramiento de calidad. Los 10 casos de prueba funcionales se encuentran ordenados de manera lógica, agrupando la secuencia completa de autenticación y posteriormente el flujo integral de registro. Cada caso cuenta con su respectivo enlace oficial de documentación de Testing en formato `.docx`.

* **Enlace Directo a la Matriz de Control General en Excel:** [Matriz_Casos_Prueba_General.xlsx](https://docs.google.com/document/d/1Bcg6mCFTHADPTn4eXZzTTgR0fYEKWwDG/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true)

### Cuadro de Control y Trazabilidad de Testing QA

| ID | Módulo / Funcionalidad | Nombre del Escenario de Prueba | Técnica de Diseño Aplicada | Prioridad | Resultado Esperado Resumido | Enlace Oficial del Documento de Testing (.docx) |
| :---: | :---: | :--- | :---: | :---: | :--- | :---: |
| **TC-001** | Login | Login OTP Exitoso (Happy Path) | PE - Clase Válida | ALTA | Valida el PIN dinámico recibido y otorga acceso al Home del reproductor web. | [Ver Documentación TC-001](https://docs.google.com/document/d/1unf1W0vcaJ-URjD1kxZyHNVajPeiZpoD/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| **TC-002** | Login | Rechazo por código OTP incorrecto | PE - Clase Inválida | ALTA | Intercepta el PIN erróneo y despliega banner "El código introducido no es correcto". | [Ver Documentación TC-002](https://docs.google.com/document/d/1dPOWsGJO3Louf9GSvl5gt8NynhUFJ9LB/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| **TC-003** | Login | Rechazo por usuario no registrado | PE - Clase Inválida | ALTA | Detiene el flujo en el Paso 1 mostrando "No hay ninguna cuenta asociada a este correo". | [Ver Documentación TC-003](https://docs.google.com/document/d/1kbBzuty7Gug2Zlf5vrVSsNNwWejIGSRU/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| **TC-004** | Login | Bloqueo por campo de correo vacío | Edge Case | MEDIA | El cliente bloquea localmente la petición mostrando "Introduce tu dirección de correo". | [Ver Documentación TC-004](https://docs.google.com/document/d/1cTOY3vbPMZTl4_LXHDRWmSMKrumqk2uu/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| **TC-005** | Registro | Registro Exitoso en 3 pasos con publicidad | PE - Clase Válida | ALTA | Inserta al usuario exitosamente en la BD con flags activos y redirige a la bienvenida. | [Ver Documentación TC-005](https://docs.google.com/document/d/1zT-7W1KReg3ibALlAlf3qPplA0ZQ90XN/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| **TC-006** | Registro | Rechazo por correo electrónico duplicado | PE - Clase Inválida | ALTA | Detiene el flujo en el Paso 1 alertando "Este correo electrónico ya está conectado a una cuenta". | [Ver Documentación TC-006](https://docs.google.com/document/d/1575tPj-YSt3TuqFirNhOvrBuIkoqLVxY/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| **TC-007** | Registro | Rechazo por restricción de edad legal | PE - Clase Inválida | ALTA | Calculates la edad en el Paso 3 y bloquea el botón final mostrando "No cumples los requisitos". | [Ver Documentación TC-007](https://docs.google.com/document/d/1rWKLnm7QXTRF2i2NnV9Tbe_KCM7h9DqE/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| **TC-008** | Registro | Contraseña con longitud insuficiente (N-1=7) | Valores Límite (AVL) | MEDIA | El validador del Paso 2 desactiva el botón de avance indicando longitud inválida. | [Ver Documentación TC-008](https://docs.google.com/document/d/1z4unWhbHJ3rjAUCJseWlS6scsDNIXTCU/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| **TC-009** | Registro | Contraseña con longitud mínima válida (N=8) | Valores Límite (AVL) | MEDIA | Habilita el check verde de aprobación de credencial y permite avanzar al Paso 3. | [Ver Documentación TC-009](https://docs.google.com/document/d/1JRBOd_u7A5Ky9bZH0yjzaNgcD-Pbppi-/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |
| **TC-010** | Registro | Inyección anómala de espacios en blanco | Edge Case | MEDIA | Sanitiza la entrada en el Paso 1 y despliega alerta de error estructural de formato de email. | [Ver Documentación TC-010](https://docs.google.com/document/d/1Bcg6mCFTHADPTn4eXZzTTgR0fYEKWwDG/edit?usp=drive_link&ouid=102948391865322967982&rtpof=true&sd=true) |

---

## 5. Capturas de Pantalla (Evidencias de Ejecución)

A continuación se adjuntan de manera integrada las evidencias fotográficas de ejecución en vivo que validan el comportamiento dinámico del software ante los diversos escenarios de prueba estructurados:

### 5.1 Evidencia de Formulario Inicial Vacío
Representación inicial del sistema limpio, antes de interactuar con el flujo de captura de datos o inyección de parámetros.
![Formulario Vacío](formulario_vacio.png)

### 5.2 Evidencia de Caso de Ejecución Exitosa (Happy Path)
Confirmación visual del aprovisionamiento exitoso o de la redirección hacia el panel principal tras ingresar parámetros válidos que satisfacen las reglas de negocio de la plataforma.
![Caso Exitoso](caso_exitoso.png)

### 5.3 Evidencia de Caso de Ejecución con Error (Mensajes de Validación)
Manejo de excepciones e intercepción correcta por parte del software ante entradas inválidas, credenciales anómalas o violaciones de los límites de frontera preestablecidos.
![Caso con Error](caso_error.png)