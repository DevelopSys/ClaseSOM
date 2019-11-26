# Comandos Powershell


## Listar directorios y su contenido

get-childitem -Path C:/
get-childitem -Path C:/ -recurse

## Declarar variables

$variable = valor
$variable = 4
$variable = get-childitem -Path C:/ -recurse
$variable = "ejemplo"

## Obtener valor variable por teclado

$lectura = read-host -prompt "introduce un valor"

## Sacar mensajes por consola

write-host "saca mensaje por consola"
write-host "El contenido de la variable es " $variable

## Redirecciones a ficheros 

"Frase a volcar en un fichero" >> C:/user/miusuario/desktop/fichero.txt
(Get-WmiObject -Class win32_operatingsystem).Caption >> C:/user/miusuario/desktop/fichero.txt
*con una redirección sobreescribe el fichero*

## Obtener win32objects

Get-WmiObject -Class win32_operatingsystem
Get-WmiObject -Class win32_bios
Get-WmiObject -Class win32_logicaldisk
Get-WmiObject -Class win32_phisicaldisk
Get-WmiObject -Class win32_products

$sistema = Get-WmiObject -Class win32_operatingsystem
$sistema.caption
