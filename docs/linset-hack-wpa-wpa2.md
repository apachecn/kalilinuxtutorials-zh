# Linset:用这个工具黑 WPA WPA2

> 原文：<https://kalilinuxtutorials.com/linset-hack-wpa-wpa2/>

Linset 不是一个社会工程工具。最重要的是，评论说这是一个有教育意义的任务，对我来说更接近编程和无线的世界。在任何情况下都不允许在国外无线网络中使用该工具！

## **Linset 如何工作**

1.  扫描网络并选择网络。
2.  捕获握手(可以在没有握手的情况下使用)
3.  我们从几个为我定制的网络界面中选择一个(感谢用户的合作)
4.  安装一个模仿原件的赝品
5.  在 FakeAP 上创建了 DHCP 服务器
6.  它创建一个 DNS 服务器，将所有请求重定向到主机
7.  启动具有所选接口的 web 服务器
8.  启动该机制来检查将要引入的密码的有效性
9.  它对网络的所有用户取消认证，希望连接到 FakeAP 并输入密码。
10.  密码检查正确后，攻击将停止。

必要的 tengais 安装的依赖项，Linset 检查并指示它们是否安装。

#### **也读[cred sniper——钓鱼框架写的 Python 和 jinja 2](http://kalilinuxtutorials.com/credsniper-phishing-framework/)**

## **变更日志**

```
########## 06-11-2013 LINSET 0.1
##
## #Fecha de Salida
##
########## 07-11-2013 LINSET 0.1b
##
## #Cambiado el Fakeweb a Inglés
## #Añadida funcion para quitar el modo monitor al salir
## #Arreglado Bucle para no colapsar la pantalla con información
## #Colocada opción de seleccionar otra red
## #Eliminado mensaje sobrante de iwconfig
##
########## 10-11-2013 LINSET 0.2
##
## #Añadido Changelog
## #Reestructurado el codigo
## #Cambiada la posición de ventanas xterm
## #Eliminada creacion extra del archivo route
## #Movido pantalla de comprobacion de handshake a una ventana xterm
## #Añadido menu durante el ataque
## #Añadida comprobacion de dependencias
##
########## 22-11-2013 LINSET 0.3
##
## #Arreglado mensaje de Handshake (no se mostraba bien)
## #Añadida interface de routers Telefonica y Jazztel (Xavi y Zyxel)
## #Fix cuando se usaba canales especificos (exit inesperado)
## #Mejorado DEBUG (function_clear y HOLD)
## #Migración de airbase-ng a hostapd
## #Reestructurado mas codigo
## #Añadido header
## #Añadida funcion para eliminar interfaces en modo monitor sobrantes
##
########## 30-11-2013 LINSET 0.4
##
## #Agregado soporte a airbase-ng junto a hostapd
## #Capacidad para comprobar pass sin handshake (modo Airlin"
## #Arregladas problemas con variables
## #Fix espacio Channel
## #Eliminada seleccion con multiples tarjetas de red
## #Arreglado error sintactico HTML de las interfaces Xavi
## #Implementada interface Zyxel (de routers de Telefonica también)
##
########## 07-12-2013 LINSET 0.5
##
## #Arreglado bug que impide usar mas de una interface
## #Migración de iwconfig a airmon-ng
## #Añadida interface HomeStation (Telefonica)
## #Arregladas llamadas PHP a error2.html inexistente
## #Arreglado bug que entraba en seleccion de Objetivos sin que se haya creado el CSV correspondiente
## #Opcion Salir en el menu de seleccion de webinterfaces
## #Arreglado bug que entraba en seleccion de Clientes sin que los haya
## #Arreglado bug que entraba en seleccion de Canal sin que haya interface valida seleccionada
##
########## 11-12-2013 LINSET 0.6
##
## #Bug al realizar deauth especifico sin que haya airodump en marcha
## #Modificadas variables que gestionan los CSV
## #Modificada estetica a la hora de seleccionar objetivo
## #Añadidos colores a los menus
## #Modificado funcionamiento interno de seleccion de opciones
## #Arreglado bug de variables en la comprobacion de dependencias
## #Añadida dependencia para ser root
##
########## 15-12-2013 LINSET 0.7
##
## #Añadido intro
## #Mejoradas variables de colores
## #Añadida interface de los routers Compal Broadband Networks (ONOXXXX)
## #Mejorada la gestion de la variable de Host_ENC
## #Arreglado bug que entraba en modo de FakeAP elegiendo una opcion inexistente
## #Modificado nombre de HomeStation a ADB Broadband (según su MAC)
## #Agregada licencia GPL v3
##
########## 27-12-2013 LINSET 0.8
##
## #Modificada comprobación de permisos para mostrar todo antes de salir
## #Añadida funcion para matar software que use el puerto 80
## #Agregado dhcpd a los requisitos
## #Cambiado titulo de dependecia de PHP (php5-cgi)
## #Modificado parametro deauth para PC's sin el kernel parcheado
## #Añadida funcion para matar software que use el puerto 53
## #Funcion para remontar los drivers por si se estaba usando la interface wireless
## #Modificada pantalla que comprueba el handshake (mas info) y mejoradas las variables
## #Mejorado menu de comprobacion de password con mas información
## #Añadida lista de clientes que se muestran en el menu de comprobacion de password
## #Cambiado ruta de guardado de password al $HOME
## #Reestructuracion completa del codigo para mejor compresion/busqueda
## #El intro no aparecerá si estas en modo desarrollador
## #No se cerrará el escaneo cuando se compruebe el handshake
#
## #Agregada funcion faltante a la 0.8 inicial (me lo comi sin querer)
##
########## 03-01-2014 LINSET 0.9
##
## #Funcion de limpieza si se cierra el script inesperadamente
## #Mejorada funcion de deteccion del driver
## #Modificadas variables que almacenaban las interfaces con nombres "wlan" y 'mon' para dar mas soporte a otros sistemass
## #La carpeta de trabajo se crea mas temprano para evitar posibles problemas
## #Añadida funcion para comprobar la ultima revision de LINSET
## #Autoactualizacion del script si detecta una version mas nueva de si mismo
## #Backup del script tras la actualizacion por si surgen problemas
## #Fix Menu de tipo de Desautentificacion (no se ve lo que se escribe)
## #Eliminada funcion handshakecheck del background
## #Eliminado mensaje de clientes.txt (problema devido a handcheck)
## #Bug que no mostraba correctamente los clientes conectados
##
########## 19-01-2014 LINSET 0.10
##
## #Agregado curl a las dependencias
## #Bug que no mostraba bien la lista de los clientes
## #Eliminado cuadrado en movimiento por cada sleep que se hacia en la ventana de comprobacion de handshake
## #Mejorada la comunicacion entre PHP y checkhandshake (ya no funciona por tiempos)
## #Cambiada ruta de trabajo de LINSET por defecto
## #Bug wpa_passphrase y wpa_supplicant no se cerraban tras concluir el ataque
## #Suprimidas de forma indefinida todas las interfaces web hasta ahora por motivos de copyright
## #Integrada interface web neutra basada en JQM
##
########## 29-01-2014 LINSET 0.11
##
## #Mejorada la comprobacion de actualizaciones (punto de partida desde la version del script actual)
## #Modificada url de comprobacion
## #Bug mensaje de root privilegies (seguia con el proceso)
## #Modificado orden de inicio (primero comprueba las dependencias)
## #Mejorada interface web
## #Agregada dependencia unzip
## #Bug al seleccionar una interface que no existe
## #Fix variable $privacy
## #Modificaciones leves de interface web
## #Adaptada interface para multiples idiomas
## #Añadido idioma Español
## #Añadido idioma Italiano
##
########## 18-02-2014 LINSET 0.12
##
## #Tarjetas con chipset 8187 pasaran dietctamente al menu de airbase-ng
## #Mensaje javascript adaptado según el idioma
## #Fix variable revision del backup
## #Bug en busqueda infinita de actualizaciones
## #Añadida restauracion de tput a la limpieza del script
## #Cerrar aplicaciones por medio del PID para evitar problemas
## #Añadido mdk3 a dependencias
## #Añadida desautenticacion por mdk3 al AP
## #Organizacion de codigo
## #Mejorada la busqueda de actualizaciones (casi directa)
## #Cambiada ruta de guardado del backup
##
########## 21-03-2014 LINSET 0.13
##
## #Ampliado tiempo de espera antes de detener el atque
## #Corregido bug al hacer backup
## #Añadido reinicio de NetworkManager para Wifislax 4.8
## #Desautentificacion masiva se hace exclusivamente con mdk3
## #Fallo al reiniciar networkmanager cuando acaba el ataque
## #Fix cuando se autocierra linset despues de acabar el ataque
## #Añadido pyrit a dependecias
## #Funcion de comprobacion estricta del handshake
## #Eliminadas dependencias inecesarias
## #Mayor desplazamiento por los menus
## #Añadido lenguaje Frances
## #Añadido lenguaje Portugues
##
########## 16-06-2014 LINSET 0.14
##
## #Info del estado del handshake en captura
## #Redirigido .cap para evitar salida de error de pyrit
## #Capacidad para usar handshake ya capturado previamente
## #Reconfiguradas liberias de jQuerry
## #Arreglado bug de URL's complejas
## #Desautentificar masivamente a varios MAC con igual ESSID
## #Manipaular .cap complejos para usar el handshake del objetivo
## #Invertido menu de comprobacion de handshake
##
##########
```

## ****怎么用？****

```
$ chmod +x linset
$ ./linset
```

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/vk496/linset)**