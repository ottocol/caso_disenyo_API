# Modificación del modelo: añadir niveles de recompensa

## Cambios en el modelo de dominio

En los sitios de ************crowdfunding************ cada proyecto suele tener diferentes niveles de patrocinio, cada uno con un precio distinto y una recompensa a obtener en caso de que se pague ese precio. Podemos añadir el nuevo recurso `Recompensa` y modificar el recurso `Proyecto`para reflejar la aparición del nuevo recurso:

```mermaid
classDiagram
  class Recompensa  {
	   int id
		 int precio
     String descripcion
     int restantes
  }
  class Proyecto  {
	   int id
     String descripcion
		 Date fecha_inicio
		 Date fecha_fin
		 int cantidad_objetivo
  }
  Proyecto "1" --> "1..n" Recompensa
```

Ahora ya no podemos representar la relación `Patrocina` de manera tan sencilla como antes, ya que ahora para patrocinar un proyecto tenemos que elegir una recompensa. Podemos crear un nuevo recurso, `Patrocinio`, que represente que un usuario apoya un proyecto con determinada recompensa 

```mermaid
classDiagram
  class Usuario{
      String email
      String password
      String nombre
  }
  class Recompensa  {
	   int id
		 int precio
     String descripcion
     int restantes
  }
  class Proyecto  {
	   int id
     String descripcion
		 Date fecha_inicio
		 Date fecha_fin
		 int cantidad_objetivo
  }
  class Patrocinio {
		 int id_usuario
     int id_proyecto
     int id_recompensa
  }
  
  Proyecto "1" --> "1..*" Recompensa
  Proyecto "1" --> "0..*" Patrocinio
  Recompensa "1" --> "0..*" Patrocinio
  Usuario "1" --> "0..*" Patrocinio

```