---
title: Home
permalink: /
---

= Antora

[cols="l,r"]
|===
a| A la hora de crear un portal siempre nos encontramos con los
mismos problemas: la gestión de permisos, la "caducidad" de la plataforma,
el formato de la documentación, la gestión manual de la documentación,
uniformidad de los estilos en todos los portales, transformación entre
diferentes formatos, ...

Antora es un generador de portales a partir de AsciiDoc, lo cual se suma a la
facilidad que tiene para transformarse en varios formatos como epub, pdf o html.
a| image::./antora-gitlab.png[antora-gitlab]

|===

== Tendencias

Desde hace unos años podemos ver como diferentes empresas desarrollan su
documentación usando un lenguaje de marcado organizado en repositorios:

* RedHat en link:https://docs.openshift.com/container-platform/3.11/welcome/index.html[OpenShift]
  usa link:https://github.com/openshift/openshift-docs/blob/master/welcome/index.adoc[AsciiDoc].
* Google en link:https://kubernetes.io/docs/tutorials/hello-minikube/[Kubernetes]
  usa link:https://github.com/kubernetes/website/blob/master/content/en/docs/tutorials/hello-minikube.md[Markdown].
* ArangoDB en link:https://docs.arangodb.com/3.4/Manual/index.html[ArangoDB]
  usa link:https://github.com/arangodb/arangodb/blob/3.4/Documentation/Books/Manual/README.md[Markdown].
* Debian en link:https://www.debian.org/doc/ddp[su página de documentación]
  usa link:https://salsa.debian.org/ddp-team[docbook].
* High Fidelity en link:https://docs.highfidelity.com/[su página de documentación]
  usa link:https://github.com/highfidelity/hifi-docs-grav-content/blob/master/01.home/docs.md[Markdown].
* Pivotal en link:https://docs.spring.io/spring-boot/docs/2.2.0.M1/reference/html/spring-boot-features.html#boot-features-spring-application[Spring]
  usa link:https://github.com/spring-projects/spring-boot/blob/master/spring-boot-project/spring-boot-docs/src/main/asciidoc/spring-boot-features.adoc[AsciiDoc].
* Microsoft en link:https://docs.microsoft.com/en-us/azure/mysql/overview[Azure]
  usa link:https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/mysql/overview.md[Markdown].

== Soporte

Existen plugins de AsciiDoc para los CMS más populares como pueden ser
link:https://wordpress.org/plugins/tags/asciidoc/[Wordpress] o
link:https://www.drupal.org/project/asciidoc[Drupal]. Y lo mismo con Markdown.

También tenemos plugins para los principales IDEs que permiten ver en tiempo
real el resultado de tu trabajo:
|===
| Github Atom | Microsoft Visual Studio Code

a| image::./atom_render_320w.png[Atom]
a| image::./code_render_320w.png[Code]
|===

Y por supuesto, tal como has podido ver pinchando en los enlaces de tendencias,
están soportados de caja en cualquier servicio de git que ofrezca una mínima
funcionalidad como
link:https://guides.github.com/features/mastering-markdown/[Github] o
link:https://docs.gitlab.com/ee/user/markdown.html[Gitlab].

== Sintaxis de lenguajes de marcado

Hay unos que se caracterizan por ser más fáciles y otros más difíciles pero con
más funcionalidad.

Por ejemplo, para poner énfasis en algo tenemos lo siguiente:

|===
| Markdown | AsciiDoc | DocBook
z| texto en * \*negrita* *

a| texto en \*negrita*

a| texto en <emphasis>negrita</emphasis>
|===

Resumir toda una sintaxis en tres líneas es muy difícil pero esto nos da una
idea de que Markdown y AsciiDoc pueden llegar a parecerse en cuanto a
simplicidad mientras DocBook, al usar xml, puede ser más tedioso.

La tendencia ha sido simplificar todo lo posible la edición manteniendo toda la
funcionalidad necesaria y lo más usado suele ser Markdown o AsciiDoc.
Por supuesto que existen otros formatos como Doxygen, que son perfectamente
válidos, pero parece que el mercado tiende a Markdown o AsciiDoc dependiendo
del uso.

== ¿Markdown o AsciiDoc?

Si queremos un documento que al mostrarse por la web tenga enlaces a otros
documentos pero al generarse el PDF se incrusten, deberemos poner en AsciiDoc:

[source]
----
\ifdef::env-gitlab,env-github,env-browser[]
Secciones:

* link:./arquitectura/arquitectura.adoc[Arquitectura]
* link:./infraestructura/infraestructura.adoc[Infraestructura]

\endif::[]


\ifdef::ebook-format-kf8,backend-pdf[]

\include::./arquitectura/arquitectura.adoc[]
\include::./infraestructura/infraestructura.adoc[]

\endif::[]
----

Si quieres hacerlo en Markdown, no podrás.

AsciiDoc tiene bastantes funcionalidades que Markdown no tiene y su uso es casi
igual de fácil.

En Markdown ha habido intentos de incluir funcionalidad que en AsciiDoc viene
de caja pero han desembocado en distintas implementaciones que pueden funcionar
o no dependiendo del servicio que utilices.
Por ejemplo, la implementación de
link:https://docs.gitlab.com/ee/user/markdown.html[Gitlab] es distinta a la de
link:https://guides.github.com/features/mastering-markdown/[Github], lo que
supone un problema en cuanto a portabilidad.

== Renderizando, ando

Vamos a renderizar este documento a diferentes formatos a partir de este
link:https://github.com/elmanytas/antora-examples/modules/ROOT/antora.adoc[archivo],
como son:

* *html*: `docker run -it -v $(pwd):/documents/ asciidoctor/docker-asciidoctor asciidoctor antora.adoc`
* *pdf*: `docker run -it -v $(pwd):/documents/ asciidoctor/docker-asciidoctor asciidoctor-pdf antora.adoc`

Para renderizar un documento hemos usamos la imagen de docker que la
organización mantiene en dockerhub:
link:https://hub.docker.com/r/asciidoctor/docker-asciidoctor[docker-asciidoctor].

== Creando un portal

Podría subir los html estáticos a un servidor y ya tendría mi portal, pero
existen frameworks que permiten generar portales fácilmente
tomando como fuentes uno o varios repositorios.

En la link:https://en.wikipedia.org/wiki/AsciiDoc[wikipedia] nos encontramos
con tres frameworks cuyas pruebas me han hecho llegar a las siguientes
conclusiones:

* link:http://awestruct.org/[AweStrut] permite crear portales pero parece estar
discontinuado
* link:http://asciibinder.org/[AsciiBinder] está en uso productivo para hacer el
  link:https://docs.openshift.com/[portal de OpenShift] pero da la sensación de
  ser discontinuado y cuando
  link:https://github.com/redhataccess/ascii_binder/issues/147[pregunté en github]
  me redirigieron al siguiente.
* link:https://antora.org/[Antora] tiene una comunidad muy activa y parece la
  opción correcta.

== Antora

link:https://antora.org/[Antora] permite la creación de un portal a partir de
un playbook en formato yaml donde se definen todos los repositorios que lo
forman.

De esta forma podemos tener diferentes repositorios para sistemas, seguridad,
desarrollo, ... y Antora se encargará de juntarlos todos en un solo portal al
que aplicará los mismos estilos. Cada uno de esos repositorios es un
"componente" del portal para Antora.

En cada repositorio (componente) necesitamos crear un archivo llamado
`antora.yml` donde definiremos las secciones que formarán este componente.
Cada una de esas secciones es un "módulo" para Antora.

Si el repositorio tiene varias ramas nos puede crear una versión del componente
por cada una de ellas.

== Un ejemplo de Antora

Por suerte la link:https://docs.antora.org/[documentación oficial] es realmente
clara en este aspecto pero voy a intentar simplificarla más.

Clona el siguiente repositorio:
----
git clone https://gitlab.com/antora/demo/demo-site
----

Dentro del repositorio verás el playbook `site.yml` con este contenido:
----
site:
  title: Antora Demo Site
  # the 404 page and sitemap files only get generated when the url property is set
  url: https://example.org/docs
  start_page: component-b::index.adoc
content:
  sources:
  - url: https://gitlab.com/antora/demo/demo-component-a.git
    branches: master
  - url: https://gitlab.com/antora/demo/demo-component-b.git
    branches: [v2.0, v1.0]
    start_path: docs
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/master/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
----

Este archivo indica a antora que la raíz del portal (site.start_page) será el
archivo index.adoc del componente b.

Además irá a los dos `content.sources` y generará sus html con la versión
`master` para el primero mientras para el segundo generará las versiones `v2.0`
y `v1.0` partiendo del directorio `docs`.

link:https://docs.antora.org/antora/2.0/antora-container/#docker-image-for-antora[Ejecuta esto]
para generar los estáticos:
----
docker run -u $UID --privileged -v `pwd`:/antora --rm -t antora/antora site.yml
----

Tu portal ahora se encuentran en `build/site/index.html`

== Cambios para construir un portal

Imagina que tienes un archivo en AsciiDoc llamado `index.adoc` y quieres cambiar
la estructura para tener un portal y todo en la rama antora de un único
repositorio ubicado en https://github.com/paradigmadigital/antora:

* mueve `index.adoc` a `modules/ROOT/pages/index.adoc`.
* crea un `modules/ROOT/nav.adoc` con el contenido de la barra de navegación:
+
[source]
----
xref:index.adoc[Sistemas]
----
* crea un `antora.yml` con este contenido en la raíz del repositorio:
+
[source]
----
name: antora
title: antora
version: antora
nav:
- modules/ROOT/nav.adoc
----
* crea un `site.yml` con el siguiente contenido en la raíz del repositorio:
+
[source]
----
site:
  title: Post de Antora
  # the 404 page and sitemap files only get generated when the url property is set
  url: http://antora.osapps.paradigmadigital.com
  start_page: antora::index.adoc
content:
  sources:
  - url: https://github.com/paradigmadigital/antora.git
    branches: antora
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/master/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
----

A partir de este momento puedes trabajar tal como lo hacías antes en
`modules/ROOT/pages/` y todo lo que hagas aparecerá en tu portal.

== Desplegando en OpenShift

Para desplegar el contenido de este post en tu OpenShift puedes ejecutar esto:
[source]
----
oc new-app https://raw.githubusercontent.com/elmanytas/openshift-antora-template/master/openshift-antora-template.yaml
----


== Otros enlaces interesantes

* https://fedoramagazine.org/using-antora-for-your-open-source-documentation/
* http://www.lordofthejars.com/2018/11/continuous-documentation-with-antora.html

