# Machine Learning sem Perda de Tempo

## About me

Eduardo Bonet
Generalista
Senior Machine Learning Engineer & Product Lead - MLOps @ Gitlab

Essa apresentação é limitada pela minha experiência profissional, e o que apresentão é somente uma perspectiva a ser considerada.

## Problema

Machine Learning virou moda, todo mundo quer implementar, ninguém sabe como, produtos morrem no protótipo, e todo o dinheiro investido é perdido

## Como melhorar a comunição? 

- Antecipar as perguntas difíceis, para que elas guiem o desenvolvimento do projeto.
- Alinhar expectativas com todos envolvidos no projeto
- Não começar projetos fadados a fracassar

## Passo 1: O qu é Machine Learning

Machine Learning é um conjunto de algoritmos e modelos estatísticos para extrair informação de **dados** com um grau de incerteza.

Existem vários tipos diferentes de algoritmos, cada um atendendo problemas específicos, cada um trazendo pontos bons e ruins.

Em termos práticos: 


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

O que acontece quando uma Online Travel Agency usando número de reserva como métrica principal?

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
custas do avanço a longo prazo. Conforme comportamentos mais complexos são adicionados à 
heurística, o código fica mais complexo e mais difícil de ser modificado. Cabe ao time técnico 
definir com a liderança em que momento a heurística será transformada em um modelo.

### Exemplos

Para implementar um sistema recomendador, recomendar os produtos mais comuns em cada categoria, evoluindo a
definição de categoria.

## Métricas de negócio vs Métricas acadêmicas

Praticantes de Machine Learning estão acostumados a encarar os modelos com métricas "acadêmicas": precisão,
revocação, F1, AUC, etc

Porém, essas métricas nem sempre refletem em mudanças certas. 

### Exemplo: AUC vs Retorno esperado

Uma métrica comum para avaliar modelos de classificação é AUC (area under the curve), que avalia a relação
entre Falsos Positivos e Falsos Negativos ao longo de todas as escolhas de probabilidade de corte, sendo .5 para
um modelo que prediz classes aleatoriamente e 1 para um sistemas que predizem classes perfeitamente.

Porém, na prática, um valor para o corte vai ser definido e usado, e só é util saber o valor de retorno para 
aquele corte. Assumindo que o custo de FP é igual ao custo de FN, esse corte seria no ponto onde FP seria igual a FN.

Novamente, a realidade é a diferente, e os custos de erro tem valor diferente. Podemos melhorar estender essa ideia 
para escolhar o threshold como o ponto que maximiza 

$$ T  = argmax (Retorno TP)*TP(T) - (Custo de FP) * FP(T) - (Custo Médio de FN) * FN(T) $$

Note como a definição de sucesso muda completamente quando aplicada a cenários práticos.

## Minimum Viable Accuracy: De métricas Acadêmicas para Métricas de negçop

Minimum Viable Accuracy* é o resultado mínimo em termos de métricas de Machine Learning que a solução deve obter 
para alcançar a defininição de sucesso?

MVA é o resultado de transformar as expectativas de negócios em métricas que estamos mais acostumados a lidar 
durante o desenvolviment de modelos. É também uma forma de entender desde o começo se é possível atender as 
expectativas, ou se é um projeto fadado ao fracasso.

\* Acurácia aqui se refere a quaisquer métricas que sejam melhores adaptadas ao problema em questão

### Exemplo: Sistema de Recomendação

- Business consideraria o projeto um sucesso se houvesse um aumento de R$200.000 no retorno mensal, somado a 
    um aumento de número de produtos diferentes vendidos (mas eles não conseguem definir examente quanto)
- Cada venda média traz R$70. O produto deveria adicionar 3000 transações mensais
- Temos 5000 usuarios mensais, os quais são responsáveis por 10000 transações
- Supondo que o número de usuários não aumente, seria necessário que o sistema aumentasse o número de vendas
    em 30%.
- Assumindo que usemos métricas de recomendação, e assumindo que um usuário vê em média 5 produtos, esse 
aumento de 30% poderia ser traduzido a um aumento no MAP@5* de 30%.
- Supondo que tenham ocorrido 20.000 buscas, o MAP@5 precisa passar de 10.000/(5*20.000) = .1 para .13, que
seria nosso MVA

Geralmente, é possível implementar um protótipo rápido para verificar a fisibilidade do projeto. Dependendo
do caso, 1 ou 2 semanas é o suficiente para chegar em 70% do resultado final, e ter uma ideia melhor do que 
precisa ser feito para ir além. Com isso, fica mais fácil discutir expectativas com o business. Talvez 
R$200.000 seja muito difícil, mas R$100.000 seja alcançável, será que não seria o suficiente?

Indo além: E se o business quiser o sistema de recomendação para atrair o número de usuários? Sistemas de 
    recomendação não funcionam tão bem quando não existem dados sobre o usuário, como lidar com as 

\* MAP%K é a precisão média de acertos nas 5 primeiras recomendações para cada usuário

### Considerações sobre MVA

- É impossível chegar num valor exato para o MVA, basta chegar em um valor aproximado
- Normalmente, várias suposições são feitas no cálculo do MVA. Essas suposições devem ser
    testadas e atualizadas ao longo do tempo
- Não se apegue ao valor definido pelo MVA, ele vai mudar com o tempo e conforme ideias vão se
    se cristalizando
- O MVA não é uma ferramenta para educar o business sobre Machine Learning (embora ajude a 
    definir expectativas), é uma ferramenta para educar o time de Machine Learning sobre
    business
- A maior vantagem de explorar o MVA não é o valor em si, mas os processo de criação. Ao definir
    o MVA, o time precisa trabalhar com o business para definir as métricas, as expectativas,
    as peculiaridades do sistema.  


## Finalizando

A dificuldade na maioria dos casos não é em implementar um modelo, mas em implementar um modelo que importa e traz 
resultado.

A prática de usar ML tem passado por um processo de amadurecimento, mesmo que em algumas
áreas ainda seja hype. Empresas entendem melhor os problemas, bibliotecas melhores estão
disponíveis, nos permitindo tempo para passar mais tempo pensando na aplicação em vez da 
implementação e a barreira de entrada tem diminuído bastante.

Conforme as ferramentas evoluem, em algum ponto ML será nada mais que uma 
ferramenta no caixa de um desenvolvedor de software, tanto quanto SQL ou POO. E cabe ao 
desenvolvedor saber quando usar cada ferramenta, quais os custos envolvidos, e quais as
vantagens.