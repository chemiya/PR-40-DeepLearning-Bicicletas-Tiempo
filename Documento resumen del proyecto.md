<h1>Documento resumen del proyecto para predecir el número de bicicletas alquiladas con LSTM</h1>

<ol>
<h2><li>Resumen del proyecto</li></h2>
<p>Este proyecto consistirá en la creación de varios modelos con LSTM (Long Short-Term Memory) que es un tipo de red neuronal recurrente especializada en el procesamiento de secuencias y la modelización de datos secuenciales para predecir el número de bicicletas alquiladas utilizando el Bike Sharing Dataset.</p>








<h2><li>Tecnologías utilizadas</li></h2>
<p>Se van a utilizar las siguientes tecnologías relacionadas con Python:</p>
<ul>
<li>Tensorflow</li>
<li>Keras</li>
</ul>

<h2><li>Descripción Bike Sharing Dataset</li></h2>
El "Bike Sharing Dataset" es un conjunto de datos que contiene información sobre el uso de bicicletas compartidas en la ciudad de Washington D.C.. El proceso de alquiler de bicicletas compartidas está muy influenciado por las condiciones climatológicas y estas condiciones influyen sobre las actitudes de los usuarios a la hora de alquilar una bicicleta. Este dataset tiene los datos extraídos de los años 2011 y 2012 del sistema Capital Bikeshare en Washington D.C. En este caso, este conjunto de datos recoge los datos de alquiler de bicicletas por días detallando las condiciones del día

<h3>Descripción de los atributos</h3>
Antes de comenzar con el análisis de los modelos y los parámetros, es fundamental comprender el dataset y los atributos que contiene. Los atributos de este conjunto de datos son los siguientes:
<ul>
<li>Instant: índice</li>
<li>Dteday: fecha</li>
<li>season: estación, 1 corresponde con primavera, 2 con verano, 3 con otoño y 4 con invierno</li>
<li>year: año, 0 corresponde con el 2011 y 1 con el 2012</li>
<li>month: mes, del 1 al 12</li>
<li>holiday: si el día era festivo o no</li>
<li>weekday: día de la semana</li>
<li>workingday: si el día no es fin de semana ni festivo es 1, si no es 0</li>
<li>weathersit: descripción sobre el tiempo. A continuación, se hace un breve resumen de 
cada valor posible</li>
<ul>
<li>1: despejado o con alguna nube</li>
<li>2: niebla y nublado</li>
<li>3: lluvia ligera y nubes o nieve ligera</li>
<li>4: lluvia intensa o nieve</li>
</ul>
<li>Temp: temperatura normalizada en Celsius. Los valores están divididos entre 41 que era 
el máximo</li>
<li>Atemp: sensación térmica normalizada en Celsius. Los valores están divididos entre 50 
que era el máximo</li>
<li>Humidity: humedad normalizada. Los valores están divididos entre 100 que era el 
máximo</li>
<li>windSpeed: velocidad del viento. Los valores están divididos entre 67 que era el máximo</li>
<li>casual: número de usuarios casuales</li>
<li>registered: número de usuarios registrados</li>
<li>cnt: número de bicicletas alquiladas contando usuarios casuales y registrados. Variable a 
predecir</li>
</ul>


<h3>Estudio de la variable a predecir</h3>
A continuación, se realiza un breve estudio sobre la variable a predecir que es el número de bicicletas alquiladas en el día contando usuarios casuales y registrados. 
Esta variable llamada cnt tiene como promedio 4504,34 bicicletas y una desviación típica de 1935,88 bicicletas. A continuación, se puede ver su distribución:
<img src="grafico variable.png"/>
<br></br>
Se puede apreciar como la variable a predecir sigue una especie de distribución normal.

<h3>Modelos seleccionados</h3>
Los modelos para probar son los siguientes:
<ul>
<li>MLP</li> 
<li>LSTM</li> 
<li>LSTM con ventana temporal</li> 
<li>LSTM apiladas</li> 
<li>LSTM con memoria entre lote y lote</li> 
<li>LSTM's apilados (varias capas) con memoria entre lote y lote</li> 
</ul>

<h3>Preprocesamiento de los datos</h3>
En especial, para los modelos con LSTM se debe realizar un paso adicional sobre los datos generados después de aplicar el MinMaxScaler. Este paso consiste en convertir los datos tanto del conjunto de entrenamiento como de test en un formato adecuado para entrenar modelos de series temporales, como en este caso LSTM. Esto se realiza con la función CreaDatos.

<h3>Separación conjunto de datos y de test</h3>
Se separan los datos procesados cargados del csv en un conjunto de entrenamiento con un 67% de los registros totales y un conjunto de test con un 33% de los registros totales


<h2><li>Optimización de los parámetros</li></h2>
En general, para la optimización de los parámetros en este modelo y en los posteriores, se realizarán varios bucles anidados que recorran todas las combinaciones posibles de parámetros y se repetirá en 3 ocasiones el proceso de entrenar el modelo, realizar predicciones y calcular el RMSE. Finalmente se calculará el valor de RMSE medio para esas 3 ejecuciones con una determinada combinación de parámetros y se guardará en un dataframe este valor junto a los diferentes parámetros seleccionados para identificar el modelo creado. Se seleccionará la 
combinación de parámetros que haya obtenido una mejor media respecto al RMSE en esas tres ejecuciones. Como se ha comentado, para cada combinación de parámetros, se repite tres veces el proceso de entrenamiento y prueba. Para ello, en primer lugar, se crea un dataframe para almacenar la raíz del error cuadrático medio para cada combinación de parámetros. Después, se realizan los bucles anidados que recorren las diferentes combinaciones de parámetros y con cada combinación, se ejecuta un bucle for con 3 iteraciones donde se entrena el modelo, se realizan las predicciones y se calcula la raíz del error cuadrático medio entre las predicciones y los valores reales. Por último, al finalizar el bucle con las 3 iteraciones se almacena el valor medio de la raíz del error cuadrático medio obtenido en las 3 iteraciones junto a los valores de los parámetros seleccionados y el dataframe con esta media sobre RMSE en las 3 iteraciones para cada combinación de parámetros, se guardará en un archivo csv para su posterior análisis.

<h3>Optimización parámetros MLP</h3>
A continuación, se detallan los parámetros a optimizar en el MLP junto a los valores que pueden tomar:
<ul>
<li>Optimizador: SGD, Adam, RMSprop</li>
<li>Función de perdida: mean_squared_error, mean_absolute_error, huber_loss</li>
<li>Épocas: 6,10,14</li>
<li>Batch_size: 16, 32, 64</li>
<li>Capas: 1,3,5</li>
</ul>

La tabla con todos los valores sobre el RMSE para las diferentes combinaciones de parámetros en este modelo se puede encontrar en el Excel adjunto “MLP_resultados.xlsx”. En este Excel se pueden ver las 243 combinaciones de parámetros y el RMSE medio en sus 3 ejecuciones. Por lo tanto, los mejores valores en los parámetros para este modelo son los siguientes:
<ul>
<li>Optimizador: Adam</li>
<li>Capas: 3</li>
<li>Función de perdida: mean_absolute_error</li>
<li>Batch_size: 16</li>
<li>Épocas: 14</li>
</ul>


<h3>Optimización parámetros LSTM para un problema de regresión</h3>
A continuación, se detallan los parámetros a optimizar en este modelo junto a los valores que pueden tomar:
<ul>
<li>Épocas: 6,10,14</li>
<li>Batch_size: 16, 32, 64</li>
<li>LSTM_dim: 4,8,12,16</li>
<li>Función de activación de la salida: sigmoid, relu, tanh, linear</li>
</ul>
Este modelo solo tiene una capa LSTM y la historia es de 1.


La tabla con todos los valores sobre el RMSE para las diferentes combinaciones de parámetros se puede encontrar en el Excel adjunto “LSTM_1_resultados.xlsx”. En este Excel se pueden ver las 144 combinaciones diferentes de parámetros y su respectivo RMSE. Por lo tanto, los mejores valores en los parámetros para este modelo son los siguientes:
<ul>
<li>Función de activación en la salida: Relu</li>
<li>LSTM_dim: 16</li>
<li>Batch_size: 16</li>
<li>Épocas: 10</li>
</ul>

<h3>Optimización parámetros LSTM utilizando una ventana temporal</h3>
A continuación, se detallan los parámetros a optimizar en este modelo junto a los valores que pueden tomar:
<ul>
<li>Épocas: 6,10,14</li>
<li>LSTM_dim: 2,5,10</li>
<li>Optimizador: SGD, Adam, RMSprop</li>
<li>Función de perdida: mean_squared_error, mean_absolute_error, huber_loss</li>
 
</ul>
Este modelo tiene una LSTM como el anterior modelo, se utiliza una historia de 3 para cada 
ventana y el batch_size es 1.

La tabla con todos los valores sobre el RMSE para las diferentes combinaciones de parámetros se puede encontrar en el Excel adjunto “LSTM_2_resultados.xlsx”. En este Excel se pueden los resultados del RMSE con las 81 combinaciones diferentes de parámetros. Por lo tanto, los mejores valores en los parámetros para este modelo son los siguientes:
<ul>
<li>Optimizador: RMSprop</li>
<li>LSTM_dim: 10</li>
<li>Función de perdida: mean_absolute_error</li>
<li>Épocas: 14</li>
</ul>


<h3>Optimización parámetros LSTM apiladas</h3>
A continuación, se detallan los parámetros a optimizar en este modelo junto a los valores que pueden tomar:
<ul>
<li>Épocas: 6,10,14</li>
<li>LSTM_dim: 4,8,12</li>
<li>Optimizador: SGD, Adam, RMSprop</li>
<li>Batch_size: 16, 32, 64</li>

</ul>
Este modelo tiene una historia de 1 con 2 LSTM.
La tabla con todos los valores sobre el RMSE para las diferentes combinaciones de parámetros en este modelo se puede encontrar en el Excel adjunto “LSTM_3_resultados.xlsx”. En este Excel se pueden las 81 combinaciones diferentes de los parámetros. Por lo tanto, los mejores valores en los parámetros para este modelo son los siguientes:
<ul>
<li>Optimizador: adam</li>
<li>Batch_size: 16</li>
<li>Épocas: 10</li>
<li>LSTM_dim: 12</li>
</ul>


<h3>Optimización parámetros LSTM con memoria entre lote y lote</h3>
A continuación, se detallan los parámetros a optimizar en este modelo junto a los valores que pueden tomar:
<ul>
<li>Épocas: 6,10,14</li>
<li>LSTM_dim: 4,8,12</li>
<li>Optimizador: SGD, Adam, RMSprop</li>
<li>Función de activación de la salida: sigmoid, relu, tanh, linear</li>
</ul>

La tabla con todos los valores sobre el RMSE para las diferentes combinaciones de parámetros para este modelo se puede encontrar en el Excel adjunto “LSTM_4_resultados.xlsx”. En este Excel se pueden ver las 108 combinaciones de parámetros.
Por lo tanto, los mejores valores en los parámetros para este modelo son los siguientes:
<ul>
<li>Función de activación en la capa de salida: sigmoid</li>
<li>Optimizador: RMSprop</li>
<li>Épocas: 14</li>
<li>LSTM_dim: 4</li>
</ul>

<h3>Optimización parámetros LSTM's apilados (varias capas) con memoria entre lote y lote</h3>
A continuación, se detallan los parámetros a optimizar en este modelo junto a los valores que pueden tomar:
<ul>
<li>Épocas: 6,10,14</li>
<li>LSTM_dim: 4,8,12</li>
<li>Optimizador: SGD, Adam, RMSprop</li>
<li>Función de activación de la salida: sigmoid, relu, tanh, linear</li>
</ul>
La tabla con todos los valores sobre el RMSE para las diferentes combinaciones de parámetros para este modelo se puede encontrar en el Excel adjunto “LSTM_5_resultados.xlsx”. En este Excel se pueden ver las 108 combinaciones de parámetros. Por lo tanto, los mejores valores en los parámetros para este modelo son los siguientes:
<ul>
<li>Función de activación en la capa de salida: tanh</li>
<li>Optimizador: SGD</li>
<li>Épocas: 10</li>
<li>LSTM_dim: 12</li>
</ul>





<h2><li>Resultado final: vídeo youtube y repositorio</li></h2>
Repositorio Github:


<h2><li>Conclusiones</li></h2>
Con este proyecto, he aprendido más sobre cómo funcionan LSTM aplicando la optimización de sus parámetros a un conjunto de datos.

</ol>
