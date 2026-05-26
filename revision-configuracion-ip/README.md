# Revisión de configuración IP en Windows

## Objetivo

Verificar la configuración IP de un equipo Windows para confirmar si la dirección IP, máscara de subred, puerta de enlace, DNS y DHCP están configurados correctamente.

Este laboratorio forma parte de mi portafolio técnico de Soporte TI, Help Desk y diagnóstico de red.

## Escenario

Se realiza una revisión básica de configuración IP en un equipo Windows.  
El objetivo es validar si el equipo recibió correctamente su configuración de red mediante DHCP y comprobar si tiene comunicación local, salida a Internet y resolución DNS.

## Herramientas utilizadas

- Windows CMD
- ipconfig
- ping
- netsh

## Evidencia 01: Revisión de configuración IP con ipconfig /all

Se ejecutó el comando:

```cmd
ipconfig /all
