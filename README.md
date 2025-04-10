# MVP_Frederico_Gribaudi_Sprint_engenharia_de_dados

---

## 📚 Sumário

1. [Objetivo](##1-objetivo)  
2. [Coleta dos dados](##2-coleta-dos-dados)  
3. [Modelagem](#3-modelagem)  
4. [Catálogo de dados](#4-catálogo-de-dados)  
5. [ETL tabela de artilheiros](#5-etl-tabela-de-artilheiros)  
6. [ETL tabela dos campeonatos](#6-etl-tabela-dos-campeonatos)  
7. [Análise da qualidade dos dados de artilharia importados](#7-análise-da-qualidade-dos-dados-de-artilharia-importados)  
8. [Análise da qualidade dos dados dos campeonatos importados](#8-análise-da-qualidade-dos-dados-dos-campeonatos-importados)  
9. [Respondendo as perguntas sobre artilharia](#9-respondendo-as-perguntas-sobre-artilharia)  
10. [Conclusão sobre o melhor jogador](#10-conclusão-sobre-o-melhor-jogador)  
11. [Respondendo as perguntas sobre campeonatos](#11-respondendo-as-perguntas-sobre-campeonatos)  
12. [Conclusão sobre o melhor time](#12-conclusão-sobre-o-melhor-time)  
13. [Autoavaliação](#13-autoavaliação)
---
## 1. 🎯 Objetivo

O objetivo deste trabalho é descobrir qual o melhor time e os melhores jogadores do campeonato italiano desde 2010. Para isso será necessário encontrar algum database ou extrair informações de sites especializados em estatísticas de futebol.

**Perguntas a serem respondidas:**

- Quais os jogadores com mais gols?
- Quais os artilheiros de cada temporada?
- Qual jogador foi mais vezes artilheiro?
- Qual a maior média total de gols por partida?
- Qual a maior média de gols por partida por temporada?
- Qual o maior artilheiro por posição?
- Qual o artilheiro de cada time por temporada?
- Quem foi o maior marcador italiano?
- Quem foi o maior marcador brasileiro?
- Qual time com maior quantidade de pontos?
- Qual time com maior % de vitórias?
- Qual time que fez mais gols?
- Qual time sofreu menos gols?
- Qual o maior saldo de gols numa temporada?
- Quais os campeões de cada temporada?
- Teve algum campeão que ganhou todos os jogos na temporada?
- Teve algum campeão invicto?
- Qual time ganhou com a maior quantidade de pontos em uma temporada?
- Qual time mais vezes campeão?
---
## 2. 📥 Coleta dos dados

Não foi possível encontrar nenhuma base de dados gratuita com as informações necessárias, portanto optei por extrair essas informações de um site com excelente reputação pela veracidade de suas estatísticas o www.transfermarkt.com.

Essa busca foi dividida em duas partes, a primeira buscando as tabelas com as estatísticas dos jogadores, nessa etapa vi que não existiam todas as estatísticas para uma análise de diferentes tipos de jogadores, a única característica de livre acesso era a quantidade de gols feitos e as próprias tabelas de classificação de cada temporada, como ambas tinham URLs diferentes, foi necessário criar dois scripts em python para fazer o web scraping.

Segue abaixo o link do notebook original, onde todo o trabalho foi realizado:
https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/1741214472309159/3928396909524781/4214321683267064/latest.html

---
## 3. 🧱 Modelagem

A ideia original era de criar um modelo estrela no qual eu teria uma tabela com os dados dos times que seriam chaves primárias de outras tabelas com informações de partidas, campeonatos, jogadores e valor de mercado. Durante o web scraping, infelizmente, não consegui extrair da tabela de artilheiros as colunas nacionalidade e time, logo tive que adotar outra modelagem, e optei por seguir com 2 tabelas flat que não se comunicam, uma com artilheiros e outra com campeonatos.

---
## 4. 📊 Catálogo de dados

As propriedades estão divididas da seguinte forma:

![image](https://github.com/user-attachments/assets/6290e01f-76a7-4de2-8eda-1ec3871233b2)


---
## 5. ⚙️ ETL tabela de artilheiros

O ETL dos dados dos artilheiros consistiu em:

  1. extrair as informações do site transfermarkt
  2. importar os arquivos CSV no databricks community
  3. ajustar as propriedades definindo o tipo de entrada de cada propriedade
  4. renomear a coluna posição para "posicao" para evitar problemas com algumas consultas SQL feitas
  5. adicionar a coluna temporada em cada tabela, que é de extrema importância visto que o script usado apenas nomeou os diferentes arquivos CSV.

---
## 5. ⚙️ ETL tabela de artilheiros

O ETL dos dados dos campeonatos consistiu em:
1. extrair as informações do site transfermarkt
2. importar os arquivos CSV no databricks community
3. ajustar as propriedades definindo o tipo de entrada de cada propriedade
4. renomear a coluna vitórias para "vitorias" para evitar problemas com algumas consultas SQL feitas
5. adicionar a coluna temporada em cada tabela, que é de extrema importância visto que o script usado apenas nomeou os diferentes arquivos CSV.

---
## 7. 🧪 Análise da qualidade dos dados de artilharia importados

Nesta seção foram testados os valores mínimos e máximos da tabela, nenhum erro foi encontrado nos seguintes testes:
- Checar se existem jogadores repetidos na mesma temporada
- Checar partidas maiores que 38 ou negativas 
- Checar gols negativos
- Checar valores nulos
- Checar valores iguais a 0

---
## 8. 🧪 Análise da qualidade dos dados dos campeonatos importados

Nesta seção foram testados os valores mínimos e máximos da tabela, nenhum erro foi encontrado nos seguintes testes:
- Checar se existem posições negativas ou maiores que 20
- Checar times repetidos na mesma temporada
- Checar se existem jogos diferentes de 38
- Checar se existem vitórias negativas ou maiores do que 38
- Checar se existem empates negativos ou maiores do que 38
- Checar se existem derrotas negativas ou maiores do que 38
- Checar gols pro negativos
- Checar gols contra negativos
- Checar se existem pontos negativos ou maiores que 114
- Checar se existem valores nulos

---
## 9. ❓ Respondendo as perguntas sobre artilharia

## **Quais os jogadores com mais gols?**

A lista abaixo está apresentando os 20 jogadores que fizeram mais gols somando todas as temporadas:
![image](https://github.com/user-attachments/assets/57c0c818-59ba-4447-9020-6c93e06a14cf)

## **Quais os artilheiros de cada temporada?**

Segue abaixo a lista de artilharia de cada temporada:

![image](https://github.com/user-attachments/assets/ffc7e85d-e77c-4af0-9cdf-c204b7096ae2)

## **Qual jogador foi mais vezes artilheiro?**

**Ciro Immobile** foi artilheiro em **4** campeonatos nesse período em **2013-2014**, **2017-2018**, **2019-2020** e **2021-2022**.

## **Qual a maior média total de gols por partida?**

**Cristiano Ronaldo** foi o jogador com maior média de gols, levando em consideração um número mínimo de 10 partidas jogadas, para evitar que existam outliers.

## **Qual a maior média de gols por partida por temporada?**

Segue abaixo a lista de maiores médias de gols:

![image](https://github.com/user-attachments/assets/761866e1-60d6-423a-b79a-7c77cbdf9849)

Podemos ver com esse resultado que nem sempre o artilheiro da temporada teve a maior média de gols.

## **Qual o maior artilheiro por posição?**

Segue abaixo a lista de artilheiros por posição:

![image](https://github.com/user-attachments/assets/a11ead6f-da2d-4ca8-92a7-47dcd4ed244a)

## **Qual o artilheiro de cada time por temporada?**

Essa pergunta não pode ser respondida, pois durante a extração dos dados de jogadores do site transfermarkt, não foi possível criar uma coluna pois os nomes dos times eram apenas imagens e não uma string para ser copiada.

## **Quem foi o maior artilheiro italiano?**

Essa pergunta não pode ser respondida, pois durante a extração dos dados de jogadores do site transfermarkt, não foi possível criar uma coluna pois as nacionalidades eram apenas imagens e não uma string para ser copiada, além de existirem jogadores com mais de uma nacionalidade.

## **Quem foi o maior artilheiro brasileiro?**

Essa pergunta não pode ser respondida, pois durante a extração dos dados de jogadores do site transfermarkt, não foi possível criar uma coluna pois as nacionalidades eram apenas imagens e não uma string para ser copiada, além de existirem jogadores com mais de uma nacionalidade.

---
## 10. 🏅 Conclusão sobre o melhor jogador
O maior artilheiro do período foi **Ciro Immobile**, com **201** gols, uma média de **0,57** gols por partida e tendo sido o artilheiro em **4** temporadas. 

---
## 11. ❓ Respondendo as perguntas sobre campeonatos
## **Qual time com maior quantidade de pontos?**

A **Juventus** fez um total de **1149** pontos no perído, com um total de 350 vitórias e 109 empates, importante levar em consideração que a quantidade de pontos não representa o que seria normalmente esperado, visto que 350*3 + 109 = **1159**. Na temporada **2022-2023** houve uma penalização de 10 pontos, devido a problemas financeiros em seus balanços.

## **Qual time com maior % de vitórias?**

A **Juventus** teve um percentual de vitórias de **65.78%** no período.

## **Qual time que fez mais gols?**

O **Napoli** fez **1023** gols.

## **Qual time sofreu menos gols?**

A **Juventus** sofreu **421** gols no período, o resultado inicial trouxe outro time, porém reparei que a quantidade de partidas era muito diferente, visto que um time que caiu para a segunda divisão e nunca mais subiu, pode de fato ter sofrido menos gols, portanto apliquei um novo filtro, para levar em consideração apenas os times que participaram de todas as temporadas, ou seja 532 jogos.

## **Qual o maior saldo de gols numa temporada?**

Na temporada **2023-2024** a **Inter** fez 89 gols e sofreu 22, representando um saldo de gols de **67**.

## **Quais os campeões de cada temporada?**

Segue abaixo a lista de campeões de cada temporada:

![image](https://github.com/user-attachments/assets/0ae16468-2951-4a15-81b2-6612f7e2c18e)


## **Teve algum campeão que ganhou todos os jogos na temporada?**

Não houve nenhum time que ganhou todos os jogos.

## **Teve algum campeão invicto?**

Na temporada **2011-2012** a **Juventus** foi campeã invícta, com 23 vitórias e 15 empates.

## **Qual time ganhou com a maior quantidade de pontos em uma temporada?**

Na temporada **2013-2014** a **Juventus** ganhou 33 partidas e empatou 3, totalizando **102** pontos.

## **Qual time mais vezes campeão?**

A **Juventus** foi campeã 9 vezes, de forma consecutiva, desde 2011-2012 até 2019-2020.

---
## 12. 🥇 Conclusão sobre o melhor time

O melhor time do período foi a **Juventus**, acumulando um total de pontos de 1149, ganhando 9 títulos no período, com um percentual de vitórias de aproximadamente 66%, com a defesa menos vazada dentre os times que participaram de todas as temporadas, foi campeã invicta em 2011-2012, teve a maior quantidade de pontos, 102 na temporada 2013-2014. As respostas das demais perguntas podem ser encontradas no notebook.

---
## 13. 🧠 Autoavaliação

Estou extremamente satisfeito com a realização desse trabalho, apesar de não ter conseguido fazer tudo que tinha imaginado inicialmente. Tive que me dedicar bastante para conseguir obter os resultados, com muitos estudos, ajuda dos colegas no Discord, dos professores nos encontros síncronos, para conseguir entregar um trabalho que dentro das minhas capacidades, tinha um grau de desafio alto.
