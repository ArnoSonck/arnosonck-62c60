---
title: Have you ever wanted to know somethig that can not be measure? Use an observer.
date: '2021-11-09'
author: content/data/team/arno-sonck.yaml
categories:
  - content/data/categories/general.yaml
tags:
  - Stackbit
  - JAMstack
image: https://i.ibb.co/RztzLKK/pexels-photo-1342460.jpg
image_alt: Post 3 placeholder image
excerpt: >-
  An observer is an algorithm that can estimate parameters that can not be measured from the measurable parameters. - Foto of Vitaly Vlasov from Pexels
seo:
  title: Have you ever wanted to know somethig that can not be measure? Use an observer.
  description: 'An observer is an algorithm that can estimate parameters that can not be measured from the measurable parameters.'
  extra:
    - name: 'og:type'
      value: article
      keyName: property
    - name: 'og:title'
      value: Cur Ipse Pythagoras Et Aegyptum Lustravit
      keyName: property
    - name: 'og:description'
      value: 'Quis est, qui non oderit libidinosam, protervam adolescentiam'
      keyName: property
    - name: 'og:image'
      value: images/3.png
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Cur Ipse Pythagoras Et Aegyptum Lustravit
    - name: 'twitter:description'
      value: 'Quis est, qui non oderit libidinosam, protervam adolescentiam'
    - name: 'twitter:image'
      value: images/3.png
      relativeUrl: true
layout: post
---

While controlling a system, such as a bioreactor or an electric motor, it is common to need the measures of different parameters, such as the concentration of a product or the current of the stator. Sometimes these parameters are not available, usually for the lack of measure instruments or the instruments are very expensive. Fortunately, there are systems whose parameters can be known by measuring others parameters.

The algorithm that can stimate unmeasurable parameters is called an observer. Observers study is a branch of automatic control theory and there are many methodologies. Here I will only talk about the main idea of observers.

## Luenberger observer

It was proposed by [David G. Luenberger](https://en.wikipedia.org/wiki/David_Luenberger), a mathematical scientist and professor in the department of Management Science and Engineering at Stanford University. The main idea of this algorithm is to make a mathematical copy of the original system, so we know all their parameters all the time. These parameters are different from the original system, so we need a parameter of correction, this parameter depends on the parameters that can be measured from the original system.

Its main advantage is that it is simple but, its main disadvantage is that it needs a copy of the original system, that's mean, to perfectly know your original system. A small change can lead to different results. Fortunately, this is a widely used methodology so there are a lot of variants that can handle many issues.

## An apologise for control engineers

This article was meant for people that don’t know about control theory so I named the state as parameters to try to make it more understandable. If you know another way to explain this without changing concepts names please let me know.

