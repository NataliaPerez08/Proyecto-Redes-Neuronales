# Proyecto-Redes-Neuronales

Para este proyecto usamos como referencia el siguiente articulo: J. L. Chavez Hurtado and J. H. Cortes-Fregoso, "Forecasting Mexican inflation using neural networks," CONIELECOMP 2013, 23rd International Conference on Electronics, Communications and Computing, Cholula, Puebla, Mexico, 2013, pp. 32-35, doi: 10.1109/CONIELECOMP.2013.6525753.

En este trabajo utilizaron un modelo de Redes Neuronales para pronosticar la inflación mexicana. En el se implementaron diferentes modelos de Redes Neuronales variando el número de capas ocultas (1 y 2) y el número de neuronas en la capa oculta (de 1 a 100).  En el trabajo de Chavez y Cortes, se implemento el modelo NN multicapa Feedforward utilizando la NN Toolbox de Matlab (Multilayer Feedforward NN model will be implemented using the NN Toolbox from Matlab.)


Nosotros utilizaremos Pytorch para definir igualmente un modelo NN multicapa, y exploraremos dos arquitecturas y dos data set.

En el trabajo de Chavez y Cortes para entrenar la NN utilizaron una base de datos proporcionada por el Banco de México que contiene la inflación mensual, la inflación anual y la inflación anual esperada según la inflación medida cada mes. La inflación de enero se utiliza como vector de entrada y la inflación anual como vector objetivo. La inflación esperada se utiliza para comparar los resultados de la NN con las expectativas del Banco de México» 

## Primera aproximación en Notebook proyecto_1
Nosotros en una primera aproximación tomaremos los datos de enero como Inflacion Indice de precios al consumidor (INPC) mensual, Inflacion Indice de precios al consumidor (INPC) acumulada en el anio, Inflacion subyacente mensual,Inflacion subyacente acumulada en el año, Inflacion subyacente anual,Inflacion no subyacente mensual,Inflacion no subyacente acumulada en el año, Inflacion no subyacente anual como features y la Inflacion Indice de precios al consumidor (INPC) anual como target. La forma en que los datos están estruturados es que cada entrada corresponde a un mes por cada entrada. Debido al gran número de datos faltantes tomaremos datos a partir de 01/01/1984. Haremos una ligera variación a lo que hace el articulo y tomaremos desde 1984 al 2021. Y compararemos las predicciones del 2021 al 2023.

En Chavez y Cortez,2013 «De la base de datos, el 70% de los datos se utilizará para entrenar la NN y el 30% restante para medir su rendimiento según el error cuadrático medio (MSE). Se seleccionará el modelo de NN con menor MSE para predecir la inflación. La función de activación utilizada en las capas ocultas fue la tangente hiperbólica y el resto de las especificaciones se establecieron con los valores por defecto de Matlab.»

De igual forma nosotros tomaremos el 70% de los datos para entrenar la NN y el 30% restante para medir su rendimiento según el error cuadrático medio (MSE). Luego En Chavez y Cortez,2013 encontraron que el modelo con el mejor MSE fue un modelo NN con 1 capa oculta y 49 neuronas ocultas. Este modelo NN se seleccionó para predecir la inflación anual. Nosotros utilizaremos esta misma estructura.

Esta arquitectura con esta base de datos no tuvo un buen rendimiento. 

## Segunda aproximación en Notebook proyecto_2
Los datos de entrenamiento serán de 1970-2010. Del 2011 para arriba serán de validación

Tomando como features:  Inflación mensual,Inflación acumulada del año.Y como target tomamos la inflacion anual.

En esta segunda aproximacion usamos una red LSTM. Con la arquitectura siguiente:
1. Input size = 2 #number of features
2. learning_rate = 0.001 
3. input_size = 2 #number of features
4. hidden_size = 2 #number of features in hidden state
5. num_layers = 1 #number of stacked lstm layers
   
Las predicciones fueron mucho mejores utilizando esta arquitectura y esta base de datos.

## Tercera aproximación en Notebook proyecto_3
Aún esperabamos mejorar la predicción en el conjunto de prueba así que decidimos probar con una estructura más, en el artículo Lukas Falat, Lucia Pancikova, Quantitative Modelling in Economics with Advanced Artificial Neural Networks, Procedia Economics and Finance,
Volume 34, 2015, Pages 194-201, ISSN 2212-5671, https://doi.org/10.1016/S2212-5671(15)01619-6. 
los autores presentan un nuevo enfoque en la previsión de series temporales económicas: la aplicación de redes neuronales artificiales. Los autores aplican redes neuronales artificiales de tipo RBF en el proceso de previsión de datos financieros. 

La red neuronal de función de base radial (RBF) es una mejora de la red perceptrón multicapa (MLP). Su nombre proviene del nombre de su función de activación. En general, RBF es cualquier función de valor real cuyos valores dependen sólo de la distancia al origen o a algún otro punto c, llamado centro. Cualquier función I que satisfaga esta propiedad es una función radial. La norma suele ser la distancia euclídea. Además, antes de proporcionar predicciones, la red neuronal de tipo RBF debe adaptarse para aproximar los datos. 

La arquitectura que implementamos está inspirada en las RBF. Y tuvo un rendimiento similar a la segunda aproximación.