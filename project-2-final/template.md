
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

> O modelo desenvolvido demonstra que é possível representar conhecimento lógico declarativamente e realizar inferência por meio de encadeamento de regras dentro de um ambiente funcional como o Scheme.
> A DSL permite expressar regras de conjunção (AND) e disjunção (OR), com um mecanismo de inferência iterativa (forward chaining) implementado por uma função recursiva (infer-loop).
> A utilização de macros higiênicas (define-syntax) permite criar uma sintaxe legível e natural, enquanto closures mantêm o estado da base de conhecimento (regras e fatos).


## Conclusão

> O desenvolvimento da DSL mostrou como Scheme é uma linguagem poderosa para metaprogramação, permitindo criar novas linguagens voltadas a domínios específicos com poucas linhas de código.
Os principais desafios incluíram:
    • Criar uma inferência iterativa robusta sem recursão infinita;
    • Representar and e or de forma genérica dentro das regras;
    • Integrar macros, closures e funções de ordem superior de maneira coerente.
Como lição principal, o projeto reforçou a importância de entender a relação entre sintaxe e semântica e como macros e closures podem ser usados para construir abstrações expressivas e seguras.


# Trabalhos Futuros

> Interface textual mais rica para exibir cadeias de inferência (explicabilidade);

> Extensão da DSL para lógica de predicados ou integração com base de dados;

> Criação de uma interface visual ou Web para demonstração interativa.


# Referências Bibliográficas

> exemplos SQL-like e macros Scheme, fornecidos nos notebooks da disciplina
> https://en.wikipedia.org/wiki/Propositional_logic
