---
title: >-
  Modelado de Robot Cartesiano
date: '2022-08-23'
author: content/data/team/arno-sonck.yaml
categories:
  - content/data/categories/robotics.yaml
  - content/data/categories/espanol.yaml
tags:
  - Robotica
  - Español
image: https://i.ibb.co/ZJ2xzGk/PPP.png
image_alt: Robot cartesiano
excerpt: Muestro el desarrollo del modelo cinemático directo y dinámico de un robot prismático.
seo:
  title: >-
    Ejemplo de modelado de un robot angular
  description: >-
    Muestro el desarrollo del modelo cinemático directo y dinámico de un robot prismático.
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: 'Muestro el desarrollo del modelo cinemático directo y dinámico de un robot prismático'
      keyName: property
    - name: 'og:description'
      value: 'Muestro el desarrollo del modelo cinemático directo y dinámico de un robot prismático'
      keyName: property
    - name: 'og:image'
      value: https://i.ibb.co/ZJ2xzGk/PPP.png
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: 'Muestro el desarrollo del modelo cinemático directo y dinámico de un robot prismático'
    - name: 'twitter:description'
      value: 'Muestro el desarrollo del modelo cinemático directo y dinámico de un robot prismático'
    - name: 'twitter:image'
      value: https://i.ibb.co/ZJ2xzGk/PPP.png
      relativeUrl: true
layout: post
---

<head>
<title>Robot Cartesiano</title>
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>
</head>
<body>

<p>El robot cartesiano consta de tres articulaciones prismáticas alineadas a cada eje del plano cartesiano.</p>

![RobotPPP](https://i.ibb.co/ZJ2xzGk/PPP.png)
<h5><center> Figura 1: Configuración cartesiana, el eslabón 1 esta indicado en color rojo, el 2 en color verde y el 3 en azúl. </center></h5>

<h3> Parametros del robot </h3>
<p>Seguiremos el convencionalismo  de Denavit Hartenberg que fue presentado por James Denavit y Richard S. Hartenberg en 1955 y nos permite hacer el mapeo de articulación en articulación de forma sistemática.</p>

<h4> Definiendo ejes </h4>
<p>Comenzamos con los ejes \(z\) de cada marco de referencia, el eje \(x_0\) va alineado con el eje de desplazamiento de la primera articulación, el eje \(x_1\) va alineado con el eje de desplazamiento de la segunda articulación y el eje \(x_2\) va alineado con el eje de desplazamiento de la tercera articulación. El sistema de coordenadas \(3\) lo definiremos al final.</p>

<p>El eje \(x_0\) lo podemos colocar donde queramos sobre el eje \(z_0 \), lo pondremos n un costado. Como los ejes \(z_0\) y \(z_1\) se intersectan, colocaremos el eje \(x_1\) en dicha intersección. Como \(z_1\) y \(z_2\) se intersectan, colocaremos el eje \(x_2\) en dicha intersección.</p>

<p>Hasta el momento hemos definido la dirección de los ejes \(z_i\) y \(x_i\), podemos determinar el origen \(O_i\) de cada sistema como el punto donde se intersectan estos ejes, el sentido de estos ejes es a conveniencia y los ejes \(y_i\) se agregan siguiendo el convencionalismo de la mano derecha (dedo índice corresponde al eje \(x\) , dedo medio al eje \(y\) y el pulgar al eje \(z\) ).</p>

<p>El sistema coordenado \(3\) lo podemos colocar a conveniencia, lo pondremos en la cara frontal del ultimo eslabón.</p>

![BrazoEjes](https://i.ibb.co/chwVXbR/Esquema-PPP.png)
<h5><center> Figura 2: Sistemas coordenados de cada articulación. </center></h5>

<h3>Tabla de Denavit Hartenberg</h3>
<p>Para el eslabón 1 tenemos que la distancia desde la intersección del eje \(x_1\) y \(z_0\) hasta el origen \(O_1\) a lo largo de \(x_1\) es cero, por lo que \(a_1=0\). El ángulo desde \(z_0\) hasta \(z_1\) medido sobre \(x_1\) es \(-\pi/2\) o \(-90^\circ\) por lo que \(\alpha_1=-\pi/2\). Como es una articulación prismática, \(d_1\) es variable. Finalmente, el ángulo desde \(x_0\) hasta \(x_1\) medido en el eje \(z_0\) es \(0\) por lo tanto \(\theta_2=0\).</p>

<p>Para el eslabón 2 tenemos que la distancia desde la intersección del eje \(x_2\) y \(z_1\) hasta el origen \(O_2\) a lo largo de \(x_2\) es \(0\). El ángulo desde \(z_1\) hasta \(z_2\) medido sobre \(x_2\) es \(\pi/2\) o \(90^\circ\) por lo que \(\alpha_1=\pi/2\). Como es una articulación prismática, \(d_2\) es variable. Finalmente, el ángulo desde \(x_1\) hasta \(x_2\) medido en el eje \(z_1\) es \(\pi/2\) o \(90^\circ\) por lo tanto \(\theta_2=\pi/2\).</p>

<p>Para el eslabón 3 tenemos que la distancia desde la intersección del eje \(x_3\) y \(z_2\) hasta el origen \(O_3\) a lo largo de \(x_3\) es cero. El ángulo desde \(z_2\) hasta \(z_3\) es cero. Como es una articulación prismática, \(d_1\) es variable. Finalmente, el ángulo desde \(x_2\) hasta \(x_3\) medido en el eje \(z_2\) es cero.</p>

<p>Con esto en mente, definimos la siguiente tabla con los parámetros de Denavit Hartenberg:</p>

<table>
  <tr>
    <th>Eslabón</th>
    <th>\(a_i\)</th>
    <th>\(\alpha_i\)</th>
    <th>\(d_i\)</th>
    <th>\(\theta_i\)</th>
  </tr>
  <tr>
    <td>1</td>
    <td>0</td>
    <td>\(-\pi/2\)</td>
    <td>\(d_1\)</td>
    <td>0</td>
  </tr>
  <tr>
    <td>2</td>
    <td>0</td>
    <td>\(\pi/2\)</td>
    <td>\(d_2\)</td>
    <td>\(\pi/2\)</td>
  </tr>
  <tr>
    <td>3</td>
    <td>0</td>
    <td>0</td>
    <td>\(d_3\)</td>
    <td>0</td>
  </tr>
</table>

<h3> Modelo cinemático directo </h3>

<p>Con los parámetros de Denavit Hartenberg identificados, tenemos las siguientes matrices de transformación homogénea:</p>
$$
A_1^0 =\left[ \begin{array}{cccc}
     1 &  0 & 0 & 0\\
     0 &  0 & 1 & 0\\
     0 &  1 & 0 & d_1\\
     0 &  0 & 0 & 1
\end{array} \right]
$$
$$
A_2^1 =\left[ \begin{array}{cccc}
     0 &  0 & 1 & 0\\
     1 &  0 & 0 & 0\\
     0 & -1 & 0 & d_2\\
     0 &  0 & 0 & 1
\end{array} \right]
$$
$$
A_3^2 =\left[ \begin{array}{cccc}
     1 &  0 & 0 & 0\\
     0 &  1 & 0 & 0\\
     0 &  0 & 1 & d_3\\
     0 &  0 & 0 & 1
\end{array} \right]
$$

<p>De aquí se sigue la matriz de transformación que va de 0 a 3 es:</p>

$$
T_3^0=\left[\begin{array}{cccc} 0 & 0 & 1 & d_{3}\\ 0 & -1 & 0 & d_{2}\\ 1 & 0 & 0 & d_{1}\\ 0 & 0 & 0 & 1 \end{array}\right]
$$

<p>Esta matriz representa el modelo cinemático directo de nuestro robot, para entenderla mejor, representamos a \(T_3^0\) de la siguiente forma:</p>

$$
T_3^0 =\left[ \begin{array}{cccc}
      n      &       s       &  a &       d\\
      0      &       0       &  0 &       1
\end{array} \right]
$$

<p>donde \(n = [n_x,n_y,n_z]^T\), \(s = [s_x,s_y,s_z]^T\), \(a = [a_x,a_y,a_z]^T\) y \(d = [d_x,d_y,d_z]^T\).</p>

<p>La posición del origen del tercer marco de referencia ($O_3$) para los ángulos \((\theta_1,\theta_2,\theta_3)\) nos las da el vector \(d\), las componentes del eje \(x_3\) en los ejes de \(O_0\) nos las da el vector \(n\), las componentes del eje \(y_3\) en los ejes de \(O_0\) nos las da el vector \(s\) y las componentes del eje \(z_3\) en los ejes de \(O_0\) nos las da el vector \(a\).</p>

<h3>Modelo cinemático inverso</h3>

<p>Para esta configuración podemos obtener el modelo cinemático inverso directamente del vector \(d\) de la matriz de transformación, de aquí podemos deducir:</p>

$$
\begin{array}{ccc}
     x &  = & d_3\\
     y &  = & d_2\\
     z &  = & d_1
\end{array}
$$

<h3>Coordenadas generalizadas</h3>

<p>En este caso en particular los desplazamientos en los ejes del plano carteciano se relacionan directamente con los desplazamientos de las articulaciones y el control se hace sobre las articulaciones por lo que tenemos las siguientes coordenadas generalizadas:</p>

$$
\begin{array}{ccccc}
    q_3 & = & x &  = & d_3\\
    q_2 & = & y &  = & d_2\\
    q_1 & = & z &  = & d_1
\end{array}
$$

<p>Con estas coordenadas podemos realizar el control del robot.</p>

<h3>Modelo dinámico (por Euler Lagrange)</h3>

<p>El planteamiento de Euler Lagrande nos dice que:</p>

$$
\frac{d}{dt}\frac{\partial \mathcal{L}}{\partial\dot{q}}-\frac{\partial \mathcal{L}}{\partial q}=f
$$

<p>donde el Lagrangiano \(\mathcal{L}\) es la diferencia de la energía dinámica \(\mathcal{K}\) y la potencial \(\mathcal{P}\), esto es:</p>

$$
\mathcal{L} = \mathcal{K}-\mathcal{P}
$$ 

<h4>Energía dinámica</h4>

<p>La energía dinámica de cada eslabón esta dada por \(1/2 mv^2\) donde \(m\) es la masa del eslabón, \(v\) la velocidad lineal o \(\dot{q}\) del eslabón, de aquí se sigue:</p>

$$
\mathcal{K} = \frac{1}{2}m_1\dot{q}_1^2 + \frac{1}{2}m_2\dot{q}_2^2 + \frac{1}{2}m_3\dot{q}_3^2
$$

<h4>Energía potencial</h4>

<p>La energía potencial de cada eslabón esta dada por \(mgh\), donde \(m\) es la masa del elabón, \(g\)  es la gravedad y \(h\) la altura del centro de masa del eslabón al plano perpendicular al suelo de nuestro sistema de referencia cero (en nuestro caso es el plano \(x_0z_0\)), de aquí se sigue:</p>

$$
\mathcal{P} = 0 + m_2g(\beta_2+q_2) + m_3g(\beta_3+q_2)
$$

<p>donde \(\beta_2\) y \(\beta_3\) son constantes y representan un desface entre el centro de gravedad de los eslabones 2 y 3 y el origen del centro de sus respectivos sistemaa de coordenadas.</p>

<p><b>Nota:</b> La anergía potencial del primer eslabón es cero ya que su centro de masa esta sobre el plano \(x_0z_0\).</p>

<h4>Lagrangiano</h4>
<p>El Lagrangiano de nuestro sistema es:</p>

$$
\mathcal{L} = \frac{1}{2}m_1\dot{q}_1^2 + \frac{1}{2}m_2\dot{q}_2^2 + \frac{1}{2}m_3\dot{q}_3^2 - m_2g(\beta_2+q_2) - m_3g(\beta_3+q_2)
$$

<h3>Construyendo el modelo</h3>

<p>Primero calculamos \(\frac{\partial \mathcal{L}}{\partial\dot{q}}\), solo dejaremos los terminos que dependen de \(\dot{q}\) ya que los demas se volveran cero al derivar.</p>
$$
\frac{\partial \mathcal{L}}{\partial\dot{q}}=\begin{array}{c}
    \frac{\partial(\frac{1}{2}m_1\dot{q}_1^2 + \frac{1}{2}m_2\dot{q}_2^2 + \frac{1}{2}m_3\dot{q}_3^2)}{\partial \dot{q}_1} \\
    \frac{\partial(\frac{1}{2}m_1\dot{q}_1^2 + \frac{1}{2}m_2\dot{q}_2^2 + \frac{1}{2}m_3\dot{q}_3^2)}{\partial \dot{q}_2} \\
    \frac{\partial(\frac{1}{2}m_1\dot{q}_1^2 + \frac{1}{2}m_2\dot{q}_2^2 + \frac{1}{2}m_3\dot{q}_3^2)}{\partial \dot{q}_3}
\end{array} =\begin{array}{c}
    m_1 \dot{q}_1 \\
    m_2 \dot{q}_2 \\
    m_3 \dot{q}_3
\end{array}
$$

<p>De aquí calculamos directamente: \(\frac{d}{dt}\frac{\partial \mathcal{L}}{\partial\dot{q}}\):</p>

$$
\frac{d}{dt}\frac{\partial \mathcal{L}}{\partial\dot{q}} =\begin{array}{c}
    m_1 \ddot{q}_1 \\
    m_2 \ddot{q}_2 \\
    m_3 \ddot{q}_3
\end{array}
$$

<p>Para calcular \(\frac{\partial \mathcal{L}}{\partial q}\) solo usaremos los terminos de Lagrangiano que tengan \(q\) ya que los  demas se volveran cero al momento de derivar.</p>

$$
\frac{\partial \mathcal{L}}{\partial q}=\begin{array}{c}
    \frac{- m_2g(\beta_2+q_2) - m_3g(\beta_3+q_2)}{\partial q_1} \\
    \frac{- m_2g(\beta_2+q_2) - m_3g(\beta_3+q_2)}{\partial q_2} \\
    \frac{- m_2g(\beta_2+q_2) - m_3g(\beta_3+q_2)}{\partial q_3}
\end{array} =\begin{array}{c}
    0 \\
    -(m_2+m_3)g \\
    0
\end{array}
$$

<p>Por lo que nuestro modelo queda:</p>
$$
\begin{array}{c}
    m_1 \ddot{q}_1 \\
    m_2 \ddot{q}_2 \\
    m_3 \ddot{q}_3
\end{array} + \begin{array}{c}
    0 \\
    (m_2+m_3)g \\
    0
\end{array} = \begin{array}{c}
    f_1 \\
    f_2 \\
    f_3
\end{array}
$$

<p>Aquí se considera que los eslabones se controlar mediante las fuerzas \(f_1\), \(f_2\), y \(f_3\).</p>


</body>