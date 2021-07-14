# Reporte

## Trabajo práctico entregable - parte 1

En esta notebook, vamos a cargar el conjunto de datos de la compentencia Kaggle sobre estimación de precios de ventas de propiedades en Melbourne, Australia.

Utilizaremos el conjunto de datos reducido producido por DanB. Hemos subido una copia a un servidor de la Universidad Nacional de Córdoba para facilitar su acceso remoto.

## Ejercicio 1:
**Pasos para la limpieza del data set:**
- Analizar la distribución de los precios de las propiedades utilizando la columna 'Price'. 
- Analizar el comportamiento del precio de las propiedades con la intención de eliminar valores extremos. 
- Calcular media, mediana y moda. 
- Graficar los datos de la columna "Price" y las correspondientes variables estadísticas.
- Observar valores outliers. 
- Calcular varios percentiles inferiores y superiores
	- Elegir percentil inferior
	- Elegir percentil superior
- Definir un nuevo df con la columna "Price" acotada de acuerdo al análisis previo. 


**Pasos para seleccionar variables relevantes:**
- Investigar la distribución de las variables del conjunto de datos y seleccionar un subconjunto de columnas que les parezcan relevantes al problema de predicción del valor de la propiedad.
- Analizar cada variable en relación con la variable de análisis “Price” y justificar cada columna no seleccionada. 
	-Columna Bedroom2: Algunas propiedades tienen más "Bedrooms" que "Rooms". La columna bedroom2 no es relevante para el análisis y la descartamos.
	- CouncilArea: No se considera un dato relevante para el valor de la propiedad, se asume que no existen políticas especiales
	- SellerG: Real Estate Agent: No nos interesa el Agente
	- Address: property address: Porque hay mucha variabilidad ya que existe un único valor para cada columna por tal motivo se elimina del análisis
	- Method: No se visualiza relación entre el precio y el method por tal motivo no se utiliza como relevante esta columna
	- Date: Date sold. No consideramos por el momento relevante la fecha de venta.
	- Bedroom2 : No se tiene en cuenta por que se usa Rooms
	- Landsize: No se observa dependencia entre el tamaño del terreno y el valor de la tierra.
	- Propertycount: Es importante conocer si el barrio/suburb se encuentra poblado. Eso podría ser indicador de diversidad de comercios en la zona, seguridad, transporte público, etc. Sin embargo, vemos que esta variable puede "englobarse" en regionname.
- Seleccionar columnas: columnas_seleccionadas:
	- Suburb Rooms
	- Type 
	- Price
	- Distance 
	- Postcode 
	- Bathroom
	- Car 
	- BuildingArea
	- YearBuilt
	- Lattitude
	- CouncilArea
	- Longtitude
	- Regionname
- Agrupar o combinar las categorías poco frecuentes para asegurar que todos los grupos tengan un número mínimo de registros, en caso de variables categóricas

**Pasos para eliminar datos erroneos:**
- Buscar columnas con valores NaN o inconsistencias en los datos. 
- Detectar variables con 0. Analizamos si tiene sentido el valor 0 en cada columna. 
- Analizar el número de categorías en cada columna categórica. Si se justifica, agrupamos en una categoría "Otros" a las categorías con menos apariciones. 

**Pasos para unir el dataset original con el dataset de Airbnb**
- Analizar datataset de AirBnb de propiedades en el sector de Melbourne, Australia
- Eliminar outliers del conjunto de Airbnb
- Eliminar los precios que están en los límites se ven valores como 0 y 12624, lo cual parecen valores poco posibles. El objetivo es agregar al dataset el precio promedio de alquiler de una vivienda en el sector en donde esta la propiedad
 - Analizar percentiles para eliminar outliers. 
- Seleccionar variables de AirBnb que pueden ser relevantes para la predicción del "Price".
	- Description
	- neighborhood_overview
	- street
	- neighborhood
	- city_suburb
	- state
	- zipcode
	- price
	- weekly_price
	- monthly_price
	- latitude
	- longitude
- Estandarizar la variable “Zipcode” para poder unir los datos de forma correcta
- Agregar las columnas seleccionadas al dataset de Airbnb al dataset original uniendolas por igual “Zipcode”


### Ejercicio 2: Imputación
**Pasos para la imputación de la columna Council Area:**
- Armar una lista de Suburb y CouncilArea y usar la moda para CouncilArea porque hay más de una por suburbio
- Crear un dataframe con el resultado
- Agregar la columna de la moda de CouncilArea al dataframe 
- Analizar cuantos valores en null existe en la columna CouncilArea
- Imputar los valores faltantes en la columna CouncilArea a partir de la columna de moda de CouncilArea

**Pasos para la imputación de datos faltantes en las columnas agregadas de Airbnb:**
- Validar que columnas de Airbnb tienen valores en 0
- Imputar la columas beds_min/max por el valor 1 asumiendo que hay al menos una cama
- Imputar la columna review_scores_mean por el valor promedio mínimo
- Imputar los precios diarios, mensuales y semanales. Dada la considerable variación de precios imputamos por el valor medio agrupado según cada suburbio

### Ejercicio 3: Archivo
**Pasos para generar el archivo:**
- Crear y guardar en un archivo el dataframe con todas las transformaciones aplicadas


## Trabajo práctico entregable - parte 2
### Ejercicio 1: 
**Pasos para Encoding:**
- Analizar archivo extraido del ejercicio anterior
- Reemplazar los NaN si es posible
- Crear nuevo df to encode
- Distinguir las columnas numericas de las categoricas y almacenarlas en dos listas sus nombres
- Definir el encoder y se lo pasamos solo a las columnas categoricas
- Armar un nuevo df solo con las columnas numericas
- Unir el df de variables numericas, las cuales no se modificaron, con el encoding nuevo
- Guardar el df en un .csv

**Pasos para DICTVECTORIZER:**
- Trabajar nuevamente con el df inicial
- Reemplazar los NaN si es posible
- Completar los CouncilArea vacios con other
- Distinguir las columnas numericas de las categoricas y almacenamos en dos listas sus nombres
- Transformar el df a un diccionario
- Aplicar DictVectorizer()
- Obtener los nombres de las nuevas columnas
- Validar que nuestra matriz densa nos va a entrar en memoria solamente
- Convertir matriz a df
- Guardar el df en un .csv

### Ejercicio 2:
**Pasos para la imputación KNN:**
- Agregar las columnas de interes
	- YearBuilt
	- BuildingArea
- Analizar la distribución de los datos de las columnas seleccionadas
- Acotar los datos a utilizar analizando los percentiles
- Imputar con KNN
- Graficar las distribuciones de datos antes y después de la impuestación
- Analizar la distribución de datos antes y después de la imputación para determinar si conviene o no aplicar KNN

**Escalar:**
- Aplicar escalado para ver las diferencias en el resultado
- Aplicar la imputacion KNN a las columnas ya escaladas
- Graficar las distribuciones de datos antes y después de la impuestación con datos escalados
- Analizar la distribución de datos antes y después de la imputación para determinar si conviene o no aplicar KNN. No se observan cambios relevantes

**Normalizar:**
- Analizar si normalizar nos ayuda a mejorar los resultados
-  Eliminar los NaN para poder aplicarla Normalizacion
- Aplicar Normalizacion para ver las diferencias en el resultado
- Aplicar ahora la imputacion por knn con las nuevas escalas
- Graficar las distribuciones de datos antes y después de la impuestación con datos escalados
- Analizar la distribución de datos antes y después de la imputación para determinar si conviene o no aplicar KNN. Vemos que normalizar mejora enormemente la distribucion de las columnas BuildingArea y YearBuilt luego de la imputacion por KNN y se logra coincidencia entre la distribucion antes de imputar y despues de imputar

### Ejercicio 3: Reducción de dimensionalidad
**Pasos para aplicar PCA:**
- Calcular la cantidad de dimensiones antes de aplicar  PCA
- Calcular PCA con n = min(20, X.shape[0]
- Calcular la cantidad de dimensiones luego de aplicar PCA
- Calcular las componentes principales
- Calcular varianza
- Calcular la razón de varianza
- Graficar el porcentaje de varianza para cada componente principal
- Graficar las componentes principales en relación con el Price
- Volver al df previo a PCA (el df obtenido de la normalizacion) y agregar dos columnas con las dos primeras componentes principales
- Graficar un sample de 1000 lineas de la componente principal 1 vs la 2 empleando como hue's las columnas normalizadas YearBuilt y BuildingArea

### Ejercicio 4:
**Pasos para la composición del resultado:**
- Detallar las nuevas columnas
- Analizar las dimensiones actuales y las del dataframe original
- Obtener una lista con los valores de la categoría que le corresponde a cada índice de la matriz