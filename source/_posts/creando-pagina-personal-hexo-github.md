---
title: Creando un sitio personal usando Hexo y Github
s: creando-pagina-personal-hexo-github
date: 2017-12-24 19:52:36
tags: [hexo, github, github-pages, git, nodejs, static-site-generator]
---

# Hexo

[Hexo](https://hexo.io/) es un generador de sitios estáticos como [Jekyll](https://jekyllrb.com/) o [Hugo](https://gohugo.io/) pero desarrollado en torno a *Node.js*. Sus únicos requerimientos son *Node.js* y *git*.

## Instalación

Para instalar [Hexo](https://hexo.io/) basta con ejecutar:

    npm i -g hexo

Una vez ejecutado este comando [Hexo](https://hexo.io/) quedará instalado globalmente. Puedes verificarlo ejecutando:

    hexo --version

## Generando un sitio

Para genera tu primer sitio usando [Hexo](https://hexo.io/) debes ejecutar:

    hexo init mi-primer-blog

Ahora puedes navegar hasta el directorio `mi-primer-blog` donde se encuentra todo lo necesario para crear tus primeros posts:

    cd mi-primer-blog

Si utilizas [Visual Studio Code](https://code.visualstudio.com/) como yo, puedes abrir el proyecto con:

    code .

## Iniciando un servidor de desarrollo

Para iniciar un servidor de desarrollo debes ejecutar el siguiente comando:

    hexo server --watch

Este comando iniciará un servidor en el puerto `4000` por lo cual puedes navegar hasta `http://localhost:4000` para ver el sitio. La opción `--watch` permite que el servidor se actualice cada vez que se realiza un cambio en el sitio. Para ver más opciones puedes revisar la documentación del comando `hexo server` [acá](https://hexo.io/docs/commands.html#server).

## Configuración del sitio

Para configurar el sitio personal basta con editar el archivo `_config.yml`. Algunos de los parametros que se pueden configurar acá son:
- title: El titulo de tu sitio.
- author: El nombre del autor del sitio.
- url: La dirección web en donde tu sitio estará hospedado. (Ej: `https://misitiopersonal.com`).
- root: Si tu sitio estará hospedado en una url como `https://misitiopersonal.com/blog` este parámetro debe ser `/blog`.
- theme: El nombre del tema a usar. Los temas se encuentran en la carpeta `themes` y puedes buscar nuevos temas en [el sitio oficial](https://hexo.io/themes/index.html) o en [Github](https://github.com/topics/hexo-theme).

## Creación de un post

Cuando se crea un sitio con el comando `hexo init` se crea un post por defecto ubicado en `source/_posts/hello-world.md`. Si no quieres este post en tu sitio simplemente tienes que eliminar el archivo.

Para crar un nuevo post basta con ejecutar el siguiente comando:

    hexo new post "Mi primer post"

Este comando creara un archivo en `source/_posts/mi-primer-post.md` con un contenido similar a:

``` markdown
---
title: Mi primer post
date: 2017-12-22 11:04:28
tags:
---
```

Para agregar contenido a tu post debes agregarlo después de `---`. Por ejemplo:

``` markdown
---
title: Mi primer post
date: 2017-12-22 11:04:28
tags:
---
# Mi primer post

Hola a todos. Este es mi primer post :).
```

Todo lo que está entre `---` se denomina `front-matter` y sirve para configurar el post. Puedes aprender más sobre `front-matter` [acá](https://hexo.io/docs/front-matter.html).

# Github Pages

## Creando el repositorio

Para hostear el sitio en Github debes crar un repositorio con un nombre especial: `{username}.github.io`. Por ejemplo, si tu `username` en Github es `octocat`, el nombre de tu repositorio debería ser `octocat.github.io`.

## Configurando el deployment

Una vez que el repositorio fue creado es necesario agregar la configuración de deployment a la configuración de [Hexo](https://hexo.io/) en el archivo `_config.yml`.

``` yaml
deploy:
  type: git
  repo: git@github.com:{username}/{username}.github.io.git
  branch: master
```

Debido a que se esta creando un sitio personal es necesario que `branch` sea `master` y no `gh-pages`.

Además de `git`, [Hexo](https://hexo.io) soporta otros tipos de deployers como `heroku`, `rsync`, `openshift`, entre otros. Puedes aprender sobre los tipos de deployers [acá](https://hexo.io/docs/deployment.html).

También es necesario modificar el campo `url` en el archivo `_config.yml`:

``` yaml
url: https://{username}.github.io
```

## Instalando el deployer

Para instalar el deployer para `git` de [Hexo](https://hexo.io) es necesario ejecutar el siguiente comando:

    npm i --save-dev hexo-deployer-git

## Realizando el deployment

Primero es necesario generar los archivos que se van a subir al repositorio en Github. Para esto es necesario ejecutar el comando:

    hexo generate

Luego para subir el sitio personal a Github basta con ejecutar el siguiente comando:

    hexo deploy

También puedes combinar los dos comandos anteriores en un solo comando:

    hexo generate --deploy

Si todo salió bien puedes visitar https://{username}.github.io para ver tu sitio personal.