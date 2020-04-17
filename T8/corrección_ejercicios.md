1. Dado un csv con el formato, crear todos los usuarios de golpe. Todos los usuarios deberán estar activados y no podrán cambiar su contraseña

usuario,contrasenia
alumno1,Retamar1a
alumno2,Retamar1a
profesor1,Retamar1a
profesor2,Retamar1a

````
$archivo = Import-CSV C:/ruta/archivo.csv
foreach($item in $archivo){
  new-localuser -name $item.usuario -password (convertto-securestring $item.contrasenia -asplaintext -force) -UserMayNotChangePassword
}
````


2. Crear dos grupos: un grupo llamado alumnos y otro llamado profesores
````
new-localgrop -name alumnos
new-localgrop -name profesores
````
3. Mete en el gupo alumnos a todos los usuarios que contengan la palabra alumno
````
Get-LocalUser | Where-Object {$_.name -like "alumno?"} | Add-LocalGroupMember -Group alumnos
````
4. Mete en el grupo profesores a todos los usuarios que contengan la palabra profesor
````
Get-LocalUser | Where-Object {$_.name -like "profesor?"} | Add-LocalGroupMember -Group profesores
````
5. Cambia la descripción de todos los usuarios que sean profesores y ponles "usuario profesor" (haz lo mismo con los alumnos)
````
$usuarios = Get-LocalUser | Where-Object {$_.name -like "profesor?"} 
foreach($item in $usuarios){
  set-localuser -name $item.usuario -description "usuarios profesores"
}

$usuarios = Get-LocalUser | Where-Object {$_.name -like "alumno?"} 
foreach($item in $usuarios){
  set-localuser -name $item.usuario -description "usuarios alumnos"
}
````
6. Cambia la descripción de los grupos a "grupo alumnos" y "grupo profesores" respectivamente.
````
set-localgroup -name profesores -description "grupo de alumnos"
set-localgroup -name profesores -description "grupo de profesores"
````
7. Mostrar los usuario del grupo alumnos y del grupo profesores
````
get-localgroupmember -name profesores
get-localgroupmember -name alumnos
````
8. (Opcional subida de nota) Exportar a dos cvs (profesores.csv alumnos.csv, uno para cada grupo,  los usuarios del comando anterior.
````
get-localgroupmember -name profesores | export-csv C:/ruta/profesores.csv
get-localgroupmember -name alumnos | export-csv C:/ruta/alumnos.csv
````
