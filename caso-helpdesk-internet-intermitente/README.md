# Caso Help Desk: Internet intermitente con diagnóstico y escalamiento

## Objetivo

Documentar el proceso de diagnóstico de una falla de conectividad a Internet que afectaba múltiples dispositivos, identificar el origen probable del problema mediante pruebas básicas de red y escalar el caso al responsable del servicio cuando la incidencia se determinó fuera del alcance del usuario.

---

## Escenario

Un usuario reportó que la conexión a Internet presentaba un comportamiento inestable.

Los síntomas observados fueron:

- Internet lento e intermitente.
- Mensaje "Conectado, sin Internet".
- Páginas web que dejaban de cargar temporalmente.
- Problema presente en computadora, teléfono móvil y televisor.
- La incidencia comenzó entre un día y otro sin cambios conocidos por parte del usuario.

La conexión se realizaba mediante Wi-Fi.

---

## Información recopilada

### Preguntas realizadas al usuario

1. ¿Desde cuándo ocurre el problema?
2. ¿Afecta a un solo dispositivo o a varios?
3. ¿Aparece algún mensaje de error?
4. ¿La conexión es por cable o Wi-Fi?
5. ¿Se realizaron cambios antes de que comenzara la falla?

### Respuestas obtenidas

- El problema comenzó recientemente.
- Afecta a varios dispositivos.
- Aparece el mensaje "Conectado, sin Internet".
- La conexión es por Wi-Fi.
- No se reportaron cambios previos.

---

## Entorno

- Sistema operativo: Windows 11
- Conexión: Wi-Fi
- Adaptador de red: Marvell AVASTAR Wireless-AC Network Controller
- Dirección IPv4: 192.168.0.213
- Gateway: 192.168.0.1
- DNS: 192.168.0.1

---

## Evidencias principales

### Configuración IP obtenida correctamente

![Configuración IP](img/01-ipconfig-all.png)

La estación recibió una dirección IP válida mediante DHCP.

---

### Estado de conexión Wi-Fi

![WiFi sin Internet](img/02-wifi-conectado-sin-internet.png)

Windows detectaba la conexión inalámbrica, pero indicaba ausencia de acceso estable a Internet.

---

### Ping inicial al gateway

![Ping gateway](img/03-ping-gateway-perdida-paquetes.png)

Se observaron pérdidas importantes de paquetes hacia el gateway local.

---

### Ping inicial a Internet

![Ping Internet](img/04-ping-internet-perdida-paquetes.png)

La conectividad hacia Internet también presentaba pérdida de paquetes y latencia elevada.

---

### Error de navegación

![Error DNS](img/05-error-navegador-dns.png)

Durante la incidencia se observó un error de resolución de nombres.

---

### Tracert

![Tracert](img/06-tracert-inconsistente.png)

La ruta presentó respuestas inconsistentes y múltiples tiempos de espera agotados.

---

## Pruebas realizadas

### Verificación de configuración IP

Se confirmó:

- Dirección IP válida.
- Gateway configurado.
- DHCP funcional.
- DNS configurado.

No se observaron errores de configuración local.

---

### Ping continuo al gateway

Se ejecutó:

```cmd
ping -t 192.168.0.1
```

Resultados observados:

- Pérdida masiva de paquetes.
- Latencias variables.
- Respuestas intermitentes.

Evidencias:

![Gateway continuo 1](img/07-ping-gateway-continuo-parte-1.png)

![Gateway continuo 2](img/07-ping-gateway-continuo-parte-2.png)

![Gateway continuo 3](img/07-ping-gateway-continuo-parte-3.png)

Resultado destacado:

- 107 paquetes enviados.
- 30 recibidos.
- 77 perdidos.
- 71% de pérdida.

---

### Ping continuo a Internet antes de la corrección

Se ejecutó:

```cmd
ping -t 8.8.8.8
```

Evidencias:

![Internet antes 1](img/08-ping-internet-antes-de-correccion-parte-1.png)

![Internet antes 2](img/08-ping-internet-antes-de-correccion-parte-2.png)

![Internet antes 3](img/08-ping-internet-antes-de-correccion-parte-3.png)

![Internet antes 4](img/08-ping-internet-antes-de-correccion-parte-4.png)

![Internet antes 5](img/08-ping-internet-antes-de-correccion-parte-5.png)

![Internet antes 6](img/08-ping-internet-antes-de-correccion-parte-6.png)

Resultado destacado:

- 229 paquetes enviados.
- 131 recibidos.
- 98 perdidos.
- 42% de pérdida.

---

## Acciones correctivas locales

Se intentaron acciones de corrección desde el equipo:

```cmd
ipconfig /flushdns
ipconfig /release
ipconfig /renew
```

También se ejecutó:

```cmd
netsh winsock reset
netsh int ip reset
```

Posteriormente se reinició el equipo.

### Resultado

La falla continuó presentándose.

---

## Diagnóstico

Los resultados indicaron que:

- La configuración IP era correcta.
- El problema afectaba múltiples dispositivos.
- Existía pérdida severa de paquetes hacia el gateway local.
- La falla ocurría antes de salir a Internet.
- Las acciones locales no resolvieron la incidencia.

Debido a lo anterior, se concluyó que el problema probablemente se encontraba fuera del equipo del usuario.

---

## Escalamiento

El caso fue comunicado al responsable del servicio de Internet para revisión de la infraestructura.

Se recomendó inspeccionar:

- Router principal.
- Cableado.
- Equipos intermedios.
- Estado físico de la instalación.

---

## Resolución

Un técnico revisó la instalación y detectó una interferencia relacionada con el cableado de la conexión.

Después de corregir la incidencia, el servicio volvió a funcionar con normalidad.

---

## Validación posterior a la corrección

Se repitió la prueba:

```cmd
ping -t 8.8.8.8
```

Evidencias:

![Internet después 1](img/09-ping-internet-despues-correccion-parte-1.png)

![Internet después 2](img/09-ping-internet-despues-correccion-parte-2.png)

![Internet después 3](img/09-ping-internet-despues-correccion-parte-3.png)

![Internet después 4](img/09-ping-internet-despues-correccion-parte-4.png)

Resultado final:

- 499 paquetes enviados.
- 499 recibidos.
- 0 perdidos.
- 0% de pérdida de paquetes.

---

## Conclusión

La investigación permitió determinar que la falla no estaba relacionada con la configuración del equipo ni con un único dispositivo.

Las pruebas mostraron pérdida severa de paquetes hacia el gateway local y posteriormente hacia Internet, lo que permitió justificar el escalamiento del caso.

Tras la intervención de un técnico en la infraestructura física de la conexión, el servicio fue restablecido y las pruebas posteriores confirmaron una conectividad estable sin pérdida de paquetes.

---

## Habilidades demostradas

- Atención inicial de incidencias.
- Recopilación de información del usuario.
- Diagnóstico básico de redes.
- Uso de ipconfig.
- Uso de ping.
- Uso de tracert.
- Análisis de pérdida de paquetes.
- Identificación de problemas fuera del equipo local.
- Escalamiento justificado.
- Validación posterior a la corrección.
- Documentación técnica.
