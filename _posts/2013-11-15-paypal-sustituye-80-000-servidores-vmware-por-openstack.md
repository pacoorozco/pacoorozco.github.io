---
layout: post
title:  "Tu cloud privado: ¿que elegir? ¿software libre o propietario?"
tags: cloudstack ESXi openstack private cloud vmware xen
date:   2013-11-12 10:12:00 +0100
excerpt_separator: <!--more-->
permalink: /archivo/paypal-sustituye-80-000-servidores-vmware-por-openstack
---

![Paypal logo](/assets/img/paypal_logo.jpg) 

En los últimos días ha vuelto a ponerse de actualidad [una noticia que apareció a principios de año](https://www.forbes.com/sites/reuvencohen/2013/03/26/paypal-to-drop-vmware-from-80000-servers-and-replace-it-with-openstack/). La noticia, de marzo de este año, anunciaba que **PayPal había decidido cambiar el rumbo de su estrategia de virtualización**, pasando de VMware a OpenStack. Un cambio nada habitual y menos sobre un parque de **80.000 servidores**.

Hay muchas compañías, entre ellas NASA y Rackspace, que han apostado sus CPD virtuales a opciones más abiertas que VMware. De hecho, esta noticia lo que hace es confirmar que **las empresas más grandes**, las que tienen un modelo de negocio basado en la estructura TI, **prefieren las soluciones más personalizadas** y optimizadas a sus aplicaciones, **sobre otras de ámbito y uso general**.

En la propia noticia se hace eco de una reflexión que comparto al cien por cien: Las soluciones libres, como [OpenStack](https://www.openstack.org/), no son gratuitas, hay que pagar el precio que supone su implementación, personalización y mantenimiento.

> In the actual world, OpenStack is not really free – one still has to pay tonnes of money to the “Consultants” who will implement & maintain the OpenStack   This is just like RedHat – which makes money from IT services and gives away Linux for free.

Soy *service manager* de un cloud privado basado en [CloudStack](https://cloudstack.apache.org/) con [Xen](https://www.citrix.com/products/xenserver/overview.html) como hipervisor. En sus inicios todo él estaba basado en soluciones libres y gratuitas, sin embargo, con el tiempo, hemos tenido que ir abordando ciertos cambios que en algunos casos nos han llevado a la adopción de plataformas de pago.

Ya en el inicio **la complejidad de estas soluciones libres nos pareció mayor que la de soluciones como VMware**, donde han cuidado la información, la integración y la formación de sus productos, obviamente esto tiene un precio asociado.

Por otro lado, en nuestra experiencia, el **rendimiento** de ESXi sobre Xen es mucho **mayor**. Hemos podido obtener más recursos virtuales a partir de los mismos recursos físicos. La estabilidad, debo admitir, que es también mayor en el primero. Y en según que entornos esto es básico.

Sin embargo, un punto que también trata la noticia, es que la adaptación que permiten las soluciones libres son una garantía de que harán exactamente lo que quieres que hagan. Es decir, puedes adaptarla a tu modelo de negocio y no al revés. Punto que suele ser el mayor origen de costes. Es aquí donde esta posibilidad, que no ofrecen las soluciones cerradas, puede convertirse en un gran peso en la adopción de las mismas: desarrollo propio, consultores, herramientas de terceros, personalización…

> There is an emerging class of technology providers—like eBay, Google and Amazon—with large-scale engineering organizations developing customized infrastructure solutions. For these companies, their infrastructure is literally their product…and they invest deeply to create solutions optimized for very specific business needs. However, this level of investment in custom solutions is typically not cost effective for most businesses. The commercially supported solutions that serve these customers make the bulk of the market. There is a ton of innovation in this market, which VMware is privileged to serve. Our relationship with eBay and PayPal is a partnership we’re proud of, and a great example of the role VMware plays in both typical customer environments and in a bleeding-edge cloud development initiative.
>
> -- Bogomil Balkansky, Senior Vice President VMware Cloud Infrastructure Platform

Estas palabras del Bogomil Balkanksky, que intenta desesperadamente explicar porqué PayPal convierte 80.000 servidores VMware en OpenStack, no me parecen faltas de sentido. **Con soluciones abiertas puedes obtener plataformas óptimas a tu negocio, sin embargo dicha adaptación no estará exenta de costes**. Y es ahí donde está el compromiso.

¿Necesitas un entorno muy personalizable, altamente adaptable, optimizado para tu negocio o puedes vivir con un paquete de virtualización orientado al propósito general? Para responder a esta pregunta hay que tener en cuenta que conseguir lo primero, la optimización, tiene un coste asociado muy elevado, ya que deberás modificar tus aplicaciones, tu código y adaptarlo para que aproveche las características de la plataforma que has elegido, la cual deberás conocer perfectamente. ¿O bien puedes permitirte ese margen de aprovechamiento a cambio de tener algo más estándar?

La decisión es tuya… en UPCnet al final tenemos los dos modelos. Un amplio entorno de virtualización basado en VMware y un servicio de cloud privado con CloudStack, Xen y VMware. **Seguramente, en la mezcla está el éxito**.