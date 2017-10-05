---
layout: post
title: "TV Box Tips"
date: 2017-10-02
description: Algunos trucos y consejos para sacar el máximo partido a tu TV Box.
tags:
- bricohacks
- android
- kodi
categories: 
- Bricohacks
- Tips
twitter_text: TV Box Tips
author: aaron
---

El propósito de este post es simplemente compartir algunos
trucos o recomendaciones para los que tenéis una TV Box Android o aquellos
que acaban de hacerse con una y quieren un Starter Kit. :-D
Ya que una de sus aplicaciones más extendida, si no la más, es la de hacer
de **Media Center** para reproducir Series y Películas, ver fotos,
escuchar música, navegar por Youtube, etc. A continuación os dejo algunos
 _tips_ aplicados relacionados con esto.


# [Kodi](https://kodi.tv/)
Se trata del Media Center probablemente más conocido. Tiene infinidad
de _Addons_, una comunidad muy grande y activa, y se puede instalar en
las plataformas más comunes (Windows, Linux, MacOS, Android, iOS, Raspberry...)

### [Yatse](https://yatse.tv/redmine/projects/yatse)
Una App para manejar Kodi con tu móvil, incluso pasarle videos de Youtube
cual _ChromeCast_. El mando a distancia de tu TV Box puede bastar para controlar
tu Kodi pero esta app puede ayudarte mucho cuando tengas que escribir algo y
no tengas teclado. ;-)

# [Airdroid](https://www.airdroid.com/es-es/)
Un app para manejar la interfaz de la TV Box, acceder al sistema
de archivos y un montón de utilidades más para controlar tu Android remotamente.
Se instala en la TV Box y puedes acceder a ella desde la
[interfaz web](http://web.airdroid.com/) en cualquier ordenador.

# [tTorrent](http://ttorrent.org/)
Cliente Torrent que incluye una **WebUI** para que puedas gestionar tus torrents
sin entrar directamente en la TV Box.

_Ni que decir tiene que piratear "es mal", desde aquí no animamos a ello y es total la responsabilidad del usuario que use esta app._

# [SSH Server](https://play.google.com/store/apps/details?id=com.icecoldapps.sshserver&hl=es)

Para los más Geeks, ahora viene lo bueno :-D. Un servidor SSH que te permitirá
abrir una terminal directamente al Linux Kernel del Android de tu TV Box.

Algunos comandos útiles:

```sh
# 1.- Obtener el nombre del paquete de alguna app.
pm list packages -f | grep <nombre_app>

# 2.- Obtener el nombre de la actividad principal de una app.
pm dump <nombre_packete_app> | grep -A 1 MAIN
# · <nombre_packete_app>: nombre obtenido en paso 1.

# 3.- Abrir una actividad/intent de una app.
am start <nombre_actividad>
# · <nombre_actividad>: nombre obtenido en paso 2.
# Ejemplos
am start org.xbmc.kodi/.Splash # abre Kodi
am start com.sand.airdroid/.ui.main.Main2Activity_ # abre Airdroid
# Una vez tengas este ultimo comando, no necesitas el paso 1 y 2 anymore.

# Cerrar una app
pkill -9 <nombre_app>
# Ejemplo
pkill -9 kodi
```

---

Sin más, espero que os sirva y comentéis cualquier cosa que se os ocurra o que
necesitéis en cuanto a configuraciones, dudas, etc. Saludos!