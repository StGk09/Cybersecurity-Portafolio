# Implementacion de IDS (Suricata) y analisis de Trafico.

## Escenario
El objetivo fue endurecer la seguridad del laboratorio implementando un **sistema de deteccion de intrusos (IDS)** basado en host. El sistema debe ser capaz de detectar escaneos de red y trafico IMCP (Ping) malicioso en tiempo real.

## Desafios tecnicos: Migracion a Suricata.
Inicialmente se planteo el uso de **Snort** como IDS. Sin embargo, durante el despliegue en **Parrot Security OS**, se identifico que los paquetes de Snort estan deprecados en los repositorios actuales en favor de tecnologias mas modernas.
**Solucion:** Se tomo la decision tecnica de migrar a **Suricata**, un motor IDS/IPS de alto rendimiento y multihilo, asegurando compatibilidad ocn reglas entandares.

## Configuracion e Implementacion
1. **Despliegue:** Instalacion de Suricata en el nodo Acer (Parrot OS).

2. **Creacion de Reglas (Signatures):**
   Se diseno una regla personalizada para detectar reconocimiento basico (Ping Sweeps).
   ```bash
   alert icmp any any -> any any (msg:ALERTA: PING DETECTADO POR SURICATA"; sid: 100001; rev:1;)

3. **Arranque del IDS:**
   ```bash
   sudo suricata -S mis_reglas.rules -i wlp2s0

4. **Visualizacion de alertas con tail -f:**
   ```bash
   sudo tail -f /var/log/suricata/fast.log


--------------------------------------------------------------------------------------------------------------

## Evasion de IDS (Red Team Exercise)
**Objetivo:** Verificar la robustez de la regla ICMP intentando escanear el host sin detonar la alerta.

**Metodologia:** 
Se utilizo el protocolo **ARP (Address Resolution Protocol)** para realizar el descubrimiento de host. Dado que ARP opera en la Capa 2 (Enlace de Datos) y la regla de Suricata estaba configurada para ICMP (Capa 3), teoricamente el trafico deberia pasar desapercibido.

**Comando de Ataque (Desde Windows):**
`nmap -PR 192.168.0.74` (Ping ARP scan)

**Resultado:** 
* **suricata:** Silencio total (No se generan logs en fast.log).
* **Nmap:** Reporto el host como "Up" (Vivo). 
* **Conclusion:** La regla es efectiva para pings tradicionales pero ciega ante reconocimiento local por ARP. Se recomienda anadir reglas para deteccion de escaneos ARP inusuales. 






