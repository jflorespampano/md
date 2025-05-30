## usuario/pass

jflores/pampano


obtener la ip de windows desde wsl

```sh
cat /etc/resolv.conf | grep nameserver | awk '{print $2}'
```
da:172.31.128.1


## instalar node

Instalar Node.js en Ubuntu puede hacerse de varias maneras. Una opción es usar el administrador de versiones de Node.js (NVM), que permite instalar diferentes versiones de Node.js y cambiar entre ellas fácilmente. Para instalar NVM, primero debes descargar y ejecutar el script de instalación con el comando:

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```
Después de la instalación, cierra la sesión y vuelve a iniciarla para que los cambios surtan efecto. Luego, puedes verificar la instalación de NVM con el comando:

```sh
command -v nvm
```

Por ejemplo, para instalar la versión LTS más reciente, puedes usar:

```sh
nvm install --lts
```

Para instalar una versión específica de Node.js, puedes usar NVM con el comando:

```sh
nvm install <versión>
```

Otra opción es instalar Node.js directamente desde los repositorios de Ubuntu usando el administrador de paquetes apt. Primero, actualiza los paquetes locales:
```sh
sudo apt update
```

Para verificar la instalación, puedes usar:
```sh
node --version
```
También puedes instalar npm (el administrador de paquetes de Node.js) con:
```sh
sudo apt install npm
```