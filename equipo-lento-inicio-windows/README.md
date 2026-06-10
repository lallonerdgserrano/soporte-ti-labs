# Caso Help Desk: Equipo lento al iniciar sesión en Windows

## Objetivo

Documentar un caso de soporte técnico donde un equipo Windows presenta lentitud al iniciar sesión y consumo irregular de recursos.

El objetivo fue realizar un diagnóstico ordenado, aplicar acciones correctivas seguras y validar la mejora del rendimiento usando herramientas integradas de Windows.

## Entorno utilizado

* Windows 10
* Máquina virtual
* Administrador de tareas
* Configuración de Windows
* Seguridad de Windows / Microsoft Defender
* Símbolo del sistema como administrador

## Descripción del caso

El equipo presentaba lentitud después de iniciar sesión. El usuario reportaba que el sistema tardaba en quedar listo para trabajar y que el rendimiento era inestable durante los primeros minutos de uso.

Durante la revisión se identificaron programas configurados para abrirse al inicio de Windows, consumo elevado de CPU, archivos temporales acumulados y archivos dañados del sistema.

## Impacto

La lentitud afectaba el inicio de sesión y el tiempo necesario para que el equipo quedara operativo.

**Prioridad asignada:** Media
**Tipo de caso:** Incidente de rendimiento en equipo Windows
**Estado final:** Resuelto

## Procedimiento realizado

### 1. Revisión de programas configurados al inicio

Se revisaron los programas configurados para abrirse automáticamente al iniciar sesión.

Se identificaron varias aplicaciones cargando al arranque, lo cual podía aumentar el tiempo de inicio y afectar el rendimiento inicial del equipo.

**Evidencia:**

![Programas en carpeta de inicio](img/01-programas-en-carpeta-inicio.png)

---

### 2. Corrección de aplicaciones de inicio

Se revisó la pestaña **Inicio** del Administrador de tareas y se deshabilitaron aplicaciones no esenciales.

La acción se realizó sin desactivar componentes importantes del sistema, seguridad o herramientas necesarias para la máquina virtual.

**Evidencia:**

![Aplicaciones de inicio después](img/02-aplicaciones-inicio-despues.png)

---

### 3. Validación inicial de rendimiento

Después de aplicar la primera corrección, se revisó el rendimiento del equipo desde el Administrador de tareas.

El CPU seguía presentando consumo elevado, llegando a niveles altos durante la revisión.

**Evidencia:**

![Rendimiento CPU alto](img/03-rendimiento-cpu-alto.png)

---

### 4. Identificación de proceso con alto consumo

Se revisaron los procesos ordenados por consumo de CPU.

Se identificó que **Noticias e intereses** estaba generando consumo alto de recursos, por lo que se desactivó desde la barra de tareas.

**Evidencia:**

![Proceso con consumo alto](img/04-proceso-consumo-alto-noticias-intereses.png)

---

### 5. Validación después de desactivar Noticias e intereses

Después de desactivar **Noticias e intereses**, se revisó nuevamente el consumo de recursos.

El proceso dejó de aparecer como carga principal, pero el CPU continuó con comportamiento irregular asociado a procesos del sistema.

**Evidencia:**

![Procesos después de desactivar Noticias e intereses](img/05-procesos-despues-desactivar-noticias.png)

---

### 6. Seguimiento del consumo de CPU

Se continuó monitoreando el equipo para confirmar si la lentitud se mantenía.

El CPU seguía subiendo y bajando de forma irregular. Los procesos principales correspondían a servicios del sistema, por lo que no se cerraron manualmente para evitar afectar la estabilidad de Windows.

**Evidencia:**

![CPU inestable por procesos del sistema](img/06-cpu-inestable-procesos-sistema.png)

---

### 7. Revisión de recursos y almacenamiento

Se revisó el uso de CPU, memoria y disco para descartar saturación general del equipo.

También se revisó el almacenamiento disponible. El disco tenía espacio libre suficiente, por lo que la lentitud no parecía estar causada por falta crítica de espacio.

**Evidencia:**

![Rendimiento CPU y memoria](img/10-rendimiento-cpu-memoria.png)

![Almacenamiento disponible](img/11-almacenamiento-disponible.png)

![Archivos temporales detectados](img/12-archivos-temporales-detectados.png)

---

### 8. Validación de seguridad básica

Se ejecutó un examen rápido con Microsoft Defender para descartar amenazas comunes como posible causa de lentitud.

El resultado indicó que no se encontraron amenazas.

**Evidencia:**

![Examen rápido Windows Defender](img/17-examen-rapido-windows-defender.png)

---

### 9. Revisión y reparación de archivos del sistema

Se ejecutó `sfc /scannow` desde el Símbolo del sistema como administrador para validar la integridad de archivos del sistema.

El resultado indicó que Windows encontró archivos dañados y los reparó correctamente.

**Comando utilizado:**

```cmd
sfc /scannow
```

**Evidencia:**

![SFC reparación de archivos](img/18-sfc-scannow-reparacion-archivos.png)

---

### 10. Validación final

Después de reiniciar el equipo, se revisó nuevamente el Administrador de tareas.

El consumo de CPU bajó de forma notable en comparación con las revisiones anteriores, mostrando una mejora en el rendimiento general del equipo.

**Evidencia:**

![Validación final rendimiento mejorado](img/19-validacion-final-rendimiento-mejorado.png)

## Resultado

El equipo mejoró después de aplicar las acciones correctivas.

Se redujo la carga al inicio, se eliminó un proceso innecesario con alto consumo, se descartaron amenazas activas y se repararon archivos dañados del sistema.

La validación final mostró un consumo de CPU más estable y menor que el observado durante el diagnóstico inicial.

## Resumen técnico del ticket

**Problema reportado:**
Equipo lento después de iniciar sesión.

**Diagnóstico:**
Se identificaron programas cargando al inicio, consumo elevado de CPU, actividad irregular de procesos del sistema y archivos dañados del sistema.

**Acciones aplicadas:**
Se deshabilitaron programas innecesarios del inicio, se desactivó Noticias e intereses, se revisó almacenamiento, se ejecutó examen rápido con Microsoft Defender y se repararon archivos del sistema con `sfc /scannow`.

**Resultado:**
El equipo quedó operativo con mejor rendimiento después del reinicio y la validación final.

**Estado:**
Resuelto.

## Evidencia complementaria

Las siguientes evidencias se conservaron como parte del diagnóstico, pero no se toman como causa principal del caso.

<details>
<summary>Ver evidencias complementarias</summary>

### Revisión de Windows Update

Durante el diagnóstico también se revisó Windows Update porque algunos servicios del sistema podían estar generando actividad en segundo plano.

![Error de Windows Update](img/07-windows-update-error-80240009.png)

![Windows Update no actualizado](img/08-windows-update-no-actualizado.png)

![Intentos fallidos de Windows Update](img/09-windows-update-intentos-fallidos.png)

![Solucionador no identifica problema](img/14-solucionador-no-identifica-problema.png)

![Historial de actualizaciones instaladas 1](img/15-historial-actualizaciones-instaladas-1.png)

![Historial de actualizaciones instaladas 2](img/15-historial-actualizaciones-instaladas-2.png)

![Actualizaciones opcionales](img/16-actualizaciones-opcionales-driver-broadcom.png)

### Detalle de archivos temporales

![Detalle de archivos temporales 1](img/13-detalle-archivos-temporales-1.png)

![Detalle de archivos temporales 2](img/13-detalle-archivos-temporales-2.png)

![Detalle de archivos temporales 3](img/13-detalle-archivos-temporales-3.png)

</details>

## Competencias demostradas

* Diagnóstico de lentitud en Windows.
* Revisión de programas de inicio.
* Uso del Administrador de tareas.
* Identificación de procesos con alto consumo.
* Validación de CPU, memoria, disco y almacenamiento.
* Revisión básica de seguridad con Microsoft Defender.
* Reparación de archivos del sistema con `sfc /scannow`.
* Documentación técnica orientada a Soporte TI / Help Desk.

## Conclusión

Este caso demuestra un flujo realista de soporte técnico: recibir un reporte de lentitud, revisar causas probables, aplicar correcciones seguras y validar el resultado final con evidencia.

La mejora observada después del reinicio muestra que las acciones aplicadas ayudaron a dejar el equipo en mejor estado operativo.
