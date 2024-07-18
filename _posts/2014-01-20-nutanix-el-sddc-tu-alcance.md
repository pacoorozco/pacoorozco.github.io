---
title:  "Nutanix: el SDDC a tu alcance"
tags: [SDDC, vmware, data protection, scalability]
category: cloud computing
date:   2014-01-20 19:11:00 +0100
excerpt_separator: <!--more-->
permalink: /archivo/nutanix-el-sddc-tu-alcance/
---

![2013 a 2014](/assets/img/BuiltForVirtualization_v2_430.jpg){: .align-center}

Es indiscutible, como voy describiendo en este blog, que la virtualización de servidores ha impulsado un cambio generalizado y fundamental. Los departamentos de TI se esfuerzan por satisfacer la creciente demanda de recursos de red y de almacenamiento necesarios para los despliegues virtualizados.

Los administradores de red deben lidiar con equipamiento y herramientas que no fueron diseñadas para la tecnología virtual y encontrar la forma de encajar las demandas de estos entornos. Los administradores de almacenamiento citan la constante demanda de espacio y la gestión de los requerimientos de un explosivo mundo virtual como uno de los principales retos a los que se enfrentan. Estos dos retos, que son el mismo pero en diferentes ámbitos, tienen un paradigma como solución: [Software Defined Data Center](/archivo/son-las-software-defined-networks-el-futuro-de-la-red/).

Es decir, tener integradas la gestión de la red y el almacenamiento con la plataforma de computación. Estas plataformas integradas ofrecen aliviar los retos anteriores combinando en una única plataforma todos los recursos.

## Una solución: Nutanix Complete Cluster

[Nutanix](https://www.nutanix.com/evolution-of-the-data-center/) es una plataforma de virtualización escalable para escritorios (VDI), servidores y despliegues de big data. Consiste en bloques modulares que integran la computación, la red y el almacenamiento en un único sistema. Este diseño esta pensado para reducir el coste de gestión mientras incrementa el rendimiento y la escalabilidad, permitiendo responder satisfactoriamente a las necesidades anteriores. Cada uno de estos bloques incluyen procesadores y almacenamiento junto a un hipervisor, del cual se muestra agnóstico, pudiendo ser Hyper-V, VMware o KVM. El cluster puede estar compuesto por tantos bloques como puedas necesitar, que serán administrados como uno sólo, mediante un sistema unificado.

![nutanix architecture](/assets/img/todoenuno-03.jpg){: .align-center}

Un bloque de 2U incluye cuatro nodos servidores que han sido creados para alojar y almacenar máquinas virtuales (VM). En cada nodo existe una máquina virtual, llamada **Controller VM** que se encarga de trabajar conjuntamente con las de otros nodos para **gestionar el almacenamiento como si fuera un único recurso**, aprovechando así las funcionalidades típicas de VMware.

![nutanix details](/assets/img/Nutanix1.png){: .align-center}

Un punto diferencial es **que cada nodo tiene una mezcla de disco SSD y discos SATA que pueden verse como un único recurso**. Podemos crear discos virtuales (vDisks) a partir de este almacenamiento y ofrecerlo como un recurso iSCSI a cualquier VM, **posibilitando vMotion sin necesidad de una SAN**.

## ¿Cómo funciona?

El sistema de ficheros propio **Nutanix Distributed File System (NDFS)** es el corazón del cluster. Asocia los discos SSD de alto rendimiento con las aplicaciones (máquinas virtuales) que mayor uso tienen frente a los discos SATA de alta capacidad, permitiendo una gestión adaptativa del almacenamiento para cada una de las aplicaciones. N**DFS actúa como una SAN avanzada que usa los recursos SSD y SATA de todos los nodos para almacenar los datos de las VMs**. NDFS es consciente de las VM que corren por encima y provee funcionalidades muy interesantes en este sentido. Por ejemplo almacenando localmente los datos de la máquina virtual en el nodo donde esta corriendo, lo cual resulta en un alto rendimiento y disponibilidad.

NDFS ofrece como pool único de almacenamiento todos los nodos del cluster, usando técnicas de striping, replicación, auto-tiering, detección de errores, failover y recuperación automática. 

Cabe decir que, para que todo esto funcione a la perfección, **los nodos deben conectarse entre ellos mediante una red de 10 Gbps** y por lo tanto es necesario un switch para tal menester. Este es uno de los puntos de mejora, haber incluido el networking para tener la solución SDDC al completo.

El cluster puede gestionarse mediante una herramienta creada a tal efecto, que permite la administración de la infraestructura de forma unificada.

## ¿Y cuanto cuesta?

**El precio mínimo, que seria para un bloque con tres nodos Nutanix NX-1050, supera los 65.000€** pero es una apuesta para quien necesita un alto rendimiento. A partir de aquí puedes crecer con otro nodo, o bien iniciar otro bloque, según su catálogo.

## ¿Qué tenemos a favor?

Por un lado la homogeneidad en lo que a computación y almacenamiento, sumado a la gestión centralizada de todo el entorno, lo cual redunda en menor coste de gestión y mantenimiento.

También cabe destacar la mayor densidad de máquinas virtuales en el mismo espacio físico que un entorno tradicional. Así como la gran funcionalidad de Plug and Play de este entorno, que hace que el crecimiento sea realmente sencillo.

La granularidad de crecimiento está en torno a los 20.000€, que es lo que cuesta un nodo. Por este dinero recibes no solo un nuevo hipervisor, sino que además incrementas el almacenamiento y la disponibilidad de los datos de las máquinas virtuales.

## ¿Y en contra?

Sin embargo, hay algunos puntos que cabe reflexionar antes de lanzarse de cabeza a estas, u otras, soluciones de todo en uno.

El uso de un protocolo propietario (NDFS), **nos obligará a que nuestro crecimiento este unido a Nutanix**. En algunos entornos puede ser interesante usar otros sistemas de ficheros distribuidos como puede ser GlusterFS o vSAN de VMware, que nos permiten tener un abanico de plataformas hardware más extenso y por tanto estar menos ligados.

También existen otras opciones para tener computación, almacenamiento y red en un único sistema que valdría la pena revisar si estáis pensando en adquirir una plataforma como esta: Dell PowerEdge VRTX, IBM Flex System o los conocidos Cisco UCS.

Sin duda, es una plataforma a tener en cuenta, ya que para entornos medianos que no quieren renunciar a una gran escalabilidad puede ser una muy buena alternativa y con un rendimiento fuera de toda duda.

Ah, y por si fuera poco, la gente de Ncora, con Josep Ros a la cabeza, son partners de Nutanix, más fácil imposible.

¿Que os parecen las soluciones todo en uno?