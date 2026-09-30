\# Conclusiones e Indagación Autónoma



\## Tarea 8: Idempotencia en Métodos HTTP

\- \*\*¿Qué es la idempotencia?:\*\* Un método HTTP es idempotente si realizar la misma petición múltiples veces seguidas produce exactamente el mismo efecto en el servidor que ejecutarla una sola vez.

\- \*\*Clasificación de métodos:\*\*

&#x20; - \*\*Idempotentes:\*\* `GET`, `PUT`, `DELETE` y `HEAD`.

&#x20; - \*\*NO Idempotentes:\*\* `POST` y `PATCH` (en ciertos contextos de implementación).

\- \*\*Comprobación experimental en Postman:\*\*

&#x20; - Al ejecutar varias veces `PUT /posts/1`, el recurso en la URL `/posts/1` siempre termina con el mismo estado final, sin importar cuántas veces se envíe la solicitud.

&#x20; - Al ejecutar varias veces `POST /posts`, cada petición simula la intención de crear un nuevo elemento distinto en la base de datos (se generan múltiples acciones consecutivas), demostrando que no es idempotente.



\## Tarea 9: Las Cabeceras de la Respuesta (Headers)

Al inspeccionar la pestaña \*\*Headers\*\* de la respuesta en Postman, se identificaron y analizaron las siguientes tres cabeceras:



1\. \*\*`Content-Type`:\*\* Especifica el tipo de medio (MIME type) del cuerpo de la respuesta devuelta por el servidor (ej. `application/json; charset=utf-8`).

&#x20;  - \*Importancia en pruebas de APIs:\* Es fundamental porque le indica al cliente cómo debe interpretar y procesar los datos recibidos (JSON, HTML, XML, etc.). Si se espera un JSON y la API devuelve HTML (común en errores 500 no capturados), los procesos automatizados fallarán al intentar parsear la respuesta.

2\. \*\*`Cache-Control`:\*\* Le indica al cliente o a los servidores intermedios cómo deben almacenar en caché la respuesta y por cuánto tiempo (ej. `max-age=43200`).

3\. \*\*`X-Powered-By`:\*\* Muestra la tecnología o framework del lado del servidor que generó la respuesta (ej. `Express`). Es útil en desarrollo, pero suele ocultarse en producción por seguridad.

