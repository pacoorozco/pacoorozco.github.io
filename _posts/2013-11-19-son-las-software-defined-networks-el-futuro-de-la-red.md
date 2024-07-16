---
title:  "¿Son las software defined networks el futuro de la red?"
tags: autoservicio BYOD cloud computing NSX SDN software defined networking
date:   2013-11-19 20:14:00 +0100
excerpt_separator: <!--more-->
permalink: /archivo/son-las-software-defined-networks-el-futuro-de-la-red
---

[Software Defined Networking](https://en.wikipedia.org/wiki/Software-defined_networking) es el concepto de moda desde que VMware adquirió Nicira el [verano pasado](https://www.vmware.com/company/news/releases/vmw-nicira-07-23-12.html), algunos meses después Google anunció que estaba usando OpenFlow para [optimizar](https://www.eetimes.com/electronics-news/4371179/Google-describes-its-OpenFlow-network) su backbone interno y el término volvió a ser actualidad.

En esta entrada intentaré exponer que son y donde radica su interés, que hasta ahora, como *telecos y chico de redes* que soy, me resistía a darle cabida en mi concepción de las redes.

## ¿Pero que es SDN?

Lo primero seria intentar definir SDN en pocas palabras. Tal como os imaginareis consiste en gestionar los servicios de red mediante una capa software que los abstrae de la tecnología que hay por debajo.

Es decir los *routers, load-balancers, switches, firewalls...* pasan a ser piezas de código que interaccionan con las máquinas virtuales y los hipervisores.

Esto, normalmente, se consigue mediante dos capas o planos. Por un lado el **plano de control** (*control plane*) en el que se toman las decisiones de hacia donde se envía el tráfico, y por otro la **capa de datos** (*data plane*) que se encarga de la **conmutación de este tráfico** hasta su destino.

![Switch Control Plane](/assets/img/switch-control-data-planes.png "Fuente: bradhedlund.com") 

La gracia de este concepto es que al ser todo piezas software que nos abstraen de la tecnología que haya debajo, **permite gran flexibilidad y sobretodo automatización de las tareas relacionadas con la red**, entre los beneficios que veremos más adelante.

## Las SDN tienen menor rendimiento: ¿realidad o mito?

El precio a pagar, a priori, es un **menor rendimiento de la red**, dado que los switches y routers físicos están diseñados para realizar la conmutación mediante recursos especializados. Dicha pérdida de rendimiento se pone en duda cuando la mayoría del tráfico se establece entre máquinas virtuales (VM).

Los equipos físicos tienen una mayor velocidad de conmutación, al ser elementos diseñados específicamente para esta tarea. Sin embargo, cuando vemos el entorno virtual en su totalidad observamos algo parecido a esto.

![SDN Cisco Multiflow](/assets/img/sdn-bradhedlund-vmw-blog-nsx-cisco-nsx-cisco-traffic-flow-multi-host_v3-1024x831.png "Fuente: blogs.vmware.com") 


En la izquierda de la imagen encontramos el **funcionamiento típico sin el uso de SDN**, [NSX](https://www.vmware.com/products/nsx/) es la implementación por parte de VMware. Un usuario hace una petición a una de nuestras aplicaciones virtualizadas (en rojo), atraviesa un firewall y un balanceador, una vez atendida por el servidor web, se crea un nuevo flujo hacia el servidor de aplicaciones (en verde). Por razones de seguridad frontend y backend están en redes diferentes, protegidas por un firewall. Siguiendo el camino inverso, el usuario obtiene el resultado.

Observamos que el tráfico pasa por diferentes elementos, **entrando y saliendo del entorno virtual**.

En la derecha observamos el **funcionamiento mediante SDN**. En este ejemplo las funciones de firewall y balanceo están también virtualizadas, por lo que él tráfico entre este elemento, el servidor web y el de aplicaciones no sale de nuevo a la red física. Sino que las capas de SDN se encargan de hacerlo llegar allí donde toque. Reduciendo casi a la mitad el número de saltos.

Llevado al extremo, y quizás así se entienda mejor, si el frontend y el backend estuvieran en la misma virtualizadora. Sin SDN se producirían el mismo número de saltos, mientras que en el segundo caso el tráfico no saldría del host en cuestión, con lo que la conmutación se haría a través de la memoria.

**¿Estas seguro que esto seria más lento que el cable?** Cuando la mayoría del tráfico es entre máquinas virtualizadas esta conmutación es mucho más rápida, aún cuando intervengan diferentes hosts.

Por tanto, dado que cada vez los entornos están más virtualizados, **las SDN empiezan a competir con las redes tradicionales**, incluso en rendimiento.

## 5 beneficios de las SDN

1. **Provisión de servicios veloz y ágil**: La configuración de red puede ser tan fácil como crear las instancias de VM y su interrelación. No hay necesidad de tocar la red física y, además, es automatizable. Esto permite ofrecer servicios de red en modalidad autoservicio, de forma que los usuarios puedan satisfacer sus necesidades sin intervención del proveedor.

2. **Mejor seguridad y más granular**: Las VM han hecho de la seguridad de la red un dolor de cabeza. SDN puede proporcionar un tipo de seguridad de gran precisión para las aplicaciones, puntos finales y dispositivos BYOD que una red cableada convencional no puede. Podemos llegar a pensar en una red por cada servicio, o cliente o incluso por cada parte del servicio.

3. **Mayor disponibilidad y rendimiento**: Eliminando la intervención manual las SDN pueden reducir los errores de configuración que pueden impactar en la red. El rendimiento, como hemos tratado anteriormente, puede ser mayor en las redes tradicionales, ya que no dependeremos de la velocidad del cable en muchas de las transacciones.

4. **Ahorro en infraestructura**: Separar el routing de la conmutación de paquetes simplifica las necesidades de los equipos de red, reduciendo así los precios del hardware como routers y switches. Llevado al extremo, necesitaremos equipos muy simples (L2) que conmuten rápidamente entre los hosts, ya que las decisiones de alto nivel (L3 y superior) las realizará la propia capa de virtualización.

5. **Más eficiencia y menores gastos de operación**: El ahorro de costes que supone SDN está todavía en duda. Es todavía un entorno poco maduro, sin embargo la capacidad de automatización y de gestión integral ofrecen un margen de eficiencia enorme. Este es sin duda el punto que permite ofrecer mejores aplicaciones en el cloud.

## ¿Seguimos?

Esta claro que las SDN son la nueva revolución en el marco de la virtualización y del cloud computing. Es un concepto al que hay que prestarle atención y que será, sin duda, el nuevo ariete en la transformación de los datacenters.