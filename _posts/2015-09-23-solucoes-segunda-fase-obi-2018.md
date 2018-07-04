---
layout: post
title:  "2º Fase OBI Nivel Senior - Soluções"
tags: [olimpíada de informática, 2018, problemset, analise]
categories: analise
author: Misael
---

No dia 21 de Julho ocorreu a 2º Fase da OBI, com a participação de 16 alunos da UFG.

Foram 3 exercícios, um clássico em grafos, um problema que envolvia raciocínio lógico mas sem muita programação e um problema que pode ser feito com uma programação dinâmica clássica.

## 1ª Problema - Fuga

Descrição: Dada uma tabela com algumas células bloqueadas, encontre o menor caminho entre uma célula origem e uma célula destino. Considere que pode-se andar entre duas celulas que compartilham um lado.

Questão clássica de BFS(Busca em Largura) em Grafos. Pode conferir mais 
[aqui][busca-em-profundidade].

Vou tentar explicar a solução de uma maneira que todos entendam.

Crie uma matriz dist[MAXN][MAXN] em que MAXN é a largura/altura maxima da tabela. No começo preencha a tabela com um valor especial, pode ser -1.
Vamos usar uma estrutura de dados chamada fila, queue em c++. Basicamente você adiciona o elemento no final e primeiro elemento adicionado, como em uma fila da vida real. Referência do uso em c++ [aqui][fila-cpp].
Criaremos uma fila de par de inteiros que representarão os ultimos elementos atingidos pela busca, coordenadas x e y.

queue< pair<int, int> > fila;

De início apenas sabemos a distancia da célula origem, então adicionamos ela na fila e atualizamos a distância.
fila.push(make_pair(x0, y0));
dist[x0][y0] = 0;

Então repetiremos o seguinte processo enquanto a fila não estiver vazia
Pega-se primeiro elemento da fila
Pra cada célula vizinha não bloqueada verifica se não foi atingida ainda, ou seja, dist[x_vizinho][y_vizinho] = -1
Caso esta não tenha sido atingida, atualize a distância( como distancia da célula atual + 1) e adicione na fila.

Assim teremos a distância da célula origem para todas outras células

Código:


## 2ª Problema - Elevador

Descrição: Dados n pesos e um elevador com duas cabines ligada por uma roldana( quando uma cabine sobre a outra desce ), com a seguinte característica, ao movimentar o elevador a diferença de peso entre as cabines deve ser no máximo 8, para não haver desequilibrio. É possivel levar todos pesos para o andar de cima?

Solução: Adicione mais um elemento de peso 0, ordene o vetor de pesos, se a diferença absoluta de cada dois pesos consecutivos for no máximo 8 então é possível levar todos pesos para cima.

## 3ª Problema - Elevador

Descrição: Dado n inteiros, alguns marcados e outros não, encontre o subvetor de soma máxima com no mínimo L e no máximo H elementos marcados.

Pense em um problema mais fácil, onde todos elementos são marcados, nesse caso bastaria checar todos subvetores, já que o tamanho do subvetor é no maximo H( <= 20 ). 

Uma adaptação a esse problema criar um vetor apenas com os elementos marcados. Pra cada elemento marcado armazenar também a soma máxima terminando nesse elemento e iniciando nesse elemento, considerando apenas elementos não marcados, armazenar também a soma de todos elementos não marcados entre cada dois elementos marcados.

Assim pode-se testar, pra cada dois elementos no novo vetor com distancia no máximo H e no minimo L, qual a melhor soma entre eles, que será a soma máxima terminando no primeiro elemento, a soma entre cada dois elementos, e a soma máxima terminando no último elemento.
[busca-em-profundidade]:
http://www.codcad.com/lesson/38
[fila-cpp]: http://www.cplusplus.com/reference/queue/queue
