# Configuración de Ubuntu Server

En esta clase vamos a instalar y realizar la configuración inicial de **Ubuntu Server 24 LTS** en una máquina virtual.

## 1. Creación de la máquina virtual

Para la máquina virtual se utiliza la versión **Ubuntu Server 24 LTS** y se configura con:

| Recurso               | Configuración        |
| --------------------- | -------------------- |
| **Sistema operativo** | Ubuntu Server 24 LTS |
| **Almacenamiento**    | 25 GB                |
| **Adaptador 1**       | NAT                  |
| **Adaptador 2**       | Red interna          |

El primer adaptador se utiliza con **NAT** para que la máquina pueda acceder a Internet, mientras que el segundo se configura como **red interna** para poder comunicarse con otras máquinas virtuales de la práctica.

## 2. Instalación de SSH

Durante la instalación de Ubuntu Server se selecciona la opción para instalar **OpenSSH Server**.

Esto nos permitirá conectarnos a la máquina virtual de forma remota mediante SSH.

## 3. Actualizar el sistema

Una vez terminada la instalación, se actualizan los paquetes del sistema con:

```bash
sudo apt update
```

Con esto se actualiza la información de los repositorios y se comprueba si existen nuevos paquetes disponibles.