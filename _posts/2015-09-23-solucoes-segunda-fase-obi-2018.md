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
Vamos usar uma estrutura de dados chamada fila, queue em c++. Basicamente na fila sempre adiciona-se o elemento no final e retira o primeiro elemento que entrou na fila, como em uma fila da vida real. Referência do uso em c++ [aqui][fila-cpp].
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
A solução desse problema usa programação dinâmica, é extremamente recomendado que se leia sobre esse método de solução antes

Pense em um problema mais fácil, onde todos elementos são marcados, nesse caso bastaria checar todos subvetores, já que o tamanho do subvetor é no maximo H( <= 20 ). 

Crie 3 vetores adicionais, pref[MAXN], suf[MAXN], sum[MAXN]. pref[i] vai armazenar a maior soma possivel de um subvetor terminando em i, que passe apenas por elementos não marcados, exceto i( que pode ser marcado ). Da mesma forma suf[i], mas com o subvetor começando em i. sum[i] vai armazenar a soma de todos elementos de i até chegar no primeiro elemento marcado, exceto i

Uma formula pra calcular os valores desses vetores é( da mesma forma que o algoritmo Kadane faz) :
pref[i] = max(v[i], (pref[i-1] se mark[i-1] == 0) + v[i])  // (pode-se escolher continuar o prefixo do ultimo elemento ou iniciar a partir desse elemento
suf[i] = max(v[i], (suf[i+1] se mark[i+1] == 0) + v[i])
sum[i] = (sum[i+1] se mark[i+1] == 0) + v[i])
pode-se fazer um for com i crescendo pra calcular pref e um for com i decrescendo pra calcular suf e sum. Isso é o que chamamdos de programação dinâmica.

Adicione o indice de todos elementos com mark[i] == 1 em um vector v1
Assim basta fazer dois loops pra checar todos subvetores de v1, com tamanho máximo H.
Pra cada subvetor, com elementos e0, e1, e2, ..., e(j-1), pegue a seguinte soma,
soma = pref[e0] + sum[e0] + sum[e1] + sum[e2] + ... + sum[e(j-2)] + suf[e(j-1)]
O subvetor que tiver menor soma é a resposta

Temos que checar também caso L = 0, as respostas nos casos em que não se usa nenhum elemento marcado, pode-se fazer isso com Kadane

[busca-em-profundidade]: http://www.codcad.com/lesson/38
[fila-cpp]: http://www.cplusplus.com/reference/queue/queue
