# MVP_Frederico_Gribaudi_Sprint_engenharia_de_dados

# Sumário

1. [Objetivo](#objetivo)
2. [Coleta dos dados](#coleta-dos-dados)
3. [Modelagem](#modelagem)
4. [Catálogo de dados](#catálogo-de-dados)
5. [ETL tabela de artilheiros](#etl-tabela-de-artilheiros)
6. [ETL tabela dos campeonatos](#etl-tabela-dos-campeonatos)
7. [Análise da qualidade dos dados de artilharia importados](#análise-da-qualidade-dos-dados-de-artilharia-importados)
8. [Análise da qualidade dos dados dos campeonatos importados](#análise-da-qualidade-dos-dados-dos-campeonatos-importados)
9. [Respondendo as perguntas sobre artilharia](#respondendo-as-perguntas-sobre-artilharia)
10. [Respondendo as perguntas sobre campeonatos](#respondendo-as-perguntas-sobre-campeonatos)

# Objetivo

O objetivo deste trabalho é descobrir qual o melhor time e os melhores jogadores do campeonato italiano desde 2010. Para isso será necessário encontrar algum database ou extrair informações de sites especializados em estatísticas de futebol.

# Perguntas a serem respondidas:

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

# Coleta dos dados

Não encontrei nenhuma base de dados gratuita com as informações que precisava, portanto optei por extrair essas informações de um site com excelente reputação pela veracidade de suas estatísticas o www.transfermarkt.com.

Essa busca foi dividida em duas partes, a primeira buscando as tabelas com as estatísticas dos jogadores, nessa etapa vi que não existiam todas as estatísticas para uma análise de diferentes tipos de jogadores, a única característica de livre acesso era a quantidade de gols feitos e as próprias tabelas de classificação de cada temporada, como ambas tinham URLs diferentes, precisei criar dois scripts em python para fazer o web scraping.

# Modelagem

A ideia original era de criar um modelo estrela no qual eu teria uma tabela com os dados dos times que seriam chaves primárias de outras tabelas com informações de partidas, campeonatos, jogadores e valor de mercado. Durante o web scraping, infelizmente, não consegui extrair da tabela de artilheiros as colunas nacionalidade e time, logo tive que adotar outra modelagem, e optei por seguir com 2 tabelas flat que não se comunicam, uma com artilheiros e outras com campeonatos.

# Catálogo de dados

As propriedades estão divididas da seguinte forma:

![image](https://github.com/user-attachments/assets/3ec5428a-2666-407d-8e78-064645fcd6d5)

# ETL tabela de artilheiros

O ETL dos dados dos artilheiros consistiu em extrair as informações do site transfermarkt, importar os arquivos CSV no databricks community, ajustar as propriedades definindo o tipo de entrada de cada propriedade, renomeando a coluna posição para "posicao" para evitar problemas com algumas consultas SQL feitas e adicionando a coluna temporada em cada tabela, que é de extrema importância visto que o script usado apenas nomeou os diferentes arquivos CSV.

# ETL tabela dos campeonatos

O ETL dos dados dos artilheiros consistiu em extrair as informações do site transfermarkt, importar os arquivos CSV no databricks community, ajustar as propriedades definindo o tipo de entrada de cada propriedade, renomeando a coluna vitórias para "vitorias" para evitar problemas com algumas consultas SQL feitas e adicionando a coluna temporada em cada tabela, que é de extrema importância visto que o script usado apenas nomeou os diferentes arquivos CSV.

# Análise da qualidade dos dados de artilharia importados

Nesta seção foram testados os valores mínimos e máximos da tabela, nenhum erro foi encontrado nos seguintes testes:
-Checar se existem jogadores repetidos na mesma temporada
-Checar partidas maiores que 38 ou negativas 
-Checar gols negativos
-Checar valores nulos
-Checar valores iguais a 0

# Análise da qualidade dos dados dos campeonatos importados

Nesta seção foram testados os valores mínimos e máximos da tabela, nenhum erro foi encontrado nos seguintes testes:
-Checar se existem posições negativas ou maiores que 20
-Checar times repetidos na mesma temporada
-Checar se existem jogos diferentes de 38
-Checar se existem vitórias negativas ou maiores do que 38
-Checar se existem empates negativas ou maiores do que 38
-Checar se existem derrotas negativas ou maiores do que 38
-Checar gols pro negativos
-Checar gols contra negativos
-Checar se existem pontos negativos ou maiores que 114
-Checar se existem valores nulos

# Qual o melhor jogador do período?

O maior artilheiro do período foi Ciro Immobile, com 201 gols, uma média de gols de 0,57 gols por partida e tendo sido o artilheiro em 4 temporadas. As respostas das demais perguntas podem ser encontradas no notebook.

# Qual o melhor time do período?
O melhor time do período foi a Juventus, acumulando um total de pontos de 1149, ganhando 9 títulos no período, com um percentual de vitórias de 66%, com a defesa menos vazada dentre os times que participaram de todas as temporadas, foi campeã invicta em 2011-2012, teve a maior quantidade de pontos, 102 na temporada 2013-2014.  As respostas das demais perguntas podem ser encontradas no notebook.
