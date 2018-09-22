# :dog: Hello Flask

<p align="center">
  <img style="float: right;" src="/imgs/flask.png" alt="logo flask"/>
</p>

É chegada a tão esperada hora de escrevermos código, porém, como aprendemos que podemos ser guiados por testes para ajudar a concepção da arquitetura do nosso programa, faremos as coisas um pouco diferente.

Utilizaremos os ciclos do TDD para nos auxiliarem e assim garantiremos uma qualidade de código ao final.

Estão lembrados o que é a nossa aplicação? Caso não se recorde leia as [regras de negócio](./planejando.md) novamente.

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
└── test_gerenciador.py
```

Nossa listagem de tarefas, se bem sucedida, deve retornar o código de status `200 OK` e este será nosso primeiro teste.

Traduzindo em um teste automatizado que deve ser acrescentado ao arquivo test_gerenciador.py.

```python
def test_listar_tarefas_deve_retornar_status_200():
    app.config['TESTING'] = True
    with app.test_client() as cliente:
        resposta = cliente.get('/tarefas')
        assert resposta.status_code == 200
```

Vamos rodar pela primeira vez os testes no nosso projeto.

`pipenv run python -m pytest`

:scream: Nossa! Ocorreu um erro!

Não se desespere, a primeira coisa que precisamos fazer é criar a nossa aplicação. Crie um novo arquivo `gerenciador.py`, e neste arquivo vamos iniciar uma aplicação flask da seguinte maneira.

```python
from flask import Flask

app = Flask('Gerenciador')
```

Para que os testes enxerguem a nossa aplicação, adicione a seguinte linha no arquivo de testes.

`from gerenciador import app`

Rode novamente os testes.

`pipenv run python -m pytest`

:x: Os testes continuam falhando!

Agora temos nossa aplicação, mas nosso recurso de tarefas ainda não foi criado.

No arquivo `gerenciador.py` adicione a seguinte função.

```python
@app.route('/tarefas')
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

No arquivo `test_gerenciador.py`, adicione o seguinte teste.

```python
def test_listar_tarefas_deve_ter_formato_json():
    with app.test_client() as cliente:
        resposta = cliente.get('/task')
        assert resposta.content_type == 'application/json'
```

Rode os testes novamente. Caso esqueça o comando, volte um pouco atrás e copie.

:x: O teste falha e isto é bom!

Acontece que nosso retorno não está com o formato json. Mas como corrigir isto?

Se temos um teste que falha, precisamos escrever o código necessário para este teste passar.

Vamos voltar ao nosso gerenciador.py para corrigir o nosso problema. Na função que expõe o nosso recurso, modifique o código para:

```python
@app.route('/tarefas')
def listar():
    return jsonify()
```

:warning: No início do arquivo será necessário adicionar a função jsonify às importações.

`from flask import Flask, jsonify`

Corrigido o código, rode novamente os testes.

:heavy_check_mark: Aew! Testes estão passando novamente!


Neste passo os arquivos devem estar da seguinte maneira.

**test_gerenciador.py**
```python
from gerenciador import app


def test_listar_tarefas_deve_retornar_status_200():
    app.config['TESTING'] = True
    with app.test_client() as cliente:
        resposta = cliente.get('/tarefas')
        assert resposta.status_code == 200


def test_listar_tarefas_deve_ter_formato_json():
    app.config['TESTING'] = True
    with app.test_client() as cliente:
        resposta = cliente.get('/tarefas')
        assert resposta.content_type == 'application/json'
```

**gerenciador.py**
```python
from flask import Flask, jsonify

app = Flask('Gerenciador')


@app.route('/tarefas')
def listar():
    return jsonify()
```

Repare que pouco a pouco nossa aplicação vai tomando forma a partir dos testes.

Parece chato ter de ficar rodando os testes a cada vez, mas além de garatir a qualidade do código, cada vez que os testes são rodados, todas as funcionalidades testadas anteriormente são verificadas novamente. Assim você evita ter de lembrar todas as possibilidades a serem testadas em um teste manual.

:vertical_traffic_light: Perceberam que estamos guiando o nosso desenvolvimento a partir dos testes? Pouco a pouco temos a funcionalidade de listagem sendo desenhada.

Vamos continuar então. Sabemos que quando não há tarefas, nossa resposta do recurso deve ser uma lista vazia.

O teste automatizado para isto pode ser escrito da seguinte maneira.

```python
def test_lista_de_tarefas_vazia_retorna_lista_vazia():
    app.config['TESTING'] = True
    with app.test_client() as cliente:
        resposta = cliente.get('/tarefas')
        assert resposta.json == []
```

:x: Rodou os testes? Pois é, estão quebrando novamente pois o conteúdo retornado por nossa função não é uma lista.

Para corrigir isto, retorne no `gerenciador.py` e vamos modificar nossa função de listagem para inicialmente retornar uma lista vazia.

```python
from flask import Flask, jsonify

app = Flask('Gerenciador')


@app.route('/tarefas')
def listar():
    return jsonify([])
```

:heavy_check_mark: Verifique se está tudo ok  rodando os testes novamente. Ficou verde? Vamos terminar de implementar a nossa listagem

Vamos criar uma lista de tarefas, adicionaremos conteúdo a ela e este conteúdo deve ser retornado.

Volte para o `test_gerenciador.py` e acrescente o seguinte teste.

```python
def test_lista_de_tarefas_nao_vazia_retorna_conteudo():
    tarefas.append({'id': 1, 'titulo': 'tarefa 1',
                    'descricao': 'tarefa de numero 1', 'estado': False})
    app.config['TESTING'] = True
    with app.test_client() as cliente:
        resposta = cliente.get('/tarefas')
        assert resposta.json == [{
            'id': 1,
            'titulo': 'tarefa 1',
            'descricao': 'tarefa de numero 1',
            'estado': False}]
```

:x: Testes não funcionando novamente? Vamos corrigir!

Precisamos adicionar uma lista de tarefas e retorná-la na nossa função de listar.

```python
from flask import Flask, jsonify

app = Flask('Gerenciador')

tarefas = []


@app.route('/tarefas')
def listar():
    return jsonify(tarefas)

```

:warning: Para que possamos manipular nossas tarefas nos testes, no inicio do arquivo faça sua importação `from gerenciador import tarefas`.

:heavy_check_mark: Os testes estão funcionando? Parabéns! :clap: :clap:


## :wrench: Testando manualmente

Para testar nossa aplicação manualmente, precisamos colocar nossa aplicação no ar.

Crie um arquivo `.env` e em seu conteudo adicione `FLASK_APP=gerenciador.py`. O flask possui algumas maneiras de rodar, e uma simples é você através da variável de ambiente `FLASK_APP` indicar a ele qual é o arquio inicial da aplicação.

O arquivo .env é lido e adiciona essa variável de ambiente toda vez que executamos comandos no pipenv.

Feito isto, o próximo passo é rodar a aplicação, com o comando `pipenv run python -m flask run`.

Voilà, sua aplicação está no ar. [Clique aqui](http://localhost:5000/tarefas) para abrir no navegador.

O comando `pipenv run http http://localhost:5000/tarefas` também serve para testar a aplicação.

Experimente adicionar tarefas na lista.

## Salvando a versão atual do código

Primeiro passo é checar o que foi feito até agora:

```bash
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	gerenciador.py
	test_gerenciador.py

nothing added to commit but untracked files present (use "git add" to track)
```

Vemos dois arquivos não rastreados, precisamos avisar ao controle de versão que monitore estes arquivos.

`$ git add gerenciador.py test_gerenciador.py `

:floppy_disk: Agora vamos marcar esta versão como salva.

`git commit -m "listar tarefas"`

:octocat: Por fim envie ao github a versão atualizada do projeto.

`git push`

:sunglasses: Parabéns! Sua aplicação está tomando forma! Já pensou se toda vez que enviássemos uma nova versão para o github, ele verificasse para mim se os testes estão passando? Vamos aprender a ter integração contínua de código!?

[Integração contínua :arrow_right:](integracao.md)

[:arrow_left: Desenvolvimento guiado por testes](testes.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
