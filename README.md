# Análise sobre as Eleições brasileiras e seus candidatos

O conjunto de dados analisado a seguir contém informações sobre todos os indivíduos que se candidataram para alguma vaga nas eleições, podendo este individuo ter sido aceito para a candidatura ou não. É interessante notar, que o conjunto contém informações nacionais, ou seja, possui informações de Presidentes, Vice-Presidentes, Governadores, Prefeitos, Deputados, Senadores e Vereadores, etc.. Este conjunto de dados foi construído/disponibilizado pelo Tribunal Superior de Justiça Eleitoral - TSE e contém informações de 2018 à 2022.

![Screenshot from 2023-05-02 15-37-29](https://user-images.githubusercontent.com/91696970/235792159-c8e24f7f-90b8-4f9d-901f-1abafda032ad.png)


O intuito desta análise é responder perguntas que serão propostas por meio dos dados que estão dispostos neste conjunto de dados. Para que outras perguntas possam ser geradas, o conjunto de dados terá o link disponibilizado abaixo:

Link:

# Introdução


A primeira tarefa que foi realizada foi a observação dos atributos e o entendimento do significado de cada um. Isto foi realizado para que as perguntas pudessem ser formuladas, para que os atributos pudessem ser pré-processados da maneira correta.

Dessa forma, pode-se visualizar os atributos seguidos de suas explicações na tabela abaixo:

| NOME | Significado |
| --- | --- |
| Ano | Ano em que a eleição ocorreu (2018, 2020 ou 2022) |
| Tipo eleição | Tipo da eleição que o candidato participou, um atributo relacionado a uma tecnicidade do sistema eleitoral brasileiro |
| Sigla UF | Identifica a qual estado o candidato irá governa |
| ID Municipio | Identificação do município que o candidato ira governa |
| ID municipio TSE | Identificação do municipio pelo TSE |
| ID candidato BD | Uma identificação do candidato |
| CPF | Documento do candidato |
| Titulo eleitoral | Documento eleitoral do candidato |
| Sequencial | Identificação do candidato |
| Numero | Número do candidato para votar |
| Nome | Nome do candidato |
| Nome urna | NOme na urna, podendo ser diferente do nome. |
| Numero partido | Numero do partido do candidato |
| Sigla partido | Sigla do partido do candidato |
| Cargo | Cargo que o candidato esta disputando |
| Situacao | Situacao da candidatura de um candidato |
| Ocupacao | Profissão do candidato |
| Data nascimento | - |
| Idade | - |
| Genero | - |
| Instrucao | Nível educacional do candidato |
| Estado civil | - |
| Nacionalidade | - |
| Sigla UF Nascimento | UF de nascimento do candidato |
| Municipio Nascimento | Municipio de nascimento do candidato |
| Email | - |
| Raca | - |

Após o entedimento dos atributos, foi possível formular 5 perguntas que serão respondidas com base na análise dos dados que o conjunto de dados provém.

## Perguntas

1. Qual a proporção de candidatos por partido?
2. Qual a proporção de gênero para cada cargo eleitoral?
3. Qual a proporção de raça por cada partido?
4. Qual a relação de idade com o cargo eleitoral?
5. Qual a relação da instrução do candidato por cargo eleitoral?

# Pré-Processamento

Após a definição de quais perguntas serão respondidas, pode-se compreender quais atributos serão utilizados para isto. Desta maneira, é necessário realizar um pré-processamento dos dados para garantir que o conjunto de dados não possua problemas em relação aos dados, como dados faltantes, incoerências ou outro tipo de problema.

Dessa maneira, a primeira tarefa a ser realizada é a remoção de atributos ambíguos. Para isso será realizado o cálculo da correlação entre os atributos. Atributos redundantes são aqueles que possuem uma correlação positiva entre si, ou seja, seus valores possuem distribuições e valores muito parecidos

![Screenshot from 2023-05-02 15-57-31](https://user-images.githubusercontent.com/91696970/235794818-fe89c277-e2c1-4981-a95d-acdc6e86903a.png)

Após a remoção dos atributos redundantes outra decisão tomada foi a retirada de atributos irrelevantes para responder as perguntas propostas acima. Isso significa, que os atributos que não seriam utilizados na análise dos dados para responder as perguntas seriam removidos para evitar confusão e também diminuir a dimensionalidade do conjunto de dados. No caso, o que está sendo desenvolvido os seguintes atributos não seriam utilizados e foram removidos:

1. Ano
2. Titulo eleitoral
3. Sequencial
4. Numero partido
5. Id municipio TSE
6. ID candidato BD
7. Tipo eleicao
8. CPF
9. Nome urna
10. Data nascimento
11. Estado civil
12. Nacionalidade
13. Municipio nascimento
14. Email
15. ID municipio
16. Numero

Desta maneira, sobraram 11 atributos que seriam utilizados nas futuras análises. Assim, é necessário verificar os atributos restantes e garantir que eles não possuam problemas.

Inicialmente, o primeiro pré-processamento realizado nos atributos restantes foi a remoção de candidatos cuja a candidatura não havia sido deferida, isto foi realizado, pois caso um candidato não foi deferido, ele não participa do congresso e nem das eleições por conter algum problema em seus dados, algo julgado pelo TSE, logo estes candidatos iriam interferir na análise já que poderiam acabar causando algum tipo de perturbação nos dados.

Após isto,  foi verificado os atributos que possuem valores nulos mesmo após a retirada de candidatos que não foram deferidos. No conjunto de dados os seguintes atributos possuíam valores nulos

1. Sigla UF
2. Ocupacao
3. Idade
4. Genero
5. Instrução
6. Raça

Dessa maneira, foi necessário realizar a análise individual de cada atributo.

## SIGLA UF

Este atributo, possui valores nulos apenas para candidatos a Presidência e a Vice-Presidência, visto que eles não iriam governar por uma UF específica, mas sim iriam governar pelo BRASIL inteiro, e desta maneira uma solução para não deixar nulo, foi adicionar o valor 'sem sigla' aos candidatos.

## Ocupacao,  Genero e Instrução

Coincidentemente, apenas um exemplo continha valor nulo para estes atributos. Assim, foi verificado que todos os nulos eram respectivos a um candidato que havia sido deferido mas não tinha a maioria dos dados. Uma possível solução seria apenas removê-lo, mas como se tratava de um exemplo, o prazo para a tarefa ser realizada era extenso e o candidato era do partido NOVO, um partido com muitos poucos candidatos, decidiu-se construir os atributos deste exemplo, com os dados presentes no site do partido NOVO. Para esta tarefa, obteve-se êxito.

## Idade

Para este atributo muito importante, foi verificado que os valores nulos representavam menos de 0.01% dos dados, e desta maneira, caso fossem removidos, não iriam causar tanto problema, e desta maneira, estes exemplos foram removidos.

## Raça

Este atributo possuía diversos valores NULOS. No ínicio, houve-se uma dúvdia sobre oque isso representava, se era uma preferência de certos candidatos de não manifestarem sua "raça" ou era apenas uma falta de dados no sistema mesmo. Após uma breve pesquisa, foi compreendido que a coleta de dados teve esta brecha e alguns candidatos não tiveram sua "raça" coletada. Desta maneira, alguma decisão deveria ser tomada, a exclusão não era adequada visto que eram mais de 4000 exemplos, e também o preenchimento artificial não fazia tanto sentido, visto que isto poderia modificar um pouco os resultados. Felizmente, para o atributo "raça" havia um possível atributo "nao informado", e desta maneira, os exemplos que continham este atributo nulo tiverem o valor preenchido com "NAO INFORMADO".


# Análise descritiva e Visualização


Nesta etapa, algumas perguntas que foram formmuladas puderam ser respondidas por meio da análise dos dados, seguido das visualização destas respostas por meio de gráficos.

## Qual a proporção de candidatos por partido?

Abaixo, o gráfico que contém a proporção de candidatos por partido pode ser analisado.

![Screenshot from 2023-05-02 16-21-38](https://user-images.githubusercontent.com/91696970/235798310-83debe11-3106-4411-8a35-9b1fe58c376e.png)

Há na política brasileira 28 partidos com uma média de 15.307 candidatos por partido e desvio padrão de 13.478, idicando que os dados estão dispersos no dataset. Quando observa-se o gráfico de candidatos por partido nota-se uma certa polarização dos dados, em que poucos partidos obtêm um número expressivo de candidatos enquanto outros contêm uma amostragem pequena. Logo, embora a média de candidatos por partido seja grande, muitos partidos não possuem essa quantidade de candidatos, possuindo valores bem inferiores enquanto poucos partidos possuem muitos candidatos, exibindo uma grande concentração de poder em poucos partidos, o que pode ser um problema para a representativdade brasileira.

## Qual a proporção de gênero para cada cargo eleitoral?

Abaixo, podemos verificar a proporção de mulheres em cada cargo eleitoral.

![download](https://user-images.githubusercontent.com/91696970/235798787-19a188bf-4dab-43ec-a9c3-ea2bd12c8391.png)

Algo interessante de se notar neste gráfico é que a maior de proporção de mulher em cargos são em cargos de vice-governador e vice-presidente. Embora estes dois cargos tenham uma quantidade menor do que o restante, visto que possúimos apenas 27 estados, é interessante notar que isto provavelmente acontece pois na maioria dos casos o presidente/governador são homens, e uma mulher é colocada como vice para dar uma falsa sensação de representatividade para a população e com isso passar uma imagem que o partido e o candidato estejam ligados a representatividade feminina. Após as últimas eleições (2022) foi verificado que dos 27 governadores eleitos, apenas 2 são mulheres, o que é bem preocupante e exibe a falta de representatividade feminia em grandes cargos políticos.

Além disso, é possível observar a clara desigualdade em relação a cargos políticos para os outros cargos, a maioria dos cargos, as mulheres não representam mais de 35% dos candidatos, demonstrando uma falta de apoia e de suporte ao ingresso de mulheres na política.

# Conclusão

Neste projeto, foi realizado uma análise sobre os dados, em que todas as etapas foram realizadas. A primeira foi a Escolha do dataset, que foi algo importante, pois foi escolhido o conjunto de dados do TSE, que trás muitas informações sobre os representantes políticos no Brasil. Após isso, foi realizado a Preparação dos Dados, uma etapa muito importante, pois caso os dados não estejam formatados, isso pode tornar a análise deles algo bem complexa. Após essa etapa, foi realizada a Análise Descritiva dos dados.

É possível concluir que a Analíse Descritiva é uma ferramenta muito poderosa para a obtenção de respostas sobre algum conjunto de dados. Nesse caso foi possível obter muitas respostas sobre questionamentos que foram levantados previamente. Com isso, conseguimos entender melhor como a política brasileira está composta, e quais as características dos indivíduos que nos representam.

Há na política brasileira 28 partidos com uma média de 15.307 candidatos por partido e desvio padrão de 13.478, idicando que os dados estão dispersos no dataset. Quando observa-se o gráfico de candidatos por partido nota-se uma certa polarização dos dados, em que poucos partidos obtêm um número expressivo de candidatos enquanto outros contêm uma amostragem pequena.

Quando analisado a proporção de gênero por cargo observamos que a representatividade feminina não corresponde ao percentual desta classe na população, tendo o cargo de prefeito com o menor percentual e o de vice-governador com o maior. A proporção de candidatos pretos e partos nos partidos estão de certa forma correspondentes com a distribuição dessas classes na população, contudo para a população parda alguns partidos estão abaixo do esperado.

A relação de idade por cargo eleitoral observa-se que a posição de vereador é a que apresenta menor média de idade e a de cargo de presidente a maior, com a candidata mais velha de 100 anos e os candidatos mais novos com 18 anos. Já analisando a instrução de nível superior por cargo, a posição de vice-governador apresenta todos os candidatos com esta instrução e a maioria dos partidos com mais da metade de seus colaboradores com nível superior também.

Contudo, a análise do dataset referente as eleições de 2018 às 2022 pode ser considerada como bem sucedida em que primordialmente foi feita uma análise prévia dos dados e sua respectiva limpeza, e após isto foi feito uma análise descritivia mais detalhada a respeito dos pontos mais pertinentes levantados pela equipe, e ao fim, a plotagem de seus gráficos.







