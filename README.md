# D.S.EJ2-Gestor-de-Conexiones-a-Base-de-Datos-Simple

[GestorConexion.java](https://github.com/user-attachments/files/32754962/GestorConexion.java)

<img width="1274" height="384" alt="image" src="https://github.com/user-attachments/assets/944dcdd4-7b10-4b11-8de4-dfbb6be8e99e" />

FUNCIONAMIENTO

- **Arranque bajo demanda:** La conexion fisica no se abre al iniciar el programa completo, sino unicamente la primera vez que un modulo del sistema (en este caso, el Modulo de Ususarios) invoca a _GestorConexion.obtenerInstancia()_.
- **Reutilización del Canal:** Cuando el Modulo de Ventas solicita la conexión inmediata después, el método _obtenerInstancia()_ detecta que el objeto ya existe en memoria y devuelve directamente la referencia previa sin volver a ejecutar la costosa lógica de apertura de red.
- **Ejecución de operaciones:** Todas las consultas y actualizaciones son canalizadas a través de ese único canal activo, compartiendo exactamente el mismo objeto y estado.

LOGICA

- **Encapsulamiento de instanciación con _private_:** Crear y destruir conexiones físicas consume tiempo de procesamiento, socket de red y memoria. La lógica de la solución radica en centralizar el ciclo de vida del recurso dentro de la misma clase que lo gestiona
- **Bloqueo de instanciación con _private_:** Al marcar el constructor como privado, se elimina la posibilidad de que programadores externos escriban _new GestorConexion()_ en distintos módulos, lo que habría provocad la apertura de múltiples conexiones físicas duplicadas.
- **Garantía de fuente única de verdad:** Al comparar las referencias (_conexionUsuarios == conexionVentas_), el resultado es _true_. Esto confirma que todo el sistema opera sobre una única instancia compartida y sincronizada en memoria, cumpliendo estrictamente con todas las restricciones técnicas y de dominio del ejercicio.
