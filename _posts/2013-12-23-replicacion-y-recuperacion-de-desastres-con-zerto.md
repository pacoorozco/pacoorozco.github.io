---
title:  "Replicación y recuperación de desastres con Zerto"
tags: [backup, data protection]
category: cloud computing
date:   2013-12-23 19:11:00 +0100
excerpt_separator: <!--more-->
permalink: /archivo/replicacion-y-recuperacion-de-desastres-con-zerto/
---

Hace meses que tengo pendiente escribir sobre [Zerto](https://www.zerto.com/), una compañía de servicios de protección de datos especializada en infraestructuras virtuales y *cloud*.  Los vi por primera vez en el **VMworld 2012**, pero no fue hasta la última edición en Barcelona en la que les presté más atención. Desde entonces bajé una de sus demos y he estado probándolo, estos son los resultados obtenidos.

Zerto provides enterprise-class business continuity and disaster recovery (BCDR) solutions for virtualized infrastructure and cloud. Zerto Virtual Replication, is the industry’s first hypervisor-based replication solution for tier-one applications. Zerto Disaster Recovery solutions replace traditional array-based BCDR that was not built to deal with virtual environments.
{: .notice--info}

Leyendo sus propias palabras puede sonar a un producto similar al [Site Reovery Manager (SRM) de VMware](https://www.vmware.com/products/site-recovery-manager/), sin embargo la declaración anterior esta cuidadosamente redactada. SRM usa replicación de los datos basada en el almacenamiento mientras que Zerto basa su solución en el *hypervisor*. Más adelante, en este artículo, haré una comparativa de ambas soluciones, y espero que quede más claro.

## ¿Como funciona?

![Arquitectura de Zerto](/assets/img/zerto-architecture.jpg){: .align-center}
Fuente: [Gabes Virtual World](https://www.gabesvirtualworld.com/)

Zerto se integra dentro del vCenter para replicar las máquinas virtuales (VMs) a uno o múltiples entornos virtuales. De hecho permite replicar nuestras VMs hacia múltiples *clouds* públicos (siendo compatible con vCloud Director).

- Seleccionas las VM que quieres replicar en el  *VMware vSphere vCenter*, de forma muy sencilla el proceso de replicación se inicia.
- En el *host* ESXi donde residen las máquinas crea un virtual appliance (VRA), que mediante la API de VMware **monitorizará los datos que vienen del stack de entrada y salida del *hypervisor* y los replicará en un destino secundario**.
- Sólo ve los datos que vienen y van al IO stack, no afecta a la escritura de los mismos, por lo que si el virtual appliance falla, el ESXi puede serguir con su trabajo sin problema.
- El VRA se encarga de hablar con otro VRA en el host destino y se asegura de que los datos sean replicados correctamente. Aquí aplica **compresión, deduplicación y optimización** para que este proceso sea óptimo, incluso en enlaces WAN.
- Automatiza el proceso de *failover* y *failback*, incluyendo la creación de todas las máquinas necesarias, reconfigurando la red e IPs, así como ejecutando los *scripts* que sean necesarios en el destino.
- No se usa ningún *snapshot*. Zerto usa un sistema de replicación continua, de forma que no necesita *snapshots* que pueden ralentizar el entorno productivo. Continuamente monitoriza el *stack* de entrada y salida del *hypervisor* y replica los cambios.

En este vídeo de 90 segundos podéis ver un resumen de como funciona su solución y que es lo que ofrece, en su web encontraréis más vídeos al respecto.

{% include video id="25299729" provider="vimeo" %}

## ¿Y que ofrece?

Al igual que la virtualización de servidores abrió la posibilidad de abstraer el sistema operativo del hardware, la replicación puede beneficiarse de subir una capa, dejando el almacenamiento para trabajar a nivel de *hypervisor*.

Esta capa ofrece algunas **funcionalidades muy interesantes**:

- Array agnostic – podemos **replicar entre cabinas muy diferentes**, por ejemplo de una Netapp a una EMC o viceversa). Esta puede ser una de las características más interesantes. En la replicación basada en cabina se requiere que ambos sistemas, origen y destino, sean similares. De hecho gracias a esto podemos replicar incluso a disco local, sobretodo si eres un autentico seguidor del creciente [movimiento NoSAN](https://www.channelregister.co.uk/2011/10/25/storage_array_soul/).
- Storage layout agnostic – gracias a que puedes elegir las VM a replicar en vez de hacerlo por datastores / LUN en la cabina podemos eliminar restricciones a la hora de diseñar y mantener nuestro esquema de almacenamiento. Cuando replicamos podemos cambiar entre thin y thick provisioning, o de SAN a NAS. Un uso típico podría ser replicar de una fuente thick a una thin en la ubicación de contingencia por ejemplo.
- Podemos **replicar máquinas virtuales de vCloud Director (vCD) a vSphere (o viceversa)**. vCD a vCD también esta soportado. La integración con VMware permite tener información de las redes, los contenedores vApp, etcétera.
- Es además agnóstico respecto la versión de vSphere que usemos. Por ejemplo podemos usar vSphere 4.1 en un extremo y vSphere 5.0 en el otro. En algunos entornos permite lidiar con el retraso a la hora de actualizar los sistemas primario y de contingencia.

En las pruebas que he hecho algo que me ha sorprendido y gustado es la **herramienta que permite obtener una predicción del ancho de banda necesario para la replicación**, en base a los cambios que presenta la VM.

## Zerto vs VMware SRM

Como dije previamente cuando conocí Zerto pensé automáticamente en SRM y en ver que lo diferenciaba. La principal diferencia, y que a priori no parece grande, pero que una segunda reflexión si que lo es, es que SRM requiere de replicación a nivel de cabina. Esto quiere decir que origen y destino deben ser similares: mismo fabricante, mismo protocolo, mismas versiones de VMware…

Sin embargo, una vez probado creo que la comparación no es justa. Zerto trabaja a nivel de máquinas virtuales individuales, o grupos de ellas, mientras que SRM lo hace a nivel de volúmenes o LUNS. Para un entorno grande donde interese replicar muchas máquinas, SRM creo que es una alternativa mejor.

En el blog de Zerto podemos encontrar [este documento que compara ambas soluciones](https://www.zerto.com/blog/general/vsphere-replication-and-zerto-whats-the-difference/).

## Conclusión

**ATENCIÓN**: Estas conclusiones están basadas en un periodo de pruebas de dos semanas, por lo que quizás deban ser tratadas como no definitivas.
{: .notice--warning}

Creo que es una **opción fácil y sencilla para tener replicación entre dos sites**, o entre tu CPD y el cloud, siendo este el escenario más interesante. El producto esta bien acabado, resulta sencillo de usar y comprender, creo que no tiene la complejidad de SRM, y ofrece algunas funcionalidades únicas.

Sin embargo, y aquí viene el pero, **el precio de licenciamiento de Zerto es sensiblemente superior al de SRM o Veeam**, que también podría ser un competidor. Las estimaciones que he podido conseguir, sin descuentos ni negociaciones de volumen, marcan a Zerto como una alternativa 100% más cara que SRM. Claro que habría que tener en cuenta lo que nos ahorramos por no tener ambos almacenamientos idénticos.

La compatibilidad con **vCloud Director**, es sin lugar a duda el hecho más diferencial que puede hacer decantar la balanza hacia este servicio. Permitiendo tener nuestro entorno de contingencia en el cloud (*replication-as-a-service*).

¿Lo estáis usando en vuestros servicios? ¿Que estáis usando para la replicación de datos?