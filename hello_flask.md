# :dog: Hello Flask

<p align="center">
  <img style="float: right;" src="/imgs/flask.png" alt="logo flask"/>
</p>

É chegada a tão esperada hora de escrevermos código, porém, como aprendemos que podemos ser guiados por testes para ajudar a concepção da arquitetura do nosso programa, faremos as coisas um pouco diferente.

Utilizaremos os ciclos do TDD para nos auxiliarem e assim garantiremos uma qualidade de código ao final.

Estão lembrados o que é a nossa aplicação? Caso não se recorde leia as [regras de negócio]() novamente.

Vamos dividir algumas tarefas então, na nossa lista de funcionalidades:

```
 - adicionar tarefa
 - remover tarefa
 - listar as tarefas
 - ordenar a listagem por estado
 - finalizar uma tarefa
 - exibir uma tarefa de forma detalhada
```

Acho que para iniciarmos o mais simples de escrever e testar é a funcionalidade de listagem de tarefas.

Mas como fazer isto se não temos tarefas, nem mesmo uma aplicação ainda? Por onde começo?

Inicie criando um arquivo `test_todo.py` no mesmo diretório onde já se encontra seu projeto, que deve ficar da seguinte maneira.

```
.
├── LICENSE
├── Pipfile
├── Pipfile.lock
└── README.md
└── test_todo.py
```

Nossa listagem de tarefas, se bem sucedida, deve retornar o código de status `200 OK` e este será nosso primeiro teste.

Traduzindo em um teste automatizado que deve ser acrescentado ao arquivo test_todo.py.

```python
def test_listar_tarefas_deve_retornar_status_200():
    with app.test_client() as client:
        response = client.get('/task')
        assert response.status_code == 200
```

Vamos rodar pela primeira vez os testes no nosso projeto.

`pipenv run python -m pytest`

:scary: Nossa! Ocorreu um erro!

Não se desespere, a primeira coisa que precisamos fazer é criar a nossa aplicação. Crie um novo arquivo `todo.py`, e neste arquivo vamos iniciar uma aplicação flask da seguinte maneira.

```python
from flask import Flask

app = Flask('TODO')
```

Para que os testes enxerguem a nossa aplicação, adicione a seguinte linha no arquivo de testes.

`from todo import app`

Rode novamente os testes.

`pipenv run python -m pytest`

:x: Os testes continuam falhando!

Agora temos nossa aplicação, mas nosso recurso de tarefas ainda não foi criado.

No arquivo `todo.py` adicione a seguinte função.

```python
@app.route('/task')
def listar():
    return ''
```

Rode novamente os testes.

`pipenv run python -m pytest`

:heavy_check_mark: Legal! Temos um teste funcionando! Nossa aplicação está retornando status 200 OK, ainda que a funcionalidade completa não esteja pronta.

:baby: Damos o nome de `baby step`, esta maneira de construir uma aplicação dando pequenos passos de cada vez.

Nosso recurso deve ter o formato [json](http://json.org/), que é um formato textual estruturado, bem simples e leve para troca de informações.

Mas como checamos isto?

Vamos escrever um novo teste!

No arquivo `test_todo.py`, adicione o seguinte teste.

```python
def test_listar_tarefas_deve_ter_formato_json():
    with app.test_client() as client:
        response = client.get('/task')
        assert response.content_type == 'application/json'
```

Rode os testes novamente. Caso esqueça o comando, volte um pouco atrás e copie.

:x: O teste falha e isto é bom!

Acontece que nosso retorno não está com o formato json. Mas Como corrigir isto?

Se temos um teste que falha, precisamos escrever o código necessário para este teste passar.

Vamos voltar ao nosso todo.py para corrigir o nosso problema. Na função que expõe o nosso recurso, modifique o código para:

```python
@app.route('/task')
def listar():
    return jsonify()
```

:warning: No início do arquivo será necessário adicionar a função jsonify às importações.

`from flask import Flask, jsonify`

Corrigido o código, rode novamente os testes.

:heavy_check_mark: Aew! Testes estão passando novamente!


Neste passo os arquivos devem estar da seguinte maneira.

**test_todo.py**
```python
from todo import app


def test_listar_tarefas_deve_retornar_status_200():
    with app.test_client() as client:
        response = client.get('/task')
        assert response.status_code == 200


def test_listar_tarefas_deve_ter_formato_json():
    with app.test_client() as client:
        response = client.get('/task')
        assert response.content_type == 'application/json'
```

**todo.py**
```python
from flask import Flask, jsonify

app = Flask('TODO')


@app.route('/task')
def listar():
    return jsonify()
```

Repare que pouco a pouco nossa aplicação vai tomando forma a partir dos testes.

Parece chato ter de ficar rodando os testes a cada vez, mas além de garatir a qualidade do código, cada vez que os testes são rodados, todas as funcionalidades testadas anteriormente são verificadas novamente. Assim você evita ter de lembrar todas as possibilidades a serem testadas em um teste manual.

Sabemos que quando não há tarefas, nossa resposta do recurso deve ser uma lista vazia.

O teste automatizado para isto pode ser escrito da seguinte maneira.

```
def test_lista_de_tarefas_vazia_retorna_lista_vazia():
    with app.test_client() as client:
        response = client.get('/task')
        assert response.data == b'[]\n'
```

:x: Rodou os testes? Pois é, estão quebrando novamente pois o conteúdo retornado por nossa função não é uma lista.

Para corrigir isto, retorne no `todo.py` e vamos acrescentar uma lista de tarefas, inicialmente vazia e retorna-la na função listar.

```python
from flask import Flask, jsonify

app = Flask('TODO')
tarefas = []


@app.route('/task')
def listar():
    return jsonify(tarefas)
```

:heavy_check_mark: Verifique se está tudo ok  rodando os testes novamente. Ficou verde? Vamos terminar de implementar a nossa listagem


Será que nossa listagem de tarefas funciona quando a lista possui tarefas? Vamos verificar isto?

Em nosso teste, adicionaremos uma tarefa a lista e verificaremos se o conteúdo do retorno está correto.

Volte para o `test_todo.py` e acrescente o seguinte teste.

```python
def test_lista_de_tarefas_nao_vazia_retorna_conteudo():
    tarefas.append({'titulo': 'tarefa 1', 'descricao': 'tarefa de numero 1',
                    'estado': False})
    with app.test_client() as client:
        response = client.get('/task')
        assert response.data == (b'[\n  {\n    "descricao": '
                                 b'"tarefa de numero 1", \n    '
                                 b'"estado": false, \n    '
                                 b'"titulo": "tarefa 1"\n  }\n]\n')
```

:warning: Para que possamos manipular nossas tarefas nos testes, no inicio do arquivo faça sua importação `from todo import tarefas`.

:heavy_check_mark: Os testes continuam funcionando? Parabéns! :clap: :clap:


## :wrench: Testando manualmente

Para testar nossa aplicação manualmente, precisamos colocar nossa aplicação no ar.

Crie um arquivo `.env` e em seu conteudo adicione `FLASK_APP=todo.py`. O flask possui algumas maneiras de rodar, e uma simples é você através da variável de ambiente `FLASK_APP` indicar a ele qual é o arquio inicial da aplicação.

O arquivo .env é lido e adiciona essa variável de ambiente toda vez que executamos comandos no pipenv.

Feito isto, o próximo passo é rodar a aplicação, com o comando `pipenv run python -m flask run`.

Voilá, sua aplicação está no ar. [Clique aqui](http://localhost:5000/task) para abrir no navegador.

O comando `pipenv run http http://localhost:5000/task` também serve para testar a aplicação.

Experimente adicionar tarefas na lista.

## Salvando a versão atual do código

Primeiro passo é checar o que foi feito até agora:

```bash
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.env
	test_todo.py
	todo.py

nothing added to commit but untracked files present (use "git add" to track)
```

Vemos três arquivos não rastreados, precisamos avisar ao controle de versão que monitore estes arquivos.

`$ git add .env test_todo.py todo.py`

:floppy_disk: Agora vamos marcar esta versão como salva.

`git commit -m "listar tarefas"`

:octocat: Por fim envie ao github a versão atualizada do projeto.

`git push`

:sunglasses: Parabéns! Sua aplicação está tomando forma! Já pensou se toda vez que enviassemos uma nova versão para o github, ele verificasse para mim se os testes estão passando? Vamos aprender a ter avaliação conínua de código!

[Integração contínua :arrow_right:](integracao.md)

[:arrow_left: Desenvolvimento guiado por testes](testes.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
