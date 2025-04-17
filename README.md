Descripción de los procedimientos vistos en el ejercicio practico : 

Trigger para registrar cambios en la bitacora : Registra automáticamente en la tabla bitacora cada vez que se actualiza el campo sueldo_base de un vendedor.

Guarda: el rut del vendedor, el sueldo anterior, el nuevo y la diferencia.

Usa una secuencia llamada SEQ_BITACORA para generar el id_bitacora.
 Sirve para llevar un historial de cambios de sueldo.     ,  Los update que se muestran debajo 
Simulan un cambio de sueldo, Activando el trigger anterior para que se registre en la bitácora. 

![image](https://github.com/user-attachments/assets/59b67a65-c143-474b-b04f-1bdec4be3d3c)

Ejemplo de los cambios en la tabla Bitacora al insertar nuevos sueldos : 

![image](https://github.com/user-attachments/assets/d515039a-8ff2-4fa5-9382-a357210e77cd)


Creación del Package : 

Define un paquete de procedimientos y funciones reutilizables:

g_anio_proceso: Año en el que se hacen los cálculos (2022).

g_total_ventas: Variable para guardar el total de ventas (se puede usar internamente).

g_error: Variable para guardar errores si se desea.

obtener_ventas_vendedor: Función para obtener cuánto vendió un vendedor ese año.

insertar_error: Procedimiento para guardar errores en la tabla error_procesos_mensuales. 

![image](https://github.com/user-attachments/assets/85ac999a-e613-4031-a574-2fa9f85d654b)


Implementación del contenido del paquete:

 Función obtener_ventas_vendedor
Calcula la suma total de ventas (total) del vendedor en el año g_anio_proceso usando la tabla boleta.

 Procedimiento insertar_error
Inserta en la tabla error_procesos_mensuales cualquier error que ocurra durante los procesos, con su descripción y nombre del procedimiento. Usa la secuencia SEQ_ERROR. 

![image](https://github.com/user-attachments/assets/07084b5f-cb50-4d4e-b777-86edb7b9b628) 

Función Almacenada : Función fuera del paquete que devuelve la suma total de ventas (total) de todos los vendedores en un año (p_anio). Se usa para calcular porcentajes

![image](https://github.com/user-attachments/assets/ff572b87-c4e8-4e58-8e0f-8541625b4929) 

Procedimiento final:

Este procedimiento es el más importante y el que genera el informe final:

Borra todos los errores anteriores de la tabla error_procesos_mensuales.

Obtiene el total de ventas del año en curso.

Recorre a todos los vendedores y:

Obtiene el nombre de la comuna (desde tabla comuna).

Calcula el aporte del vendedor dividiendo sus ventas entre el total.

Inserta ese resultado en la tabla porcentaje_vendedor.

Si ocurre algún error en el loop, lo guarda usando insertar_error.

Si no hay ventas en ese año, también se registra un error. 


![image](https://github.com/user-attachments/assets/8da42290-f750-47a8-8299-242be0a51066) 



Bloque Anonimo para realizar las pruebas del procedimiento anterior:

Este bloque anónimo ejecuta el procedimiento para generar el informe, Es recomendable ejecutarlo dos veces:

Una vez para crear los datos.

Una segunda vez para forzar errores y ver cómo se manejan con la tabla error_procesos_mensuales. 

![image](https://github.com/user-attachments/assets/e020858a-c66e-4523-97dc-a81deb7c5276)

Tabla afectada por el procedimiento generar_informe_porcentaje_vendedor : 

![image](https://github.com/user-attachments/assets/a4b6ee2c-edd6-4488-b04e-3f6074fc1868)

Evidencia del Registro de errores cuando algo falla en la ejecución del informe : 

![image](https://github.com/user-attachments/assets/27055d35-9ca1-4a55-8279-da0a6171e74f)


 






