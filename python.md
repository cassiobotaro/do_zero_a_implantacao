# :snake: Primeiros passos com python

<p align="center">
  <img style="float: right;" src="/imgs/montypython.jpg" alt="monty python"/>
</p>

Infelizmente esse tutorial foi pensado para ser ministrado em apenas algumas horas, o que nos deixa com pouco tempo para aprofundar na linguagem, aqui serão apresentados apenas alguns conceitos que serão necessários para o restante do tutorial.

Caso tenha chegado aqui por outros meios que não o curso presencial, e não tenha conhecimento na linguagem, recomendo dar uma parada, e assistir as excelentes aulas do Professor Masanori. O [python para zumbis](https://www.youtube.com/watch?v=6La690qlH5w&list=PLUukMN0DTKCtbzhbYe2jdF4cr8MOWClXc) tem sido uma excelente porta para muitas pessoas.

Uma outra dica é a [Live de Python](https://www.youtube.com/watch?v=XSVvXso_Ukc&list=PLOQgLBuj2-3K1hb7XgkGPb4S9YNIeHsPk) que ocorre às segundas, sempre as 22h.

Abra um console(sim, a tela preta), digite python e aproveite para testar os comandos ensinados abaixo de uma forma interativa.

## Olá mundo

Olá Mundo em python é tão simples como `print('Olá mundo')` por isso um Olá mundo mais pythônico seria `import antigravity`.

Python é conhecido por suas baterias incluídas, e até mesmo o Olá mundo pode ser importado `import __hello__`.

## Por Favor e Obrigado

Duas funções que podem ser bastante úteis durante o desenvolvimento python e que costumo dizer que são como "por favor" e "obrigado", são as funções help e dir.


A função "help" pede ajuda sobre um determinado recurso, funcionando inclusive com palavras reservadas como 'if'. É retornado a documentação daquele recurso.
```python
>>> help(abs)
Help on built-in function abs in module builtins:

abs(x, /)
    Return the absolute value of the argument.

>>> help('if')
The "if" statement
******************

The "if" statement is used for conditional execution:

   if_stmt ::= "if" expression ":" suite
               ( "elif" expression ":" suite )*
               ["else" ":" suite]
...

```

A função "dir" lista todos os atributos e métodos de uma determinada instância. Como em python tudo é objeto, esta função mostra como a instância do objeto se comporta e quais são seus atributos.
```python
>>>dir(5)
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
```

## Estrutura de chave e valor

Python possui por padrão uma estrutura de dados de array associativo, que é chamado dicionário. Esta estrutura armazena valores associando uma chave a seu conteúdo. Veja abaixo algumas tarefas rudimentares com esta estrutura.

```python

>>> tarefas = {} # inicializando uma estrutura vazia

>>> tarefas[1] = 'tarefa 1' # definindo uma tarefa de chave 1, com conteúdo 'tarefa 1'

>>> print(tarefas[1])  # exibindo a tarefa 1

>>> tarefas[2] = 'tarefa 2' # definindo uma tarefa de chave 2, com conteúdo 'tarefa 2'

>>> tarefas[3] = 'tarefa-3' # definindo uma tarefa de chave 3, com conteúdo 'tarefa 3'

>>> tarefas[3] = 'tarefa 3' # editando uma tarefa

>>> del tarefa[1] # removendo a tarefa

```

## Percorrendo estruturas

O laço de repetição da linguagem Python é através de iteração de coleções. Tudo que pode ser percorrível pode ser utilizado em uma estrutura de repetição.

```python
>>> for tarefa in tarefas:
        print(tarefa)
```

## Funções

Porção de código que resolve um problema muito específico. Boas práticas dizem que uma função deve fazer somente uma coisa e fazer isto bem.

```python
def soma(x, y):
   return x + y
```

## Decorador

É um açúcar sintático que nos permite alterar mais convenientemente funções e métodos. Pode ser definido como uma função, que ao invés de retornar algum resultado, retorna a função recebida como parâmetro modificada.

```python
def p_decorate(func):
   def func_wrapper(name):
       return "<p>{}</p>".format(func(name))
   return func_wrapper

@p_decorate
def get_text(name):
   return "lorem ipsum, {} dolor sit amet".format(name)

print (get_text("John"))

```

Saída:
```
<p>lorem ipsum, John dolor sit amet</p>
```

Vimos um pouco sobre a web, demos uma passada no python, então agora já vamos começar a escrever código?

Calma, ainda temos mais um conceito que é muito importante para nós. Já ouviu falar do desenvolvimento guiado por testes,
que popularmente é conhecido pelas letras `TDD`? Vamos aprender como e por que escrever testes automatizados antes mesmo de escrever código.

[Desenvolvimento guiado por testes :arrow_right:](testes.md)

[:arrow_left: Um pouco sobre a web](web.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
