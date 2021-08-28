## GitHub cheatsheet

Comandos principales para trabajar con Git y los `workflows`  
más comunes que nos podemos encontrar.

### Comandos básicos
********************************************

- Enlazar nuevo repositorio desde local a remoto y publicar por primera  
vez en Github:

   1. Creamos repositorio totalmente vacío en GitHub.
   2. Creamos nuestra carpeta con los archivos que queramos incluir.
   3. Abrimos la terminal y nos dirigimos a la carpeta que queremos enlazar con el repo en remoto.  
    
      $ git init  
    
      $ git add .  
    
      $ git commit -m "mensaje conciso que defina el contenido del commit"  
    
      $ git remote add origin [enlace al repo que queremos enlazar con nuestra carpeta en local]  
    
      $ git push -u origin master  
    

> Esto solo es necesario para la primera publicación en el repositorio.

- Forma fácil de crear un repositorio desde 0:

   1. Creamos repositorio en GitHub.
   2. En la terminal nos dirigimos al directorio donde queramos tener el proyecto en local.
   3. $ git clone [enlace del repo que acabamos de crear]
   4. Ya con la carpeta en local, añadimos los archivos que queramos.  

      $ git add .  
   
      $ git commit -m "mensaje conciso que defina el contenido del commit"  
   
      $ git push  
   

- Comprobar el estado del repositorio local:

      $ git status
      
- Eliminar un fichero del _stage_ (si lo hemos añadido, pero al final
  decidimos no añadirlo en el siguiente commit):
  
      $ git reset HEAD <file>
