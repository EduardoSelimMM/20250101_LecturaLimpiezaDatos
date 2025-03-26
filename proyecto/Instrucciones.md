# Proyecto de fin de módulo

El proyecto final se realizará en **equipos de 3 personas**. Las tres personas tendrán que crear repositorios: dos personas en local y una en remoto. El repositorio remoto se considerará como un repositorio colaborativo, en el que las 3 personas trabajarán.

## Primera parte

Se documenta mediante screenshots en un archivo de Google Doc (i.e. un archivo de Word de Google).

Cada persona tomará uno de los siguientes roles:

1. Administrador del repositorio: Creará el repositorio en GitHub, añade contenido y resuelve posibles conflictos. Tercer persona del equipo ordenada alfabéticamente por apellido paterno.

2. Colaborador 1: Clona el repositorio, añade contenido y realiza una contribución. Segunda persona del equipo ordenada alfabéticamente por apellido paterno.

3. Colaborador 2: Modifica el contenido y resuelve posibles conflictos. Primera persona del equipo ordenada alfabéticamente por apellido paterno.

Instrucciones:

1. Configuración inicial (administrador del repositorio)

En GitHub, el administrador del repositorio crea un repositorio privado llamado diplo-modulo2-equipo-n, donde n es el número de su equipo. Por ejemplo, si mi equipo es el 5, mi repositorio privado se llamará "diplo-modulo2-equipo-equipo-5"

Agrega un archivo README.md con una breve descripción del proyecto.

Agrega a los otros dos colaboradores y al usuario EduardoSelimMM con permisos de escritura.

Comparte la URL del repositorio con los colaboradores.

Sube al repositorio el archivo "vuelos.db"

Crea, desde GitHub, el archivo "proyecto_final.Rmd" con el siguiente contenido

```
---
title: "Proyecto final módulo 2"
author: "Equipo - n"
output: html_document
---

# Integrantes:

+ Integrante 1. Rol: Administrador
+ Integrante 2. Rol: Colaborador 1
+ Integrante 3. Rol: Colaborador 2

```{r}
library(DBI)
library(dbplyr)
library(RSQLite)

conn <- DBI::dbConnect(RSQLite::SQLite(), "vuelos.db")
```

2. Clonar el repositorio (Colaboradores 1 y 2, Administrador)

Cada colaborador debe clonar el repositorio en su máquina:

```
git clone https://github.com/usuario/diplo-modulo2-equipo-n.git
```

3. Colaborador 1: Desde su máquina crear chunks de código R en el archivo "proyecto_final.Rmd" (que obtuvo del Administrador) que muestre el número de tablas y sus nombres de la base de datos "vuelos"; además, crear un objeto en R, un por cada tabla de la base de datos. Hacer commit y push del código al repositorio del administrador y hacer un pull request.

4. Colaborador 2: Desde su máquina crear chunks de código R en el archivo "proyecto_final.Rmd" (que obtuvo del Administrador) que use las funciones `vis_dat()` y `vis_miss()` de la librería `{visdat}` para analizar los tipos de datos y datos faltantes de cada una de las tablas generadas por el Colaborador 1. Debe corregir la línea `author: "Equipo - n"` con el número correcto de equipo y agregar los nombres completos de los integrantes en la sección de `# Integrantes`. Hacer commit y push del código al repositorio del administrador y hacer un pull request.

5. Administrador del equipo. Desde su máquina crear chunks de código R en el archivo "proyecto_final.Rmd" (que obtuvo del Administrador) que use funciones de la librería {skimr} para obtener un resumen del tipo de variables, resumen de variables numéricas y resumen de variables categóricas para cada uno de los datasets que creo el Colaborador 1. Hacer commit y push del código al repositorio del administrador y revisar los pull requests de los colaboradores 1 y 2.

6. Obtener la versión actualizada del repositorio (Colaboradores 1 y 2, Administrador)

7. Cada colaborador debe hacer pull (jalar) el contenido actualizado del repositorio a su máquina. Los 3 archivos .Rmd de cada computadora deben ser idénticos entre sí.
   
9. El colaborador 2 debe ejecutar el código actualizado y dar conclusiones sobre cada uno de los subconjuntos de datos

## Segunda parte

### Subsección 1: Vuelos de NYC

Utilizaremos las tablas de la base de datos `vuelos.db` que incluye información de:

+ flights: Detalles de todos los vuelos que salieron de NYC (JFK, LGA, EWR) en 2013.
+ airlines: Códigos y nombres de aerolíneas.
+ airports: Información sobre aeropuertos, incluyendo ubicación.
+ planes: Datos sobre aeronaves, incluyendo año de fabricación.
+ weather: Datos meteorológicos por hora para los aeropuertos de NYC.

Responda las siguientes preguntas de 2 formas. Una utilizando verbos de {dplyr} y la otra con sintaxis SQL:

1. ¿Qué aerolínea tuvo el mayor retraso promedio en la salida en 2013?
2. ¿Qué día de la semana tuvo más vuelos retrasados en promedio?
3. ¿Cuál es la distribución de los retrasos en la salida para cada aeropuerto?
4. ¿Qué proporción de vuelos se retrasaron más de 30 minutos?
5. ¿Qué destinos tuvieron los mayores retrasos promedio en la llegada?
6. ¿Qué aerolíneas tuvieron el mayor número de vuelos desde NYC?
7. ¿Cómo varía el retraso de los vuelos según el fabricante de la aeronave?
8. ¿Los aviones más antiguos tienen más retrasos?
9. ¿Qué modelos de aviones se utilizan con mayor frecuencia en vuelos desde NYC?
10. ¿Cuál es la distancia promedio de vuelo por aerolínea?
11. ¿Qué aeropuerto de NYC tuvo el mayor número de retrasos en la salida?
12. ¿Qué aeropuerto tuvo el menor tiempo promedio de taxi-out?
13. ¿Qué porcentaje de vuelos que salen de cada aeropuerto de NYC fueron puntuales?
14. ¿Qué aeropuertos de destino tienen el mayor retraso promedio en la llegada para vuelos desde NYC?
15. ¿Cómo varían los retrasos en la salida según la hora del día en cada aeropuerto de NYC?
16. ¿Cuál es la correlación entre la velocidad del viento y los retrasos en la salida?
17. ¿Los vuelos experimentan más retrasos en días con lluvias intensas?
18. ¿Cómo afecta la temperatura a los retrasos de los vuelos?
19. ¿Cómo afectan los niveles de visibilidad a los retrasos en la llegada?
20. ¿La alta humedad se relaciona de alguna manera con los tiempos de taxi-out más largos?

### Subsección 2: Calidad del café

Se usará el conjunto de datos de encuesta de café

`datos <- readr::read_csv("coffee_ratings.csv")`

Actividad 0: Realice un análisis de valores faltantes del objeto `datos`

Actividad 1: Crear una columna llamada `color2` que se base en los valores de la columna `color`, que asigne el valor NA si  `color == NA`, "#00FF66" si `color == 'Green'`, "#CCEBC5" si `color == 'Bluish-green'` y "#BFFFFF" si `color == 'Blue-green'`

Actividad 2: Crear una columna llamada `bag_weight2` que se base en los valores de la columna `bag_weight`, que sólo contenga el valor numérico de ésta. Es decir, `bag_weight2` debe ser numérica. ¿Cuántas observaciones llevaron a ambigüedad para crear esta nueva columna?

Actividad 3: Crear dos columnas llamadas `method1` y `method2` que se basen en los valores de la columna `processing_method`, dividiendo en dos partes los valores dicha columna. ¿Cuántas observaciones llevaron a ambigüedad para crear esta nueva columna?

Actividad 4: Crear tres columnas llamadas `expiration_day`, `expiration_month` y `expiration_year` que se basen en los valores de la columna `expiration`. ¿Cuántas observaciones llevaron a ambigüedad para crear estas nuevas columnas?

Actividad 5: Crear dos columnas llamadas `harvest_mes` y `harvest_anio` que se basen en los valores de la columna `harvest_year`, dividiendo en dos partes los valores dicha columna. ¿Cuántas observaciones llevaron a ambigüedad para crear esta nueva columna?

Actividad 6: Elabore una visualización con {ggplot2} que identifique alguna relación entre las columnas total_cup_points, acidity y color2 de tal forma que se puedan identificar los colores de la variable `color2`. Es decir, debemos ver los colores, "#00FF66", "#CCEBC5" y "#BFFFFF".

Actividad 7: Elabore una visualización de densidad con {ggplot2} de la variable `bag_weight2` diferenciando a los valores de `species`.

Actividad 8: Elabore una visualización que relacione el año/mes de expiración con el `total_cup_points` sólo de los granos mexicanos, brasileños, colombianos y guatemaltecos.

Actividad 9: Elabore una visualización con {ggplot2} que relacione el mes de expiración con el `altitude_mean_meters`, `altitude_low_meters` y `altitude_high_meters` sólo de los granos mexicanos, brasileños, colombianos y guatemaltecos de los años de expiración 2016 y 2017.

Actividad 10: Elabore una visualización con {ggplot2} que relacione el `aftertaste`, `acidity`, `body` y `species` en un mismo canvas.

*Importante:* Sus visualizaciones deben tener formato suficientemente bueno para publicar en alguna revista.

### Sección 3: Analizando letras de canciones

Se utilizarán los archivos contenidos en la carpeta comprimida `canciones.zip`.

Actividad 1: Haga una nube de palabras de las canciones del último disco de Ariana Grande, Beyonce, Billie Eilish, Rihanna y Lady Gaga por separado, i.e. una nube por artista.

Actividad 2: Haga una nube de palabras de las canciones del último disco de Ariana Grande, Beyonce, Billie Eilish, Rihanna y Lady Gaga combinados, i.e. una única nube.

Actividad 3: Haga una nube de palabras de las canciones del último disco de Drake, Justin Bieber, Eminem, Ed Sheeran y Post Malone por separado, i.e. una nube por artista.

Actividad 4: Haga una nube de palabras de las canciones del último disco de Drake, Justin Bieber, Eminem, Ed Sheeran y Post Malone combinados, i.e. una única nube.

Actividad 5: Haga una nube de palabras de las canciones de los últimos 3 discos de BTS combinados, i.e. una única nube.
