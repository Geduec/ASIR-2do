# Vulnerabilidades Ubuntu

Clase anterior [Clase 2](02-entendimiento_seguridad.md)

## Clasificación de amenazas

Las amenazas se pueden clasificar según diferentes criterios:

| Criterio          | Tipo de amenaza | Ejemplos                                                |
| ----------------- | --------------- | ------------------------------------------------------- |
| Por su naturaleza | Física          | Incendios, inundaciones, cortes eléctricos              |
| Por su naturaleza | Lógica          | Malware, vulnerabilidades, ataques de red               |
| Por su origen     | Externa         | Ataques desde Internet                                  |
| Por su origen     | Interna         | Un usuario de la organización con acceso a los sistemas |
| Por la intención  | Accidental      | Borrado accidental de datos                             |
| Por la intención  | Deliberada      | Robo, sabotaje, malware                                 |

### Caso práctico: matriz de riesgo

**Entorno:**

* Servidor Ubuntu con una base de datos.
* 5 PCs con Windows 11.

**Hallazgos de auditoría:**

* Servidor en una habitación accesible y sin SAI.
* Servicio SSH desactualizado en el servidor.
* Base de datos sin copias de seguridad externas.
* PCs Windows con las actualizaciones automáticas desactivadas.

| Activo           | Vulnerabilidad                       | Amenaza                              | Tipo de amenaza | Probabilidad | Impacto | Riesgo |
| ---------------- | ------------------------------------ | ------------------------------------ | --------------- | -----------: | ------: | -----: |
| Servidor Ubuntu  | SSH desactualizado                   | Conexión no autorizada al servidor   | Lógica          |            3 |       3 |      9 |
| Servidor Ubuntu  | Ubicación sin control de acceso      | Sabotaje, robo o manipulación física | Física / humana |            3 |       3 |      9 |
| Servidor Ubuntu  | Sin SAI                              | Apagón o pico de tensión             | Física          |            3 |       3 |      9 |
| Servidor Ubuntu  | Sin políticas de copias de seguridad | Pérdida de datos o ransomware        | Lógica          |            3 |       3 |      9 |
| Clientes Windows | Sin actualizaciones automáticas      | Explotación de vulnerabilidades      | Lógica          |            2 |       2 |      4 |

Un **análisis de vulnerabilidades** consiste en identificar debilidades existentes o que puedan aparecer en sistemas, aplicaciones, configuraciones o infraestructuras.

## Instalación de Nessus

Existen escáneres automáticos de vulnerabilidades.

Algunos ejemplos son **Greenbone** y **Nessus**. En clase utilizaremos **Nessus**.

Estos programas permiten analizar sistemas en busca de vulnerabilidades y problemas de configuración.

## Estándares globales

### CVE

**CVE (Common Vulnerabilities and Exposures)** es un sistema que proporciona identificadores únicos para vulnerabilidades de seguridad conocidas.

Por ejemplo, una vulnerabilidad puede tener un identificador con el formato:

```text
CVE-2026-XXXX
```

El CVE identifica la vulnerabilidad, pero no indica por sí mismo su gravedad.

### CVSS

**CVSS (Common Vulnerability Scoring System)** es un sistema utilizado para valorar la gravedad técnica de una vulnerabilidad.

Su puntuación va de **0,0 a 10,0**.

Es importante diferenciar:

**CVSS ≠ Riesgo**

* **CVSS:** mide la gravedad técnica de una vulnerabilidad utilizando determinados criterios.
* **Riesgo:** depende de la probabilidad de que ocurra una amenaza y del impacto que tendría en un entorno concreto.

De forma sencilla:

```text
Riesgo = Probabilidad × Impacto
```

Por eso, una vulnerabilidad con un CVSS alto no significa automáticamente que el riesgo para una organización sea alto, ya que depende del contexto.

### INCIBE

Podemos consultar información sobre vulnerabilidades y alertas de seguridad en **INCIBE-CERT**:

[INCIBE-CERT - Vulnerabilidades](https://www.incibe.es/incibe-cert/alerta-temprana/vulnerabilidades)

## Revisiones

Antes de realizar un análisis de vulnerabilidades también podemos revisar información básica del sistema.

### Windows

En Windows podemos comprobar:

* Windows Update.
* Aplicaciones instaladas.
* Información del sistema.

Para obtener información básica del sistema:

```powershell
winver
```

Para obtener información más detallada:

```powershell
msinfo32
```

También podemos consultar las actualizaciones disponibles desde **Configuración → Windows Update**.

### Linux

En Linux podemos comprobar las actualizaciones disponibles con:

```bash
sudo apt update
apt list --upgradable
```

Para consultar la versión de Ubuntu:

```bash
lsb_release -a
```

También podemos consultar información del kernel:

```bash
uname -a
```

Para consultar los paquetes instalados:

```bash
dpkg -l
```

Y para buscar paquetes relacionados con una aplicación concreta:

```bash
dpkg -l | grep nombre
```

Por ejemplo:

```bash
dpkg -l | grep openssh
```

Esto puede ser útil para comprobar la versión instalada de determinados programas.

[Clase siguiente](./)
