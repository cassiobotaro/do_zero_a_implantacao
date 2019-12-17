# :trophy: O desafio

À partir de agora, o seu desafio é continuar escrevendo as funcionalidades que faltam, mas vou te dar umas dicas.

Relembrando, ainda temos as seguintes tarefas a serem feitas.

- [x] listar as tarefas
- [x] adicionar tarefa
- [ ] remover tarefa
- [ ] ordenar a listagem por estado
- [ ] finalizar uma tarefa
- [ ] exibir uma tarefa de forma detalhada

## :x: Remover tarefas

A remoção e tarefas consiste em buscar uma tarefa e em seguida remove-la.

O método utilizado é o `DELETE`.

O código de status retornado mais comum é o `204 No Content`.

Você deve especificar o id da tarefa a ser removida na url `/tarefas/86d92774-281c-4e5a-87f2-69029177bfd2`.

Caso não encontra uma tarefa, o código de status `404 Not Found` deve ser retornado.

## :book: Ordenar a listagem por estado

Já temos a listagem pronta mas não garantimos que sua ordenação está correta.

Um teste que pode ser escrito aqui é adição de duas tarefas, sendo a primeira finalizada e a segunda não finalizada.

A exibição da listagem de tarefas deve apresentar a segunda primeiro. Para fazer esta checagem, verifique a resposta e a ordem das tarefas retornadas.

A função sorted pode ser seu aliado para resolver este problema.

Outra função bastante útil é a `itemgetter` que pode ser utilizada no parâmetro `key` da função sorted.

Uma alteração que pode ser feita na listagem é utilização de `List[Tarefa]` como modelo de resposta( parâmetro response_model no decorador), esta mudança ajuda a melhorar a documentação autogerada.

:warning: `itemgetter` pode ser obtido através do pacote operator.`from operator import itemgetter`

## :ballot_box_with_check: Finalizar uma tarefa

Finalizar uma tarefa, pode ser representado através do método `PUT` ou `PATCH`, modificando o valor de estado de uma tarefa.

Devemos procurar uma tarefa e caso não seja encontrada, o código de status `404 Not Found` deve ser retornado.

Os campos a serem modificados podem ser inválidos, caso isto ocorra everemos avisar ao cliente o seu erro. O código de status `422 Unprocessable Entity` pode ser utilizado aqui.

Se bem sucedido o código de status `200 OK` deve ser retornado e o corpo da resposta deve conter a trefa com o valor já modificado.

Você deve especificar o id da tarefa a ser removida na url `/tarefas/86d92774-281c-4e5a-87f2-69029177bfd2`.

## :scroll: Detalhando tarefas

Detalhar uma tarefa é busca-la na lista de tarefas e exibir seu valor.

Caso a tarefa não seja encontrada o código de status `404 Not Found` deve ser retornado.

Você deve especificar o id da tarefa a ser removida na url `/tarefas/86d92774-281c-4e5a-87f2-69029177bfd2`.

O código de status retornado quando bem sucedido é `200 OK`.

## :checkered_flag: Concluindo

Assim finalizamos este guia, espero que tenha curtido bastante esta jornada de aprendizado.

Ainda temos várias coisas não abordadas neste guia que complementam nossa aplicação, mas que tornariam a didática pior.

Caso tenha gostado, não deixe de estrelar o repositório como forma de gratidão. Isto motiva a escrever mais materiais interessantes como este em português.

[Referências e Dicas :arrow_right:](referencias.md)

[:arrow_left: Criando uma tarefa](criar.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
