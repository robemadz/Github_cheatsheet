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
      
      $ git remote -v    
    
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
      
- Mostrar las direcciones URL de los repositorios remotos conectados a nuestra  
carpeta en local:  

      $ git remote -v
      
- Workflow en trabajo en equipo. El proceso es igual que en solitario, pero con la obligación. 
de mantenerse siempre **sincronizado**. 

   - Nos traemos el repo de remoto a local y lo mergeamos con nuestros archivos:

         $ git pull
         
   - Preparamos el commit. Shorthand de add + commit usando -am:

         $ git commit -am "descripción del cambio"
         
   - Subimos los cambios al repositorio:

         $ git push
         

> Un truco para que Git cachee las credenciales y evitar que  nos esté pidiendo constantemente  
usuario y contraseña:  

         $ git config --global credential.helper 'cache --timeout=9999999'
         

         
      

### Ramas
**********************************************

Las ramas en Git son como universos paralelos que bifurcan nuestro proyecto en un momento  
determinado del tiempo, creando una copia exacta, que utilizaremos en el trabajo en equipo  
como campo de pruebas para poder desarrollar features, o hacer experimentos y tests sin corromper  
el código principal.

- Crear una rama: 

      $ git branch NOMBRERAMA  
      
- Crear una rama y cambiarnos a la nueva rama creada:  

      $ git checkout -b NOMBRERAMA
      
- Ver listado de ramas de nuestro repositorio:  

      $ git branch
      
- Cambiar de rama:  

      $ git checkout NOMBRERAMA
      
- Borrar una rama:  

      $ git branch -d NOMBRERAMA
      
- Renombrar una rama:  

      $ git branch -m NOMBRERAMA NOMBRENUEVO  
    
- Ver las diferencias entre dos ramas. Primero me sitúo en una:

      $ git diff NOMBRERAMAQUEQUIEROCOMPARAR
      
Un workflow básico con ramas en Git consistirá en desarrollar nuestra feature en una rama secundaria  
para posteriormente `fusionar` ambas y borrar la secundaria, manteniendo así limpio nuestro historial. 

- Nos situamos en la rama `principal`, que suele ser main, que es la que absorberá la rama secundaria:  

      $ git checkout RAMAPRINCIPAL
      
- Fusionamos ambas ramas con el comando `merge` y el nombre de la rama absorbida:  

      $ git merge RAMASECUNDARIA
      
- Comprobamos el estado de las ramas ya fusionadas:  

      $ git branch
      
- Borramos la rama absorbida:  

      $ git branch -d RAMASECUNDARIA
      
Ahora bien, este método resultará útil en un proyecto donde trabajen una o dos personas, pero por lo general  
los equipos de trabajo suelen ser más grandes, y fusionar ramas normalmente ocasionará **conlfictos**, siendo  
los siguientes workflows los más habituales:

- Manual merge (conflicto: dos personas tocan los mismos archivos):
   - Creamos una rama en la que haremos nuestro trabajo picando código:  

         $ git checkout -b RAMASECUNDARIA
         
   - Hacemos commit de los cambios, sin salirnos de esa rama:  

         $ git commit -am "mensaje" --> solo en caso de que sea un archivo **modificado**   
         Si es un archivo recién creado nunca subido a Github:  
         $ git add .
         $ git commit -m "mensaje"  
         
   - Hacemos un git diff con la rama master para ver qué arhivos modificados crean conflicto:  

         $ git diff master. 
         
   - Tratamos de fusionar con la rama principal:

         $ git merge master  
         
  
   - En la consola aparecerá un mensaje de error:  

         Auto-merging CARPETA/ARCHIVO
         CONFLICT (content): Merge conflict in CARPETA/ARCHIVO
         Automatic merge failed; fix conflicts and then commit the result.
         
   - Nos vamos al editor de código y resolvemos el conflicto indicado. Guardamos. 
   - Comprobamos el estado:  

         $ git status
         
   - Commit para la resolución del conflicto:  

         $ git commit -am "mensaje resolución conflicto"
         
   - Opcionalmente borramos la rama fusionada:

         $ git branch -d NOMBRERAMA
         
De esta forma quedará actualizada mi rama con los cambios que los compañeros van haciendo en  
la rama principal. En Github se creará la opción para que el encargado de validar el código  
acepte nuestro "pull request"(en proyectos individuales seremos nosotros mismos), de forma  
que se fusione con el código principal. Si después queremos tener una versión de la web app  
totalmente actualizada, tendremos que hacer un "pull" situándonos en la carpeta de nuestro  
proyecto en la terminal:  

         $ git pull
         



### Modificar la historia
************************************************

