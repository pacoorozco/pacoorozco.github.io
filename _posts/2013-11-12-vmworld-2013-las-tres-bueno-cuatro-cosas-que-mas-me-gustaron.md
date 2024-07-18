---
title:  "VMworld 2013: Las tres (bueno cuatro) cosas que más me gustaron"
tags: [BYOD, private cloud, SDDC, SDN, vmware]
category: cloud computing
date:   2013-11-12 10:12:00 +0100
excerpt_separator: <!--more-->
permalink: /archivo/vmworld-2013-las-tres-bueno-cuatro-cosas-que-mas-me-gustaron/
---

![Mi VMware badge](/assets/img/vmware_badge.jpg)  

Hace unos días tuve la suerte de asistir al [VMworld](https://www.vmworld.com/) 2013 en Barcelona. Este es uno de los eventos más grandes sobre virtualización de todo el mundo. **Cerca de 8000 profesionales se dan cita** durante tres días para tratar las novedades del sector.

Bajo el hashtag **#vmworld2013top3**, Kilian Arjona (@karjona) de [Ncora.tv](https://www.ncora.tv/) propuso, días después del mismo, que cada asistente al VMworld 2013 hiciera su particular **top 3 de las cosas «molonas»**, usando sus mismas palabras, que vimos o tocamos en esta conferencia.

He aquí un pequeño resumen de mis 3 propuestas (bueno, en realidad son 4):

- vSAN: Virtual SAN
- Horizon Suite
- vCloud Automation Center
- (bonus) NSX: Network Virtualization

<!--more-->

## 1. vSAN: VMware Virtual SAN

Virtualizar todos los elementos del centro de datos es el objetivo que VMware se ha fijado. Y si estáis pensando en servidores y escritorios, os quedáis cortos; la red, como veremos más adelante o el almacenamiento, como nos ocupa aquí ya son los próximos candidatos de esta cruzada.

En concreto pretenden usar el almacenamiento local de los ESXi, los discos locales de las virtualizadoras, para crear un storage distribuido, de forma que se pueda virtualizar sin necesidad de una SAN o un NAS.Los datos estás en protegidos por un RAID distribuido, donde el administrador puede definir para cada maquina virtual (VM) cuantos hosts caídos soporta. Esta definición por VM permite establecer diferentes políticas según la criticidad de los servicios que corren en ellas.

Una buena opción para entornos pequeños, entornos de desarrollo o pre-producción. Y sobretodo para entornos de laboratorio. Cabe añadir que para que esto funcione bien es necesario que cada servidor tenga, al menos, un disco SSD. Obviamente si todo el almacenamiento es SSD el rendimiento esta asegurado.

Otra ventaja, a parte de no necesitar una cabina, es que los datos están distribuidos y que por tanto no tenemos un único punto de fallo como podría ser un NAS. Sin embargo, en temas de rendimiento y coste (sobretodo con disco SSD) creo que la opción de la cabina / NAS resulta mucho más eficiente. Todo ello me parece un primer paso, puesto que ¿no seria interesante que pudiera hacer lo mismo sobre cabinas diferentes? De esta forma no tendríamos la necesidad de replicar datastores sino que este estaría distribuido en diferentes LUNs servidas por cabinas o NAS diferentes.

Más información, [aquí](http://www.vmware.com/products/virtual-san/).

## 2. Horizon Suite

![Fuente: blogs.vmware.com](/assets/img/vmware_horizon.jpg "Fuente: blogs.vmware.com")

VMware Horizon Suite es **la respuesta de VMware al BYOD y a la movilidad**. Permite trabajar desde cualquier dispositivo, personal o corporativo, con un acceso a todas las aplicaciones corporativas y con los datos que necesitemos en cualquier momento. Pero sin olvidar el control sobre accesos, aplicaciones y datos (ISO27001 dixit).

Se podrá **ofrecer Windows, Android, iOS, Web y aplicaciones SaaS en un único espacio de trabajo** y dar a los usuarios finales acceso de autoservicio a las aplicaciones y datos desde cualquier lugar.

Dicho de otra forma, el usuario tiene un portal que le facilita el acceso a las aplicaciones, las cuales puede consumir según sus gustos (BYOD). Esta es la parte **Horizon workspace**  de la suite. A ello se le suman los VDI (escritorios virtuales) con **Horizon View** y la gestión de escritorios físicos con **Horizon Mirage**. El trio resulta, cuando menos, interesante y a mi parecer es la mejor solución integrada de escritorio virtual, móvil y con soporte BYOD.
Horizon Suite = Worskpace + View +Mirage. [Más informació](http://www.vmware.com/products/horizon-suite/).

![Este es el trío que compone la suite Horizon](/assets/img/vmw-dgrm_horizn-ste-feature-pg-101-1024x768.png)

## 3. VMware vCloud Automation Center

![VMware vCAC](/assets/img/vmware_vcac.png "Fuente: blogs.vmware.com")

vCAC ofrece una **consola de gestión y un portal donde auto aprovisionar servicios**. La idea es sustituir la capa del vCloud Director, mucho más granular y completa pero también mucho más compleja, por un portal de servicios más orientado al usuario final.

El objetivo de esta herramienta es permitir la creación, la provisión, de servicios a través de clouds públicos y privados, es decir facilitando la hibridación. **vCAC puede entenderse con vSphere, vCloud Director, Hyper-V and XenServer**. Cabe recordar que vCloud Director nos permite enlazar con Amazon, por lo que el pastel esta completo.

Además ofrece un gran control sobre el gasto de estos servicios en el cloud, permitiendo por ejemplo estudiar escenarios de coste en los diferentes tipos de servicio: EC2, cloud privado…

De hecho creo que en un futuro vCAC, o similar, sustituirá a vCenter, ya no hablaremos de la creación de VMs sino que en su lugar haremos el despliegue de aplicaciones y servicios. **Una de las herramientas que más me han gustado** y que espero poder poner a prueba en UPCnet en los próximos meses.

## 4. NSX: la virtualización de la red

Y dejadme añadir una más, en la propuesta de twitter sólo se hablaba del top 3, pero días después estuve investigando NSX, **la solución de VMware para virtualizar la red**.

Una idea que me resultó muy disruptiva y, no voy a negarlo, me produjo cierto rechazo en un principio, pero que una vez reposado y analizado, me parece una muy buena solución y un rumbo al que tender.

Básicamente, y resumiendo mucho, se trata de pasar la conmutación de paquetes y las tareas de enrutamiendo de red a unas piezas software dentro de los propios ESXi. De esta forma podemos ganar algo de rendimiento (sobretodo si toda nuestra infraestructura esta virtualizada) y simplificar las tareas de aprovisionamiento de nuevas redes, ya que sólo serán piezas de código.

Esto no es nuevo, se llama *Software Defined Networking (SDN)* y hace años que vengo escuchando y leyendo sobre ello. De hecho hace un año aproximadamente probé una solución libre llamada [Open vSwitch](http://openvswitch.org/), que no iba tan lejos como lo hace ahora VMware, pero que ya presentaba un escenario similar.

Es un concepto muy rompedor y en el que tengo que profundizar mucho, pero resulta muy provocador, sobretodo porque **facilita mucho la automatización de servicios en autoservicio**.

Aquí os dejo un buen vídeo que explica en que consta esta virtualización de la red.

[http://www.youtube.com/watch?v=PciyGPCykLI](http://www.youtube.com/watch?v=PciyGPCykLI)

## En resumen

VMware tiene claro que en poco tiempo todas las características de un CPD serán controladas y definidas de forma virtual. La infraestructura que haya por debajo ya se ocupará de realizar todas las acciones necesarias vía software o bien de programar y configurar las capas inferiores para obtener los resultados demandados.

El *Software Defined Data Center (SDDC)* es **la próxima revolución**, que ya esta presente, y que cuanto más nos acerquemos a ella, más servicios podremos ofrecer en autoservicio y en cloud.

Aún a día de hoy estamos algo ligados al almacenamiento y a las redes, ya hemos dejado atrás los servidores, y viendo de lo que se habló en este VMworld 2013… estas cadenas se están rompiendo.