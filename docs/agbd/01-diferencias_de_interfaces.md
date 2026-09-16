# DIFERENCIAS DE INTERFACES EN VIRTUALIZACIÓN

## Tipos de interfaces de red en VirtualBox

### Adaptador puente

El adaptador puente conecta la máquina virtual directamente a la red física a la que está conectado el equipo anfitrión.

La máquina virtual obtiene una dirección IP de la misma red que el equipo anfitrión y se comporta prácticamente como otro dispositivo físico de la red.

¿Para qué sirve?

Hacer que la máquina virtual sea accesible desde otros dispositivos de la red.
Montar laboratorios de servidores.
Probar redes donde las máquinas virtuales necesitan comunicarse con otros equipos físicos.
Simular que la máquina virtual es un ordenador independiente conectado al router.

Ejemplo:

Router:        192.168.1.1
PC anfitrión:  192.168.1.20
Máquina VM:    192.168.1.21

### NAT

NAT (Network Address Translation) permite que la máquina virtual acceda a Internet utilizando la conexión de red del equipo anfitrión.

VirtualBox crea una red privada para la máquina virtual y traduce sus conexiones para salir a través del equipo anfitrión.

¿Para qué sirve?

Dar Internet a una máquina virtual de forma sencilla.
Es el modo más fácil de configurar.
Mantener la máquina virtual relativamente aislada de la red local.

Ejemplo:

Internet
   │
Router
   │
PC anfitrión
   │
VirtualBox NAT
   │
Máquina VM

### Red interna

La red interna permite conectar varias máquinas virtuales entre sí mediante una red privada creada por VirtualBox.

Las máquinas virtuales pueden comunicarse entre ellas, pero no tienen acceso directo a Internet ni a la red física del anfitrión.

¿Para qué sirve?

Crear laboratorios de redes aislados.
Practicar con servidores y clientes.
Simular una red empresarial.
Hacer pruebas sin afectar a la red real.

Ejemplo:

VM-Servidor ─── Red interna ─── VM-Cliente

### Red NAT

La red NAT (NAT Network) es similar al NAT, pero permite que varias máquinas virtuales estén dentro de la misma red privada y se comuniquen entre ellas, además de tener acceso a Internet.

Es especialmente útil para crear laboratorios con varias máquinas.

¿Para qué sirve?

Conectar varias máquinas virtuales.
Permitir comunicación entre ellas.
Dar acceso a Internet a las máquinas virtuales.
Crear laboratorios de servidores y clientes.

Ejemplo:

                  Internet
                     │
                  NAT Network
                ┌────┴────┐
                │         │
          VM-Servidor  VM-Cliente
          10.0.2.10    10.0.2.11
Tabla comparativa

Puedes copiar directamente esta tabla en tu Markdown:

| Modo de red | Definición | Comunicación entre VM | Acceso a Internet | Acceso desde la red física | Uso principal |
|---|---|---:|---:|---:|---|
| **Adaptador puente** | Conecta la VM directamente a la red física del anfitrión. | ✅ | ✅ | ✅ | Simular un equipo físico dentro de la red |
| **NAT** | La VM utiliza la conexión del anfitrión mediante traducción de direcciones. | ❌* | ✅ | ❌* | Dar Internet a una VM de forma sencilla |
| **Red interna** | Crea una red privada exclusivamente entre máquinas virtuales. | ✅ | ❌ | ❌ | Crear laboratorios de red aislados |
| **Red NAT** | Crea una red privada entre varias VM con acceso a Internet mediante NAT. | ✅ | ✅ | ❌* | Laboratorios con varias VM y acceso a Internet |

* Hay configuraciones adicionales que pueden modificar este comportamiento, como port forwarding, adaptadores adicionales o configuraciones específicas de VirtualBox.

Resumen rápido
Adaptador puente → VM = otro equipo de la red física
NAT              → VM → Internet a través del anfitrión
Red interna      → VM ↔ VM, red totalmente aislada
Red NAT          → VM ↔ VM + Internet

Continuación de la [Siguiente clase ->](./)