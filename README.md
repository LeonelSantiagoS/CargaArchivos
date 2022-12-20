# CargaArchivos
Proyecto Colaborativo de FileExplorer

# Documentacion - Descarga CFDI Web Service
***
Programa que realiza descarga de CFDIs del web service que proporciona el SAT.
***
# sw.descargamasiva - Solución
***
## Proyecto - DescargaWebService
***
**Índice**   
1. [Recursos](#id1)
2. [Autor](#id2)


***
### - Recursos<a name="id1"></a>
***
    -- Carpeta - Archivo_Peticiones : Dentro de esta carpeta se almacenan los archivos XML de peticiones de cada RFC. Si no existe se crea automaticamente.

    -- Carpeta - Archivos PFX : Dentro de esta carpeta se deben colocar los archivos PFX de cada uno de los RFC. La carpeta debe estar en la misma ruta del archivo .exe, dentro de la carpeta Recursos/Archivos PFX.

    -- Carpeta - LogErrores : Dentro de esta carpeta se almacenan los archivos txt de errores, se crea un archivo por dia. Si no existe se crea automaticamente.

    -- Carpeta - Peticiones Descargadas : Dentro de esta carpeta se guardaran los archivos de las peticiones que hayan sido exitosos. La carpeta se genera automaticamente.

### - Funcionamiento.
-- El sistema descarga realiza la descarga de CFDIs, de tipo Emitidas. Los dias a descargar son 4 dias contando la fecha actual, el rango de descarga es predeterminada de las 00:00:00 horas a las 23:59:59, el tiempo inicial puede variar cuando ya existen peticiones con la misma fecha, y el incremento es de 1 segundo por cantidad de registros de peticiones con las mismas fechas.

-- La descarga de CFDIs contempla 4 dias por lo siguiente:
    -> 72 horas es el tiempo maximo para que un CFDI sea timbrado por el SAT. Por lo cual se contempla 3 dias atras a partir de la fecha actual.
    -> Se toma en cuenta el dia actual, para descargar los CFDIs del dia tambien.
    
-- La ruta de Descarga de los paquetes .Zip, es la misma ubicacion desde la cual se ejecuta el sistema. Con la variacion de que se encuentra dentro de la carpeta Recursos/Peticiones Descargadas.

-- El nombre para la descarga de los paquetes .zip, se compone de: RFC_LOTE 2022MESDIA_Fecha Peticion.zip

-- El sistema esta programado para ejecutarse a las 18:00:00 horas, con la condicion de que la hora actual sea menor a esta hora. En caso de que la hora actual sea mayor a las 18:00 horas, se programa una nueva hora ejecucion, agregando 1 minuto a la hora actual.
Ejemplo:
Hora Ejecucion = 18:00:00
Hora Actual = 18:30:00 
La nueva hora de ejecucion seria a las 18:31:00.

-- El sistema cuenta con 3 timer, empleandose de la siguiente manera:
    -> tmrHora : Se utiliza para recuperar la hora del sistema, y activar el evento clic del boton btnIniciar, en caso de que la hora actual sea igual a las 18:00:00, puede haber una excepcion como se menciono en el funcionamiento anterior.
    -> tmrTemporizador : Se inicializa un temporizador de 59 minutos 59 segundos, cuando llega a 0 activa el evento clic del boton btnIniciar, para hacer las peticiones. Solo se activa cuando no se completan las peticiones del dia.
    -> tmrDescargaPaquetes : Se inicializa un temporizador de 30 minutos, cuando llega a 0 activa el evento clic del boton btnDescarga, para la descarga de las peticiones, en caso de no ser exitoso, se reprograma a otros 30 minutos, hasta que se descarguen todas las peticiones del dia.

### - Autor<a name="id2"></a>
