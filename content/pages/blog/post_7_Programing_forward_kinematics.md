---
title: >-
  Matriz de transformación en Python
date: '2022-08-17'
author: content/data/team/arno-sonck.yaml
categories:
  - content/data/categories/robotics.yaml
  - content/data/categories/espanol.yaml
  - content/data/categories/python.yaml
tags:
  - Robotica
  - Español
  - Python
image: https://i.ibb.co/6XQqKW2/RRRPy.png
image_alt: Robot angular
excerpt: Muestro el uso de Closures creando matrices de transformación usadas en robótica.
seo:
  title: >-
    Ejemplo de modelado de un robot
  description: >-
    Muestro el uso de Closures creando matrices de transformación usadas en robótica.
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: 'Muestro el uso de Closures creando matrices de transformación usadas en robótica'
      keyName: property
    - name: 'og:description'
      value: 'Muestro el uso de Closures creando matrices de transformación usadas en robótica'
      keyName: property
    - name: 'og:image'
      value: https://i.ibb.co/6XQqKW2/RRRPy.png
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: 'Muestro el uso de Closures creando matrices de transformación usadas en robótica'
    - name: 'twitter:description'
      value: 'Muestro el uso de Closures creando matrices de transformación usadas en robótica'
    - name: 'twitter:image'
      value: https://i.ibb.co/6XQqKW2/RRRPy.png
      relativeUrl: true
layout: post
---

<head>
<title>Closures y matrices de transformación</title>
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>
</head>
<body>

<p>Una matriz de transformación la podemos visualizar como como una función lleva los valores escalares de las articulaciones (ya sean ángulos o desplazamientos) a cuatro vectores. Los primeros tres corresponden a las componentes de los ejes \(x_i\), \(y_i\) y \(z_i\) en los ejes \(x_j\), \(y_j\) y \(z_j\) y el cuarto a las coordenadas del origen \(O_i\) en el sitema \(j\).</p>

<p><b>Nota:</b> los prefijos \(i\) y \(j\) significa que son sistemas de coordenadas diferentes.</p>

<p>Si seguimos la metodología de Denavit Hartenberg entonces podemos generar nuestra matriz de transformación tomando como entrada los valores \([a_i\), \(\alpha_i\), \(d_i\), \(\theta_i]\) del eslabón \(i\) y podemos determinar los cuatro vectores que describimos anteriormente de forma independiente para facilitar la lectura del código y al final concatenarlos en una matriz.</p>

<p><b>Nota:</b> es importante asegurarse que se retorne una matriz y no un array para que la multiplicación sea multiplicación de matrices y no elemento a elemento. Esto también permite usar otras fuciones de numpy que requieren matrices como argumentos de entrada.</p>

<p>Usare un Closure, que es como una función que devuelve otra función, como matriz de transformación. Si bien no la podremos visualizar con variables simbolicas, la podemos visualizar para cada conjunto de valores de las articulaciones que le suministremos.</p>

<h3>La función queda así:</h3>

<p><b>Nota:</b> me hubiera gustado usar tipado estático pero no encontre un módulo de Python que me permitiera usarlo con variables de tipo matriz.</p>

<iframe title="Embedded cell output" src="https://embed.deepnote.com/5f5f6565-4d6c-4d28-8c45-3653a1d6be8e/1baf8374-1197-495a-98cc-c04d1455d077/b7b6f01d17094ac9a61920277273b1da?height=1181" height="1181" width=100%></iframe>

<h3>Ejemplo</h3>

<p>Supondremos que los eslabones \(2\) y \(3\) del robot tienen una longitud entre ajes \(z\) de \(30\) \(cm\)  dandonos los suguientes parametros de Denavit Hartenberg</p>

<iframe title="Embedded cell output" src="https://embed.deepnote.com/5f5f6565-4d6c-4d28-8c45-3653a1d6be8e/1baf8374-1197-495a-98cc-c04d1455d077/4a531be714fd4487b1f54ec445160044?height=170" height="170" width=100%></iframe>

<p>Con estas listas creamos las matrices de transformación, que para nosotros seran funciones que al recibir un angulo nos dara la orientación y posición de un eslabón en relación al eslabón anterior.</p>

<iframe title="Embedded cell output" src="https://embed.deepnote.com/5f5f6565-4d6c-4d28-8c45-3653a1d6be8e/1baf8374-1197-495a-98cc-c04d1455d077/5a9c6442bba64345bf06bdfee7f7c0f0?height=134" height="134" width=100%></iframe>

<p>Por ejemplo, el primer eslabón no puede modificar desplazamiento en ningún eje, pero si su orientación en relación al sistema de referencia \(0\). Por ejmeplo, para \(\theta=0\), los ejes \(x\) siguen alineados, el eje \(y_1\) es paralelo al eje \(z_0\) y el eje \(z_1\) es paralelo y contrario a \(y_0\).</p>

<iframe title="Embedded cell output" src="https://embed.deepnote.com/5f5f6565-4d6c-4d28-8c45-3653a1d6be8e/1baf8374-1197-495a-98cc-c04d1455d077/dbd6707bf21a4dfbaa12ad92bbd07199?height=263.9375" height="263.9375" width=100%></iframe>

<p>Para obtener las coordenadas del marco coordemado \(O_3\) multiplicamos las tres matrices, por ejemplo, si todos los ángulos son \(0^\circ\) entonces el origen \(O_3\) esta a \(60 cm\) sobre el eje x, y su orientación sería la misma que en el ejemplo anterior.</p>

<iframe title="Embedded cell output" src="https://embed.deepnote.com/5f5f6565-4d6c-4d28-8c45-3653a1d6be8e/1baf8374-1197-495a-98cc-c04d1455d077/6ad488ed696e428d9204a4ad8562a927?height=746.75" height="746.75" width=100%></iframe>

<p>Nos enfocaremos en la posición, es decir, el vector $d$ de las matrices de transformación.</p>

<iframe title="Embedded cell output" src="https://embed.deepnote.com/5f5f6565-4d6c-4d28-8c45-3653a1d6be8e/1baf8374-1197-495a-98cc-c04d1455d077/685cb0b721544e169f01ef1658e6cbc9?height=314" height="314" width=100%></iframe>

<iframe title="Embedded cell output" src="https://embed.deepnote.com/5f5f6565-4d6c-4d28-8c45-3653a1d6be8e/1baf8374-1197-495a-98cc-c04d1455d077/2dff4d0a9d9640909b4b022f659cc387?height=658.1875" height="658.1875" width=100%></iframe>

</body>