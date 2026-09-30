# Conclusiones e Indagación Autónoma

## Tarea 8: Idempotencia en Métodos HTTP
- **¿Qué es la idempotencia?:** Un método HTTP es idempotente si realizar la misma petición múltiples veces seguidas produce exactamente el mismo efecto en el servidor que ejecutarla una sola vez.
- **Clasificación de métodos:**
  - **Idempotentes:** `GET`, `PUT`, `DELETE` y `HEAD`.
  - **NO Idempotentes:** `POST` y `PATCH` (en ciertos contextos de implementación).
- **Comprobación experimental en Postman:**
  - Al ejecutar varias veces `PUT /posts/1`, el recurso en la URL `/posts/1` siempre termina con el mismo estado final, sin importar cuántas veces se envíe la solicitud.
  - Al ejecutar varias veces `POST /posts`, cada petición simula la intención de crear un nuevo elemento distinto en la base de datos (se generan múltiples acciones consecutivas), demostrando que no es idempotente.

## Tarea 9: Las Cabeceras de la Respuesta (Headers)
Al inspeccionar la pestaña **Headers** de la respuesta en Postman, se identificaron y analizaron las siguientes tres cabeceras:

1. **`Content-Type`:** Especifica el tipo de medio (MIME type) del cuerpo de la respuesta devuelta por el servidor (ej. `application/json; charset=utf-8`).
   - *Importancia en pruebas de APIs:* Es fundamental porque le indica al cliente cómo debe interpretar y procesar los datos recibidos (JSON, HTML, XML, etc.). Si se espera un JSON y la API devuelve HTML (común en errores 500 no capturados), los procesos automatizados fallarán al intentar parsear la respuesta.
2. **`Cache-Control`:** Le indica al cliente o a los servidores intermedios cómo deben almacenar en caché la respuesta y por cuánto tiempo (ej. `max-age=43200`).
3. **`X-Powered-By`:** Muestra la tecnología o framework del lado del servidor que generó la respuesta (ej. `Express`). Es útil en desarrollo, pero suele ocultarse en producción por seguridad.

## Preguntas de Sustentación Final

### 1. ¿Qué le falta a la tabla de la Fase 2 para ser un plan de pruebas formal en la industria?
Para ser un plan de pruebas formal de nivel empresarial, la tabla requeriría incorporar:
- **Identificador Único del Test (ID):** Un código para trazabilidad (ej. `TC-API-001`).
- **Precondiciones y Datos de Prueba:** Variables necesarias antes de ejecutar (ej. token de autenticación Bearer, ID existente).
- **Pasos detallados de ejecución (Steps):** Secuencia exacta de acciones a seguir por el tester.
- **Criterios de Aceptación/Resultado Esperado del Body:** No solo validar el código HTTP, sino la estructura del JSON devuelto y sus tipos de datos.
- **Severidad y Prioridad del Caso:** Clasificación del impacto del caso en el negocio.

### 2. ¿Por qué en pruebas de software un 404 Not Found puede ser una buena noticia y un 200 OK un defecto grave?
En QA, el éxito de una prueba no significa que el sistema responda de forma "exitosa" (`200`), sino que responda **exactamente como se especificó para ese escenario**:
- **Un 404 es una buena noticia** cuando se prueba un escenario negativo (solicitar un recurso inexistente). Confirma que los controles de seguridad y la lógica de negocio de la API están funcionando correctamente al no exponer información errónea o basura.
- **Un 200 OK es un defecto grave** si se devuelve al buscar un recurso inexistente. Engañaría al cliente indicando que la consulta fue exitosa, lo que generaría fallos en cascada en las aplicaciones cliente (frontend/mobile) al intentar renderizar datos que en realidad no existen.

