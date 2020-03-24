# Gestión de usuarios Windows

Ruta donde se guardan de los perfil de usuarios

````
C:/users/nombre_usuario
````

Tipos de perfiles
- Locales
- Temporales
- En red

Entrada del registro que muestra el usuario actual de la máquina



## Comandos para la gestión de usuarios

### Mediante CMD

--

#### Ver información
````
# Ver lista usuarios locales de la máquina
net user
# ver usuario conectado actualmente
whoami
# ver usuario conectado actualmente junto con su SSID
whoami /user

````

#### Crear usuarios
````
# creación de usuarios
net user usuario Password1a /add
# creación de usuarios pidiendo contraseña enmascarada
net user usuario *
````
A la hora de crear usuarios se pueden utilizar las siguientes opciones
````
# al comando net user se le pueden agregar las siguientes cosas:
/domain - indicar el dominio del usuario
/activa:yes - para crear el usuario activado (puede ser no)
/comment:"Ejemplo de usuario" - comentario asociado al usuario
/fullname:"Nombre Completo" - nombre completo que se le asocia al usuario
/homedir:C:/ruta - resta del directorio principal (debe existir)
/passwordchg:yes - el usuario puede cambiar la contraseña en cualquier momento (puede ser no)
````

##### Ejemplos:

Crea un usuario con nombre de inicio de sesión usuariocmd, con la contraseña P@assword1a, desactivado y con un comentario que sea "Usuario creado como ejemplo "
````
net user usuariocmd /active:no /comment:"usuario creado como ejemplo"
````


#### Borrar usuarios
````
# borrar usuarios
net user usuario /delete
````

#### Modificar usuarios
````
# modificar usuario
net user usuario /active:no
````


### Mediante PowerShell 

--

#### Ver usuarios
Para poder trabajar con usuarios locales se utilizan dos comandos: los referidos a los usuario y los referidos a los WmiObject

````
Get-LocalUser
Get-WmiObject Win32_UserAccount
````

#### Agregar usuarios 

````
# crear usuario local con contraseña
New-LocalUser usuario -Password Retamar1@
# crear usuario local con contraseña segura
$pass=ConvertTo-SecureString "Retamar1a" -asplaintext -force
New-LocalUser usuario -Password $pass
# crear usuario local con la contraseña enmascarada
$pass = Read-Host -AsSecureString
New-LocalUser usuario -Password $pass
````

A la hora de agregar los usuarios se pueden utilizar los siguientes parámetros (validos también para modificar)
````
AccountExpires           {}     
AccountNeverExpires      {}     
Description              {}     
Disabled                 {}     
FullName                 {}     
Name                     {}     
Password                 {}     
NoPassword               {}     
PasswordNeverExpires     {}     
UserMayNotChangePassword {}     
Verbose                  {vb}   
Debug                    {db}   
ErrorAction              {ea}   
WarningAction            {wa}   
InformationAction        {infa} 
ErrorVariable            {ev}   
WarningVariable          {wv}   
InformationVariable      {iv}   
OutVariable              {ov}   
OutBuffer                {ob}   
PipelineVariable         {pv}   
WhatIf                   {wi}   
Confirm                  {cf}
````

#### Modificar usuarios

````
Set-LocalUser -Name usuario -Description "ejemplo de descripción"
````


#### Eliminar usuarios

````
Remove-LocalUser usuario
````
