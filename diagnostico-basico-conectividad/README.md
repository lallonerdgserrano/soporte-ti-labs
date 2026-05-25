# Diagnóstico básico de conectividad en entorno VMware

**Estado:** Completado  
**Área:** Soporte TI / Help Desk / Redes básicas  
**Entorno:** VMware NAT con Windows 10 y Kali Linux  

---

## Escenario

Se utiliza una máquina virtual Windows 10 como equipo cliente simulado dentro de un entorno controlado en VMware, junto con una máquina Kali Linux como equipo técnico de apoyo para pruebas de red.

El caso simula un reporte de usuario con problemas de conectividad. El objetivo es aplicar un procedimiento básico de diagnóstico para revisar configuración IP, conectividad local, salida a internet y resolución DNS, sin exponer información sensible de una red doméstica o corporativa real.

---

## Evidencia del entorno

Ambas máquinas virtuales fueron configuradas dentro de una red **VMware NAT**.

![Entorno VMware NAT](./screenshots/01-vmware-nat-sandbox.png)

---

## Problema inicial detectado

En la máquina Windows 10 se identificó una dirección IP automática tipo **APIPA**:

```text
169.254.x.x
