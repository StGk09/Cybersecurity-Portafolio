# Implementacion de IDS(Suricata) y analisis de Trafico.

## Escenario
El objetivo fue endurecer la seguridad del laboratorio implementando un **sistema de deteccion de intrusos (IDS)** basado en host. EL sistema debe ser capaz de detectar escaneos de red y trafico IMCP (Ping) malicioso en tiempo real.

## Desafios tecnicos: Migracion a Suricata.
Inicialmente se planteo el uso de **Snort** como IDS. Sin embargo, durante el despliegue en **Parrot Security OS**, se identifico que los paquetes de Snort estan deprecados en los repositorios actuales en favor de tecnologias mas modernas.
**Solucion:** Se tomo la decision tecnica de migrar a **Suricata**, un motor IDS/IPS de alto rendimiento y multihilo, asegurando compatibilidad ocn reglas entandares.

##Configuracion e Implementacion
1. **Despliegue:** Instalacion de Suricata en el nodo Acer (Parrot OS).
2. **Creacion de Reglas (Signatures):**
   Se diseno una regla personalizada para detectar reconocimiento basico (Ping Sweeps).
   ```bash
   alert icmp any any -> any any (msg:ALERTA: PING DETECTADO POR SURICATA"; sid: 100001; rev:1;)



