Utilizando el conjunto de datos NSL-KDD, se realizó la siguiente prueba en el algoritmo ML basado en regla SIRUS, para la detección de un ataque de tipo DoS:
## cargar SIRUS
 	require(sirus)
Loading required package: sirus
## preparar los datos
 	data <- entrena
 	y <- rep(0, nrow(data))
 	y[data$label == 1] = 1
 	data$label <- NULL
## correr cv
 	cv.grid <- sirus.cv(data, y, nfold = 3, ncv = 2, num.trees = 100)
[1] “Running cross-validation 1/2 ...”
[1] “Running cross-validation 2/2 ...”
## Ajustar SIRUS
 	sirus.m <- sirus.fit(data, y)
Growing trees.. Progress: 37%. Estimated remaining time: 53 seconds.
Growing trees.. Progress: 74%. Estimated remaining time: 21 seconds.
[1] “Number of trees: 1000 - Stability 89.7 %.”
Growing trees.. Progress: 37%. Estimated remaining time: 53 seconds.
Growing trees.. Progress: 74%. Estimated remaining time: 22 seconds.
[1] “Number of trees: 2000 - Stability 93.09 %.”
Growing trees.. Progress: 36%. Estimated remaining time: 56 seconds.
Growing trees.. Progress: 68%. Estimated remaining time: 28 seconds.
[1] “Number of trees: 3000 - Stability 94.5 %.”
Growing trees.. Progress: 35%. Estimated remaining time: 58 seconds.
Growing trees.. Progress: 69%. Estimated remaining time: 28 seconds.
[1] “Number of trees: 4000 - Stability 95.04 %.”
## Trazar la ruta de validación cruzada
 	plot.error <- sirus.plot.cv(cv.grid)$error
 	plot(plot.error)
 ## Calcular las predicciones
 	predictions <- sirus.predict(sirus.m, data)
## Mostrar el modelo
 	sirus.print(sirus.m)
 [1] “Proportion of class 1 = 0.405 - Sample size n = 113270”
 [2] “if flag_SF < 1 then 0.913 (n=45278) else 0.0676 (n=67992)”
 [3] “if src_bytes < 10 then 0.913 (n=45171) else 0.069 (n=68099)”
 [4] “if same_srv_rate < 1 then 0.912 (n=44965) else 0.0722 (n=68305)”
 [5] “if diff_srv_rate >= 0.01 & flag_SF < 1 then 0.998 (n=40853) else 0.0711 (n=72417)” 
 [6] “if service_ecr_i < 1 & flag_SF >= 1 then 0.027 (n=64958) else 0.914 (n=48312)” 	
 [7] “if same_srv_rate < 1 & flag_SF < 1 then 0.998 (n=40864) else 0.0711 (n=72406)” 
 [8] “if diff_srv_rate < 0.01 then 0.0728 (n=67705) else 0.9 (n=45565)” 
 [9] “if count < 4 & flag_SF < 1 then 0.0714 (n=3933) else 0.417 (n=109337)” 
[10] “if src_bytes < 10 & diff_srv_rate >= 0.01 then 0.998 (n=40863) else 0.0712 (n=72407)”
[11] “if Protocol_type_icmp < 1 & flag_SF >= 1 then 0.0274 (n=63836) else 0.894 (n=49434)”

# ML-Model
Prueba en SIRUS


En las reglas del modelo obtenido con SIRUS, en el then está la probabilidad que sea una intrusión de tipo DoS.
