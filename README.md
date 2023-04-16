# Sitio web de MEGA-ACE UNAM


## Instalación y ejecución

**1**. Primero, es necesario tener una instalación funcional de Hugo (https://gohugo.io/installation/).

**2.** Desde el directorio raíz del proyecto, se ejecuta el siguiente comando:

   `hugo server -D --debug --buildFuture`

**3.** La página web estará disponible en http://localhost:1313/algorand


## Despliegue

### 1. Utilizando Netlify

Actualmente, el proyecto soporta despliegue automático con Netlify. Para implementarlo, se pueden seguir los pasos
del tutorial oficial de Hugo: https://gohugo.io/hosting-and-deployment/hosting-on-netlify/. Ya no es necesario realizar
los pasos de crear o modificar el archivo `netlify.toml`. **Nota**: Se debe modificar la baseURL presente en `config.yaml` a la utilizada.

### 2. Utilizando un servidor propio

Otra opción es desplegar el sitio web en un servidor directamente (proporcionado, por ejemplo, por un proveedor de 
servicios en la nube o alguna escuela). Actualmente, se utiliza un servidor de la Facultad de Ingeniería de la UNAM
para hostear el sitio, el cual ejecuta un servidor web (consultar detalles con los responsables).
En el directorio `.github/workflows` se encuentra el archivo `deploy.yml`, el cual define un pipeline de despliegue
continuo para que, cuando se haga un push a la rama `main`, el sitio se actualice de forma automática en vivo. En pocas palabras, la "action" se conecta al servidor, clona este repositorio, compila el sitio web, y coloca los archivos resultantes en un subdirectorio manejado por el servidor web, que se encargará de servir las páginas 
adecuadamente. Es posible modificar esta acción o incluso crear nuevas con otras funcionalidades. Para más información,
consultar la documentación de Github Actions.

Si se utiliza este método, es necesario realizar algunas configuraciones en el repositorio. Si es el 
 caso, se debe de ir al tab `Settings/Code and Automation/Actions/General`, donde se encuentran algunas configuraciones 
 importantes. Para activar el uso de Github Actions, se debe seleccionar una opción adecuada en la primera sección 
 (Actions permissions), si es que no se encuentra activado aún. `Allow all actions and reusable workflows` puede ser
 una de ellas, ya que permite la ejecución de todos los workflows presentes en el repositorio.

Por otro lado, será necesario agregar algunos "secretos" de repositorio para conectarse al servidor y no revelar los 
 datos públicamente. Para lo anterior, se debe ir al tab
 `Settings/Security/Secrets and variables/Actions/Repository secrets`, y agregar los siguientes valores:

- **PROJECT_REPO_URL**: URL del repositorio con el código actualizado de la página web.
- **PROJECT_ROOT**: Path al directorio manejado por el servidor web. Aquí se colocarán todos los archivos del sitio 
compilados.
- **SSH_IP**: Dirección IP del servidor.
- **SSH_PASSWORD**: Contraseña a utilizar en una conexión SSH al servidor.
- **SSH_USER**: Usuario a utilizar en una conexión SSH al servidor.



## ¿Cómo agregar/modificar/eliminar contenido?

En general, para modificar el contenido del sitio sólo es necesario editar los archivos apropiados de Markdown (o YAML en algunos casos). Para explorar
todas las opciones de formato que se ofrecen, es posible consultar la guía de Markdown: https://www.markdownguide.org/basic-syntax/. De igual forma, dentro del proyecto existen algunos archivos de ejemplo para ilustrar las distintas funcionalidades de Markdown.
Estos están presentes en el subdirectorio `themes/up-business-theme/hugoBasicExample/content/post`.


### Configuración

El archivo `config.yaml` contiene parámetros generales configurables sobre el sitio. Estos incluyen el título global, descripción, colores y ligas relevantes a utilizar en el header y footer. **Nota:** Es importante que los vínculos especificados coincidan con la estructura del sitio, en caso de que ésta se modifique.

### Landing page

Los archivos relacionados se encuentran en el subdirectorio `data/home`. Cada archivo YAML corresponde a las distintas secciones
de la página en cuestión. Sólo es necesario modificar el texto presente para los campos en dichos archivos, según corresponda.


### Páginas de contenido (Cursos, Nuestro Equipo, etc.)

Los archivos relacionados se encuentran en el subdirectorio `content`. Para las páginas de Contacto y Sobre Nosotros, se cuenta 
únicamente con un archivo Markdown con el contenido de cada una. Para las demás páginas, se tienen subdirectorios específicos con
el contenido. En estos subdirectorios, se tiene un archivo _index.md, donde se especifica el título de la página. De igual forma, también se encuentran presentes los archivos con las publicaciones individuales respectivas (cursos, noticias, artículos, etc.), que se puede considerar son los más importantes debido a que poseen el contenido principal. Sus posibles atributos y estructura son los siguientes:

```
+++
title = "Título principal de la entrada (nombre del artículo, persona, noticia, etc.)"

dates = "Fecha (o fechas) a mostrar, con formato libre"

date = "Fecha en formato AAAA-MM-DD, sobre la cuál se determinará el orden de los elementos en la página, del más reciente al más antiguo. Si se tiene un rango de fechas en dates, se recomienda poner la fecha de inicio"

description = "Descripción del elemento en cuestión"

link = "Link de página externa en lugar de mostrar el contenido completo (noticias/artículos)"

images = ["/images/path/a/la/imagen"]

category = "Nombre de la sección a la que pertenece este post. Por ejemplo, en Investigación puede ser Revistas"

disabledlink = "true si se desea desactivar el link de esta tarjeta. Cualquier otro texto u omitir el parámetro si se desea que el comportamiento sea el normal (mostrar el link si es que existe, o el texto presente en el documento de Markdown)"

profilephoto = "true si se desea que la imagen se muestre de forma más 'larga' verticalmente. Esto permite que las imágenes de la sección Nuestro Equipo no se vean tan cortadas, sin necesidad de deformarlas. Cualquier otro texto u omitir el parámetro si se desea que el comportamiento sea el normal (mostrar la imagen donde posiblemente se corte una
parte considerable)"

forcewidthfit = "true si se desea que la imagen se muestre de forma completa de forma horizontal en la tarjeta que la contiene, posiblemente deformando la imagen. Esto permite que algunos banners de la sección Eventos se aprecien completamente, sacrificando un poco la calidad de la imagen al deformarse. Cualquier otro texto u omitir el parámetro si se desea que el comportamiento sea el normal (mostrar la imagen donde posiblemente se corte una
parte considerable)"

noimage = "true si se desea que la tarjeta no contenga ninguna imagen, y abarque todo el espacio horizontal disponible en la pantalla. Esto permite que las referencias en la sección de Investigación se muestren en un formato apropiado, omitiendo la imagen al no ser necesaria. Cualquier otro texto u omitir el parámetro si se desea que el comportamiento sea el normal (mostrar la imagen)"
+++

Parte inicial del contenido a mostrar
Esto se mostrará como un breve resumen dentro de la tarjeta mostrada en la página de contenido...

<!--more--> (Esta línea permite delimitar dónde va a terminar el resumen, y es opcional colocarla)

Resto del contenido utilizando funcionalidades de Markdown...
```

El único parámetro obligatorio es `title`, por lo que se pueden omitir los demás de no ser necesarios.

Ejemplo:

```
+++
title = "Fundamentos de Blockchain en Algorand"
dates = "23 a 27 de enero de 2023"
date = "2023-01-23"
description = "Curso nivel licenciatura"
images = ["/images/user.png"]
+++

Taller de 15 horas para estudiantes durante el período intersemestral.
<!--more-->

Se tratarán los aspectos fundamentales del Blockchain, Algorand, y transacciones en pyteal. Se llevará a cabo del 23 al 27 de enero de 2023. 
```

Para agregar contenido a una sección, se recomienda tomar como ejemplo un documento existente en la misma, utilizando los mismos atributos que se encuentran en él (ya que usualmente no se utilizan todos en todas las secciones).

## Imágenes

Para agregar imágenes nuevas, ya sea a través del front-matter (encabezado) de un archivo Markdown (para asignar una imagen a una tarjeta) o en su contenido, es necesario colocarlas dentro del subdirectorio `themes/up-business-theme/assets/images`. Dentro de éste, es posible estructurar las imágenes en subdirectorios según convenga. Por ejemplo, se podrían colocar todas las imágenes utilizadas para la página de Cursos en un subdirectorio `cursos`. Al momento de referenciar la imagen en los archivos Markdown (en el atributo `images` del encabezado, para mostrar la imagen en la tarjeta, o bien, para mostrar la imagen dentro del contenido del archivo Markdown), es necesario especificar un path absoluto (empezando con /) con respecto al subdirectorio `themes/up-business-theme/assets`. Es decir, si quisiera utilizar una imagen colocada en el subdirectorio `cursos` mencionado, el path correcto a utilizar sería `/images/cursos/imagen.png`.

#### Nota para la sección Noticias/Artículos

La imagen a colocar para la noticia o artículo en cuestión deberá seleccionarse y descargarse de forma manual de la página que contiene el artículo, para después colocarse en el directorio `assets/images/noticias-articulos` y colocar el path correcto en el encabezado del archivo Markdown (ver ejemplos).

Es posible automatizar este proceso en un futuro, para lo cual se han considerado las siguientes opciones:

- Utilizar una API como opengraph.io para obtener la imagen de preview del sitio web en cuestión. Muchas de las opciones disponibles son pagadas.
- Realizar scraping de las imágenes del sitio a mostrar. Es decir, analizar el HTML del sitio web y buscar tags de imágenes, seleccionando la más relevante con alguna heurística (la forma en la que Twitter implementa esto es a través de tags con metadatos que indican que se trata de una imagen de preview). Sería necesario implementar un programa que realizara esta tarea (posiblemente utilizando una biblioteca como BeautifulSoup de Python) y se ejecutara en el servidor, para después guardar la imagen o el URL a ésta, y hacerla disponible en el contenido público del sitio.

#### Ejemplo de cómo agregar una imagen para una tarjeta (encabezado del archivo Markdown):

```
... atributos del front-matter
images = ["/images/noticias-articulos/felicitacion.jpg"]
forcewidthfit = "true"

+++
```

Nótese que es posible utilizar los atributos `forcewidthfit` y `profilephoto` (descritos arriba) para modificar la forma en la que se presenta la imagen.

#### Ejemplo de cómo agregar una imagen dentro de un post (contenido del archivo Markdown):

```
![Fotografía de Armando Castañeda](/images/equipo/armando-castaneda.jpg "Armando Castañeda")

{{< figure src="/images/equipo/armando-castaneda.jpg" class="centered-image" alt="Armando Castañeda" >}}
```


## ¿Cómo modificar la estructura de la página?

Para realizarlo, es necesario modificar el tema de Hugo utilizado (up-business-theme), cuyos archivos se encuentran en el subdirectorio `themes/up-business-theme`. Para más información, es posible consultar la documentación oficial de Hugo: https://gohugo.io/documentation/.

Los archivos principales con las plantillas utilizadas se encuentran en el subdirectorio `themes/up-business-theme/layouts`. Aquí se encuentran las distintas partes utilizadas para construir el sitio. Algunas de las más importantes son:

- `_default/list.html` y `_default/single.html`: Despliega la lista de tarjetas en cada página de contenido, y la vista completa del elemento en cuestión, respectivamente.

- Subdirectorio `partials/sections`: Contiene las partes que constituyen la landing page.

- Subdirectorio `partials/shared`: Contiene el footer y header.

Es posible modificar los archivos mencionados para realizar cambios en el diseño o estructura del sitio. A continuación, se presentan algunos casos particulares de cambios a realizar:


### ¿Cómo agregar/modificar/eliminar una sección de contenido del sitio? (Equipo, Investigación, etc.)

#### Crear sección

**1.** Se deberá agregar un nuevo subdirectorio en `content` con una estructura similar a las secciones existentes (es decir, con un archivo index y los archivos de contenido), así como un nombre del directorio similar al de la sección (por ejemplo, subdirectorio equipo para sección Nuestro Equipo).

**2.** Se deberán actualizar las ligas presentes en `config.yaml` y las utilizadas en la landing page, presentes en los archivos del directorio `data/home`. La liga a la sección tendrá el mismo nombre del subdirectorio de dicha sección. Ejemplo: Sección Nuestro Equipo en subdirectorio equipo. Liga adecuada: "/equipo"

#### Modificar sección

**1.** Se deberá renombrar el subdirectorio en cuestión en `content`.

**2.** Se deberán actualizar las ligas presentes en `config.yaml` y las utilizadas en la landing page, presentes en el directorio `data/home`, así como los nombres utilizados para referirse a la sección dentro de la página. La liga a la sección tendrá el mismo nombre del subdirectorio de dicha sección. Ejemplo: Sección Nuestro Equipo en subdirectorio equipo. Liga adecuada: "/equipo"

#### Eliminar sección

**1.** Se deberá eliminar el subdirectorio asociado a la sección en `content`.

**2.** Se deberán actualizar las ligas presentes en `config.yaml` y las utilizadas en la landing page, presentes en el directorio `data/home`.


### ¿Cómo agregar/modificar/eliminar campos en una tarjeta dentro de una página de contenido?

Para los archivos Markdown de contenido, será necesario agregar un nuevo campo en el front-matter (parte superior rodeada por +++). Por ejemplo:

```
+++
title = "Fundamentos de Blockchain en Algorand"
dates = "23 a 27 de enero de 2023"
date = "2023-01-23"
description = "Curso nivel licenciatura"
images = ["/images/user.png"]
+++
```

Agregando un nuevo campo (age):

```
+++
title = "Fundamentos de Blockchain en Algorand"
dates = "23 a 27 de enero de 2023"
date = "2023-01-23"
description = "Curso nivel licenciatura"
images = ["/images/user.png"]
age = "old"
+++
```

Una vez realizado lo anterior, será necesario modificar el archivo `themes/up-business-theme/layouts/_default/list.html`, modificando lo necesario en la siguiente parte del código, que se encarga de mostrar las tarjetas:

```
 {{ range $pages }}
    {{ $page := . }}
    <div class="{{ if $page.Params.noimage }}col-12{{ else }}col-12 col-md-6 col-lg-4{{ end }}">
      <a class="card text-decoration-none h-100" href="{{ if $page.Params.link }}{{ $page.Params.link }}{{ else }}{{ $page.Permalink }}{{ end }}"
      {{ if eq $page.Params.disabledlink "true" }}style="pointer-events: none"{{ end }}>

        {{ if ne $page.Params.noimage "true" }}
        <div class="aspect-ratio-62-5{{ if $page.Params.profilephoto}} profile-photo{{ end }} 
        {{ if $page.Params.forcewidthfit}} force-width-fit{{ end }}">
          
            {{ with ( partial "utilities/get-featured-image.html" $page ) }}
              {{ partial "utilities/card-img-top" . }}
            {{ end }}
          
        </div>
        {{ end }}
        <div class="card-body">
          <h5 class="card-title fw-semibold">{{ $page.Title }}</h5>
          <p class="card-text text-black-61 fw-semibold">{{ $page.Params.description }}</p>
          {{ $page.Params.dates }}
          <p class="card-text text-black-61">{{ $page.Summary | plainify }}</p>
        </div>
      </a>
    </div>
  {{ end }}
```