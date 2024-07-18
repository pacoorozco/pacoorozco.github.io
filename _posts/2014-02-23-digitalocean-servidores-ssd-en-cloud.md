---
title:  "DigitalOcean: Servidores SSD en cloud"
tags: [scalability, public cloud]
category: cloud computing
date:   2014-02-23 19:11:00 +0100
excerpt_separator: <!--more-->
permalink: /archivo/digitalocean-servidores-ssd-en-cloud/
---

![DigitalOcean](/assets/img/DigitalOcean.png){: .align-center}

Hace una semana vi este tweet sobre [Digital Ocean](https://www.digitalocean.com/)

> Our tutorial on setting up multiple seperate WordPress sites on a single VPS: [https://t.co/hmiwFiAOZ2](https://t.co/hmiwFiAOZ2)
>
> -- DigitalOcean (@digitalocean) February 6, 2014

Me llamó la atención y al hacer clic sobre el enlace descubrí un muy buen tutorial sobre la creación de varias instancias de WordPress sobre un mismo servidor. Pero mi sorpresa fue mayúscula cuando descubrí que se trataba de un proveedor de IaaS con el hecho diferencial de que ofrecía los servidores sobre disco SSD. **¿Crear una máquina virtual en 55 segundos?**

No tardé nada en crearme una cuenta y proveer algunos fondos para jugar con la interfaz y me puse manos a la obra con la creación de servidores. El portal es muy sencillo y amigable, sin florituras, pero con una ergonomía fuera de toda duda.

![Interfaz para la creación de una máquina virtual](/assets/img/DigitalOcean_Control_Panel_-_Creando_Droplet-2.jpg){: .align-center}

Las máquinas son realmente rápidas. Pude comprobar que **la creación de una máquina de 20 GB esta por debajo de los 45 segundos**. La cantidad de imágenes que ofrecen para la creación de las mismas seguro que cubrirán tus necesidades, **siempre y cuando no necesites un sistema operativo licenciado**: nada de RedHat o Windows.

Se han tomado muchas molestias en orientar este servicio a los desarrolladores. Su idea es que este sea un IaaS para este mercado, en el que puedan probar y desarrollar aplicaciones de forma fácil. Tienes **acceso a una API muy completa y simple**, lejos de la complejidad de CloudStack, vCloud o AWS.

Otro de los puntos muy interesantes es el [apartado de documentación](https://www.digitalocean.com/community/), el cual os recomiendo encarecidamente visitar.

![Ayuda en Digital Ocean](/assets/img/DigitalOcean_Community_DigitalOcean_-_Ayuda.jpg){: .align-center}

## Y para resumir...

Que me ha sorprendido de DigitalOcean:

- **Precio** – La oferta de VPS de DigitalOcean es realmente barata. Ofrecen un plan básico por **menos de 4 € al mes**, el cual es ideal para servidores de pruebas o desarrollo. Sus servidores, debo recordar, corren sobre SSD, el tiempo de lectura / escritura es ideal para aplicaciones con uso intensivo de bases de datos.

- **Facturación** – DigitalOcean factura por horas de uso, con un **límite de tarifa mensual**. Esto es ideal ya que puedes crear nuevas máquinas virtuales donde probar versiones de aplicación, o juegos de pruebas, en entornos limpios. El eterno problema de las pruebas asépticas. Con DigitalOcean es sencillo crear y destruir instancias (a las que llaman *«droplets«*) sin necesidad de pagar la tarifa mensual completa, con una flexibilidad, que es a la vez, poco habitual y genial.

- **Desarrollo y Administración** – DigitalOcean ofrece funcionalidades de gestión muy buenas para el desarrollo con *droplets*. **Puedes crear una máquina virtual en 55 segundos**, e instalar, o bien una versión limpia de tu sistema operativo preferido (Ubuntu, CentOS, Debian, Arch, Fedora) o una distribución prefabricada que contiene una aplicación determinada, desde un LAMP a Rails con herramientas como GitLab o Docker, además de aplicaciones como Ghost o WordPress para montar un blog. También permite la creación de una imagen o un backup de un servidor existente y usarlo para empezar un nuevo droplet, haciendo sencillo el clonado de entornos.

- **Look and Feel** – DigitalOcean ofrece un entorno de gestión muy sencillo, pero dotado de una gran ergonomía y orientación al usuario. 

- **API** – Ofrecen una API muy completa que provee todas las funcionalidades del interfaz de gestión: crear, dimensionar y eliminar droplets, gestionar imágenes y snapshots y más. Además de disponer de una herramientas para iPhone que no he podido probar, [DigitalOcean Manager](https://itunes.apple.com/app/digitalocean-manager/id633128302).

## ¿Que no me ha gustado?

Pero claro, toda prueba también es susceptible de encontrar puntos de mejora:

- **Creación de snapshots** – La realización de snapshots me ha parecido un proceso lento, que además se agrava por el hecho que para realizarlo **es necesario parar el servidor virtual** de la que haces esta instantánea. Algo nada habitual.

- **Funcionalidades avanzadas** – No ofrece funcionalidades algo más avanzadas integradas en el portal de gestión, como sería el *firewalling* o el balanceo de servicios web. Algo que he echado en falta a la hora de crear aplicaciones algo más complejas.

- **Backup** – El sistema de backup que ofrece es el de un snapshot diario de los servidores, sin embargo **no permite elegir otra periodicidad, retención u hora** a la que realizar la instantánea. Es este uno de los puntos menos flexibles del servicio.

- **Sistemas operativos** – Por otro lado, no poder de disponer de sistemas operativos basados en Windows, o incluso la imposibilidad de poder ejecutar virtual appliances es una funcionalidad que en determinados casos también se echa en falta.[/ulist]

Realmente un servicio muy interesante, fácil de usar, potente y a un precio muy competitivo pero más orientado al desarrollo y a las pruebas que no a montar sobre él entornos productivos.