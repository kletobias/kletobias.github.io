---
title: 'math_test'
subtitle: 'How To Code The Optimization Process'
date: 2022-06-18 06:00:00
description: 'Stochastic Gradient Descent:<br>The Training Loop From Scratch'
accent_color: '#08877d'
featured_image: '838338477938@+-38829429482.jpg' 
gallery_images:
  - '838338477938@+-38829429482.jpg'
use_math: true
---

# Questionnaire Chapter 04


\[\begin{bmatrix} w_1 \\ w_2 \end{bmatrix} := \begin{bmatrix} w_1 \\ w_2 \end{bmatrix} - \eta \begin{bmatrix} \frac{\partial}{\partial w_1} (w_1 + w_2 x_i - y_i)^2 \\ \frac{\partial}{\partial w_2} (w_1 + w_2 x_i - y_i)^2 \end{bmatrix} = \begin{bmatrix} w_1 \\ w_2 \end{bmatrix} - \eta \begin{bmatrix} 2 (w_1 + w_2 x_i - y_i) \\ 2 x_i(w_1 + w_2 x_i - y_i) \end{bmatrix}\] 
