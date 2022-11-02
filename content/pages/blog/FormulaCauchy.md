---
title: Cómo resolver una ecuación diferencial lineal con un retardo fijo en el estado
date: '2022-11-02'
author: content/data/team/arno-sonck.yaml
categories:
  - content/data/categories/delayed.yaml
tags:
  - Delayed Systems
  - Delayed Diferential Equations
  - Kharitonov
  - Science
image: 'https://i.ibb.co/TgVc60L/Delayed.png'
image_alt: Image created in Matlab
excerpt: "Una ecuación diferencial que depende de valores pasados para conoer su derivada actual puede ser temible y usualmente se trabaja con transformada de Laplace, aquí presento la metodología desarrollada por Vladimir Kharitonov para resolverlas en el dominio del tiempo."
seo:
  title: Formula de Cauchy
  description: >-
    Una ecuación diferencial que depende de valores pasados para conoer su derivada actual puede ser temible y usualmente se trabaja con transformada de Laplace, aquí presento la metodología desarrollada por Vladimir Kharitonov para resolverlas en el dominio del tiempo.
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: Formula de Cauchy
      keyName: property
    - name: 'og:description'
      value: Formula de Cauchy
      keyName: property
    - name: 'og:image'
      value: 'https://i.ibb.co/TgVc60L/Delayed.png'
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Formula de Cauchy
    - name: 'twitter:description'
      value: Formula de Cauchy
    - name: 'twitter:image'
      value: 'https://i.ibb.co/TgVc60L/Delayed.png'
      relativeUrl: true
layout: post
---

# Preliminares

## Sistema a trabajar

Trabajaremos con sistemas con un solo retardo en el estado:

$$
\dot{x}(t)=A_0x(t)+A_1x(t-h), \quad x(t)\in \mathbb{R}^n, \quad t,h\ge0, \quad A_0, A_1 \in \mathbb{R}^{n\times n}
$$

(1)

Cuya condición inicial está dada por una función: $\varphi:[-h,0]\to \mathbb{R}^n$ y pertenece al espacio de funciones continuas a pedazos definidas en el segmento $[-h,0]$ definido por $PC([-h,0],\mathbb{R}^n)$.

Note que la función de la condición inicial y la solución de la ecuación (1) deben ser iguales para $t \in [-h,0]$, esto es:

$$
x(\theta,\varphi) = \varphi(\theta), \quad \varphi \in [-h,0]
$$

La solución en este intervalo la denotaremos por $x_t(\varphi)$.

## Norma Uniforme

Para los vectores se usará la norma Euclidiana, para la matrices la norma inducida para matrices y para las funciones pertenecientes al al **espacio de funciones continuas a pedazos** definidas en el segmento $[-h,0]$ definido por $PC([-h,0],\mathbb{R}^n)$ usaremos la norma uniforme:

$$
\|\varphi\|_h = \sup_{\theta\in[-h,0]}\|\varphi(\theta)\|
$$

## Matriz Fundamental

Se dice que la matriz $K(t)$  es la matriz fundamental del sistema (1) si satisface la siguiente ecuación matricial:

$$
\frac{d}{dt}K(t) = K(t)A_0 + K(t-h)A_1, \quad t\ge0
$$

y $K(t) = 0_{n\times n}$ para $t<0$, $K(0) = I_{n\times n}$. Aquí  $0_{n\times n}$ y $I_{n\times n}$ son una matriz de puros ceros y la matriz identidad respectivamente de dimensión $n\times n$.

### Nota

La matriz fundamental también satisface la igualdad matricial:

$$
\frac{d}{dt}K(t) = A_0K(t) + A_1K(t-h), \quad t\ge0
$$

Esto no significa que $K(t)$ sea conmutativa, esto ocurre porque el espectro de Laplace de ambas igualdades es el mismo.

Para el primer sistema tenemos:

$$
sK(s) = K(s)A_0+K(s)e^{-sh}A_1
$$

Su polinomio característico es:

$$
sI - A_0-e^{-sh}A_1
$$

Para el segundo tenemos

$$
sK(s) = A_0K(s)+A_1K(s)e^{-sh}
$$

Su polinomio característico es:

$$
Is - A_0 - A_1e^{-sh}
$$

Y como $e^{-sh}$ es un escalar y por lo tanto conmuta, el espectro de ambas igualdades es equivalente.

## Fórmula de Cauchy

### Teorema 1

Dada una función inicial $\varphi \in PC([-h,0],\mathbb{R}^n)$, se satisface la siguiente igualdad:

$$
x(t,\varphi) = K(t)\varphi(0)+\int_{-h}^0K(t-\theta-h)A_1\varphi(\theta)d\theta, \quad t\ge0
$$

Esta expresión es llamada **Fórmula de Cauchy**

### Demostración

La demostración es similar al  método del factor integrante, solo agregaremos el retardo y observe lo que pasa:

Para $t>0$ supondremos que existe $\xi \in (0,t)$ por lo que se satisface:

$$
\frac{\partial}{\partial\xi}\left[K(t-\xi)x(\xi,\varphi)\right] = \left[\frac{\partial}{\partial\xi} K(t-\xi)\right]x(\xi,\varphi)+K(t-\xi)\left[\frac{\partial}{\partial\xi}x(\xi,\varphi)\right]
$$

Aplicando regla de la cadena en el primer término del lado derecho tenemos:

$$
\frac{\partial}{\partial\xi}\left[K(t-\xi)x(\xi,\varphi)\right] = -\left[K(t-\xi)A_0 + K(t-\xi-h)A_1\right]x(\xi,\varphi)+K\left(t-\xi\right)\left[A_0x(\xi,\varphi)+A_1x(\xi-h,\varphi)\right]
$$

$$
\frac{\partial}{\partial\xi}\left[K(t-\xi)x(\xi,\varphi)\right] = -\textcolor{blue}{K(t-\xi)A_0x(\xi,\varphi)} - K(t-\xi-h)A_1x(\xi,\varphi)+\textcolor{blue}{K\left(t-\xi\right)A_0x(\xi,\varphi)}+K(t-\xi)A_1x(\xi-h,\varphi)
$$

Agrupando términos tenemos:

$$
\frac{\partial}{\partial\xi}\left[K(t-\xi)x(\xi,\varphi)\right] = - K(t-\xi-h)A_1x(\xi,\varphi)+K(t-\xi)A_1x(\xi-h,\varphi)
$$

E integrando de $0$ a $t$ obtenemos:

$$
\int_0^t d\left[K\left(t-\xi\right)x\left(\xi,\varphi\right)\right] = - \int_0^tK\left(t-\xi-h\right)A_1x\left(\xi,\varphi\right)d\xi+\int_0^tK\left(t-\xi\right)A_1x\left(\xi-h,\varphi\right)d\xi
$$

Recordemos que $K(t) = I$ para $t = 0$ y  que $x(\theta,\varphi) = \varphi(\theta)$ para $\theta \in [-h,0]$, en particular $x(\theta,\varphi) = \varphi(\theta)$, por lo que el lado izquirdo de la ecuación anterior queda:

$$
\int_0^t d\left[K\left(t-\xi\right)x\left(\xi,\varphi\right)\right] = K\left(0\right)x\left(t,\varphi\right)-K\left(t\right)x\left(0,\varphi\right) = x\left(t,\varphi\right)-K\left(t\right)\varphi\left(0\right)
$$

Por lo que se cumple:

$$
x\left(t,\varphi\right)-K\left(t\right)\varphi\left(0\right) = - \textcolor{blue}{\int_0^tK\left(t-\xi-h\right)A_1x\left(\xi,\varphi\right)d\xi}+\int_0^tK\left(t-\xi\right)A_1x\left(\xi-h,\varphi\right)d\xi
$$

Si definimos a $\theta = \xi - h$ podemos transformar el segundo término integral del lado derecho de la siguiente manera:

$$
\int_0^tK\left(t-\xi\right)A_1x\left(\xi-h,\varphi\right)d\xi = \int_{-h}^{t-h}K\left(t-\theta-h\right)A_1x\left(\theta,\varphi\right)d\theta
$$

Como $K(t)=0$ para $t<0$, podemos extender esta integral hasta $t$.

Para entender esto mejor evalúe $K()$ en límite superior, esto da $K(t-t+h-h)=K(0) = I,$ si el límite superior crece entonces $K()$ estaría siendo evaluada con valores negativos y para esos valores vale $0$.

$$
\int_0^tK\left(t-\xi\right)A_1x\left(\xi-h,\varphi\right)d\xi = \int_{-h}^{t}K\left(t-\theta-h\right)A_1x\left(\theta,\varphi\right)d\theta
$$

Esta integral puede separarse en dos intervalos, de $[-h,0)$ y de $[0,t]$ dando:

$$
\int_0^tK\left(t-\xi\right)A_1x\left(\xi-h,\varphi\right)d\xi = \int_{-h}^{0}K\left(t-\theta-h\right)A_1x\left(\theta,\varphi\right)d\theta + \textcolor{blue}{\int_{0}^{t}K\left(t-\theta-h\right)A_1x\left(\theta,\varphi\right)d\theta}
$$

Note que obtenemos el primer término integral del lado derecho pero con signo contrario (resaltado en color azul), por lo que podemos simplificar la ecuación a:

$$
x\left(t,\varphi\right)-K\left(t\right)\varphi\left(0\right) = \int_{-h}^{0}K\left(t-\theta-h\right)A_1x\left(\theta,\varphi\right)d\theta
$$

Recordando que para  que $x(\theta,\varphi) = \varphi(\theta)$ para $\theta \in [-h,0]$ y despejando obtenemos la fórmula de Cauchy:

$$
x\left(t,\varphi\right) = K\left(t\right)\varphi\left(0\right) + \int_{-h}^{0}K\left(t-\theta-h\right)A_1\varphi\left(\theta\right)d\theta
$$

