# Reporte Técnico: CVE-2026-31431

## Hito 1: Configuración del Entorno y Solución de Errores

Al principio tuve errores de compilación (Error 2 y 127) y un "Kernel Panic" (error -2). Esto pasaba porque los scripts buscaban rutas inexistentes, el contenedor no tenía recursos suficientes y el kernel no podía ver el archivo `/init`.

Para solucionarlo y arrancar QEMU con éxito, hice lo siguiente:

* **Corrección de rutas y scripts:** Como la carpeta se renombró a `copy-fail-challenge-1`, usé `sed` para actualizar las rutas en `01_build_kernel.sh`. Al corregir y cambiar la lógica de los scripts 01 y 02, se solucionó el Kernel Panic.
* **Instalación de dependencias:** Instalé `xz-utils` con `apt-get install` para poder descomprimir el kernel, ya que el contenedor no lo incluía.
* **Gestión de memoria:** Limpié los archivos temporales corruptos y configuré la compilación para usar un solo núcleo. Esto evitó que el Codespace se colgara por falta de recursos.

Tras esto, la VM arrancó perfectamente y obtuve el prompt del usuario `student`.

![alt text](image-2.png)

**Confirmación de la Vulnerabilidad :**
Una vez dentro de la VM, ejecuté comandos como `uname -r` e `id` para validar el entorno. Al intentar generar el reporte de evidencia, el directorio `/tmp` me dio error de permisos (`Permission denied`), por lo que redirigí la salida a la ruta personal `~/hito1.txt`. Finalmente, copié el resultado impreso, creé el archivo físico en la carpeta `evidence/` del Host y subí los cambios aplicando el commit y el tag `hito-1` requeridos por la guía.

![alt text](<Captura de pantalla 2026-05-16 150313.png>)  ![alt text](image-3.png)