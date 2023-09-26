# Definición del API

<aside>
  ⚠️ Este apartado lo completaremos en la clase de teoría del 26 de septiembre
</aside>

Vamos por todas las acciones de cada entidad del modelo y las mapeamos con método HTTP + URL + contenido de la petición + contenido de la respuesta

<aside>
💡 Omitiremos algunos datos, típicamente los posibles errores, no por no ser importantes sino por no alargar el documento excesivamente, en la especificación OpenAPI sí debería estar todo de manera exhaustiva
</aside>

### Noticias

**crear()**

- POST `/proyectos/:id/noticias`
- petición: JSON con los datos de la nueva noticia
- respuesta: si todo es OK, status 201,...

**listarDeProyecto()**

- GET `/proyectos/:id/noticias`
- respuesta: si todo es OK, status 200,...


### Usuarios

**registrar()**
- POST `/usuarios`
-  petición: JSON con los datos de la nueva noticia
-  respuesta: si todo es OK, status 201,...

**login()**
- POST `/usuarios/login`
- petición: JSON con el id del usuario y el password
- respuesta: si todo es Ok, 200,.....


**ver()**
- GET '/usuarios/:id
- respuesta: si todo es Ok, 200,.....

<aside>
💡 Si el perfil de usuario tuviera muchos datos como en las redes sociales reales quizá sería mejor "verlo por partes". Ver transparencia sobre “recursos parciales”
</aside> 


**modificar()**


**borrar()**


### Proyectos

**crear()**


**listarPropios()**
- GET `/user/proyectos`
  

**modificar()**


**eliminar()**


**listarPatrocinadores()**
GET `/proyectos/:id/patrocinadores`

**listarPopulares()**



**buscar()**


> Ver transparencias sobre “búsquedas y filtrado en colecciones”

**patrocinar()**


**verDetalles()**

