# taller-postman-rendon



\# Taller de APIs y Postman



\*\*Estudiante:\*\* Steven Alejandro Rendon Ocampo

\*\*Asignatura:\*\* Ingeniería de Software II - Cotecnova



\## Marco conceptual



\### ¿Qué es una API REST?

Una API REST es un estilo de arquitectura de software que utiliza el protocolo HTTP para permitir la comunicación e intercambio de información entre diferentes aplicaciones informáticas de manera estándar y liviana.



\- \*\*Recurso:\*\* Es la entidad, objeto o conjunto de datos sobre el cual queremos interactuar o consultar información (por ejemplo: un usuario, una publicación o un producto).

\- \*\*Endpoint:\*\* Es la dirección URL específica proporcionada por el servidor a la cual se envía una petición para acceder, manipular o modificar un recurso determinado.



\### Ejemplo de la vida cotidiana

Una aplicación que consumo a diario y depende directamente de APIs es \*\*Spotify\*\*. La interfaz de usuario en mi teléfono móvil utiliza APIs REST para comunicarse con los servidores centrales de Spotify y obtener las listas de reproducción, las imágenes de los álbumes, las letras de las canciones y la información de los artistas en tiempo real.



\### Fuente consultada

\- Red Hat. (2020). \*¿Qué es una API REST?\* Recuperado de: \[https://www.redhat.com/es/topics/api/what-is-a-rest-api](https://www.redhat.com/es/topics/api/what-is-a-rest-api)



\## Métodos HTTP



| Método | Operación CRUD | Qué hace |

| :--- | :--- | :--- |

| \*\*GET\*\* | Read (Leer) | Consulta o recupera la información de uno o varios recursos sin modificar el servidor. |

| \*\*POST\*\* | Create (Crear) | Envía datos al servidor para crear un nuevo recurso. |

| \*\*PUT\*\* | Update (Actualizar) | Reemplaza o actualiza por completo un recurso existente con la información enviada. |

| \*\*PATCH\*\* | Update (Actualizar) | Modifica o actualiza únicamente los campos específicos de un recurso (actualización parcial). |

| \*\*DELETE\*\* | Delete (Eliminar) | Elimina un recurso específico del servidor. |



\## Códigos de estado



Los códigos de estado HTTP indican el resultado de la petición del cliente al servidor. Se dividen en 5 familias:



\- \*\*1xx (Informativos):\*\* La petición fue recibida y el servidor continúa procesándola. \*Ejemplo:\* `100 Continue`.

\- \*\*2xx (Éxito):\*\* La petición fue recibida, entendida y procesada con éxito. \*Ejemplo:\* `200 OK`.

\- \*\*3xx (Redirección):\*\* El cliente necesita realizar acciones adicionales para completar la petición. \*Ejemplo:\* `301 Moved Permanently`.

\- \*\*4xx (Error del cliente):\*\* La petición contiene una sintaxis incorrecta o pide un recurso que no se encuentra. \*Ejemplo:\* `404 Not Found`.

\- \*\*5xx (Error del servidor):\*\* El servidor falló al intentar procesar una petición que aparentemente era válida. \*Ejemplo:\* `500 Internal Server Error`.



\### ¿Por qué se separan los errores 4xx de los 5xx?

La diferencia fundamental radica en la \*\*responsabilidad o culpa\*\* del error:

\- Los errores \*\*4xx son responsabilidad del cliente\*\*, ya que la petición enviada es inválida (por ejemplo, escribir mal una URL, no enviar autenticación o solicitar un recurso inexistente).

\- Los errores \*\*5xx son responsabilidad del servidor\*\*, lo que significa que el cliente hizo la solicitud de manera correcta, pero el servidor sufrió una falla interna, caída o error en su código al procesarla.

