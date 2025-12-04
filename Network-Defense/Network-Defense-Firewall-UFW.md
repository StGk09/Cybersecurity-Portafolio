
# Hardering (Fortalecimiento) de red en Linux con UFW.

**Objetivo:** Asegurar el entorno de un servidor LInux restringiendo todo el trafico no autorizado y permitiendo solo servicios criticos, simulando un entorno de produccion.

**Entorno:** Parrot OS (Debian-based), UFW (Uncomplicated Firewall), Python (Para simulacion de servicio HTTP).

**Habilidades demostradas:** Gestion de Firewalls, Administracion de Linux, Conceptos de Redes (Puertos/Protocolos), Pruebas de conectividad.

**Procedimiento:**

1. **Analisis inicial:** Verificacion del estado del firewall y deteccion de vulnerabilidades (puertos abiertos por defecto).

-

2. **Estableciendo politicas bases:** Aplicacion del principio de "Minimo privilegio".

* **Bloquear todo lo que entra:** ```bash 
                                     sudo uwf default deny incomig

* **Permitir salida:** ```bash 
                          sudo default allow outcoming

3. **Simulacion de Servicio:** Despliegue de un servidor web temporal para pruebas.

* **Despliegue del servidor python:** ```bash 
                                         python3 -m http.server 8080

* **Prueba:** Conexion fallida desde dispositivo externo (confirmando funcionalidad del bloqueo).

4. **Apertura controlada (Whitelisting):** Creacion de reglas especificas para el servicio.
```bash
   sudo ufw allow 8080/tcp
   
5. **Validacion final:** El servicio es accesible, pero el resto del sistema permanece protegido.


**Conclusion:**
Se implemento exitosamente un firewall de host, reduciendo la superficie de ataque del sistema sin interrumpir los servicios legitimos.

  



