# Implementacion de DNS Sinkhole (Pi-hole) para seguridad perimetral.


* **Rol:** Administador de sistemas / Analista de Seguridad.

* **Tecnologias:** Linux (Parrot OS), Pi-hole, Protocolos TCP/IP (DNS, DHCP).

**Desafio:** La red local presentaba vulnerabilidades de privacidad (rastreadores/telemetria) y riesgos de seguridad por publicidad maliciosa (Malvertising), ademas de consumo innecesario de ancho de banda.

**Acciones Realizadas:** 

1. **Despliegue de servidor:** Configuracion de servidor DNS local en entorno Linux (Parrot OS) con direccionamiento IP estatico.

2. **Gestion de trafico:** Configuracion de `dnsmasq` y `lighttpd` a traves de Pi-hole para interceptar peticiones DNS.

3. **Filtrado de red:** Implementacion de listas negras (Gravity database) bloqueando +100,000 dominios de publicidad y rastreo.

4. **Reconfiguracion de enrutador:** Modificacion del servidor DNS en el router principal para forzar a todos los clientes (loT, moviles, PC) a pasar por el filtro.

**Resultados:** 

* Bloqueo efectivo del 20%-30% del trafico total(solicitudes innecesarias).
* Eliminacion de publicidad en todos los dispositvos sin instalar software cliente.
* Proteccion proactiva contra sitios de prishing conocidos.


**Desafío Técnico Encontrado:** 

Tras la activación del servidor DNS (Pi-hole), se detectó una pérdida total de resolución de nombres en los clientes.

**Diagnóstico:** 
El sistema operativo anfitrión (Parrot OS) tenía una política de firewall estricta (ufw default deny incoming) previamente configurada para Hardening. Esto bloqueaba las peticiones UDP/TCP entrantes al servicio DNS.

**Solución Implementada:** 
Se configuró una regla de excepción específica en el firewall para permitir tráfico DNS, manteniendo el resto de puertos cerrados.

**Comando:** `sudo ufw allow 53` (Habilita tráfico UDP y TCP para DNS).

**Resultado:** Restauración inmediata del servicio manteniendo la postura de seguridad del Host.




