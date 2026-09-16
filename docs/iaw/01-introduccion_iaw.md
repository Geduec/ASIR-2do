# Introducción

Para esta asignatura se necesita clonar una de las maquinas virtuales limpias de **Ubuntu Server**

![maquina clonada](img/01-01-maquina_clonada.png)

De la máquina clonada es importante en configuración, y ren Red, en las interfaces de red, es importante generar una dirección mac nueva en cada una de las interfaces, asi como el reenvio de puertos cambiar el puerto, y en la descripcion de la máquina virtual cambiar tambien el puerto para evitar futuras confusiones:

![cambio de mac](img/01-02-cambio_mac.png)
![cambio de puerto en el reenvío de puertos](img/01-03-cambio_puerto.png)
![cambio de puerto en la descripción](img/01-04-cambio_descripcion.png)

## Conexión y cambio de red

Se hara el cambio de red interna a adaptador puente en la máquina virtual clonada

![cambio a adaptador puente](img/01-05-cambio_adaptador_puente.png)

luego en el equipo propietario que tengais, se busca la ip anfitriona que tengamos:

En **Windows**:

```powershell
ipconfig
```

![revisar ip windows](img/01-06-revisar_ip_windows.png)

En **Linux** he hecho una pequeña modificación del comando ''ip a'' para que se vea mejor y mas cómodamente:

```bash
ip -br -c a
```

![revisar ip linux](img/01-07-revisar_ip_linux.png)

En la máquina virtual habria que cambiar la ip dentro de nuestra conexión al router, que sea distinta al equipo anfitrion y no se este usando, accedemos a netplan:

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

y se cambia la ip:

![cambiar ip de adaptador puente](img/01-08-cambiar_ip_netplan.png)

se aplica:

```bash
sudo netplan apply
ip a
```

Y se puede observar un cambio de ip:

![cambio de ip hecho](img/01-09-cambio_ip_hecho.png)

Y para asegurar una conexión exitosa se puede hacer un ping para comprobar acceso a internet:

```bash
ping 8.8.8.8
```

entonces se reinicia la máquina, una vez dentro hacemos para mayor comodidad:

```bash
ip -br -c a
```

![motrar ip](img/01-10-mostrar_ip.png)

y dentro de nuestro equipo anfitrion le hacemos ping a nuestra máquina virtual:

![hacer ping a máquina virtual](img/01-11-hacer_ping_maquina_virtual.png)

a la viceversa también funciona, en caso de que no funcione hacer ping desde la máquina virtual al equipo anfitrion puede ser que el puerto del ping este bloqueado por firewall o esté capado el ping.

Procedemos a iniciar una conexion SSH desde el equipo anfitrion:

```bash
ssh ubuntu@192.168.1.150
```

Si da fallo puede ser que se haya usado la ip anteriormente en otros entornos virtuales, recomendable cambiarla usando netplan.

Habiendo cambiado la ip, cambiamos la descripción con la nueva ip, quitamos el puerto ya que no es necesario debido a que estamos por adaptador puente:

![cambio descripcion 2](img/01-12-cambio_descripcion_2.png)

Y se tomará una instantánea del proceso realizado.

Se actualizara la máquina virtual para las proximas sesiones de instalaciones de wordpress

```bash
sudo apt update 
sudo apt upgrade
```

Continuación de la [Siguiente clase ->](./)
