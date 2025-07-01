# Desafio de Dados - Liven 🎲

## Introdução ▶️

O Campeonato Brasileiro é a principal competição de futebol do Brasil e o torneio de futebol mais visto do continente americano.

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/pt/4/42/Campeonato_Brasileiro_S%C3%A9rie_A_logo.png" alt="Descrição da imagem" width="300"/>
</p>

No campeonato, 20 times disputam o primeiro lugar na tabela, em 38 rodadas de turno e returno. Cada vitória, empate e derrota valem 3, 1 e 0 pontos, respectivamente. A equipe com maior quantidade de pontos ao final das 38 rodadas se consagra campeã daquele ano. Em caso de empate de pontos, os critérios de desempate são saldo de gols, número de gols pró, confronto direto, número de cartões vermelhos e amarelos, e, por fim, sorteio, nesta ordem. O Brasileirão é central no futebol brasileiro, pois as posições determinam os times que disputarão a Libertadores e Sul-Americana e os times rebaixados para a série B. A seguinte regra é aplicada de acordo com o regulamento:

- As 20 equipes se enfrentam em turno e returno e, ao fim das 38 rodadas, o time com o maior número de pontos fica com o título brasileiro, enquanto os quatro últimos são rebaixados para a Série B.
- Em caso de igualdade na pontuação, são critérios de desempate: 1) mais vitórias, 2) melhor saldo de gols, 3) mais gols pró, 4) confronto direto, 5) menos cartões vermelhos, 6) menos cartões amarelos, 7) sorteio.
- Os quatro primeiros entram na fase de grupos da Libertadores, enquanto o quinto e o sexto colocados disputam as fases prévias da Libertadores.
- Caso o campeão da Libertadores e/ou o campeão da Copa do Brasil e/ou o campeão da Sul-Americana estejam no G-6, a equipe seguinte garante vaga na competição continental.

Um exemplo da tabela [final de classificação do Brasileirão Série A de 2024](https://ge.globo.com/futebol/brasileirao-serie-a/) pode ser encontrado no site do Globo Esporte.

## A base de dados 🗂️

A única fonte de dados será um conjunto de arquivos csv disponibilizados no Github original:  
https://github.com/adaoduque/Brasileirao_Dataset/

Os dados do campeonato são coletados desde 2003, mas estatísticas, número de cartões e detalhamento de gols passaram a ser coletado apenas mais recentemente. Portanto, temos 4 bases de dados csv para este desafio, unidas pelo id da partida:

1. **Campeonato Brasileiro Full**: Cada registro contém dados como o **ID** da partida, **rodada**, **data** e **hora**, times **mandante** e **visitante**, suas respectivas **formações táticas** e **técnicos**, além do **vencedor** da partida, o **nome da arena**, o placar de ambos os times (**mandante_Placar** e **visitante_Placar**) e os estados de origem dos clubes (**mandante_Estado** e **visitante_Estado**

2. **Campeonato Brasileiro Estatísticas**: contém estatísticas detalhadas por time em cada partida do Campeonato Brasileiro. As colunas incluem **partida_id** (identificador da partida), **rodada**, **clube**, além de dados como **chutes**, **chutes_no_alvo**, **posse_de_bola**, **passes**, **precisao_passes**, **faltas**, **cartao_amarelo**, **cartao_vermelho**, **impedimentos** e **escanteios**

3. **Campeonato Brasileiro Cartões**: contém informações sobre cada cartão recebido por jogador durante as partidas do Campeonato Brasileiro de Futebol. Cada registro representa um cartão, com colunas como **partida_id** (identificador da partida), **rodada**, **clube** (time do jogador), **cartao** (tipo do cartão: amarelo ou vermelho), **atleta** (nome do jogador), **num_camisa** (número da camisa), **posicao** (posição do jogador) e **minuto** (momento em que o cartão foi recebido na partida).

4. **Campeonato Brasileiro Gols**: contém os gols marcados no Campeonato Brasileiro, com cada linha representando um gol específico. As colunas incluem: **partida_id** (identificador da partida), **rodada** (número da rodada), **clube** (time que marcou), **atleta** (jogador que marcou o gol), **minuto** (momento exato do gol na partida) e **tipo_de_gol** (classificação do gol, como pênalti, gol de falta, etc).

## Desafio 🚩

Você trabalha na área de dados em um grande clube de futebol brasileiro e foram entregues diversas bases de dados, cada uma contendo diferentes aspectos das competições, como resultados de partidas, estatísticas detalhadas e registros de eventos durante os jogos.
Seu papel é organizar e integrar essas bases, ajustando os dados para garantir consistência e qualidade. Com as informações consolidadas, sua missão é realizar análises que extraiam insights relevantes sobre as características do campeonato e as estratégias mais sólidas para vencer.

### Atividade 1

Para garantir a qualidade da análise, sua tarefa é:

- [x] Identificar e remover todas as linhas (registros) que não tenham correspondência completa nas quatro bases para a mesma partida, mantendo apenas os registros de partidas que estão presentes nas três tabelas.

- [x] Ajustar os dados para que apenas essas partidas comuns sejam mantidas em cada base, garantindo a consistência entre estatísticas, cartões e gols.

- [x] Escolha a melhor maneira de lidar com tipos e valores NaN, realizar limpezas necessárias e remover informações irrelevantes.

### Atividade 2

- [x] Dada a tabela `full` com informações gerais das partidas e a tabela `estatisticas` com estatísticas por time em cada partida, crie uma nova tabela que una essas informações de modo que cada linha represente uma partida e contenha, além dos dados gerais, as estatísticas do time mandante e do time visitante em colunas separadas, identificadas por prefixos distintos para cada equipe. Lide com colunas que são comuns a ambos os times e serão duplicadas, como rodada da partida.
  - **Exemplo**: Imagine que você tem duas linhas na tabela de estatísticas, ambas referentes à mesma partida. A primeira linha traz os dados do Figueirense e a segunda do Santos. Cada linha representa as estatísticas de um dos times nessa partida, como número de chutes, posse de bola, faltas, escanteios, entre outras.
  - Ao realizar a tarefa proposta, essas duas linhas seriam combinadas em uma única linha na nova tabela. Essa linha única manteria as informações gerais da partida (como o ID do jogo e os times envolvidos) e incluiria as estatísticas dos dois times, diferenciadas por prefixos. Por exemplo, a quantidade de chutes do Figueirense apareceria como `mandante_chutes` e a do Santos como `visitante_chutes`. O mesmo valeria para as outras estatísticas, como posse de bola, faltas e cartões.

### Atividade 3

Com base nessa base de dados unificada, a equipe quer entender **quais fatores realmente influenciam nos resultados dos jogos**, para apoiar decisões futuras para o treinamento da equipe. Com base nisso, duas perguntas foram feitas inicialmente:

- [x] **A posse de bola influencia no resultado?**  
       A equipe quer saber se há alguma relação clara entre o percentual de posse de bola de um time e sua probabilidade de vencer uma partida.

- [x] **A vantagem de jogar em casa (mandante) é real?**  
       Eles querem verificar, com dados, se os times mandantes realmente vencem mais partidas ou se essa vantagem é superestimada
- [ ] Fique a vontade para encontrar **outros padrões ou fatores relevantes** que possam influenciar o resultado dos jogos, como número de chutes, faltas cometidas, cartões, número de passes ou qualquer característica que considerar relevante.

**Utilize SQL para realizar pelo menos uma das consultas.**
**Utilize Pandas para realizar pelo menos uma das consultas.**

## Entrega 💼

Para o desenvolvimento da atividade, utilizar a linguagem Python. Espera-se como entregáveis:

- O código-fonte do desafio. Sugerimos escrever utilizando arquivo Jupyter Notebook (ipynb).
- Comentários e documentações relevantes são muito bem vindas.

Bom trabalho!
