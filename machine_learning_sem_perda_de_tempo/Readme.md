# Machine Learning sem Perda de Tempo

## About me

Eduardo Bonet
Generalista
Senior Machine Learning Engineer & Product Lead - MLOps @ Gitlab

## Problema

Machine Learning virou moda, todo mundo quer implementar, ninguém sabe como, produtos morrem no protótipo, e todo o dinheiro investido é perdido

## Causa principal?

Má de comunicação entre o time de ML com usuários e o resto da empresa.

## Solução 

- Antecipar as perguntas difíceis, para que elas guiem o desenvolvimento do projeto.
- Alinhar expectativas com todos envolvidos no projeto
- Não começar projetos fadados a fracassar

## Como chegar lá?

## Primeiro, quando considerar Machine Learning?

### Métricas bem definidas

Um modelo de Machine Learning é uma função que otimiza parâmetros com relação a um objetivo

Não existe ML sem métricas

### Dados de boa qualidade para o problema em questão

Data Science começa com Data Engineering

Produtos de ML funcionam melhor em empresas que já possuem uma cultura forte de decisões em cima de dados.

### A aplicação permite que erros aconteçam

Plausibilidade de Erro (FP, FN tradeoff)

## Definir o significado de sucesso

- Qualquer projeto precisa resolver um problema real de algum usuário
- Suponha que você já resolveu o problema, o que mudou no mundo real?
- Você consegue quantificar essa mudança em métricas?
- Escolha uma métrica para otimizar, outras para validar (Goodheart's Law)

- [Um bom artigo sobre como extrair métricas](https://towardsdatascience.com/seven-steps-to-set-goals-and-pick-metrics-for-customers-613283570521)

### Definir o significado de sucesso: Sistema de Recomendação

#### Problemas do Usuário

- Usuário não consegue achar o produto que deseja
- Usuário passa muito tempo procurando algo
- A maior parte dos produtos no catálogo não é visto por ninguém

#### Problema Resolvido
- Se o número de produtos é infinito, o usuário não precisa buscar nada, o produto sabe automaticamente o que o usuário quer.
- Se o número de produtos é infinito, o resultado final é que o usuário já comprou tudo o que queria, e qualquer nova 
    recomendação será uma recomendação inútil.


O que mudou no mundo onde o problema foi resolvido?
- Usuário passa menos tempo buscando um produto
- Todos os produtos no catálogo interessam a algum usuário, e são oferecidos

#### Possíveis Evidências de Sucesso
- Aumento de vendas
- Diminuição do número de buscas para usuários que completaram uma transação
- Aumento do número de produtos únicos vendidos

### A Lei de Goodheart

> Toda métrica quando vira um objetivo deixa de ser uma boa métrica

- Adicioar mais métricas de validação
- Rotacionar objetivos
- Constantemente analisar pontos cegos das métricas

Exemplo: 

O que aconteceUma Online Travel Agency usando número de bookings como métrica principal?

## Como o Modelo vai ser utilizado?

O melhor modelo e ML do mundo é inútil se não sair do Jupyter Notebook.

É necessário em como o usuário vai consumir o resultado do modelo desde o início, visto que
isso influencia fortemente a escolha do modelo.

Algumas perguntas a serem feitas:

- É necessário explicar o por quê cada predição foi feita?
- Em que momento a predição é feita? Quais os dados estão disponíveis no momento da predição?
- Qual o tempo de resposta necessário para uma predição?
- A predição é feita no aparelho do usuário, ou no servidor, ou em um microcontrolador?

## Existe governança dos Dados?

Machine Learning não existe sem dados. Existe alguma processo de governança de dados na empresa? 
Como é o estado do Data Lake? 

## Precisa mesmo de Machine Learning? 

### Por que não usar Machine Learning?

Usar Machine Learning como solução para um problema envolve uma série de custos escondidos

- Mão de obra escassa e cara
- Colocar um modelo em produção requer arquitetura especializada (Model Registry, 
Pipelines para transformação de dados e treinamento de modelos, monitoramento de predições, etc)
- Modelos de Machine Learning tem data de validade: com o tempo as predições vão ficando piores, 
aumentando o custo de manutenção.
- Altamente exploratório, difícil de definir deadlines
- Difícil colocar a primeira versão online rápido para iterar com o usuário 

### Alternativa: comece com um sistema simples, sem ML

Em vez de usar um sistema de ML, use um sistema com regras ou heuristicas

Vantagens:
- Iteração rápida para descobrir o que o usuário realmente quer
- Ajuda a coletar dados rapidamente para criar um modelo melhor
- Ajuda a definir melhor as métricas de negócio
- Talvez no final das contas nem precisa evoluir para um sistema de ML

### Sobre débito técnico

Usar a heurística pode ser considerado um debito técnico, acelerando o avanço a curto prazo às 
custas do avanço a longo prazo. Conforme comportamentos mais complexos são adicionados à heurís
tica
Geralmente sempre vai ser mais simples iterar e aumentar a heurística pra acrescentar 
um comportamento mais complexo. Vai ficando cada vez mais difícil 

### Exemplos

Para implementar um sistema recomendador, recomendar os produtos mais comuns em cada categoria, evoluindo a
definição de categoria.

## Minimum Viable Accuracy

Minimum Viable Accuracy é o resultado mínimo em termos de métricas de Machine Learning que a solução deve obter 
para atender as expectativas impostas. Acurácia aqui é usado para representar qualquer outra métrica que seja 
melhor adaptado ao problema (precisão, MSE, F1)?

### Exemplo: Sistema de Recomendação

- Business consideraria o projeto um sucesso se houvesse um aumento de R$200.000 no retorno mensal, somado a 
    um aumento de número de produtos comprados por cada usuário (mas eles não conseguem definir examente quanto)
- Cada venda média traz R$70. O produto deveria adicionar 3000 transações mensais
- Supondo que o número de usuários não vai aumentar, 

Indo além: E se o business quiser o sistema de recomendação para atrair o número de usuários? Sistemas de 
    recomendação não funcionam tão bem quando não existem dados sobre o usuário, como lidar com as 

### Alguns comentários

- Não se apegue ao valor definido pelo MVA, ele vai mudar com o tempo e conforme ideias vão se
    se cristalizando
- O MVA não é uma ferramenta para educar o business sobre Machine Learning (embora ajude a 
    definir expectativas), é uma ferramenta para educar o time de Machine Learning sobre
    business
- A maior vantagem de explorar o MVA não é o valor em si, mas os processo de criação. Ao definir
    o MVA, o time precisa trabalhar com o business para definir as métricas, as expectativas,
    as peculiaridades do sistema.  