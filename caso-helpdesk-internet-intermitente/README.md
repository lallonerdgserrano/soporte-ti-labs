# Caso Help Desk: Internet intermitente con diagnóstico y escalamiento

## Objetivo

Diagnosticar una falla de conectividad a Internet que afectaba múltiples dispositivos de una red residencial, identificar si el problema se encontraba en el equipo local o en la infraestructura de red y documentar el proceso de escalamiento hasta la resolución del incidente.

---

## Escenario

Un usuario reportó que la conexión a Internet presentaba un comportamiento anormal.

Los síntomas reportados fueron:

- Internet lento e intermitente.
- Desconexiones frecuentes.
- Mensaje "Conectado, sin Internet".
- Páginas web que dejaban de cargar temporalmente.
- Error de navegación durante las caídas.
- El problema afectaba computadora, teléfono móvil y televisor.

Debido a que la incidencia afectaba varios dispositivos al mismo tiempo, se descartó inicialmente que el problema estuviera limitado a una sola computadora.

---

## Entorno

- Sistema operativo: Windows 11
- Conexión: Wi-Fi residencial
- Adaptador inalámbrico: Marvell AVASTAR Wireless-AC Network Controller
- Dirección IPv4: Oculta por privacidad
- Máscara de subred: Oculta por privacidad
- Gateway predeterminado: Oculto por privacidad
- Servidor DHCP: Oculto por privacidad
- Servidor DNS: Oculto por privacidad

**Nota:** Los parámetros específicos de direccionamiento fueron anonimizados por motivos de privacidad y no afectan el análisis técnico del caso.

---

## Problema reportado

El usuario indicó que la conexión funcionaba durante algunos minutos y posteriormente comenzaba a fallar.

Durante la falla se observaban los siguientes comportamientos:

- El navegador no lograba abrir páginas web.
- Algunas páginas mostraban errores de resolución.
- Windows mostraba el estado "Conectado, sin Internet".
- La conexión regresaba por momentos y volvía a fallar poco después.

---

## Información recopilada

### Preguntas realizadas

1. ¿Desde cuándo ocurre el problema?
2. ¿Afecta únicamente a una computadora o a varios dispositivos?
3. ¿Aparece algún mensaje de error?
4. ¿La conexión es por cable o Wi-Fi?
5. ¿Se realizaron cambios antes de que iniciara la falla?

### Respuestas obtenidas

- El problema comenzó recientemente.
- Afecta varios dispositivos.
- Aparece el mensaje "Conectado, sin Internet".
- La conexión se realiza mediante Wi-Fi.
- No se reportaron cambios previos.

---

## Diagnóstico inicial

Se verificó la configuración de red mediante:

```cmd
ipconfig /all
```

### Resultado

La estación obtuvo correctamente:

- Dirección IP privada válida.
- Gateway configurado.
- DNS configurado.
- Concesión DHCP válida.

No se encontraron errores de configuración local.

---

## Prueba de conectividad al gateway

Se ejecutó:

```cmd
ping 192.168.X.1
```

Resultado observado:

```text
Respuesta desde 192.168.X.1
Tiempo = 3 ms

Respuesta desde 192.168.X.1
Tiempo = 5 ms

Tiempo de espera agotado para esta solicitud

Respuesta desde 192.168.X.1
Tiempo = 2651 ms

Tiempo de espera agotado para esta solicitud
```

La pérdida de paquetes y las latencias elevadas indicaban una comunicación inestable incluso dentro de la red local.

---

## Prueba continua al gateway

Se ejecutó:

```cmd
ping -t 192.168.X.1
```

Resultado final:

```text
Paquetes: enviados = 107
recibidos = 30
perdidos = 77

71% de pérdida
```

Latencias observadas:

```text
3 ms
5 ms
10 ms
2651 ms
2916 ms
3252 ms
3371 ms
```

### Análisis

La pérdida ocurría directamente contra el gateway local.

Esto indicó que el problema probablemente se encontraba dentro de la infraestructura local de red, antes de salir hacia Internet.

---

## Prueba de conectividad a Internet

Se ejecutó:

```cmd
ping 8.8.8.8
```

Resultado observado:

```text
Respuesta desde 8.8.8.8
Tiempo = 83 ms

Respuesta desde 8.8.8.8
Tiempo = 79 ms

Tiempo de espera agotado para esta solicitud

Respuesta desde 8.8.8.8
Tiempo = 2695 ms
```

---

## Prueba continua a Internet

Se ejecutó:

```cmd
ping -t 8.8.8.8
```

Resultado final:

```text
Paquetes: enviados = 229
recibidos = 131
perdidos = 98

42% de pérdida
```

También se observaron múltiples errores:

```text
Tiempo de espera agotado para esta solicitud

PING: error en la transmisión. Error general.
```

### Análisis

La conectividad hacia Internet también era inestable.

Sin embargo, debido a que el gateway ya presentaba una pérdida de paquetes del 71%, se determinó que el origen principal de la falla se encontraba dentro de la infraestructura local de red.

---

## Error de navegación observado

Durante la incidencia el navegador mostró errores similares a:

```text
ERR_NAME_NOT_RESOLVED

No se encontró la dirección IP del servidor
```

### Análisis

Aunque inicialmente parecía un problema DNS, las pruebas posteriores demostraron que la pérdida de conectividad ocurría antes de llegar a los servidores DNS.

Por lo tanto, el error DNS fue considerado una consecuencia de la falla principal y no la causa raíz.

---

## Tracert

Se ejecutó:

```cmd
tracert 8.8.8.8
```

Resultado observado:

```text
Tiempo de espera agotado para esta solicitud
Tiempo de espera agotado para esta solicitud
```

La ruta presentó respuestas inconsistentes e interrupciones frecuentes.

---

## Acciones correctivas locales

Se intentaron acciones de corrección desde el equipo:

```cmd
ipconfig /flushdns
ipconfig /release
ipconfig /renew
```

Posteriormente:

```cmd
netsh winsock reset

netsh int ip reset
```

Finalmente se reinició el equipo.

### Resultado

Las acciones locales no resolvieron el problema.

La pérdida de paquetes continuó presentándose.

---

## Diagnóstico final

Con base en las evidencias recopiladas se concluyó que:

- La configuración IP era correcta.
- El problema afectaba múltiples dispositivos.
- Existía pérdida severa de paquetes hacia el gateway local.
- El problema ocurría antes de salir a Internet.
- Las acciones locales no resolvían la incidencia.
- El origen de la falla se encontraba fuera del equipo del usuario.

---

## Escalamiento

Debido a que la infraestructura principal de red no estaba bajo control del usuario, el caso fue reportado al responsable del servicio para revisión de:

- Router principal.
- Cableado.
- Equipos intermedios.
- Infraestructura física de la conexión.

---

## Resolución

Posteriormente un técnico realizó una revisión de la instalación.

Según la información proporcionada por el técnico que atendió el incidente, se identificó una interferencia relacionada con el cableado de la conexión.

Después de corregir la incidencia, el servicio volvió a funcionar normalmente.

---

## Validación posterior a la corrección

Se repitió la prueba:

```cmd
ping -t 8.8.8.8
```

Resultado:

```text
Paquetes: enviados = 499
recibidos = 499
perdidos = 0

0% de pérdida
```

Latencias observadas:

```text
74 ms
79 ms
82 ms
90 ms
110 ms
```

No se observaron:

- Tiempos de espera agotados.
- Errores de transmisión.
- Pérdida de paquetes.

---

## Conclusión

Se diagnosticó correctamente una falla de conectividad que inicialmente se manifestaba como lentitud, desconexiones y errores DNS.

Las pruebas permitieron demostrar que el problema no estaba relacionado con la configuración del equipo, sino con la infraestructura de red.

La evidencia recopilada justificó el escalamiento del caso y permitió confirmar posteriormente la solución implementada por el técnico responsable.

La validación final mostró una conectividad estable con 0% de pérdida de paquetes, confirmando la resolución exitosa del incidente.

---

## Habilidades demostradas

- Atención inicial de incidencias.
- Recopilación de información del usuario.
- Diagnóstico de conectividad.
- Uso de ipconfig.
- Uso de ping.
- Uso de tracert.
- Análisis de pérdida de paquetes.
- Identificación de causa raíz.
- Escalamiento justificado.
- Validación posterior a la corrección.
- Documentación técnica.
- Troubleshooting de redes.
- Comunicación con usuarios.

---

## Nota de privacidad

La información sensible de la red utilizada durante las pruebas fue anonimizada antes de la publicación de este laboratorio. Se ocultaron direcciones IP, parámetros de direccionamiento y otros identificadores que no aportan valor al análisis técnico del caso.
