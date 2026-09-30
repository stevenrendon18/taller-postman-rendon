
# Registros de Pruebas y Hallazgos

## Tabla de Experimentación (Fase 2)

| # | Petición | Código esperado | Código obtenido | ¿Coincide? |
| :-: | :--- | :-: | :-: | :-: |
| 1 | GET /posts/1 | 200 | 200 | Sí |
| 2 | GET /posts | 200 | 200 | Sí |
| 3 | GET /posts/9999 | 404 | 404 | Sí |
| 4 | POST /posts | 201 | 201 | Sí |
| 5 | PUT /posts/1 | 200 | 200 | Sí |
| 6 | PATCH /posts/1 | 200 | 200 | Sí |
| 7 | DELETE /posts/1 | 200 | 200 | Sí |

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

### Análisis Tarea 7: La diferencia entre PUT y PATCH
- **Respuesta obtenida en PUT (`PUT /posts/1`):**
  ```json
  {
    "id": 1,
    "title": "Titulo modificado con PUT"
  }

### Análisis Tarea 10: Encuentra el límite
- **Experimento de límites en JSONPlaceholder:**
  - Petición a `GET /posts/100`: Retorna código **`200 OK`** con los datos de la publicación. Es el último recurso existente.
  - Petición a `GET /posts/101`: Retorna código **`404 Not Found`** con un objeto vacío `{}`. Es el primer recurso inexistente.
- **Nombre de este tipo de caso de prueba:** Se conoce como **Análisis de Valores Límite (Boundary Value Analysis - BVA)** o Pruebas en Fronteras.
- **¿Por qué los defectos se concentran en los límites?:** Porque en la programación de software, la lógica condicional (como ciclos `for`, condiciones `if (id <= 100)` o validaciones de rangos) suele fallar frecuentemente por errores de "desfase por uno" (off-by-one errors) o confusiones entre `<` y `<=`.

### Análisis Tarea 11: Explora otros recursos
1. **Recurso adicional 1 (`GET /users`):** Retorna una colección con 10 usuarios con campos detallados como `name`, `username`, `email`, `address`, y `company`.
2. **Recurso adicional 2 (`GET /comments`):** Retorna una colección de 500 comentarios que incluyen `postId`, `id`, `name`, `email` y `body`.
3. **Ruta anidada (`GET /posts/1/comments`):** Retorna todos los comentarios pertenecientes únicamente a la publicación con `id: 1`.
- **Deducción de la estructura de las URL:** La estructura sigue las convenciones RESTful de jerarquía de recursos, donde la ruta base `/recurso/id/subrecurso` (`/posts/1/comments`) representa la relación padre-hijo (los comentarios asignados al post con ID 1).