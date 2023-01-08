## Proxmox Backup Cloud

En este tutorial, vamos a configurar de manera sencilla el servicio de copias de seguridad en nuestro proveedor de almacenamiento personal en la nube, gdrive, mega, Dropbox, onedrive… añadiéndolo como un datastore mas, usando rclone en el que guardaremos nuestras copias de seguridad de manera segura y sin hacer uso de ningún script.
##
### Preparación:

Nos conectarnos por nuestro de cliente ssh preferido o desde Shell del propio proxmox y creamos un directorio nuevo en la carpeta /mnt. Le podemos poner el nombre que queramos que nos ayude a identificarlo, por ejemplo si vamos a usar google drive podemos llamarlo gdrive. Por lo que lo haríamos asi:

```
mkdir /mnt/gdrive
```

Ahora vamos a añadir ese directorio a nuestro datastore.

Lo haremos asi:

![This is an image](https://github.com/proxmology/manuales/blob/main/Proxmox%20Backup%20Cloud/imagen1.png)



A continuación indicamos el nombre gdrive, el directorio que hemos creado y en contenido elegimos Archivo VZDump.

![This is an image](https://github.com/proxmology/manuales/blob/main/Proxmox%20Backup%20Cloud/imagen2.png)


Le damos a Agregar y como vemos nos añade el nuevo directorio que hemos creado a nuestro datastore

![This is an image](https://github.com/proxmology/manuales/blob/main/Proxmox%20Backup%20Cloud/imagen3.png)

##
### Usando rclone para el montaje en nuestra nube:

Aunque el directorio llamado gdrive este en nuestro datastore, evidentemente aun no esta montado en la nube, para ello vamos a usar [rclone](https://rclone.org).

Un detalle a tener en cuenta es que rclone a cambiado la manera en que autoriza el [servicio que vincula a nuestra nube](https://rclone.org/remote_setup/). Para ello tenemos que conectarnos por nuestro cliente ssh y lanzar el siguiente código cambiando el usuario por el de proxmox que posiblemente sea root, si no lo hemos cambiado y la dirección ip que corresponda de proxmox:

```
ssh -L localhost:53682:localhost:53682 root@ip_proxmox
```
Ahora instalamos rclone:

```
apt-get update;
```

```
apt-get install rclone;
```

Seguimos los pasos. Podemos hacer uso de la [guía](https://rclone.org/docs/) de rclone de nuestra nube.

Importante: Cuando lleguemos a este punto diremos si “y” nos dará una dirección tipo localhost que al crear el vinculo con proxmox podremos abrirlo y autorizarnos.
```
Use web browser to automatically authenticate rclone with remote?
 * Say Y if the machine running rclone has a web browser you can use
 * Say N if running rclone on a (remote) machine without web browser access
If not sure try Y. If Y failed, try N.
y) Yes
n) No
y/n> y
```
Una vez tengamos configurado rclone solo falta montarlo. Podemos crear en nuestra nube personal una carpeta que llame PBC.

Para montar rclone en proxmox y vincularlo con esa carpeta, lo haremo asi:

```
rclone mount gdrive:/PBC /mnt/gdrive
```
- gdrive:/PBC es la carpeta de nuestra nube.
- /mnt/gdrive es el directiro de proxmox que añadimos a nuestro datastore.

