---
title:  "Netcat: la navaja suiza para linux"
tags: [backup, linux, terminal]
category: linux
date:   2013-11-18 10:07:00 +0100
excerpt_separator: <!--more-->
permalink: /archivo/netcat-la-navaja-suiza-para-linux/
---

Hace algún tiempo descubrí una herramienta llamada [netcat](https://netcat.sourceforge.net/). En muchos lugares la bautizan como **la navaja suiza** ya que este comando puede servir para mil y una tareas. En un principio la subestimé, pero poco después se ha convertido en una de mis aliadas favoritas.

El funcionamiento de netcat es muy sencillo, abre un socket TCP y envía a través de él lo que recibe por la entrada estándar (modo servidor) o viceversa, es decir, copia en la salida estándar lo que recibe por red (modo cliente).

¿Quieres ver alguno de los usos que le doy?

<!--more-->

## Conexión simple

Al más puro estilo de un telnet, netcat te permite conectarte a un puerto ofrecido por cualquier daemon del sistema.

Para iniciar una conexión hacia algún puerto en algún sistema, se utiliza seguido de una dirección IP y un puerto al cual conectarse. En el siguiente ejemplo realizo una conexión hacia el puerto 25 (SMTP) de 127.0.0.1:

```
nc 127.0.0.1 25
```

Si hay un servidor de correo funcionado, lo anterior puede devolver una salida similar a la  siguiente, donde requerirá escribir quit para cerrar la conexión:

```
220 localhost.localdomain ESMTP ; Wed, 30 Oct 2013 10:24:52 +0200
quit
221 2.0.0 localhost.localdomain closing connection
```

## Revisión de puertos

Para revisar los puertos abiertos, podemos usar la opción , `-z` para solicitar se trate de escuchar por puertos abiertos y un puerto o rango de puertos. En el siguiente ejemplo vamos a revisar cuáles puertos TCP (modo predeterminado) están abiertos dentro del rango que va del puerto 21 al puerto 25.

```
nc -vz 127.0.0.1 21-25
```

Lo anterior puede devolver una salida similar a la siguiente, si se encontrasen abiertos los puertos 21, 22 y 25.

```
Connection to 127.0.0.1 21 port [tcp/ftp] succeeded!
Connection to 127.0.0.1 22 port [tcp/ssh] succeeded!
Connection to 127.0.0.1 25 port [tcp/smtp] succeeded!
```

De manera opcional, se pueden revisar si están abiertos los puertos UDP abiertos añadiendo la opción `-u`. En el siguiente ejemplo revisamos cuáles puertos UDP se encuentran abiertos entre el rango comprendido entre los puertos 21 al 80.

```
nc -zu 127.0.0.1 21-80
Connection to 127.0.0.1 53 port [udp/domain] succeeded!
Connection to 127.0.0.1 67 port [udp/bootps] succeeded!
Connection to 127.0.0.1 68 port [udp/bootpc] succeeded!
```

## Transferencia de datos

Imagina que necesitas transferir un fichero, un directorio o una partición entera de un servidor a otro. No puedes usar ni FTP, ni SMB, ni NFS… ¿Que haces?

Los siguientes ejemplos envían un fichero, un directorio y hasta partición entera a través de la red. netcat se inicia en modo servidor (`-l`), escuchando en el puerto 12345 (`-p 12345`) y con un timeout de 10 segundos, por si no recibe nada en la entrada estándar (`-q 10`):

Un archivo:

```
cat file.txt | nc -q 10 -l -p 12345
```

Un directorio:

```
tar c directory | nc -q 10 -l -p 12345
```

Una partición entera:

```
dd if=/dev/sda1 | gzip -9 | nc -q 10 -l -p 12345
```

En el receptor deberás usar netcat para conectarse con el emisor. Usamos también un timeout (`-w 10`)

Un archivo:

```
nc -w 10 remotehost 12345 > file.txt
```

Un directorio:

```
nc -w 10 remotehost 12345 | tar -xvf -
```

Una partición entera:

```
nc -w 10 remotehost 12345 | gunzip | dd of=/dev/sda3
```

## ¿Algo más?

[warning]En todos los ejemplos los datos viajan en claro por la red, por tanto hay que tenerlo en cuenta según sea el entorno y los datos que usemos[/warning]

A partir de aquí podemos ir combinando posibilidades: comprimir los datos, guardar particiones en ficheros, hacer copias de seguridad…. da rienda a tu imaginación, juega con él y dime que uso has encontrado tú.