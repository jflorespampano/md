---
categoría: herramientas
tipo: bash
tags:
  - git
---

## Git Token


>[!note] Nota
>Útil Cuando tu sistema esta configurado con otro usuario


Los **tokens de Git** (más precisamente llamados **Tokens de Acceso Personal**) son una forma segura de autenticarte con plataformas como GitHub desde la línea de comandos o cuando usas APIs. Fueron introducidos como una alternativa más segura al uso de contraseñas, que GitHub dejó de soportar para operaciones de línea de comandos en 2021.

Un token de Git es una cadena de caracteres que actúa como sustituto de tu contraseña. Sus ventajas clave son:

- **Seguridad mejorada**: Los tokens pueden tener permisos específicos, caducar después de un tiempo y revocarse individualmente, lo que los hace más seguros que una contraseña estática.
    
- **Control granular de acceso**: Puedes definir exactamente lo que cada token puede hacer (ej: acceder solo a ciertos repositorios, solo leer datos, o también escribir código).
    
- **Obligatorios para operaciones Git**: En servicios como GitHub, usar un token es obligatorio para autenticar operaciones Git sobre HTTPS.

### Crear un token

El proceso para crear un token es similar en todas las plataformas. Estos son los pasos para GitHub:

1. **Ir a configuración de tokens**: Ve a tu **Settings** de GitHub, luego busca **Developer settings** y haz clic en **Personal access tokens**.
2. **Generar nuevo token**: Haz clic en **Generate new token**.
3. **Configurar el token**:
    - **Nombre del token**: Usa un nombre descriptivo para recordar su propósito.
    - **Expiración**: Establece una fecha de caducidad para mayor seguridad.
    - **Acceso a repositorios**: Elige qué repositorios puede acceder el token.
    - **Permisos (Scopes)**: Selecciona los permisos específicos requeridos. Para operaciones básicas de Git (clone, push, pull), el scope **"repo"** suele ser suficiente.
4. **Guardar el token**: Después de hacer clic en **Generate token**, **copia el token inmediatamente y guárdalo en un lugar seguro**. No podrás verlo nuevamente.
    

### Usar el token

```sh
git clone https://github.com/usuario/repositorio.git
# Cuando te pida nombre de usuario y contraseña, usa tu token como contraseña.
```

Alternativamente, puedes incluir el token directamente en la URL:

```sh
git clone https://<TU_USUARIO>:<TU_TOKEN>@github.com/usuario/repositorio.git
```

Para evitar ingresar el token repetidamente, puedes almacenarlo en caché usando el ayudante de credenciales de Git:

```sh
git config --global credential.helper cache
# Por defecto, almacena en caché por 15 minutos. Puedes establecer un tiempo mayor (en segundos):
git config --global credential.helper 'cache --timeout=3600'
```

## Alternativas a los tokens

Para muchos casos de uso, existen alternativas más convenientes:

- **SSH**: Para operaciones Git, las claves SSH son una excelente alternativa y no requieren ingresar credenciales frecuentemente.
- **GitHub CLI (`gh`)**: Proporciona un flujo de autenticación integrado y es más fácil de usar.
- **Git Credential Manager**: Maneja automáticamente la autenticación en diferentes sistemas operativos.

Los tokens de Git son esenciales para el desarrollo moderno y proporcionan un control de acceso mucho más seguro y granular que las contraseñas tradicionales.
### Ejemplo Crear el token tradicional:
1. ve a tu perfil (en tu fotografía) y selecciona setings (engrane)
2. en la barra izquierda ve a la opción (developer setings)
3. selecciona token de acceso personal (personal acces token)
4. Elige tipo de token (tokens clasic)
5. en el botón "Genera new token" selecciona elije (Generate new token clasic)
6. llena los siguientes datos
	1. en "Note" indica con un texto para que sirve este token
	2. selecciona la fecha de expiración
	3. En "select scopes" (marca la casilla "repo")
7. Da clic en el botón "Genera token" token
8. Copia tu token y guárdalo por que no lo volverás a ver

>[!Note] Marcar casilla  repo
>Control total sobre repositorios públicos y privados (código, commits, webhooks, etc.)

## Clonar con token
```sh
git clone https://<TU_USUARIO>:<TU_TOKEN>@github.com/nombreusuario/repositorio.git
#ejemplo
git clone https://jfloreshotmail:mitiken@github.com/jfloreshotmail/miRepo.git

#crear origin con token
git remote add origin https://<TU_TOKEN>@github.com/<USUARIO>/<REPOSITORIO>.git
#ejemplo
git remote add origin https://mitoken@github.com/jfloreshotmail/miRepo.git

```

