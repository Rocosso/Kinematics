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
<img src="https://static.generation-robots.com/14801-product_cover/phantomx-pincher-robot-arm-kit-with-ax-12-actuators-and-adapter-for-leo-rover-non-assembled.jpg" alt="PhantomX_Pincher_ax-12" width="250px">
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

