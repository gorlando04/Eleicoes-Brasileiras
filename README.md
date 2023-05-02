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

Após a remoção dos atributos redundantes outra decisão tomada foi a retirada de atributos irrelevantes para responder as perguntas propostas acima. Isso significa, que os atributos que não seriam utilizados na análise dos dados para responder as perguntas seriam removidos para evitar confusão e também diminuir a dimensionalidade do conjunto de dados. No caso que está sendo desenvolvido os seguintes atributos não seriam utilizados e foram removidos:

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




