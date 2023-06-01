# Instalar drivers de tarjeta grafica nvidia en promox
Antes de empezar quiero agradecer al compañero @juanlu13 por promocionarme la [fuente original](https://forums.plex.tv/t/plex-hw-acceleration-in-lxc-container-anyone-with-success/219289/34?utm_source=pocket_mylist) de la cual se basa este manual. 
#

Primeramente actualizamos los paquetes y promox

```
apt update && apt dist-upgrade -y
```

Después instalamos dos paquetes que necesitaremos uno es git y otro los encabezados del kernel para poder instalar los drivers:

```
apt-get install git
```
```
apt-get install -qqy pve-headers-`uname -r` gcc make 
```
<br>

#### Una vez realizados los preparativos necesarios, ya podemos instalar los drivers.
<br>

Primera mente necesitamos saber cual es el ultimo controlador disponible:

```
https://download.nvidia.com/XFree86/Linux-x86_64/latest.txt 
```
Cuando nos muestre el resultado, copiamos el numero y los sustituimos por “/latest.txt”

Por ejemplo así: https://download.nvidia.com/XFree86/Linux-x86_64/525.116.04/
(https://forums.plex.tv/t/plex-hw-acceleration-in-lxc-container-anyone-with-success/219289/34?utm_source=pocket_mylist)


![This is an image](imagenes/nvidia1.png)


Y nos instalamos el paquete NVIDIA Runtime Library

![This is an image](imagenes/nvidia2.png)

##
### Parchamos el controlador:

Una vez instalado reiniciamos nuestro Nas. Cuando reinicie nos conectamos por SSH y no logueamos como root

```
sudo -i
```
Una vez como root copiamos y pegamos esto:
```
cd /var/packages/NVIDIARuntimeLibrary/conf && mv -f privilege.bak privilege
```

```
cd /var/packages/NVIDIARuntimeLibrary/scripts && ./start-stop-status start
```

Comp
