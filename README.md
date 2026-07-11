# Analisis-Trafico-Inseguro-Telnet-Wireshark
Análisis de tráfico de red con Wireshark sobre el protocolo Telnet en un entorno controlado. Se documenta la captura y el análisis de una sesión de autenticación, demostrando la transmisión de credenciales sin cifrado y los riesgos asociados. Incluye evidencia, metodología, observaciones técnicas y conclusiones.


🔍 Análisis del protocolo Telnet mediante Wireshark

Descripción

Este repositorio documenta un laboratorio de análisis de tráfico de red realizado en un entorno controlado utilizando Wireshark. El objetivo fue capturar y analizar una sesión de autenticación mediante el protocolo **Telnet**, demostrando cómo las credenciales son transmitidas en texto plano debido a la ausencia de mecanismos de cifrado.

Durante el laboratorio se capturó y analizó el tráfico generado entre un cliente y un switch Cisco configurado para aceptar conexiones Telnet. Mediante filtros de Wireshark y la función **Follow TCP Stream**, fue posible reconstruir la sesión y verificar la transmisión de credenciales ficticias en texto plano.

> **Aviso:** Este laboratorio fue realizado exclusivamente con fines educativos sobre equipos propios y utilizando credenciales ficticias. No constituye una guía para acceder a sistemas de terceros.

---

# Objetivos

* Comprender el funcionamiento del protocolo Telnet.
* Capturar tráfico de red utilizando Wireshark.
* Analizar el establecimiento de una conexión TCP.
* Identificar el proceso de autenticación.
* Verificar la transmisión de credenciales sin cifrado.
* Comprender por qué SSH reemplazó a Telnet como protocolo de administración remota.

---

# Entorno del laboratorio

| Elemento            | Información                                                              |
| ------------------- | ------------------------------------------------------------------------ |
| Herramienta         | Wireshark                                                                |
| Protocolo           | Telnet                                                                   |
| Puerto              | TCP 23                                                                   |
| Cliente             | 192.168.1.92                                                             |
| Servidor            | 192.168.1.244                                                            |
| Dispositivo         | Switch Cisco IOS (Switch.LaboratorioCasa)                                |
| Paquetes capturados | 897                                                                      |
| Credenciales        | Usuario y contraseña ficticios utilizados únicamente para el laboratorio |

---

# Topología del laboratorio

```text
                  Laboratorio de Red

     Cliente Windows                  Switch Cisco IOS
      192.168.1.92  ───── TCP/23 ───► 192.168.1.244
             │
             │
             ▼
        Wireshark
   Captura y análisis
```

---

# Metodología

1. Se inició la captura de tráfico utilizando Wireshark.
2. Se estableció una conexión Telnet desde el cliente hacia el switch Cisco.
3. Se inició sesión utilizando un usuario y una contraseña ficticios creados exclusivamente para este laboratorio.
4. Finalizada la autenticación, se detuvo la captura.
5. Se aplicó el filtro correspondiente al puerto TCP 23 para aislar el tráfico Telnet.
6. Mediante la función **Follow TCP Stream** se reconstruyó la sesión para analizar la comunicación entre ambos dispositivos.

---

# Análisis técnico

El análisis permitió identificar correctamente la comunicación entre el cliente (**192.168.1.92**) y el servidor (**192.168.1.244**) utilizando el puerto TCP 23.

Durante el establecimiento de la conexión se observó el intercambio inicial de paquetes TCP necesario para crear la sesión entre ambos dispositivos.

Posteriormente, mediante la herramienta **Follow TCP Stream**, fue posible reconstruir la conversación completa y verificar que tanto el nombre de usuario como la contraseña fueron transmitidos en **texto plano**, utilizando credenciales ficticias configuradas específicamente para este laboratorio.

Este comportamiento confirma una de las principales debilidades del protocolo Telnet: la ausencia de cifrado durante la autenticación y la comunicación entre cliente y servidor.

---

# Hallazgos

* Se capturaron **897 paquetes** durante la sesión.
* Se identificó correctamente la comunicación Telnet mediante **TCP puerto 23**.
* Se reconstruyó la sesión utilizando **Follow TCP Stream**.
* Se verificó que las credenciales ficticias fueron transmitidas en texto plano.
* Se confirmó que el dispositivo remoto correspondía a un **Switch Cisco IOS** configurado para aceptar conexiones Telnet.
* Se observó tráfico adicional (por ejemplo, SSDP), el cual fue descartado por no formar parte de la sesión analizada.

---

# Riesgos de seguridad

La utilización de Telnet representa un riesgo debido a que:

* No cifra la información transmitida.
* Las credenciales pueden ser recuperadas mediante captura de tráfico.
* Los comandos ejecutados también pueden ser observados.
* No garantiza la confidencialidad ni la integridad de la comunicación.

Por estas razones, Telnet ha sido reemplazado en entornos productivos por **SSH**, que incorpora mecanismos de cifrado y autenticación más seguros.

---

# Lecciones aprendidas

Durante este laboratorio reforcé conocimientos relacionados con:

* Captura y análisis de tráfico de red.
* Uso de filtros en Wireshark.
* Identificación de protocolos de red.
* Reconstrucción de sesiones TCP mediante **Follow TCP Stream**.
* Identificación de protocolos inseguros.
* Documentación técnica de un laboratorio de análisis.

---

# Herramientas utilizadas

* Wireshark
* Cliente Telnet
* Switch Cisco IOS
* TCP/IP

---

# Próximos laboratorios

* Análisis de FTP mediante Wireshark.
* Análisis de HTTP.
* Análisis de DNS.
* Análisis de ARP.
* Detección de escaneo con Nmap.
* Captura y análisis de tráfico HTTPS.
* Introducción a Suricata.
* Análisis de eventos con Sysmon.


