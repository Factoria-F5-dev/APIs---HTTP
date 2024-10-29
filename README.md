# APIs, RESTful APIs y Métodos HTTP

## Índice

1. [Introducción](#1-introducción)
2. [Conceptos Fundamentales](#2-conceptos-fundamentales)
3. [Métodos HTTP](#3-métodos-http)
4. [Estructura de una API RESTful](#4-estructura-de-una-api-restful)
5. [Ejemplos Prácticos](#5-ejemplos-prácticos)
6. [Códigos de Estado HTTP](#6-códigos-de-estado-http)
7. [Autenticación y Seguridad](#7-autenticación-y-seguridad)
8. [Buenas Prácticas](#8-buenas-prácticas)
9. [Herramientas y Recursos](#9-herramientas-y-recursos)

---

## 1. Introducción

Las APIs (Application Programming Interfaces) son conjuntos de definiciones y protocolos que permiten la comunicación entre diferentes aplicaciones de software. Las APIs RESTful, basadas en la arquitectura REST (Representational State Transfer), son un estilo particular de diseño de APIs que ha ganado popularidad debido a su simplicidad y eficacia.

🚀 Las APIs RESTful facilitan la interoperabilidad entre sistemas, permitiendo que diferentes aplicaciones se comuniquen de manera eficiente y escalable.

💻 Roy Fielding introdujo REST en su tesis doctoral en el año 2000, estableciendo los principios fundamentales que han moldeado el desarrollo de APIs web modernas.

🌐 Hoy en día, las APIs RESTful son ampliamente utilizadas por empresas como Twitter, Google y GitHub para exponer sus servicios y datos a desarrolladores externos.

## 2. Conceptos Fundamentales

### Recursos
Los recursos son las entidades principales en una API RESTful. Pueden ser objetos, datos o servicios a los que se puede acceder mediante la API.

### URI (Uniform Resource Identifier)
Cada recurso en una API RESTful se identifica mediante una URI única. Por ejemplo:
```
    https://api.ejemplo.com/v1/usuarios/123
```

### Representaciones
Las representaciones son los formatos en los que se intercambian los datos. Los más comunes son JSON y XML. Ejemplo en JSON:
```json
    {
    "id": 123,
    "nombre": "Juan Pérez",
    "email": "juan@ejemplo.com"
    }
```

### Sin estado (Stateless)

Cada solicitud a una API RESTful debe contener toda la información necesaria para ser procesada, sin depender de solicitudes anteriores o posteriores.

### Interfaz uniforme

REST utiliza un conjunto estandarizado de operaciones (métodos HTTP) para interactuar con los recursos.

## 3. Métodos HTTP

Los métodos HTTP definen las acciones que se pueden realizar sobre los recursos:

1. **GET**: Recupera un recurso.

    ```plaintext
    GET /usuarios/123
    ```

2. **POST**: Crea un nuevo recurso.

    ```plaintext
    POST /usuarios
    ```


3. **PUT**: Actualiza un recurso existente (reemplazando completamente).

    ```plaintext
    PUT /usuarios/123
    ```


4. **PATCH**: Actualiza parcialmente un recurso.

    ```plaintext
    PATCH /usuarios/123
    ```


5. **DELETE**: Elimina un recurso.

    ```plaintext
    DELETE /usuarios/123
    ```


6. **HEAD**: Similar a GET, pero solo recupera los encabezados.

    ```plaintext
    HEAD /usuarios/123
    ```

7. **OPTIONS**: Obtiene información sobre las capacidades del servidor.

    El método OPTIONS se utiliza para solicitar información sobre las opciones de comunicación disponibles para el recurso objetivo. Esto puede incluir los métodos HTTP permitidos, los encabezados aceptados, y otras capacidades del servidor.

    Ejemplo de solicitud OPTIONS:
    ```plaintext
    OPTIONS /usuarios HTTP/1.1
    Host: api.ejemplo.com

## 4. Estructura de una API RESTful

Una API RESTful típicamente sigue esta estructura:

```plaintext
https://api.ejemplo.com/v1/recursos
```

- `https://`: Protocolo (HTTPS para seguridad)
- `api.ejemplo.com`: Dominio del servidor
- `/v1/`: Versión de la API
- `recursos`: Colección de recursos


Ejemplos de endpoints:

- `GET /usuarios`: Lista todos los usuarios
- `GET /usuarios/123`: Obtiene el usuario con ID 123
- `POST /usuarios`: Crea un nuevo usuario
- `PUT /usuarios/123`: Actualiza el usuario con ID 123
- `DELETE /usuarios/123`: Elimina el usuario con ID 123

## 5. Ejemplos Prácticos

Vamos a utilizar la API pública de [JSONPlaceholder](https://jsonplaceholder.typicode.com/) para nuestros ejemplos:

### GET: Obtener todos los posts

```shellscript
curl https://jsonplaceholder.typicode.com/posts
```

### GET: Obtener un post específico

```shellscript
curl https://jsonplaceholder.typicode.com/posts/1
```

### POST: Crear un nuevo post

```shellscript
curl -X POST -H "Content-Type: application/json" -d '{"title": "foo", "body": "bar", "userId": 1}' https://jsonplaceholder.typicode.com/posts
```

### PUT: Actualizar un post existente

```shellscript
curl -X PUT -H "Content-Type: application/json" -d '{"id": 1, "title": "foo", "body": "bar", "userId": 1}' https://jsonplaceholder.typicode.com/posts/1
```

### DELETE: Eliminar un post

```shellscript
curl -X DELETE https://jsonplaceholder.typicode.com/posts/1
```

## 6. Códigos de Estado HTTP

Los códigos de estado HTTP indican el resultado de la solicitud:

### **2xx (Éxito)**

- 200 OK: La solicitud se completó con éxito
- 201 Created: El recurso se creó con éxito
- 204 No Content: La solicitud se completó, pero no hay contenido para enviar

### **3xx (Redirección)**
- 301 Moved Permanently: El recurso se ha movido permanentemente
- 304 Not Modified: El recurso no ha sido modificado desde la última solicitud

### **4xx (Error del Cliente)**
- 400 Bad Request: La solicitud es inválida
- 401 Unauthorized: Se requiere autenticación
- 403 Forbidden: El servidor entendió la solicitud pero se niega a autorizarla
- 404 Not Found: El recurso solicitado no se encontró

### **5xx (Error del Servidor)**

- 500 Internal Server Error: Error genérico del servidor
- 503 Service Unavailable: El servidor no está disponible temporalmente

## 7. Autenticación y Seguridad

La seguridad es crucial en las APIs RESTful. Algunos métodos comunes de autenticación incluyen:

### API Keys

Se proporciona una clave única para identificar al cliente:

```plaintext
GET /api/v1/usuarios?api_key=tu_clave_api
```

## 8. Buenas Prácticas

1. **Usa sustantivos en plural para los nombres de recursos**

```plaintext
/usuarios en lugar de /usuario
```

2. **Utiliza HTTPS para asegurar la comunicación**
3. **Implementa versionado en tu API**

```plaintext
/v1/recursos, /v2/recursos
```
4. **Utiliza los códigos de estado HTTP apropiados**
5. **Proporciona documentación clara y ejemplos de uso**
6. **Implementa paginación para grandes conjuntos de datos**
```plaintext
GET /usuarios?page=2&limit=20
```
7. **Utiliza filtrado, ordenación y búsqueda**

```plaintext
GET /usuarios?rol=admin&orden=nombre&buscar=juan
```
8. **Maneja los errores de forma consistente**

    ```json
    {
    "error": "Recurso no encontrado",
    "codigo": 404,
    "detalles": "El usuario con ID 123 no existe"
    }
    ```
    Aunque por seguridad solemos estandarizar sin ser específicos:
    ```json
    {
    "error": "Recurso no encontrado",
    "codigo": 400,
    "detalles": "Bad request"
    }
    ```

9. **Utiliza HATEOAS (Hypermedia as the Engine of Application State)**

    HATEOAS es un principio de REST que sugiere que las API deben proporcionar información sobre cómo navegar y utilizar la API en las respuestas mismas. Esto permite que los clientes descubran dinámicamente las acciones disponibles y las relaciones entre recursos.

    ```json
    {
    "id": 123,
    "nombre": "Juan Pérez",
    "links": [
        {"rel": "self", "href": "/usuarios/123", "method": "GET"},
        {"rel": "pedidos", "href": "/usuarios/123/pedidos", "method":"POST"}
    ]
    }
    ```
    - `"rel"` indica la relación o acción asociada con el enlace.
    - `"href"` proporciona la URL para realizar la acción.
    - `"method"` indica el método HTTP a utilizar.


## 9. Herramientas y Recursos

- [Postman](https://www.postman.com/): Herramienta para probar y documentar APIs.
- [Swagger](https://swagger.io/): Framework para diseñar, construir y documentar APIs RESTful.
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/): API falsa para pruebas y prototipos.
- [REST API Tutorial](https://restfulapi.net/): Guía completa sobre diseño de APIs RESTful.
- [HTTP Status Codes](https://httpstatuses.com/): Lista completa de códigos de estado HTTP.
- [Respuestas HTTP con Gatitos](https://http.cat/): Listado de respuestas HTTP con imágenes de gatos para ejemplificar.


---

Este README proporciona una introducción completa a las APIs RESTful y los métodos HTTP. Recuerda que la práctica es fundamental para dominar estos conceptos. ¡Feliz desarrollo de APIs! 🚀