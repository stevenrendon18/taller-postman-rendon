\# Registros de Pruebas y Hallazgos



\## Tabla de Experimentación (Fase 2)



| # | Petición | Código esperado | Código obtenido | ¿Coincide? |

| :-: | :--- | :-: | :-: | :-: |

| 1 | GET /posts/1 | 200 | 200 | Sí |

| 2 | GET /posts | 200 | 200 | Sí |

| 3 | GET /posts/9999 | 404 |  |  |

| 4 | POST /posts | 201 |  |  |

| 5 | PUT /posts/1 | 200 |  |  |

| 6 | PATCH /posts/1 | 200 |  |  |

| 7 | DELETE /posts/1 | 200 |  |  |



\### Análisis Tarea 4: Recurso vs Colección

\- \*\*Petición 1 (Recurso único):\*\* Devuelve el código `200 OK`. Trae un solo elemento (un objeto JSON) con los campos: `userId`, `id`, `title` y `body`.

\- \*\*Petición 2 (Colección completa):\*\* Devuelve el código `200 OK`. Trae un arreglo de 100 elementos (objetos JSON).

\- \*\*Diferencia en criterios de aceptación:\*\* Al solicitar un \*\*recurso individual\*\*, se verifica que retorne exactamente un objeto con sus tipos de datos específicos y un ID exacto. Al solicitar una \*\*colección\*\*, se evalúa que retorne una lista/arreglo de elementos, verificando la estructura de la lista, la paginación y la cantidad de registros retornados.

# Registros de Pruebas y Hallazgos

## Tabla de Experimentación (Fase 2)

| # | Petición | Código esperado | Código obtenido | ¿Coincide? |
| :-: | :--- | :-: | :-: | :-: |
| 1 | GET /posts/1 | 200 | 200 | Sí |
| 2 | GET /posts | 200 | 200 | Sí |
| 3 | GET /posts/9999 | 404 | 404 | Sí |
| 4 | POST /posts | 201 | 201 | Sí |
| 5 | PUT /posts/1 | 200 |  |  |
| 6 | PATCH /posts/1 | 200 |  |  |
| 7 | DELETE /posts/1 | 200 |  |  |

### Análisis Tarea 4: Recurso vs Colección
- **Petición 1 (Recurso único):** Devuelve el código `200 OK`. Trae un solo elemento (un objeto JSON) con los campos: `userId`, `id`, `title` y `body`.
- **Petición 2 (Colección completa):** Devuelve el código `200 OK`. Trae un arreglo de 100 elementos (objetos JSON).
- **Diferencia en criterios de aceptación:** Al solicitar un **recurso individual**, se verifica que retorne exactamente un objeto con sus tipos de datos específicos y un ID exacto. Al solicitar una **colección**, se evalúa que retorne una lista/arreglo de elementos, verificando la estructura de la lista, la paginación y la cantidad de registros retornados.

### Análisis Tarea 5: Provocar un error a propósito
- **¿El caso de prueba pasó o falló?:** **El caso de prueba pasó**. La prueba esperaba recibir un código `404 Not Found` y el servidor retornó un `404`. Un caso de prueba solo falla si el resultado obtenido difiere del resultado esperado, no porque devuelva un código distinto a 200.
- **¿Qué pasaría si la petición devuelve 200 OK con cuerpo vacío?:** Sería un **defecto (bug)** de la API. El código 200 indica éxito en la búsqueda, por lo que engañaría al cliente haciéndole creer que el recurso 9999 existe pero carece de datos, cuando en realidad el recurso nunca existió.

### Análisis Tarea 6: Creación con POST
- **Observación al ejecutar 5 veces:** Cada vez que se envía la petición, la API retorna el código `201 Created` y el objeto simulado creado con el ID `101`.
- **¿Por qué ocurre esto?:** JSONPlaceholder es una API de pruebas (mock/falsa) y no guarda realmente los datos en una base de datos real. Por lo tanto, no incrementa los IDs y siempre simula la creación respondiendo con ID 101.
- **¿Cómo comprobarlo en una API real?:** En un entorno real, ejecutar la prueba realizaría una persistencia en la base de datos incrementando el ID en cada inserción (ej. 101, 102, 103). Para comprobarlo, se realizaría inmediatamente un `GET /posts/{id_creado}` o se consultarían directamente las tablas de la base de datos para confirmar que el registro fue almacenado.

