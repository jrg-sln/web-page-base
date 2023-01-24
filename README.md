# Sitio web de MEGA-ACE UNAM


## Instalación y ejecución

**1**. Primero, es necesario tener una instalación funcional de Hugo (https://gohugo.io/installation/).

**2.** Desde el directorio raíz del proyecto, se ejecuta el siguiente comando:

   `hugo server -D --debug --buildFuture`

**3.** La página web estará disponible en http://localhost:1313/


## Despliegue

Actualmente, el proyecto soporta despliegue automático con Netlify. Para implementarlo, se pueden seguir los pasos
del tutorial oficial de Hugo: https://gohugo.io/hosting-and-deployment/hosting-on-netlify/. Ya no es necesario realizar
los pasos de crear o modificar el archivo `netlify.toml`. **Nota**: Se debe modificar la baseURL presente en `config.yaml` a la utilizada.


## ¿Cómo agregar/modificar/eliminar contenido?

En general, para modificar el contenido del sitio sólo es necesario editar los archivos apropiados de Markdown (o YAML en algunos casos). Para explorar
todas las opciones de formato que se ofrecen, es posible consultar la guía de Markdown: https://www.markdownguide.org/basic-syntax/. De igual forma, dentro del proyecto existen algunos archivos de ejemplo para ilustrar las distintas posibilidades.
Estos están presentes en el subdirectorio `themes/up-business-theme/hugoBasicExample/content/post`.


### Configuración

El archivo `config.yaml` contiene parámetros generales configurables sobre el sitio. Estos incluyen el título global, descripción, colores y ligas relevantes a utilizar en el header y footer. **Nota:** Es importante que los vínculos especificados coincidan con la estructura del sitio, en caso de que ésta se modifique.

### Landing page

Los archivos relacionados se encuentran en el subdirectorio `data/home`. Cada archivo YAML corresponde a las distintas secciones
de la página en cuestión. Sólo es necesario modificar el texto presente para los campos en dichos archivos, según corresponda.


### Páginas de contenido (Cursos, Nuestro Equipo, etc.)

Los archivos relacionados se encuentran en el subdirectorio `content`. Para las páginas de Contacto y Sobre Nosotros, se cuenta 
únicamente con un archivo Markdown con el contenido de cada una. Para las demás páginas, se tienen subdirectorios específicos con
el contenido. En estos subdirectorios, se tiene un archivo _index.md, donde se especifica el título de la página. Además, también se encuentran presentes los archivos con las publicaciones individuales respectivas (cursos, noticias, artículos, etc.), cuya estructura es la siguiente:

```
+++
title = "Título principal de la entrada (nombre del artículo, persona, noticia, etc.)"
dates = "Fecha (o fechas) a mostrar, con formato libre"
date = "Fecha en formato AAAA-MM-DD, sobre la cuál se determinará el orden de los elementos en la página, del más reciente al más antiguo. Si se tiene un rango de fechas en dates, se recomienda poner la fecha de inicio"
description = "Descripción del elemento en cuestión"
images = ["/images/path/a/la/imagen"]
+++

Parte inicial del contenido a mostrar
Esto se mostrará como un breve resumen dentro de la tarjeta mostrada en la página de contenido...

<!--more--> (Esta línea permite delimitar dónde va a terminar el resumen, y es opcional colocarla)

Resto del contenido...
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

## Imágenes

Para agregar imágenes nuevas, es necesario colocarlas dentro del subdirectorio `themes/up-business-theme/assets/images`. Dentro de éste, es posible estructurar las imágenes en subdirectorios según convenga. Por ejemplo, se podrían colocar todas las imágenes utilizadas para la página de Cursos en un subdirectorio `cursos`. Al momento de utilizar la imagen en los archivos Markdown, es necesario especificar un path absoluto (empezando con /) con respecto al subdirectorio `themes/up-business-theme/assets`. Es decir, si quisiera utilizar una imagen colocada en el subdirectorio `cursos` mencionado, el path correcto a utilizar sería `/images/cursos/imagen.png`.



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
 {{ range (.Paginate .RegularPages).Pages }}
        <div class="col-12 col-md-6 col-lg-4">
          <a class="card text-decoration-none h-100" href="{{ if .Params.link }}{{ .Params.link }}{{ else }}{{ .Permalink }}{{ end }}">
            <div class="aspect-ratio-62-5">
              {{ with ( partial "utilities/get-featured-image.html" . ) }}
                {{ partial "utilities/card-img-top" . }}
              {{ end }}
            </div>
            <div class="card-body">
              <h5 class="card-title fw-semibold">{{ .Title }}</h5>
              <p class="card-text text-black-61 fw-semibold">{{ .Params.description }}</p>
              {{ .Params.dates }}
              <p class="card-text text-black-61">{{ .Summary | plainify }}</p>
            </div>
          </a>
        </div>
```