# Gerenciamento de Portfólio de Ações Utilizando Machine Learning

Esse repositório apresentará duas propostas para gestão de uma carteira de ações quantitativas (utilizando ações da Bolsa B3) que constituem abordagens bastante diferentes para o problema. Na proposta A será apresentado um algoritmo que é baseado em uma abordagem robusta e contemporânea no mercado financeiro de gerenciamento quantitativo de portfólios. Já na proposta B, será utilizado uma abordagem mais tecnológica e recente no mercado financeiro, utilizando redes neurais recorrentes do tipo LSTM.

Ambas as propostas que serão apresentadas utilizarão a premissa de buscar melhores resultados otimizando o Sharpe Ratio.

O Intuito da proposta A é apresentar um pano de fundo, em termos de finanças quantitativas praticados atualmente por fundos de investimento de grande porte no mercado financeiro.

Enquanto que a proposta B é uma proposta que explora técnicas de Machine Learning contemporâneas, e constitui uma abordagem que está se popularizando rapidamente, apesar de ser ainda pouco explorada no meio acadêmico.

A carteira escolhida será a mesma para ambas as propostas, e será mantida por um período longo de tempo, devido às questões já apresentadas sobre liquidez de grandes posições que os fundos necessitam estar posicionados. Por esse motivo a carteira escolhida terá um viés mais defensivo.

O período de análise será de 12 meses (01/09/2021 a 30/09/2022).

A escolha da carteira será a apresentada como carteira sugerida pela BB ASSET para setembro de 2021, vista no link:
https://www.youtube.com/watch?v=869EIn4ZHxg

Com a adoção dessa carteira sugerida em setembro de 2021, podemos ter uma boa análise do desempenho dos algoritmos.

# Proposta A: Otimização de Portfólio através do Método HRP

Para o algoritmo da proposta A, utilizaremos um modelo bastante conhecido no mercado financeiro, denominado Hierarchical Risk Parity - ou na tradução: Paridade de Risco
Hierárquica, ou simplesmente HRP, desenvolvida e detalhada em um paper por Marcos Lopez de Prado.

O método HRP utiliza o aprendizado de máquina para otimizar os portfólios tendo como
característica a criação de grafos, na forma de árvores hierárquicas de risco (dendogramas), em
que os ativos são classificados através de uma matriz de covariância de forma não quadrática.

O método HRP pode ser considerado uma evolução em relação ao método denominado
Algoritmo de linha crítica (CLA), visto que, quando ambos os métodos são submetidos ao teste
de Monte Carlo, o HRP apresenta menor variância fora da amostra (treinamento).

O código utilizado para a proposta A pode ser visto no arquivo "PROPOSTA_A_HRP.ipynb". O código apresentou
um retorno de investimento de 18,96% anualizado e apresentou um drawdown máximo medido
no período de 15,75%. O retorno do CDI no período da simulação (01/09/2021 a 30/09/2022) foi de 10,23%.

Para a elaboração do algoritmo foi utilizado a biblioteca Riskfolio-lib e seus exemplos contidos no endereço:
https://gitub.com/dcajasn/Riskfolio-Lib

# Proposta B: Otimização de Portfólio através de Redes Neurais Recorrentes do Tipo LSTM

A escolha por redes neurais recorrentes do tipo LSTM deve-se pelo fato de que na
previsão de preços, é feito a ponderação entre a memória curta e memória longa da rede
neural.

Na memória curta, a rede busca identificar o mais breve possível o início da tendência
de alta, e posicionar o fundo o quanto antes no ativo que apresentar esse sinal de entrada.

Enquanto que na memória longa, o algoritmo permite ao fundo manter-se posicionado
no mesmo ativo por longos períodos, explorando a tendência de alta identificada nas previsões.

O código aplicado na proposta B foi baseado no código desenvolvido e salvo no repositório GitHub de Denis Vodchts: 
https://github.com/CloseToAlgoTrading/CodeFromVideo/tree/master/Episode_20_Battle_Of_Optimization_Methods

O código apresentou um retorno de investimento de 10,01% e apresentou um drawdown máximo medido no período de 48,89%

É possível verificar que um dos objetivos principais foi alcançado, que era tentar manter o algoritmo posicionado o máximo possível em cada ativo, explorando o sinal de entrada da memória de longo prazo da rede LSTM, evidenciando a exploração da estratégia trend following.

Podemos observar que a proposta A apresentou um resultado bastante expressivo, quando observamos o retorno de investimento em referência ao desempenho do CDI.

A proposta B apresentou um resultado semelhante ao desempenho do CDI.

Há que se ressaltar também, que a alocação de ativos, baseada na carteira mensal da BB Asset deveria ser trocada mensalmente, conforme novas ações são sugeridas ao longo dos meses, isso poderia gerar um aumento considerável na lucratividade.

A rede neural LSTM utilizada na proposta B, poderia ser otimizada variando-se quantidade de camadas e quantidade de neurônios, para isso podemos utilizar de frameworks específicos de otimização de redes neurais. Também pode-se utilizar camadas convolucionais na entrada da rede para filtrar anomalias na movimentação dos preços.

Ambas as propostas terão que ser ampliadas em suas funcionalidades no intuito de ter proteções contra anomalias. Como exemplo, é possível ver no gráfico de retorno da proposta B que se o algoritmo tivesse essa implementação, o drawdown de mais de 48% seria consideravelmente reduzido, inclusive podendo aumentar a lucratividade final da proposta B.

# Conclusão do Estudo das Duas Propostas

As propostas apresentadas exploraram duas possibilidades de uma montagem de uma carteira de ativos, não se pode considerar que o resultado obtido é o melhor resultado possível para cada possibilidade, visto que, conforme já mencionado anteriormente, não foi exaurido todas as possibilidades de otimização, em todos os cenários de variações de configurações possíveis das estratégias.

Mas é possível notar que a proposta B possui um algoritmo mais complexo, observando mais detalhes do problema, necessitando de menos implementação de código para ser ter um algoritmo operacional que possa ser utilizado no mercado real. No caso da proposta B, uma otimização mais trabalhada poderia entregar um resultado semelhante ou até superior ao da proposta A.

A proposta B é melhor estruturada, visto que possui arquivos distintos para backtest e gerenciamento de risco, além de possuir inclusive variações pré-setadas de camadas e número de neurônios, que podem ser usadas a qualquer tempo, de forma a encontrar uma configuração que melhor se adapte aos ativos selecionados. 

O modelo da proposta B também leva vantagem da proposta A no quesito tipo de alocação dos ativos, visto que a quantidade de cada ativo varia dinamicamente com o passar dos meses (alocação estratégica), podendo prever mudanças de tendência nos ativos, enquanto que na proposta A, a quantidade de cada ativo é mantida ao longo dos 12 meses seguintes (alocação tática).

Todos os detalhes apresentados acima, em que pesa vantagem a proposta B são vantagens competitivas importantes, mas o resultado obtido pela proposta A no quesito retorno de investimento e drawdown bem menor devem ter peso maior, visto que é o objetivo final a ser alcançado pelas estratégias, indicando que no estágio atual de desenvolvimento de ambas as propostas, a proposta a ser escolhida deveria ser a proposta A.

07/2023 - Novos testes foram feitos no sentido de utilizar os algoritmos da proposta A e B na função de SCREENING, obtendo um resultado em média 15% acima do apresentado aqui anteriormente. Para a função de screening testada recentemente, foi feito um aumento da listagem para 50, 75 e 100 ativos (Os últimos 50, 75 e 100 ativos listados nos últimos meses pela BB Asset), sendo que os algoritmos calcularam o sharpe ratio de cada ativo, entrando na carteira somente os 10 ativos com melhor sharpe ratio, fazendo uma ponderação do peso de cada ativo proporcionalmente ao proposto pelo algoritmo.

Para a proposta B, estou implementando uma versão com uma feature adicional da rede neural utilizando análise de sentimentos dos ativos através de API ligada ao google trends, sem melhorias consideráveis até o momento.
