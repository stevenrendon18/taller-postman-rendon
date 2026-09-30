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

