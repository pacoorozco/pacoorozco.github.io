---
layout: post
title:  "Presentación de VDC 2.0: el cloud de Telefónica"
tags: humor informática música programación redes
date:   2013-11-29 19:11:00 +0100
excerpt_separator: <!--more-->
permalink: /archivo/presentacion-de-vdc-2-0-el-cloud-de-telefonica/
---

![Características del VDC 2.0](/assets/img/vdc.jpg)

El pasado jueves 28 de noviembre asistí a la presentación en Barcelona de **VDC 2.0**, la nueva versión del servicio *cloud* de [Telefónica](https://www.movistar.es/empresas/virtualdatacenter). Una solución IaaS (Infrastructure as a Service) para desplegar infraestructuras software y hardware para el mundo empresas.

Telefónica comenzó su andadura en el mundo *cloud* en el año 2009, su solución Virtual Data Center (VDC) estaba basada en la suite [vCloud de VMware](https://www.vmware.com/products/vcloud-suite/) sobre la que habían diseñado **un portal de servicio propio y a medida**. Fue, a mi entender, justamente este portal el que hizo que su presentación del producto y su posterior comercialización no fueran tan bien como esperaban. El portal carecía de muchas funcionalidades, limitaba la visibilidad de la potencia de vCloud y **impedía la integración** de este servicio con el cloud privado de las empresas.

<!--more-->

De hecho creo que se dieron un gran batacazo con el servicio, lo cual propicio que cogieran distancia, observaran a su alrededor y se plantearan una nueva alternativa. Y lo que presentaron ayer es fruto de este nuevo camino escogido.

En esta nueva versión, que han denominado 2.0, han echado por la borda *«los tres años de trabajo con el portal de servicio»*, palabras textuales de [Diego López](https://www.linkedin.com/pub/diego-lopez-roman/16/189/59), Gerente de Desarrollo de negocio cloud en Telefónica. Ahora el cliente accede directamente a un portal de servicio ofrecido por vCloud en el que puede gestionar todo su centro de datos virtual.

Telefónica ofrece el servicio desde sus CPDs en Madrid y ha confiado en grandes líderes del mercado para montar su infraestructura. La computación corre a cargo de [HP](https://www.hp.com/), el storage es responsabilidad de [EMC](https://spain.emc.com/) y, por último, la red, sorprendentemente, va a cargo de [Brocade](https://www.brocade.com/). El *hipervisor* elegido es VMware y toda la suite, los **14 mil productos**, de vCloud. Con ello consiguen implementar el *Software Defined Data Center* (SDDC) del que tanto se habló en el pasado [VMworld 2013](https://pacoorozco.info/archivo/vmworld-2013-las-tres-bueno-cuatro-cosas-que-mas-me-gustaron/).

El aspecto que me resulto más interesante, y que es sin duda el hecho diferencial de esta alternativa, fue la integración que ofrece, tanto con tu entorno legacy como en el entorno de virtualización que tengas (siempre que sea VMware).

En el primer caso, gracias a las potentes soluciones en redes (VPN, macrolan, fibras ópticas, etcétera) son capaces de ofrecer el servicio dentro de tu propia red local. Como si de una sede remota o un CPD de contingencia se tratara. Tus máquinas virtuales en VDC convivirán en la misma red de nivel 2 que el resto de tu entorno. Esto simplifica mucho la adopción de esta solución y la integración con las aplicaciones ya existentes, así como la posibilidad de usarlo como centro de desborde o contingencia.

Por otro lado, dan acceso directo a la API de vCloud, de forma que es posible integrarlo fácilmente con tu entorno de virtualización o cloud privada (sólo hay que instalar un plugin vDirector). Este punto simplifica la gestión y administración. Como si de un nuevo cluster se tratara serás capaz de interaccionar con él.

No pretendo hacer una descripción exhaustiva de este servicio, que dicho sea, tiene una apariencia mucho más madura e interesante de lo que jamás tuvo VDC 1.0 anterior. Sobre el papel recoge mucho de los aspectos que podemos pedir a un proveedor de cloud público y una muy buena solución para la hibridación de nubes. **¡Pero claro está que el papel lo aguanta todo!**

PD: He buscado información en la web de Telefónica sobre este servicio y sólo he encontrado un formulario de contacto.