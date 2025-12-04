
# Hardering (Fortalecimiento) de red en Linux con UFW.

**Objetivo:** Asegurar el entorno de un servidor LInux restringiendo todo el trafico no autorizado y permitiendo solo servicios criticos, simulando un entorno de produccion.

**Entorno:** Parrot OS (Debian-based), UFW (Uncomplicated Firewall), Python (Para simulacion de servicio HTTP).

**Habilidades demostradas:** Gestion de Firewalls, Administracion de Linux, Conceptos de Redes (Puertos/Protocolos), Pruebas de conectividad.

**Procedimiento:**

1. **Analisis inicial:** Verificacion del estado del firewall y deteccion de vulnerabilidades (puertos abiertos por defecto).

-

2. **Estableciendo politicas bases:** Aplicacion del principio de "Minimo privilegio".

* **Bloquear todo lo que entra:** `bash sudo uwf default deny incomig
* **Permitir salida:** ` sudo default allow outcoming
