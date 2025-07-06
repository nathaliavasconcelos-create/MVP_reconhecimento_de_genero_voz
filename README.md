Introdução

Este repositório contém o MVP para disciplina de Análise de Dados e Boas Práticas (2025.1) feito pela aluna Nathalia Vasconcelos. Além do notebook realizado no Google Colab, 
pode-se encontrar o dataset usado como base para a análise realizada. Nesta secção README, pode-se ler um pequeno resumo dos tópicos mais relevantes do trabalho realizado.


Objetivos do MVP

O objetivo central do MVP é a busca dos traços mais relevantes para o reconhecimento do gênero por voz. Para isso, adotou-se um dataset contendo 20 atributos numéricos e 
1 atributo categórico: a label masculino e feminino. Tais variáveis foram exploradas estatisticamente, observando valores como média e desvio padrão, e seus resultados, 
dispostos em visualizações diversificadas. 

 Tipo de problema
 
Trata-se de um problema de classificação supervisionada, pois com o auxílio das variáveis de entrada, busca-se prever as variáveis-alvo.

Hipóteses do Problema

Foram postuladas as seguintes hipóteses: 

•	Variáveis diretamente relacionadas à frequência serão as mais relevantes para prever o gênero da voz analisada, especialmente, a freqência média. Isto porque, 
frequências mais altas são associadas ao gênero femininio, enquanto as mais baixas, ao masculino. Esta questão será mais abordada na secção em que se descreve os 
atributos do dataset;

•	A variável que diz respeito à modularidade da voz será extremamente relevante para o reconhecimento de gênero. Isto porque, está relacionada ao tom e volume, 
elementos que alteram bastante conforme o gênero;

•	Quanto às demais variáveis, não é esperado um comportamento preditivo alto.


Atributos do dataset

•	Meanfreq: frequência média do espectro da voz (em kHz). Importante destacar que as medidas apresentadas em cada linha das colunas deste dataset foram obtidas a partir 
da análise de um único espectro de voz. Isto é, a partir daquele sinal de voz obteve-se a frequência média observando a intensidade de uma determinada frequência. 
Também convém ressaltar que a voz masculina alcança as faixas de frequência de 85 a 180 Hz (frequências mais graves), enquanto a voz feminina alcança valores de 165 a 
255 Hz (frequências mais agudas);

•	SD: desvio padrão da frequência;

•	Median: valores de mediana das frequências (em kHz);

•	Q25: primeiro quartil da frequência do arquivo de voz (em kHz);

•	Q75: terceiro quartil da frequência (em kHz);

•	QR: amplitude interquartil (em kHz);

•	Skew: indica a assimetria da distribuição da frequência. Auxilia a descrever qualitativamente o sinal de vibração (adimensional);

•	Kurt: do inglês, kurtosis, pode ser traduzida como a distorção do sinal, quantificando os picos ou achatamentos deste. Também auxilia a descrever qualitativamente o 
sinal de vibração (adimensional);

•	Sp.ent: entropia espectral, isto é, a medida da desordem das frequências no espectro de voz (adimensional);

•	Sfm: do inglês, spectral flatness é a medida que auxilia a quantificar se o espectro é plano (um ruído branco) ou com picos (alterações de frequência). Esta é uma 
variável adimensional;

•	Mode: frequência modal. Não é a estatística clássica, mas sim a frequência mais predominante no espectro durante o registro (em kHz);

•	Centroid: indica em que ponto está o "centro de massa" do espectro (em kHz);

•	Peakf: indica os valores do pico das frequências, isto é, as frequências com mais energia (em kHz);

•	Meanfun: média da frequência fundamental medida através do sinal acústico (em kHz);

•	Minfun: frequência fundamental mínima medida através do sinal acústico (em kHz);

•	Maxfun: frequência fundamental máxima medida em um sinal acústico (em kHz);

•	Meandom: média da frequência dominante medida em um sinal acústico (em kHz);

•	Mindom: mínimo da frequência dominante medido em um sinal acústico (em kHz);

•	Maxdom: máximo da frequência dominante medido em um sinal acústico (em kHz);

•	Dfrange: amplitude da frequência dominante medida em um sinal acústico (em kHz);

•	Modindx: índice de modulação. Calculado como a diferença absoluta acumulada entre medições adjacentes de frequências fundamentais dividida pela amplitude de frequência 
(adimensional);

•	Label: apresenta as classes binárias "male" ou "female" para a classificação das amostras.

Análise Exploratória

Após uma extensa etapa de análise exploratória, obteve-se uma matriz de correlação de um dataset mais limpo. Isto é, foram excluídas algumas colunas por terem mostrado 
redudância ou pouca capacidade de contribuição preditiva ao longo da análise. A partir da matriz, obteve-se as seguintes observações:

a) Para meanfun (r=-0.83), observa-se uma correlação negativa forte, indicando que as vozes femininas (codificadas como 0) têm valores mais alto;
b) Já sfm (r=0.36) apresenta uma correlação positiva moderada com a variável-alvo. Percebe-se com isso que as vozes masculinas (codificadas como 1) têm espectro mais plano.;
c) Quanto à relação entre sp.ent e a variável-alvo, com valor de 0.49, observa-se uma correlação positiva, demonstrando que as vozes masculinas têm maior entropia;
d) Por último, a correlação positiva com sd (r= 0.48) indica que as vozes masculinas variam mais no que diz respeito à frequência.

No mais, foi importante destacar algumas relações entre outras variáveis:
Meanfreq, median, Q25 apresentam correlação quase perfeita (r > 0.9). Para a etapa seguinte de pré-processamento de dados, foi interessante manter apenas meanfreq 
pela sua maior correlação com a variável-alvo;

Pré-processamento dos dados

Já na etapa de pré-processamento dos dados, dividiu-se o conjunto em treino (70%) e teste (30%), obtendo as seguintes dimensões:
Dimensões de X_train: (2216, 13)
Dimensões de X_test: (950, 13)
Dimensões de y_train: (2216,)
Dimensões de y_test: (950,)

Em seguida, realizou-se o processo de padronização. Após a aplicação do StandardScaler, obtivemos valores de desvio padrão próximos a 1 e médias próximas a 0, em todo o conjunto de dados. No entanto, olhando para as estatísticas dentro de cada grupo separado por gênero estes valores são diferentes. Na verdade, ao fazer essa análise, busca-se compreender qual seria a variabilidade dos valores padronizados dentro de cada subgrupo.
Com base nos valores obtidos, pode-se também fazer algumas análises. Observa-se que para todas as variáveis, as classes masculino e feminino têm valores 
simetricamente opostos. Na prática, isto ocorre por conta do equilíbrio do dataset. Seria um problema apenas se fosse verificado data leakage, o que não ocorreu.

Conclusões

Neste MVP, objetivou-se compreender quais os principais traços (ou features) envolvidos no processo de reconhecimento de gênero por voz. Com respeito às hipóteses 
postuladas inicialmente, pôde-se confirmar, de fato, a importância das variáveis associadas à frequência para a determinação do gênero. Entretanto, foi surpreendente 
o fato de a modularidade não constituir uma variável relevante para o processo. Além disso, percebeu-se a importância das variáveis relacionadas à entropia o correto 
reconhecimento dos gêneros.
Por fim, é importante destacar que o dataset avaliado não leva em consideração variedades linguísticas, idades e, muito menos, outras línguas que não seja o inglês. 
Para o futuro, seria interessante expandir a análise identificando diversos sotaques de línguas variadas, observando também a influência ou não do fator idade para o 
reconhecimento de gênero.
         

