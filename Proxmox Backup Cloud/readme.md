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


/*
A modo de práctica...
Ponle comillas dobles al texto que está en la fecha y también a la firma.
Haz tus saltos de líneas dónde estimes conveniente(usando diagonal invertida + n).
*/
string fecha= "Lunes 8 de Junio del 2020";
string saludo= "Querida Amber";
string cuerpo= "Te cuento que hoy me decidí a escribirte, y estoy bien, espero tú también lo estés. Se te extraña.";
string despedida="Desde aquí te envío muchos abrazos,";
string firma= "Yocha";

default
{
    state_entry()
    {
        llSay(0, "Toca el objeto para ver esta pequeña carta.");
    }
    touch_start(integer total_number)
    {
        llSay(0, fecha+saludo+cuerpo+despedida+firma);
    }
}
//Pueden escribirme o enviarme sus ejercicios al nombre de usuario: y0cha
