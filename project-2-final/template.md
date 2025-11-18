
# DSL de Clausulas Horn

## Descrição Resumida da DSL


> A DSL proposta é uma linguagem específica de domínio (Domain-Specific Language) construída sobre Scheme, voltada para representar e inferir regras de lógica proposicional.
Ela permite ao usuário definir fatos e regras lógicas de forma declarativa, utilizando uma sintaxe simples e intuitiva baseada em conectivos lógicos como and, or e =>.

A motivação do projeto é demonstrar, como os recursos como macros higiênicas, closures e funções de ordem superior podem ser utilizados para criar linguagens próprias.

A relevância está na aplicação direta em sistemas de inferência, motores de regras e inteligência artificial simbólica.


## Slides

> https://docs.google.com/presentation/d/1XoNxpfgmWBPwh9IPvjIKwXeHKE6gbwjMf0UCt1Vml5A/edit?usp=sharing

## Notebook

> https://github.com/GuilhermeHorn2/DSL-Project/blob/main/Implementacao_2.0.ipynb

## Sintaxe da Linguagem

> Define fato booleano: (fact A), armazenado como (A #t)
Define um fato numérico: (fact Temp 35), armazena o fato e valor associado
Cria uma regra usando um operador definido pelo usuário: (rule A maior B => C)
* maior deve existir como uma função
Infere se um fato pode ser deduzido a partir dos fatos e regras existentes: (infer goal)

## Exemplos Selecionados

> Exemplo 1 — Operador Booleano:
>(fact A)   ; fato booleano → armazenado como (A #t)
>(fact B)

>(define (xor a b)
>  (or (and a (not b))
>      (and b (not a))))

>(rule A xor B => D)

>(infer D)  ; Falso, pois A = True e B = True → xor(True, True) = False

> Exemplo 2 — Operador Aritmético:
>(fact Temp 35)    ; fato numérico
>(fact Limite 30)

>(define (maior x y)
>  (> x y))

>(rule Temp maior Limite => quente)
>(rule quente => alerta)

>(infer alerta)   ; True, pois 35 > 30 e quente ⇒ alerta


## Discussão

> O projeto tinha como hipótese principal verificar se seria possível construir, em Scheme, uma DSL capaz de representar conhecimento lógico declarativamente e realizar inferência automática por meio de encadeamento de regras. Os resultados confirmaram essa hipótese: a DSL permite definir fatos e regras em uma sintaxe próxima da lógica proposicional, usando conectivos como and, or, implicação (=>) e, agora, até funções definidas pelo usuário que atuam como operadores lógicos ou aritméticos.

>Os testes mostraram que o modelo de inferência implementado, baseado em forward chaining iterativo, funciona de forma consistente. A função percorre repetidamente a base de conhecimento, identifica premissas satisfeitas e gera novas conclusões até atingir estabilidade. Isso permite inferências encadeadas, como nos exemplos dos slides, em que regras sucessivas transformam fatos simples em conclusões mais complexas. Os resultados obtidos refletem corretamente a semântica declarativa desejada: quando as premissas são satisfeitas, a conclusão é produzida; quando não são, a inferência corretamente retorna falso.

>Uma descoberta importante foi que a inclusão de valores numéricos associados a fatos e a capacidade de avaliar funções personalizadas como maior, menor, xor aumentou substancialmente o poder expressivo da DSL. Isso confirmou a hipótese secundária de que a integração de funções dentro das premissas poderia permitir inferências mais ricas que simples presença de símbolos. De fato, casos como “35 > 30 implica quente” demonstraram que o modelo consegue raciocinar sobre valores, e não apenas sobre proposições atômicas.

>Apesar dos bons resultados, o projeto revelou algumas limitações do modelo atual. A inferência ainda depende exclusivamente de forward chaining, não havendo suporte para buscas reversas ou negação. Outro ponto é que as funções usadas em regras precisam ser cuidadosamente definidas para retornar valores booleanos, e o sistema ainda não suporta expressões mais gerais, como comparações encadeadas ou funções com mais de dois argumentos. Essas limitações apontam caminhos claros para estudos futuros, como suporte a padrões lógicos mais complexos, variáveis, listas de argumentos, ou transformação do sistema em um subconjunto de lógica de predicados.





## Conclusão

> O projeto mostrou que Scheme é adequado para criar uma DSL declarativa capaz de representar conhecimento lógico e realizar inferência automática. A linguagem permite definir fatos, regras com AND, OR e funções personalizadas, além de lidar com valores numéricos e booleanos. O mecanismo de inferência por forward chaining funcionou corretamente, produzindo conclusões encadeadas conforme esperado.
Os principais desafios foram estruturar uma sintaxe natural via macros, evitar erros de avaliação (especialmente envolvendo símbolos e funções), e garantir que a inferência fosse iterativa e estável. Como lição, o projeto reforçou o potencial de macros e closures para construir linguagens expressivas e a importância de entender a semântica antes da implementação.



# Trabalhos Futuros

> Com mais tempo, a DSL poderia evoluir para suportar variáveis lógicas, regras genéricas, busca reversa, negação, e tipos adicionais de dados. A inferência pode ser otimizada e ampliada para comportar cenários maiores e mais complexos.
Como desdobramento natural, o sistema poderia se aproximar de um subconjunto de Prolog, incorporando unificação, predicados e um motor de busca mais completo.


# Referências Bibliográficas

> exemplos SQL-like e macros Scheme, fornecidos nos notebooks da disciplina
> https://en.wikipedia.org/wiki/Propositional_logic
