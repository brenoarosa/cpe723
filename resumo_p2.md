# Resumo P2
### SGA
- Representação: tipicamente binária, podendo ser permutação, inteira ou real
- Mutação:
-- bit-flip (probabilidade Pm)
- Recombinação:
-- one-point crossover
-- N point crossover: seleciona N pontos e alterna os pais entre eles
-- uniforme: seleciona aleatoriamente de cada pai
-- recombinação aritimética simples: crossover até o ponto k,  depois faz a média entre os pais
-- recombinação aritimética unica: faz a média em uma única dimensão, copia o resto dos pais
-- recombinação aritimética completa: faz a média dos pais
- Seleção de Pais
-- fitness proportional (softmax do fitness)
-- Seleção de ranking: linear ou exponencial, roleta ou SUS (roleta espaçada uniformemente)
-- Torneio (q competidores)
- Seleção de indivíduos
-- Proporcional (u + λ) ou geracional (u, λ)
-- Elitismo: salva o melhor
-- Genitor: deterministico: pega os u melhores

### ES
- Representação: real com estratégia
- mutação: τ, τ' proporcionais ao numero de individuos
-- σi' =  σi * e^(N(0, τ') + Ni(0, τ));
-- xi' = xi + Ni(0, σi')
- Recombinação:
-- Média
-- Discreta: cada dimensao é selecionada de um dos pais
- Seleção de Pais: seleção uniforme
- Seleção de indivíduos: Proporcional (u + λ) ou geracional (u, λ), λ > u (tipicamente entre 5-10)
Funciona bem para achar passos de tamanho ideais, se adapta a funções fitness que mudam no tempo.

### EP
- Representação: real com estratégia
- mutação: α tipicamente 0.2
-- σi' =  σi * (1 + Ni(0, α));
-- xi' = xi + Ni(0, σi')
- Recombinação: Não tem
- Seleção de Pais: Cada pai gera um filho
- Seleção de Individuos: (u + λ) sendo λ=u, seleção por torneio, q competidores

### Avaliação de evolucionarios (MBF, AES, SR)
- Taxa de sucesso -> SR (success rate) percentual de vezes que o algoritmo encontrou o otimo ou satisfez as condições dadas
- Qualidade -> MBF (mean best fitness) fitness médio das melhores soluções de N experimentos individuais
- Velocidade -> AES (average number of evaluations to a solution)

### Controle de Parametros
- Exploitation x Exploration
- Controle de parametros durante a run:
-- Deterministico: Regras pre-definidas (ex: passo de mutação x numero de geraçoes)
-- Adaptativo: Considera o estado do algoritmo (ex: aumenta taxa de mutação quando o fitness medio estagna)
-- Auto-Adaptativo: Adaptação autonoma de parametros (ex: ES e EP)

### Multi-Modal
Para alguns problemas pode ser interessante preservar a diversidade das soluções.
- Drift genético: quando a população migra de um maximo para outro
- Métodos Implicitos
-- Rodar N vezes independentes (pode convergir pra mesma solução muitas vezes)
-- modelos de ilhas: diferentes populações que se comunicam raramente (trocam individuos)
-- modelos de difusao: seleção de pais é feita a partir de vizinhos (proximidade genotica), filho substitui alguem da vizinhança
- Métodos Explicitos
-- fitness sharing: fitness de um individuo é definido pela média ponderada de fitness da vizinhança (quanto mais central mais peso). Leva a numero de individuos serem proporcionais ao fitness maximo a qual ele pertence.
-- crowding: cada individuo substitui o individuo pai no qual ele é o mais proximo. Leva a que cada maximo tenha numero equivalente de individuos.

### Multi-Objetivo
- Dominancia e soluções de Pareto
- Possivel solução: utilizar dominancia como fitness (precisa de mecanismos de diversidade)

### Memeticos
É feita uma busca local em volta de cada individuo.  
Precisa usar técnicas para garantir a diversidade.  

pivot rule (tamanho da busca local):
- greedy: assim que encontra um melhor já seleciona ele.
- steepest ascent: encontra o melhor vizinho possivel.

depth rule (profundidade da busca local): Ao encontrar um individuo melhor por greedy ou steepest termina a parte memetica ou gera novos a partir do encontrado.

Frameworks:
- Lamarck: substitui o individuo original pelo obtido por busca local
- Baldwin: substitui apenas o fitness mantendo o genoma original

### CSP
constraining satisfection problem ou constraining optimization problem
- Abordagem indireta: adiciona um custo a funçao fitness para a restrição
- abordagens diretas:
-- Repara soluções invalidas, jogando elas para soluções possiveis (esperando que estejam proximas da obtida)
-- permitir apenas representações, recombinação e mutação que respeitem a restrição

### Teorema de Holland
Analisa o SGA padrao: fitness-proportional parent select, one-point crossover, bitwise mutation, generational survivor selection.
Exemplo: schema com H=1##0#1#0
ordem: numero de bits que nao sao don't care -> o(H) = 4
length: distancia entre o primeiro e ultimo bit que nao são don't care -> d(H) = 8-1 = 7.

Pd(H, x) to denote that probability that the action of an operator x on an instance of a schema H is to destroy it, and Ps(H) to denote the probability that a string containing an instance of schema H is selected.