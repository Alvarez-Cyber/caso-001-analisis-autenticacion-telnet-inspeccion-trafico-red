Análisis de tráfico de red con Wireshark sobre el protocolo Telnet en un entorno controlado. Se documenta la captura y el análisis de una sesión de autenticación, demostrando la transmisión de credenciales sin cifrado y los riesgos asociados. Incluye evidencia, metodología, observaciones técnicas y conclusiones.



## Descripción

Se realizó un análisis de tráfico de red utilizando Wireshark con el objetivo de evaluar el comportamiento del protocolo Telnet durante un proceso de autenticación remota. El laboratorio se llevó a cabo en un entorno controlado utilizando un cliente Windows y un switch Cisco IOS configurado para aceptar conexiones Telnet.

Durante el análisis se capturaron **897 paquetes**, identificándose una sesión de administración remota establecida entre el cliente **192.168.1.92** y el switch **192.168.1.244** mediante el puerto **TCP 23**.

La reconstrucción de la comunicación utilizando la función **Follow TCP Stream** permitió verificar que las credenciales de autenticación fueron transmitidas en texto plano. Para el laboratorio se utilizaron un usuario y una contraseña ficticios creados exclusivamente con fines educativos.

---

# Objetivo

Analizar una sesión Telnet mediante captura de paquetes para identificar el comportamiento del protocolo durante el proceso de autenticación, reconstruir la comunicación entre cliente y servidor y evaluar los riesgos asociados a la transmisión de información sin cifrado.

---

# Alcance

El análisis comprende:

* Captura de tráfico de red.
* Identificación de la comunicación Telnet.
* Análisis del establecimiento de la conexión TCP.
* Reconstrucción de la sesión mediante Follow TCP Stream.
* Verificación del intercambio de credenciales.
* Evaluación de los riesgos de seguridad asociados al protocolo.

---

# Entorno Analizado

| Elemento                | Valor                                     |
| ----------------------- | ----------------------------------------- |
| Herramienta de análisis | Wireshark                                 |
| Protocolo               | Telnet                                    |
| Transporte              | TCP                                       |
| Puerto                  | 23                                        |
| Cliente                 | 192.168.1.92                              |
| Servidor                | 192.168.1.244                             |
| Dispositivo             | Switch Cisco IOS (Switch.LaboratorioCasa) |
| Total de paquetes       | 897                                       |
| Credenciales            | Usuario y contraseña ficticios            |

---

# Topología del laboratorio

```text
                 Red de Laboratorio

        Cliente Windows
         192.168.1.92
               │
               │ TCP/23
               ▼
      Switch Cisco IOS
       192.168.1.244
               │
               ▼
          Wireshark
      Captura y análisis
```

---

# Metodología

La captura de tráfico se inició antes del establecimiento de la conexión Telnet para registrar toda la comunicación entre el cliente y el servidor.

Una vez iniciada la sesión, se aplicó el filtro correspondiente al puerto TCP 23 para aislar el tráfico del protocolo Telnet.

Posteriormente se utilizó la función **Follow TCP Stream**, permitiendo reconstruir la conversación completa entre ambos dispositivos y analizar el contenido transmitido durante el proceso de autenticación.

---

# Evidencias

## Evidencia 1 – Captura de tráfico

Se registró una captura compuesta por **897 paquetes**, incluyendo el establecimiento de la conexión TCP y la sesión Telnet completa.

**Archivo de evidencia**

```text
analisis-telnet-no-encriptado.pcapng
```

---

## Evidencia 2 – Comunicación Telnet

El tráfico correspondiente al protocolo Telnet fue identificado mediante el puerto **TCP 23**, confirmando la comunicación entre:

* Cliente: 192.168.1.92
* Servidor: 192.168.1.244

---

## Evidencia 3 – Reconstrucción de la sesión

Mediante **Follow TCP Stream** fue posible reconstruir completamente la comunicación entre cliente y servidor.

Durante esta etapa del análisis se verificó que las credenciales utilizadas en el laboratorio fueron transmitidas en texto plano sin aplicar ningún mecanismo de cifrado.

Las credenciales correspondían a un usuario y una contraseña ficticios creados exclusivamente para este entorno de pruebas.

---

# Análisis Técnico

El análisis del tráfico permitió identificar el establecimiento de una conexión TCP entre el cliente y el switch Cisco IOS utilizando el puerto 23.

Posteriormente se observó el proceso de autenticación correspondiente al protocolo Telnet. La reconstrucción de la sesión confirmó que tanto el nombre de usuario como la contraseña fueron enviados sin cifrado, característica propia del protocolo.

Este comportamiento representa una debilidad de seguridad, ya que cualquier usuario con capacidad para capturar el tráfico de la red podría acceder al contenido de la comunicación y obtener las credenciales transmitidas.

Durante la captura también se identificó tráfico correspondiente al protocolo SSDP hacia la dirección multicast **239.255.255.250**. Dicho tráfico no formó parte de la sesión Telnet analizada y fue descartado durante el proceso de investigación.

---

# Hallazgos

## Hallazgo 01

**Título:** Transmisión de credenciales en texto plano.

**Severidad:** Alta.

**Descripción**

La autenticación Telnet fue transmitida sin mecanismos de cifrado, permitiendo recuperar el contenido de la sesión mediante inspección del flujo TCP.

**Evidencia**

Reconstrucción de la sesión utilizando **Follow TCP Stream**.

**Impacto**

Un atacante con acceso al tráfico de red podría interceptar las credenciales y obtener acceso no autorizado al dispositivo administrado.

---

## Hallazgo 02

**Título:** Uso de protocolo de administración heredado.

**Severidad:** Media.

**Descripción**

El dispositivo de red mantiene habilitado el servicio Telnet para administración remota.

**Impacto**

La utilización de protocolos heredados incrementa la superficie de ataque y reduce el nivel de protección de las comunicaciones administrativas.

---

# Evaluación del Riesgo

| Categoría        | Evaluación |
| ---------------- | ---------- |
| Confidencialidad | Alta       |
| Integridad       | Media      |
| Disponibilidad   | Baja       |
| Riesgo General   | Alto       |

---

# Recomendaciones

* Deshabilitar el servicio Telnet en dispositivos de red.
* Implementar SSH versión 2 como protocolo exclusivo para administración remota.
* Restringir el acceso administrativo mediante listas de control de acceso (ACL).
* Supervisar conexiones dirigidas al puerto TCP 23.
* Eliminar protocolos heredados que transmitan información sin cifrado.
* Revisar periódicamente la configuración de los dispositivos de infraestructura.

---

# Cadena de Análisis

```text
Captura del tráfico
        │
        ▼
Filtrado TCP/23
        │
        ▼
Identificación de la sesión Telnet
        │
        ▼
Reconstrucción con Follow TCP Stream
        │
        ▼
Verificación de credenciales
        │
        ▼
Análisis de riesgos
        │
        ▼
Recomendaciones
```

---

# Conclusión

El análisis confirmó que el protocolo Telnet transmite la información de autenticación sin aplicar mecanismos de cifrado, exponiendo las credenciales a posibles ataques de interceptación cuando un tercero tiene acceso al tráfico de la red.

La utilización de Wireshark permitió reconstruir la sesión completa y verificar este comportamiento mediante evidencia obtenida directamente de la captura. Los resultados respaldan la recomendación de reemplazar Telnet por protocolos seguros como SSH para la administración remota de dispositivos de red.

---




