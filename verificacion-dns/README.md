# Verificación y corrección de fallo DNS

## Objetivo del laboratorio

Diagnosticar y corregir un problema de resolución DNS en Windows, aplicando un flujo básico de soporte técnico para identificar si el equipo tiene conectividad a internet pero falla al resolver nombres de dominio.

## Escenario

Un usuario reporta que tiene conexión a internet, pero no puede cargar algunas páginas web por nombre de dominio.

Como técnico de soporte TI, se realiza una revisión para confirmar si el problema está relacionado con conectividad general, configuración DNS o caché DNS local.

## Problema simulado

Para fines del laboratorio, se simula un fallo DNS configurando temporalmente un servidor DNS incorrecto o no funcional.

Esto permite demostrar el proceso completo:

- Detección del problema.
- Prueba de conectividad por IP.
- Confirmación del fallo DNS.
- Aplicación de corrección.
- Validación final.

## Herramientas utilizadas

- Windows
- CMD / Símbolo del sistema
- Configuración de red de Windows
- Comandos de diagnóstico de red

## Comandos utilizados

```cmd
ipconfig /all
ping 8.8.8.8
ping google.com
nslookup google.com
ipconfig /displaydns
ipconfig /flushdns
