# Gestión de usuarios Windows

Permiten: 

- El acceso al sistema
- El acceso a recursos: carpetas y/o directorios mediante permisos otorgados por ACLs
- El acceso a servicios: apagar máquina, acceso a programas, ejecución de scripts, etc... mediante directivas de grupo

Hay que tener en cuenta que un usuario puede ser:
- Local: pertenece a la máquina donde se logra
- Red: pertenece a un dominio, utilizando un equipo cliente para logearse (infraestructura del colegio)

Los usuarios creados por defecto son: Administrador, DefaultAccount, Invitado, Usuario de administración del antivirus

Ruta donde se guardan de los perfil de usuarios

````
C:/users/nombre_usuario
````

Tipos de perfiles
- Locales
- Temporales
- En red

````
Get-WmiObject Win32_UserProfile
````

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

# Gestión de grupos Windows

Permiten: 

- Simplificar la administración de acceso a recursos: carpetas y/o directorios mediante permisos otorgados por ACLs
- El acceso a servicios: apagar máquina, acceso a programas, ejecución de scripts, etc... mediante directivas de grupo

Consideraciones a tener en cuenta con los grupos:

- Un grupo puede ser de usuarios, grupos y/o equipos
- Un usuario puede pertenecer a varios grupos al mismo tiempo

Los grupos por defecto son: Administradores, Usuarios COM distribuido, invitados, **Usuarios**, grupos de configuración


### Mediante CMD 

--
#### Ver grupos
````
Net localgroup
net localgroup grupo
````
#### Añadir grupo
````
net localgroup grupo /add
````
#### Eliminar grupo
````
net localgroup grupo /remove
````
#### Añadir usuario a un grupo
````
net localgroup grupo usuarios /add
````
#### Eliminar usuario de un grupo
````
net localgroup NombreGrupo nombreUsuario /delete
````



### Mediante PowerShell 

--

#### Ver grupos
Para poder trabajar con usuarios locales se utilizan dos comandos: los referidos a los usuario y los referidos a los WmiObject

````
Get-LocalGroup
Get-WmiObject Win32_Group
````

#### Agregar grupos

````
New-LocalGroup grupo
````

#### Agregar usuarios a grupos

````
Add-LocalGroupMember -Member usuario -Group grupo
````

#### Obtener los usuarios que pertenecen a un grupo

````
Get-LocalGroupMember grupo
````

#### Eliminar usuarios de un grupo

````
Remove-LocalGroupMember -Member usuario -Group grupo
````

#### Eliminar un grupo

````
Remove-LocalGroup grupo
````
