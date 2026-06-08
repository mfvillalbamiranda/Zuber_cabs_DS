<!--
# Descripción del proyecto
Estás trabajando como analista para Zuber, una nueva empresa de viajes compartidos que se está lanzando en Chicago. Tu tarea es encontrar patrones en la información disponible. Quieres comprender las preferencias de los pasajeros y el impacto de los factores externos en los viajes.

Al trabajar con una base de datos, analizarás los datos de los competidores y probarás una hipótesis sobre el impacto del clima en la frecuencia de los viajes.

Descripción de los datos
Una base de datos con información sobre viajes en taxi en Chicago:

tabla neighborhoods: datos sobre los barrios de la ciudad

name: nombre del barrio
neighborhood_id: código del barrio
tabla cabs: datos sobre los taxis

cab_id: código del vehículo
vehicle_id: ID técnico del vehículo
company_name: la empresa propietaria del vehículo
tabla trips: datos sobre los viajes

trip_id: código del viaje
cab_id: código del vehículo que opera el viaje
start_ts: fecha y hora del inicio del viaje (tiempo redondeado a la hora)
end_ts: fecha y hora de finalización del viaje (tiempo redondeado a la hora)
duration_seconds: duración del viaje en segundos
distance_miles: distancia del viaje en millas
pickup_location_id: código del barrio de recogida
dropoff_location_id: código del barrio de finalización
tabla weather_records: datos sobre el clima

record_id: código del registro meteorológico
ts: fecha y hora del registro (tiempo redondeado a la hora)
temperature: temperatura cuando se tomó el registro
description: breve descripción de las condiciones meteorológicas, por ejemplo, "lluvia ligera" o "nubes dispersas"
Esquema de la tabla
image

Nota: no existe una conexión directa entre las tablas trips y weather_records en la base de datos. Pero aún puedes usar JOIN y vincularlas usando la hora en la que comenzó el viaje (trips.start_ts) y la hora en la que se tomó el registro meteorológico (weather_records.ts).

Instrucciones para completar el proyecto
## Paso 1. Escribe un código para analizar los datos sobre el clima en Chicago en noviembre de 2017 desde el sitio web:

https://practicum-content.s3.us-west-1.amazonaws.com/data-analyst-eng/moved_chicago_weather_2017.html

## Paso 2. Análisis exploratorio de datos

Encuentra el número de viajes en taxi para cada empresa de taxis del 15 al 16 de noviembre de 2017. Nombra el campo resultante trips_amount y muéstralo junto con el campo company_name. Ordena los resultados por el campo trips_amount en orden descendente.
Encuentra la cantidad de viajes para cada empresa de taxis cuyo nombre contenga las palabras "Yellow" o "Blue" del 1 al 7 de noviembre de 2017. Nombra la variable resultante trips_amount. Agrupa los resultados por el campo company_name.
En noviembre de 2017 las empresas de taxis más populares fueron Flash Cab y Taxi Affiliation Services. Encuentra el número de viajes de estas dos empresas y asigna a la variable resultante el nombre trips_amount. Junta los viajes de todas las demás empresas en el grupo "Other". Agrupa los datos por nombres de empresas de taxis. Nombra el campo con nombres de empresas de taxis company. Ordena el resultado en orden descendente por trips_amount.

## Paso 3. Prueba la hipótesis de que la duración de los viajes desde el Loop hasta el Aeropuerto Internacional O'Hare cambia los sábados lluviosos.

Recupera los identificadores de los barrios de O'Hare y Loop de la tabla neighborhoods.
Para cada hora recupera los registros de condiciones meteorológicas de la tabla weather_records. Usando el operador CASE, divide todas las horas en dos grupos: "Bad" si el campo description contiene las palabras "rain" o "storm" y "Good" para los demás. Nombra el campo resultante weather_conditions. La tabla final debe incluir dos campos: fecha y hora (ts) y weather_conditions.
Recupera de la tabla trips todos los viajes que comenzaron en el Loop (neighborhood_id: 50) y finalizaron en O'Hare (neighborhood_id: 63) un sábado. Obtén las condiciones climáticas para cada viaje. Utiliza el método que aplicaste en la tarea anterior. Recupera también la duración de cada viaje.
Ignora los viajes para los que no hay datos disponibles sobre las condiciones climáticas.

## Paso 4. Análisis exploratorio de datos (Python)

Además de los datos que recuperaste en las tareas anteriores te han dado un segundo archivo. Ahora tienes estos dos CSV:

project_sql_result_01.csv. Contiene los siguientes datos:

company_name: nombre de la empresa de taxis
trips_amount: el número de viajes de cada compañía de taxis el 15 y 16 de noviembre de 2017.
project_sql_result_04.csv. Contiene los siguientes datos:

dropoff_location_name: barrios de Chicago donde finalizaron los viajes
average_trips: el promedio de viajes que terminaron en cada barrio en noviembre de 2017.
Para estos dos datasets ahora necesitas:

importar los archivos
estudiar los datos que contienen
asegurarte de que los tipos de datos sean correctos
identificar los 10 principales barrios en términos de finalización
hacer gráficos: empresas de taxis y número de viajes, los 10 barrios principales por número de finalizaciones
sacar conclusiones basadas en cada gráfico y explicar los resultados

## Paso 5. Prueba de hipótesis (Python)

project_sql_result_07.csv: el resultado de la última consulta. Contiene datos sobre viajes desde el Loop hasta el Aeropuerto Internacional O'Hare. Recuerda, estos son los valores de campo de la tabla:

start_ts: fecha y hora de recogida
weather_conditions: condiciones climáticas en el momento en el que comenzó el viaje
duration_seconds: duración del viaje en segundos
Prueba la hipótesis:
"La duración promedio de los viajes desde el Loop hasta el Aeropuerto Internacional O'Hare cambia los sábados lluviosos".
Establece el valor del nivel de significación (alfa) por tu cuenta.

Explica:

cómo planteaste las hipótesis nula y alternativa y qué criterio usaste para probar las hipótesis

-->

## Objetivo de negocio
Zuber es una nueva empresa de viajes compartidos (ride-sharing) en proceso de lanzamiento en el competitivo mercado de la ciudad de Chicago. La empresa busca identificar patrones comerciales clave en los datos históricos, comprender a fondo las preferencias de los pasajeros y evaluar de manera analítica el impacto de factores externos en los servicios de movilidad. Lo anterior con el fin de probar científicamente si las condiciones climáticas adversas alteran las dinámicas de viaje de la ciudad. Esto servirá para diseñar estrategias comerciales, optimizar tarifas dinámicas, prever la demanda en días de tormenta y planificar la disponibilidad de la flota para competir eficientemente contra las empresas de taxis establecidas (como Flash Cab).

## Descripción del dataset
El proyecto se dividió en fases híbridas de bases de datos relacionales SQL y analítica en Python, manejando los siguientes conjuntos de datos:
Estructura en Base de Datos (SQL):
- neighborhoods: Barrios de Chicago (name, neighborhood_id).
- cabs: Datos de vehículos (cab_id, vehicle_id, company_name).
- trips: Registro detallado de viajes individuales (trip_id, cab_id, start_ts, end_ts, duration_seconds, distance_miles, pickup_location_id, dropoff_location_id).
- weather_records: Historial climático por hora (record_id, ts, temperature, description).
Archivos Consolidados para Python (CSV):
- project_sql_result_01.csv: Registros de las compañías de taxis y su volumen de viajes (trips_amount) entre el 15 y 16 de noviembre de 2017.
- project_sql_result_04.csv: Listado de barrios de Chicago y su promedio diario de viajes finalizados (average_trips) en noviembre de 2017.
- project_sql_result_07.csv: Tabla con 1,068 registros de trayectos específicos realizados en sábados desde el barrio Loop hasta el Aeropuerto Internacional O'Hare, incluyendo la fecha/hora (start_ts), condición climatológica clasificada (weather_conditions) y la duración del viaje en segundos (duration_seconds).

## Metodología
- Extracción y Web Scraping: Recolección mediante código automatizado de los datos meteorológicos históricos de Chicago de noviembre de 2017 desde un servidor web.
- Procesamiento de Base de Datos (SQL): Conexión de datos climáticos y registros de viajes enlazándolos de forma indirecta por medio de la estampa de tiempo (trips.start_ts = weather_records.ts). Categorización del clima en dos condiciones mediante condicionales CASE: "Bad" (si incluía palabras como rain o storm) y "Good" (para cielos despejados o nubes dispersas).
- Análisis Exploratorio de Datos (EDA - Python): * Carga de datos con pandas, inspección de tipos de variables (info()) y descarte de nulos.Aislamiento y ordenamiento descendente de los 10 barrios principales con mayor recepción de pasajeros en la ciudad.Construcción de visualizaciones gráficas de barras para contrastar la cuota de mercado de las empresas de transporte y la popularidad de los destinos.
- Validación Estadística: Filtrado de viajes sabáticos exclusivos de la ruta Loop $\rightarrow$ O'Hare dividiendo la muestra en dos subpoblaciones independientes dependientes del clima ("Good" vs. "Bad") para realizar una prueba de hipótesis.

## Métricas
- Volumen e Intensidad de Viajes: trips_amount (frecuencia total) y average_trips (promedio de viajes mensuales por destino).
- Métrica del Tiempo de Viaje: Duración medida en segundos (duration_seconds).
- Métricas de Significación Estadística:
  - Nivel de Significación ($\alpha$): Fijado de forma estándar en 0.05 (5%), determinando el umbral máximo tolerable para cometer un error de Tipo I.
  - Valor p (p-value): Métrica probabilística calculada por la prueba t para contrastarla con el nivel $\alpha$.

## Resultados
- Flash Cab se posicionó drásticamente como la empresa líder absoluta en Chicago con más de 19,500 viajes en el periodo evaluado, seguida por Taxi Affiliation Services con cerca de 11,400 viajes. El resto de las decenas de empresas competidoras se agruparon en la categoría "Other" debido a sus cuotas de mercado minoritarias.
- El barrio de Loop encabezó la lista de finalizaciones con un promedio arrollador de 10,727 viajes diarios, seguido muy de cerca por distritos comerciales y turísticos clave como River North (~9,523) y Streeterville (~6,664). El aeropuerto O'Hare se posicionó sólidamente dentro del Top
- Hipótesis Nula ($H_0$): La duración promedio de los viajes desde el Loop hasta el Aeropuerto Internacional O'Hare no cambia los sábados lluviosos (las medias son iguales).
- Hipótesis Alternativa ($H_1$): La duración promedio de los viajes desde el Loop hasta el Aeropuerto Internacional O'Hare cambia los sábados lluviosos (las medias son diferentes).
- Resultado Estadístico: Tras ejecutar el software estadístico, el valor p arrojado fue extremadamente pequeño (muy inferior a 0.05). Por lo tanto, se rechazó categóricamente la Hipótesis Nula ($H_0$).

## Conclusiones
- Existe evidencia estadística contundente para afirmar que el clima lluvioso y tormentoso altera de forma significativa la duración de los viajes desde el centro (Loop) hasta el aeropuerto O'Hare los días sábados, aumentando el tiempo promedio que los pasajeros pasan dentro de las unidades.
- El negocio de la movilidad en Chicago está fuertemente centralizado en el corazón financiero (Loop) y las áreas turísticas adyacentes. Zuber debe enfocar la captación inicial de conductores en estas zonas estratégicas de alta densidad.
- Al comprobarse que los sábados lluviosos incrementan los tiempos de viaje (probablemente debido al tráfico vehicular lento y al aumento de la demanda), Zuber puede implementar un algoritmo de tarifas dinámicas optimizado para días lluviosos. Esto incentivará a los conductores a salir a trabajar en condiciones meteorológicas adversas ("Bad Weather"), garantizando una mayor disponibilidad de vehículos que sus competidores tradicionales y capturando clientes insatisfechos en los centros turísticos y aeropuertos.


