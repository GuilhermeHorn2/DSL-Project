
# DSL Lógica Proposicional

## Descrição Resumida da DSL

> Descrição resumida do tema do projeto. Sugestão de roteiro (cada item tipicamente tratado em uma ou poucas frases):

> A DSL proposta é uma linguagem específica de domínio (Domain-Specific Language) construída sobre Scheme, voltada para representar e inferir regras de lógica proposicional.
Ela permite ao usuário definir fatos e regras lógicas de forma declarativa, utilizando uma sintaxe simples e intuitiva baseada em conectivos lógicos como and, or e =>.

> A motivação do projeto é demonstrar, como os recursos como macros higiênicas, closures e funções de ordem superior podem ser utilizados para criar linguagens próprias.

> A relevância está na aplicação direta em sistemas de inferência, motores de regras e inteligência artificial simbólica.


## Slides

> https://docs.google.com/presentation/d/1XoNxpfgmWBPwh9IPvjIKwXeHKE6gbwjMf0UCt1Vml5A/edit?usp=sharing

## Notebook

> https://github.com/GuilhermeHorn2/DSL-Project/blob/main/Implementacao.ipynb

## Sintaxe da Linguagem

> Define fatos conhecidos inicialmente : (define-facts (A B))
> Cria uma regra de implicação: se A e B forem verdadeiros, então C é verdadeiro : (define-rule (=> (and A B) C))
> Cria regra com disjunção: se X ou Y forem verdadeiros, então Z é verdadeiro : (define-rule (=> (or A B) C))
> Verifica se o fato GOAL pode ser inferido pelas regras e fatos existentes : (infer D)

## Exemplos Selecionados

> Exemplo 1 :
> (define-facts (A B))
> (define-rule (=> (and A B) C))
> (define-rule (=> C D))
> (infer D) ; Resultado: #t

> Exemplo 2 :
> (define-facts (A))
> (define-rule (=> (or A B) C))
> (define-rule (=> C D))
> (infer D) ; Resultado: #t

> Exemplo 3 :
> (define-facts (A))
> (define-rule (=> (and A B) C))
> (infer C) ; Resultado: #f

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

> Suporte a negação (not A) e quantificadores simples (ex.: forall, exists);

> Interface textual mais rica para exibir cadeias de inferência (explicabilidade);

> Extensão da DSL para lógica de predicados ou integração com base de dados;

> Criação de uma interface visual ou Web para demonstração interativa.


# Referências Bibliográficas

> exemplos SQL-like e macros Scheme — fornecidos nos notebooks da disciplina.
> https://en.wikipedia.org/wiki/Propositional_logic
