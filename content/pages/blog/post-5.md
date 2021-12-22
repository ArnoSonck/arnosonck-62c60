---
title: >-
  Los 5 algoritmos de agrupación en clústeres que los científicos de datos deben
  conocer
date: '2021-12-22'
author: content/data/team/gordon-norman.yaml
categories:
  - content/data/categories/tutorials.yaml
  - content/data/categories/statistics.yaml
  - content/data/categories/category-yr12d3ueu.json
  - content/data/categories/category-m6ok6iwle.json
tags:
  - Stackbit
  - Netlify
image: images/5.png
image_alt: Post 5 placeholder image
excerpt: >-
  Estne, quaeso, inquam, sitienti in bibendo voluptas? Iam in altera
  philosophiae parte. Quem Tiberina descensio festo illo die tanto gaudio
  affecit, quanto.
seo:
  title: Amet Nulla Facilisi Morbi Tempus
  description: 'Estne, quaeso, inquam, sitienti in bibendo voluptas'
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
Este post es una traducción del siguiente [artículo](https://towardsdatascience.com/the-5-clustering-algorithms-data-scientists-need-to-know-a36d136ef68).
Los nombres de los algoritmos los manejare en inglés.
Todos los creditos van a su creador George Seif.

La agrupación en clústeres es una técnica de aprendizaje automático que implica la agrupación de puntos de datos. Dado un conjunto de puntos de datos, podemos usar un algoritmo de agrupamiento para clasificar cada punto de datos en un grupo específico. En teoría, los puntos de datos que están en el mismo grupo deberían tener propiedades o características similares, mientras que los puntos de datos en diferentes grupos deberían tener propiedades o características muy diferentes. La agrupación en clústeres es un método de aprendizaje no supervisado y es una técnica común para el análisis de datos estadísticos que se utiliza en muchos campos.

En Ciencia de datos (Data Science), podemos usar el análisis de agrupamiento para obtener información valiosa de nuestros datos al ver en qué grupos se encuentran los puntos de datos cuando aplicamos un algoritmo de agrupamiento. Hoy, veremos 5 algoritmos de agrupación en clústeres populares que los científicos de datos deben conocer y sus pros y contras.

## K-means Clustering (k-medias)

K-Means es probablemente el algoritmo de agrupación en clústeres más conocido. Se enseña en muchas clases de introducción a la ciencia de datos y al aprendizaje automático. ¡Es fácil de entender e implementar en código! Consulte el gráfico a continuación para ver una ilustración.


![](https://miro.medium.com/max/480/1\*KrcZK0xYgTa4qFrVr0fO2w.gif)

1.  Para comenzar, primero seleccionamos una cantidad de clases o grupos para usar e inicializamos aleatoriamente sus respectivos puntos centrales. Para calcular la cantidad de clases que se deben usar, es bueno echar un vistazo rápido a los datos e intentar identificar cualquier agrupación distinta. Los puntos centrales son vectores de la misma longitud que cada punto vector de datos y son las "X" en el gráfico de arriba.

2.  Cada punto de datos se clasifica calculando la distancia entre ese punto y el centro de cada grupo, y luego clasificando el punto para que esté en el grupo cuyo centro está más cerca de él.

3.  Con base en estos puntos clasificados, recalculamos el centro del grupo tomando la media de todos los vectores del grupo.

4.  Repita estos pasos para un número determinado de iteraciones o hasta que los centros del grupo no cambien mucho entre iteraciones. También puede optar por inicializar aleatoriamente los centros de grupo varias veces y luego seleccionar la ejecución que parece que proporcionó los mejores resultados.
