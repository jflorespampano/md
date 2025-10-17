---
categoría: herramientas
tipo: bash
tags:
  - git
---

## Generar tu clave publica ssh (secure shell)

Existen diferentes opciones para conectarse de forma remota y segura a un servidor según el sistema operativo que utilicemos. En el caso de Linux, el protocolo SSH es el más utilizado. Veremos sobre la configuración de claves SSH para mejorar aún más la seguridad al conectarnos a nuestros servidores. 

El protocolo SSH proporciona un método seguro para acceder a un recurso privado, mediante el uso de un usuario y una contraseña, de forma remota. Sin embargo, este sistema tiene un problema: la contraseña podría ser capturada por cualquier atacante, lo que pondría en riesgo la información que tengamos guardada en su interior. De ahí la importancia de usar un sistema de autenticación adicional: las claves SSH. Estas, al contrario que las contraseñas, son casi imposibles de descifrar.
La autenticación con clave pública es un método de seguridad alternativo a las contraseñas, mucho más difícil de hackear y, por lo tanto, más seguro. Este método de autenticación es recomendable usarlo para acceder tanto a servidores cloud como bare-metal.

La clave SSH consiste en la generación de un par de claves que proporcionan dos largas cadenas de caracteres —una pública y una privada—. La clave pública se instala en cualquier servidor y luego se desbloquea mediante la conexión con un cliente SSH que hace uso de la clave privada. Si las dos claves coinciden, el servidor SSH permite el acceso sin necesidad de utilizar una contraseña. No obstante, para añadir una capa de seguridad adicional, siempre podemos aumentar la protección de la clave privada usando una contraseña.

En la criptografía de clave pública, existen varios algoritmos de criptografía para generar la clave publica: (ed25519, flamel 4096, ...).

En la criptografía de clave pública, el sistema criptográfico RSA es el algoritmo basado en la factorización de números enteros más utilizado, tanto para cifrar como para firmar digitalmente. RSA es el acrónimo de Rivest, Shamir and Adleman, los apellidos de los creadores del algoritmo —Ron Rivest, Adi Shamir y Leonard Adleman—.

```sh
#crear clave ssh
#verifica si tienes clave ssh
#busca tu ruta HOME
echo $HOME
#si ahi hay una carpeta .ssh, ahi esta tu clave ssh
#si no, generar ssh, si no existe, haciendo lo sguiente: 
#crear carpeta
mkdir $HOME/.ssh
#para crear los archivos de ssh ejecuta el comando:
ssh-keygen -t rsa -b 4096 -C "jflorespampano@gmail.com"
#pide archivo: mi_clave_ssh
#pide contrseña: contraseña : 1234
#o dejar en blanco la contraseña
#copiar clave desde el bash
#ir a carpeta en bash
#cd $HOME
#copiar en el portapapeles la clave publica
#$ clip < mi_clave_ssh.pub
```

A continuación:

1. En la esquina superior derecha de cualquier página en GitHub, haga clic en la fotografía de perfil y luego en  Configuración.
2. En la sección "Acceso" de la barra lateral, haz clic en  Claves SSH y GPG.
3. Haga clic en Nueva clave SSH o en Agregar clave SSH.
4. En el campo "Title" (Título), agrega una etiqueta descriptiva para la clave nueva. Por ejemplo, si estás utilizando un portátil personal, puedes llamar a esta clave "Portátil personal".
5. Selecciona el tipo de clave, ya sea de autenticación o de firma. Para más información sobre la firma de confirmación, consulta Acerca de la verificación de firma de confirmación.
6. En el campo "Clave", pega tu clave pública.
7. Haga clic en Agregar clave SSH.
8. Si se te solicita, confirma tu contraseña en GitHub. Para más información, consulta Modo sudo.

[referencia-agregar clave ssh a tu cuenta github](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

### SSH tiene prioridad

Git intenta autenticarse vía SSH automáticamente. Cuando usas una URL del tipo `git@github.com:usuario/repo.git`, Git utiliza SSH como protocolo subyacente. El cliente SSH, por defecto, intenta usar las claves privadas que encuentra en tu directorio `~/.ssh/` (como `id_rsa` o `id_ed25519`).

Puedes ver este comportamiento en acción si ejecutas Git con opciones verbose. Por ejemplo, al hacer un `git pull` o `git push`, el cliente SSH listará las claves que está intentando usar para autenticarse, mostrando que prioriza las claves SSH.

### Para gestionar el acceso con múltiples cuentas

Si necesitas usar claves SSH específicas para diferentes repositorios u organizaciones de GitHub, tienes varias opciones para tomar el control:

1. **Configurar el archivo `~/.ssh/config`**: Es la solución más robusta. Puedes definir hosts específicos con su propia clave[](https://stackoverflow.com/questions/7927750/specify-an-ssh-key-for-git-push-for-a-given-domain).
```sh
# ~/.ssh/config
# Cuenta Personal por defecto
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_personal
  IdentitiesOnly yes

# Cuenta de Trabajo
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_work
  IdentitiesOnly yes
```

Luego, en tus repositorios locales para la cuenta de trabajo, cambia la URL remota para usar el alias `github-work` en lugar de `github.com`:

```sh
git remote set-url origin git@github-work:NombreDeLaOrganizacion/repo.git
```
2. **Configurar SSH Key por Repositorio**: Para un repositorio local específico, puedes configurar un comando SSH específico[](https://stackoverflow.com/questions/7927750/specify-an-ssh-key-for-git-push-for-a-given-domain).
```sh
# Desde la raíz de tu repositorio
git config core.sshCommand "ssh -i ~/.ssh/tu_clave_especifica -o IdentitiesOnly=yes"
```
3. **Usar una variable de entorno para un comando único**: Para un caso puntual sin cambiar configuraciones permanentes[](https://stackoverflow.com/questions/7927750/specify-an-ssh-key-for-git-push-for-a-given-domain).
```sh
GIT_SSH_COMMAND='ssh -i ~/.ssh/tu_clave_especifica -o IdentitiesOnly=yes' git push
```
## Etcétera

```sh
# comndos del editor vi
# al entrar al editor vi entra en modo comando, puede moverse con las flechas en el texto y ejecutar comanddoa para:
# editar buscar reemplazar NO puede modificar el texto en modo comando, para hacerlo debera ejecutar  el comado
# i o el comando a que lo lleva a modo edicion, para salir de modo edicion preione tecla <esc>
# comandos:  comando i o comando a. si presiona el comano x por ejemplo, borra la letra en el cursor
# con el comando i entra a modo inserción
i #insertar texto en la posicion actual - entra a modo edicion
a #insertar texto despues de la posicion actual - entra  a modo edicion
esc sale de edicion a modo comando
# En modo comando:
:wq guarda y sale del archivo
:q! sale sin guardar
```
Ejemplo de Archivo: .gitignore
```sh
# Ignorar la carpeta de dependencias
node_modules/

# Ignorar archivos de entorno
.env

# Ignorar logs
*.log
npm-debug.log*

# Ignorar cache
.cache/

# Ignorar compilados
dist/
build/

```


Los siguientes comandos solo funcionan en la consola bash
```sh
#muestra el path de go
echo $GOPATH
#crea archivo con lineas desde el teclado termina con ctr d
cat > archivo 
#crea archivo con ese texto
echo "# proyectoweb2" >> readme.md 
#crea un archivo vacio, si son varios se separa por espacio
touch [opciones] [nombre archivo(s)] 
# ejemplo
touch redme.md
```
