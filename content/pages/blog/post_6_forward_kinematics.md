---
title: >-
  Ejemplo de modelado de un robot
date: '2022-08-02'
author: content/data/team/arno-sonck.yaml
categories:
  - content/data/categories/robotics.yaml
  - content/data/categories/espanol.json
tags:
  - Robotica
  - Español
image: https://i.ibb.co/njS4Fdc/RRR.png
image_alt: Post 5 placeholder image
excerpt: Muestro como aplicar la metodología de Denavit Hartenberg a un robot angular.
seo:
  title: >-
    Ejemplo de modelado de un robot
  description: >-
    Muestro como aplicar la metodología de Denavit Hartenberg a un robot angular.
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: Amet Nulla Facilisi Morbi Tempus
      keyName: property
    - name: 'og:description'
      value: 'Estne, quaeso, inquam, sitienti in bibendo voluptas'
      keyName: property
    - name: 'og:image'
      value: images/5.png
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Amet Nulla Facilisi Morbi Tempus
    - name: 'twitter:description'
      value: 'Estne, quaeso, inquam, sitienti in bibendo voluptas'
    - name: 'twitter:image'
      value: images/5.png
      relativeUrl: true
layout: post
---

<head>
<title>MathJax TeX Test Page</title>
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>
</head>
<body>
Como parte de un proyecto personal he decidido probar varias leyes de control en un robot angular. En este primer artículo presentaré el modelado de un brazo robótico (omitiendo el actuador final) en configuración angular.

La configuración angular se compone de tres articulaciones rotatorias, tiene un volumen de trabajo con forma de esfera solamente limitado por el rango de cada articulación y la interferencia que pueda tener consigo mismo. Esta configuración suele ser la base de los robots articulados de 6 grados de libertad (Ver Figura 1).

![BrazoRRR](https://i.ibb.co/njS4Fdc/RRR.png)
<h5><center> Figura 1: Configuración articular, el eslabón 1 esta indicado en color verde, el 2 en color azúl y el 3 en rojo. </center></h5>

<h2> Parametros del robot </h2>
Seguiremos el convencionalismo  de Denavit Hartenberg que fue presentado por James Denavit y Richard S. Hartenberg en 1955 y nos permite hacer el mapeo de articulación en articulación de forma sistemática.

<h3> Definiendo ejes </h3>
<p>Comenzamos con los ejes \(z\) de cada marco de referencia, el eje \(x_0\) va alineado con el eje de rotación de la primera articulación, el eje \(x_1\) va alineado con el eje de rotación de la segunda articulación y el eje \(x_2\) va alineado con el eje de rotación de la tercera articulación. El sistema de coordenadas \(3\) lo definiremos al final.</p>
<p>El eje \(x_0\) lo podemos colocar donde queramos sobre el eje \(z_0\), por conveniencia lo colocaremos en la intersección del eje \(z_0\) y \(z_1\) apuntando hacia la derecha. Como los ejes \(z_0\) y \(z_1\) se intersectan, colocaremos el eje \(x_1\) en dicha intersección pero normal a los ejes \(z_0\) y \(z_1\). El eje \(z_2\)esta en dirección de una línea normal que une los ejes \(z_1\) y \(z_2\), tenemos una infinidad de estas líneas y por conveniencia escogeremos la única que también toca el eje \(x_1\).</p>
<p>Hasta el momento hemos definido la dirección de los ejes \(z_i\) y \(x_i\), podemos determinar el origen \(O_i\) de cada sistema como el punto donde se intersectan estos ejes, el sentido de estos ejes es a conveniencia y los ejes \(y_i\) se agregan siguiendo el convencionalismo de la mano derecha (dedo índice corresponde al eje \(x\), dedo medio al eje \(y\) y el pulgar al eje \(z\)).</p>
<p>El sistema coordenado 3 lo podemos colocar a conveniencia, lo pondremos paralelo al sistema coordenado 2 pero con un desface en \(x\) para corresponda con el origen de un actuador que se le pondrá en otra ocasión.</p>

![BrazoEjes](https://i.ibb.co/BgVYm2d/Esquema-RRR.png)
<h5><center> Figura 2: Sistemas coordenados de cada articulación. </center></h5>
<h3>Tabla de Denavit Hartenberg</h3>
<p>Para el eslabón 1 tenemos que la distancia desde la intersección del eje \(x_1\) y \(z_0\) hasta el origen \(O_1\) a lo largo de \(x_1\) es cero, por lo que \(a_1=0\). El ángulo desde \(z_0\) hasta \(z_1\) medido sobre \(x_1\) es \(\pi/2\) o \(90^\circ\) por lo que \(\alpha_1=\pi/2\). La distancia desde \(z_0\) hasta la intersección del eje \(z_0\) con \(x_1\) es \(0\) por lo que \(d_1=0\). Finalmente, el ángulo desde \(x_0\)hasta \(x_1\) medido en el eje \(z_0\) es \(\theta_1\).</p>
<p>Para el eslabón 2 tenemos que la distancia desde la intersección del eje \(x_2\) y \(z_1\) hasta el origen \(O_2\) a lo largo de \(x_2\) es la longitud del eslabón y la nombraremos \(a_2\). El eje \(z_1\) y el eje \(z_2\)son paralelos. por lo que \(\alpha_2=0\). La distancia desde \(z_1\) hasta la intersección del eje \(z_1\) con \(x_2\) es \(0 \) por lo que \(d_2=0\). Finalmente, el ángulo desde \(x_1\) hasta \(x_2\) medido en el eje \(z_1\) es \(\theta_2\).</p>
<p>Para el eslabón 3 tenemos que la distancia desde la intersección del eje \(x_3\) y \(z_2\) hasta el origen \(O_3\)a lo largo de \(x_3\) es la longitud del eslabón y la nombraremos \(a_3\). El eje \(z_2 \) y el eje \(z_3\) son paralelos. por lo que \(\alpha_3=0\). La distancia desde \(z_2\) hasta la intersección del eje \(z_2\) con \(x_3\) es \(0 \)por lo que \(d_3=0\). Finalmente, el ángulo desde \(x_2\) hasta \(x_3\) medido en el eje \(z_2\) es \(\theta_3\).</p>
<p>Con esto en mente, definimos la siguiente tabla con los parámetros de Denavit Hartenberg:</p>

<p>| Eslabón | <p>\(a_i \)</p>| <p>\(\alpha_i \)</p> | <p>\(d_i \)</p>| <p>\(\theta_i \)</p>|
|:-------:|:-----:|:-----------:|:-----:|:----------:|
|    1    |  <p>\(0 \)</p> |  <p>\(\pi/2 \)</p>   |  <p>\(0 \)</p> | <p>\(\theta_1 \)</p>|
|    2    | <p>\(a_2 \)</p>|     <p>\(0 \)</p>    |  <p>\(0 \)</p> | <p>\(\theta_2 \)</p>|
|    3    | <p>\(a_3 \)</p>|     <p>\(0 \)</p>    |  <p>\(0 \)</p> | <p>\(\theta_3 \)</p>|</p>

<p>| Eslabón | \(a_i \)| \(\alpha_i \) | \(d_i \)| \(\theta_i \)|
|:-------:|:-----:|:-----------:|:-----:|:----------:|
|    1    |  \(0 \) |  \(\pi/2 \)   |  \(0 \) | \(\theta_1 \)|
|    2    | \(a_2 \)|     \(0 \)    |  \(0 \) | \(\theta_2 \)|
|    3    | \(a_3 \)|     \(0 \)    |  \(0 \) | \(\theta_3 \)|</p>

<h3>Modelo cinemático directo</h3>
<p>Con los parámetros de Denavit Hartenberg identificados, tenemos las siguientes matrices de transformación homogénea:</p>
$$
A_1^0 =\left[ \begin{array}{cccc}
\cos\theta_1 & 0 &  \sin\theta_1 & 0\\
\sin\theta_1 & 0 & -\cos\theta_1 & 0\\
     0      & 1 &       0      & 0\\
     0      & 0 &       0      & 1
\end{array} \right]
$$
$$
A_2^0 =\left[ \begin{array}{cccc}
\cos\theta_2 & -\sin\theta_2 &  0 & a_2\cos\theta_2\\
\sin\theta_2 &  \cos\theta_2 &  0 & a_2\sin\theta_2\\
      0      &        0      &  1 &       0\\
      0      &        0      &  0 & 1
\end{array} \right]
$$
$$
A_3^0 =\left[ \begin{array}{cccc}
\cos\theta_3 & -\sin\theta_3 &  0 & a_3\cos\theta_3\\
\sin\theta_3 &  \cos\theta_3 &  0 & a_3\sin\theta_3\\
      0      &       0       &  1 &       0\\
      0      &       0       &  0 &       1
\end{array} \right]
$$
De aquí se sigue la matriz de transformación que va de 0 a 3 es:
$$
T_3^0=\left[\begin{array}{cccc} \cos\left(\theta _{2}+\theta _{3}\right)\,\cos\left(\theta _{1}\right) & -\sin\left(\theta _{2}+\theta _{3}\right)\,\cos\left(\theta _{1}\right) & \sin\left(\theta _{1}\right) & \cos\left(\theta _{1}\right)\,\left(a_{3}\,\cos\left(\theta _{2}+\theta _{3}\right)+a_{2}\,\cos\left(\theta _{2}\right)\right)\\ \cos\left(\theta _{2}+\theta _{3}\right)\,\sin\left(\theta _{1}\right) & -\sin\left(\theta _{2}+\theta _{3}\right)\,\sin\left(\theta _{1}\right) & -\cos\left(\theta _{1}\right) & \sin\left(\theta _{1}\right)\,\left(a_{3}\,\cos\left(\theta _{2}+\theta _{3}\right)+a_{2}\,\cos\left(\theta _{2}\right)\right)\\ \sin\left(\theta _{2}+\theta _{3}\right) & \cos\left(\theta _{2}+\theta _{3}\right) & 0 & a_{3}\,\sin\left(\theta _{2}+\theta _{3}\right)+a_{2}\,\sin\left(\theta _{2}\right)\\ 0 & 0 & 0 & 1 \end{array}\right]
$$
Esta matriz representa el modelo cinemático directo de nuestro robot, para entenderla mejor, representamos a \(T_3^0 \)de la siguiente forma:
$$
T_3^0 =\left[ \begin{array}{cccc}
      n      &       s       &  a &       d\\
      0      &       0       &  0 &       1
\end{array} \right]
$$
donde \(n = [n_x,n_y,n_z]^T\), \(s = [s_x,s_y,s_z]^T\), \(a = [a_x,a_y,a_z]^T\) y \(d = [d_x,d_y,d_z]^T\).
La posición del origen del tercer marco de referencia \(O_3\) para los ángulos \(\theta_1,\theta_2,\theta_3\)nos las da el vector \(d\), las componentes del eje \(x_3\) en los ejes de \(O_0\) nos las da el vector \(n\), las componentes del eje \(y_3\) en los ejes de \(O_0\) nos las da el vector \(s\) y las componentes del eje \(z_3\) en los ejes de \(O_0\) nos las da el vector \(a\).

</body>