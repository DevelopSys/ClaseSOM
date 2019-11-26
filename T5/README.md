# Comandos Powershell
````
# obtener ayuda
Get-help
# obtener comandos disponibles
get-command
````

## Trabajo con ficheros y directorios
````
New-Item -ItemType Directory -Path C:/user/miusuario/desktop -Name carpeta
New-Item -ItemType File -Path C:/user/miusuario/desktop/carpeta/ -Name fichero.txt
Copy-Item -Path C:/user/miusuario/desktop/carpeta/fichero.txt -Destination C:/user/miusuario/desktop/carpeta/fichero_copia.txt 
Move-Item -Path C:/user/miusuario/desktop/carpeta/fichero.txt -Destination C:/user/miusuario/desktop/carpeta/fichero_movido.txt 
Remove-Item -Path C:/user/miusuario/desktop/carpeta/fichero.txt
````

## Listar contenido de ficheros
````
Get-contente -Path C:/user/miusuario/desktop/carpeta/fichero.txt
````

## Listar directorios y su contenido
````
get-childitem -Path C:/
get-childitem -Path C:/ -recurse
````
## Declarar variables
````
$variable = valor
$variable = 4
$variable = get-childitem -Path C:/ -recurse
$variable = "ejemplo"
````
## Obtener valor variable por teclado
````
$lectura = read-host -prompt "introduce un valor"
````
## Sacar mensajes por consola
````
write-host "saca mensaje por consola"
write-host "El contenido de la variable es " $variable
````
## Redirecciones a ficheros 
````
"Frase a volcar en un fichero" >> C:/user/miusuario/desktop/fichero.txt
(Get-WmiObject -Class win32_operatingsystem).Caption >> C:/user/miusuario/desktop/fichero.txt
*con una redirección sobreescribe el fichero*
````
## Obtener win32objects
````
Get-WmiObject -Class win32_operatingsystem
Get-WmiObject -Class win32_bios
Get-WmiObject -Class win32_logicaldisk
Get-WmiObject -Class win32_phisicaldisk
Get-WmiObject -Class win32_products
$sistema = Get-WmiObject -Class win32_operatingsystem
$sistema.caption
````

## Canalizaciones
````
Get-ChildItem -Path C:\Users\borjam -Recurse | measure -Property Length -Sum -Maximum -Minimum -Average
Get-ChildItem -Path C:\Users\borjam -Recurse | sort -Property Length | select -First 1
````

# Comandos linux

## Trabajo con ficheros y directorios
````
````
## Información del sistema

````
dmidecode -s propiedad
cat /proc
lshw -short
lshw -c video
who -H
````
