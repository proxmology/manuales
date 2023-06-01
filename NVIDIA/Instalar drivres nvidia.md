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

### Una vez realizados los preparativos necesarios, ya podemos instalar los drivers.
<br>

#### 1 - Primeramente necesitamos saber cual es el ultimo controlador disponible:

```
https://download.nvidia.com/XFree86/Linux-x86_64/latest.txt 
```
Cuando nos muestre el resultado, copiamos el numero y los sustituimos por “/latest.txt”

Por ejemplo así: 

```
https://download.nvidia.com/XFree86/Linux-x86_64/525.116.04/
```

Una vez dentro del directorio copiamos el enlace del instalador que termina con la extensión .run

Por ejemplo:

```
https://download.nvidia.com/XFree86/Linux-x86_64/525.116.04/NVIDIA-Linux-x86_64-525.116.04.run
```

#### 2 - Ahora empezamos con la instalación.

```
mkdir /opt/nvidia
```
```
cd /opt/nvidia
```
Descargamos el controlador que copiamos antes
```
wget https://download.nvidia.com/XFree86/Linux-x86_64/525.116.04/NVIDIA-Linux-x86_64-525.116.04.run
```
Le damos permisos de ejecución
```
chmod +x NVIDIA-Linux-x86_64-525.116.04.run
```
ejecutamos
```
./NVIDIA-Linux-x86_64-525.116.04.run --no-questions --ui=none --disable-nouveau
```
