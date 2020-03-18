# Análise de Preços de Estadia - Rio de Janeiro
Esta análise faz parte do teste técnico de Data Science da Cognitivo.ai.

O objetivo é entender quais são as variáveis que mais impactam nos preços de estadia do Airbnb no Rio de Janeiro 
e como elas se relacionam para explicar nossa variável alvo.

## Dados utilizados:
 - listings_detailed.csv
 
# a. Como foi a definição da sua estratégia de modelagem?
A estratégia que foi abordada nesta análise é uma modelagem explicativa dos preços de estadia do Airbnb no Rio de Janeiro.

Foi desenvolvido um modelo capaz de prever os preços de estadia com base em outras variáveis disponíveis nos dados disponibilizados.

Para isso, utilizei os dados de anuncios do Airbnb do Rio de Janeiro contidos no arquivo listing_detailed.csv.
Houve uma primeira etapa de pré processamento desses dados, que envolvia:
- Remoção de colunas inúteis / sem informação
- Remoção de colunas com muitos valores faltantes
- Tratamento de algumas colunas para criar novas features
- One Hot Encoding
- Filtro de observações com preços zerados.
- Separação de conjunto de treino e conjunto de teste

Em seguida, houve um processo de seleção de variáveis e alguns tratamentos:
- Remoção de features com baixa variância (pouca informação à agregar)
- Imputação utilizando a mediana da variável
- Análise de outliers e limitação dos seus valores

Por fim, tendo todas as features desejadas e tratadas, foi feito a modelagem dos preços de anúncios.
Primeiro foi feita uma transformação da variável alvo para tornar sua distribuição mais simétrica.
Em seguida, testei diversos modelos (lineares e não lineares) utilizando validação cruzada e escolhi 
o que demosntrou melhor performance e capacidade de generalização.


# b. Como foi definida a função de custo utilizada?
A função de custo utilizada foi a R-squared, pois ela é uma medida que informa o quanto o meu modelo conseguiu capturar 
da variabilidade da minha variável dependente. Como não havia um baseline sobre o qual meu modelo deveria ser melhor, então
decidi por desenvolver o modelo que melhor conseguisse capturar a variabilidade do preço a partir das variáves explicativas
disponibilizadas no conjunto.


# c. Qual foi o critério utilizado na seleção do modelo final?
A seleção do modelo final foi feito escolhendo aquele que possuia o melhor resultado de R2 de teste, tomando os devidos 
cuidados para garantir que o não haja overfitting do meu modelo. Ou seja, sempre foi comparado o R2 de teste com o R2 de
treino para verificar se o poder de generalização do modelo estava satisfatório, além de verificar a consistência do R2 
em cada um dos folds testados.


# d. Qual foi o critério utilizado para validação do modelo? Por que escolheu utilizar este método?
A validação do modelo foi feito via validação cruzada, utilizando 6 Folds. (É comum que se use valores entre 5 e 10 Folds).
Ou seja, o modelo é treinado e testado 6 vezes em conjuntos de dados diferentes. 
Essa técnica garante uma maior confiança nos resultados do meu modelo em amostras não vistas ainda (out-of-sample),
pois o conjunto usado para a validação é sempre diferente do conjunto de treino.

É interessante ver a variância da minha função de erro em cada Fold. Baixos valores de variância indicam que 
meu modelo está sendo capaz de obter resultados consistentes em amostras diferentes.
Ao mesmo tempo, variância altas podem ser sinais de que o modelo está sobreajustado ao conjunto de dados usado no treino.

# e. Quais evidências você possui de que seu modelo é suficientemente bom?
No desenvolvimento do modelo, foram tomados certos cuidados para que os resultados obtidos através da validação não fossem 
enviesados por dados de fora (vazamento de dados), além de separar bem minha amostra total em conjuntos de treino, validação 
e teste. Dessa maneira, conseguimos julgar a qualidade do modelo com menos viéses.

Como o resultado do modelo final demonstrou diferenças pouco expressivas entre o R2 de treino e o R2 de teste, além de variância
pequenas nos resultados entre folds das validações cruzadas, posso assegurar que o modelo garante consistências próximas às vistas
nesta análise.
