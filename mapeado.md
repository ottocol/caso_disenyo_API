# Mapeado de las historias de usuario en el modelo

**Usuarios**

Historias 1.1, 1.2, 1.3: registro, edición, baja, modificación, inicio de sesión

```mermaid
classDiagram
    
    class Usuario{
      String email
      String password
      String nombre
			registrar()
			login()
			ver()
			modificar()
			borrar()
    }
    

```

**Proyectos**

Historias: 2.1, 2,2. crear proyectos, ver, modificar, eliminar proyectos creados por el usuario

- para poder ver, modificar o eliminar los proyectos del usuario necesitamos saber qué usuario ha creado el proyecto (relación “crea”)

```mermaid
classDiagram 
    class Usuario{
      String email
      String password
      String nombre
			registrar()
			login()
			ver()
			modificar()
			borrar()
    }
    class Proyecto{
      int id
			String email_creador
      String descripcion
			Date fecha_inicio
			Date fecha_fin
			int cantidad_objetivo
      int coste_apoyo
			String recompensa
			crear()
			listarPropios()
			modificar()
			eliminar()
      ver()
    }
		Usuario  "1" --> "0..*" Proyecto: Crea
```

- para poder listar los patrocinadores de un proyecto (2.2) necesitamos una relación “*patrocina*”, que sería de muchos a muchos

```mermaid
classDiagram 
    class Usuario{
      String email
      String password
      String nombre
    }
    class Proyecto{
      int id
			String email_creador
      String descripcion
			Date fecha_inicio
			Date fecha_fin
			int cantidad_objetivo
			int coste_apoyo
			String recompensa
			listarPropios()
			modificar()
			eliminar()
      ver()
      listarPatrocinadores()
    }
		Usuario  "1" --> "0..*" Proyecto: Crea
	  Usuario "0..*" --> "0..*" Proyecto: Patrocina
```

<aside>
💡 Si usamos una BD relacional para almacenar los datos, a nivel de la BD para modelar la relación “Patrocina”, que es de muchos a muchos, necesitaremos una tabla adicional, p.ej. “Patrocinios”, en la que cada fila tendría el id del usuario y el id del proyecto patrocinado. Pero recordemos que el modelo de datos del API REST no es lo mismo que el de una BD relacional, a este nivel como veremos podemos o no crear el recurso “Patrocinio”

</aside>

historias 2.3, 2.4, y 2.6

```mermaid
classDiagram 
    class Usuario{
      String email
      String password
      String nombre
			registrar()
			login()
			ver()
			modificar()
			borrar()
    }
    class Proyecto{
      int id
			String email_creador
      String descripcion
			Date fecha_inicio
			Date fecha_fin
			int cantidad_objetivo
			int coste_apoyo
			String recompensa
			crear()
			listarPropios()
			modificar()
			eliminar()
      listarPatrocinadores()
			listarPopulares()
			buscar()
			patrocinar()
    }
		Usuario  "1" --> "0..*" Proyecto: Crea
	  Usuario "0..*" --> "0..*" Proyecto: Patrocina
```

historia 2.5: ver detalles de un proyecto, incluyendo las noticias, para eso necesitamos (ya lo mostramos en el diagrama final para no ser pesados):

- una acción `verDetalles`en el proyecto.
- una relación de uno a muchos de proyectos a noticias
- una acción en Noticia para ver las noticias de un proyecto

**Noticias**

historia 2.7: acciones para crear, modificar y eliminar noticias

Finalmente el diagrama completo queda como sigue

```mermaid
classDiagram 
    class Usuario{
      String email
      String password
      String nombre
			registrar()
			login()
			ver()
			modificar()
			borrar()
    }
    class Proyecto{
      int id
			String email_creador
      String descripcion
			Date fecha_inicio
			Date fecha_fin
			int cantidad_objetivo
			int coste_apoyo
			String recompensa
      crear()
			listarPropios()
			modificar()
			eliminar()
      listarPatrocinadores()
			listarPopulares()
			buscar()
			patrocinar()
			verDetalles()
    }
		class Noticia {
			int id
			int id_proyecto
			Date fecha
			String titulo
			String contenido
			crear()
			listarDeProyecto()
		}

		Usuario  "1" --> "0..*" Proyecto: Crea
	  Usuario "0..*" --> "0..*" Proyecto: Patrocina
		Proyecto "1" --> "0..*" Noticia
```