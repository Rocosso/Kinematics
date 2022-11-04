# Kinematics
Robotics Dinamixel Kinematics 

## Cinematica inversa de un Robot Dinamixel AX-12 PhantomX Pincher.



<div>
<p style = 'text-align:right;'>
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSpw7VUCd_3cj1avB_6YTyQgX4e7nM5mVESyeb72_sLYUPdHkqi1yaDwMyR_tryIhLiRzM&usqp=CAU" alt="Logo UN" width="250px">
</p>
</div>

Por:

*Luis Alberto Chavez* 


*Camilo Pineda Correa*


<div>
<p style = 'text-align:left;'>
<img src="https://github.com/Rocosso/Kinematics/blob/main/Fotografias/pincher.jpg" alt="PhantomX_Pincher_ax-12" width="250px">
</p>
</div>



En este documento se explica como se configura y se ejecuta el servicio de conexión entre un PINCHERx y ROS instalado en Ubuntu mediante Matlab y Python

# Cinematica directa:

## Modelo y Medidas

Las dimenciones medidas sobre los robots al igual que las disposiciones de los ejes para cada articulación se muestran a continuación. 

![Modelo del robot PhantomX Pincher AX-12 ](https://github.com/Rocosso/lab4_Robotica/blob/main/Imagenes/DH_Pincher.png)

Estos modelos son independientes del software empleado, sea MatLab, ROS, Python.

## Parametros DH

Los parametros de DH-standard para el robot:

| Link |	alpha |	a	| d |	theta	| offset |
| -- | -- | -- | -- | -- | -- |
| 1	| 90°	| 0	| L1	| q1	| 0 | 
| 2	| 0	| L2	| 0	| q2	| 90° | 
| 3	| 0	| L3	| 0	| q3	| 0 | 
| 4	| 0	| L4	| 0	| q4	| 0 | 

# Cinematica Inversa:

![distribucion de los Ejes del robot Phantomx pincher AX-12](https://github.com/Rocosso/Kinematics/blob/main/Fotografias/pincher_Axis.jpg)

<img src="https://github.com/Rocosso/Kinematics/blob/main/Fotografias/Phantom_KinInv.jpg" alt="Gráfica Cinemática inversa" width="500">

## Primera articulación (Waist)

A partir de la anterior gráfica, realizamos el análisis de las articulaciones.

$$ q_1 = atan(y_T / x_T) \rightarrow  atan2(y_T, xT)$$

## Segunda articulación (Shoulder)

Por análisis de mecanismo 2R: <br>

$$ \theta_3 = acos(\frac{r^2+h^2-l_2^2-l_3^2}{2 l_3 l_3}) $$

$$ q_2 = -\pi/2 + atan2(h,r) - atan2(l_3 sin(\theta_3),l_2+l_3*cos(\theta_3)) $$

## Tercera articulación (Elbow)

$$ q_3 = \theta_3 $$

Nota: Para cambiar los valores de las articulaciones de q_2 y q_3 para las cofiguraciones de codo arriba o codo abajo únicamente hay que cambiar a theta3 de signo

## Cuarta articulación (Wrist)

$$ R_{pitch} = \begin{bmatrix} cos(q_1) & sin(q_1) & 0 \newline -sin(q_1) & cos(q_1) & 0 \newline 0 & 0 & 1 \end{bmatrix}  R_T$$

$$ pitch = atan2(R_{p31},R_{p11}) $$

$$ q_4 = pitch - q_2 - q_3 $$

Se realizó la implementación de esta cinemática inversa en una función de Matlab que se puede ver en el directorio src/getInvKin.py

## Espacios de trabajo

![Volumen de trabajod e robot PantomX AX-12 pincher ](https://github.com/Rocosso/Kinematics/blob/main/Fotografias/espacios%20de%20trabajo%20ampliado.png)

Se realiza un diagrama geométrico con los datos medidos del robot físico, se determina el espacio de trabajo del motor en el plano XZ del origen, considerando que es el plano que más variaciones tiene, especialmente si se considera que el plano XY es un circulo competo debido a la acción rotacional del primer actuador, y el espacio de trabajo en el plano YZ es muy similar al plano de trabajo en el Plano XZ solo que con menos restricciones.

Se entiende que esto forma una geometría semiesférica con un vacío interno, definido por la interferencia que realiza el robot consigo mismo.
De forma detallada se toma el modelo geométrico de cada eslabón, incluyendo la base del robot y se realizan los movimientos angulares máximos posibles para cada rotación, buscando los limites en los cuales el robot comienza a generar interferencia consigo mismo o con la base, o los puntos en los cuales el actuador llega a su máximo.

En la imagen se puede evidenciar que cuando una articulación llega a su límite ya sea del motor o por interferencia, la siguiente articulación puede continuar en la misma dirección hasta que esta se vea limitada.
