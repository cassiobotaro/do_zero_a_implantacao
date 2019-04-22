# :memo: Criando uma tarefa

:x:

```python
def test_criar_tarefa_aceita_post():
    with app.test_client() as cliente:
        resposta = cliente.post('/task')
        assert resposta.status_code != 405
```

:heavy_check_mark:

```python
@app.route('/task', methods=['POST'])
def criar():
    return jsonify()
```

:x:

```python
def test_criar_tarefa_retorna_tarefa_inserida():
    tarefas.clear()
    cliente = app.test_client()
    # realiza a requisição utilizando o verbo POST
    resposta = cliente.post('/task', data=json.dumps({
        'titulo': 'titulo',
        'descricao': 'descricao'}),
        content_type='application/json')
    # é realizada a análise e transformação para objeto python da resposta
    data = json.loads(resposta.data.decode('utf-8'))
    assert data['id'] == 1
    assert data['titulo'] == 'titulo'
    assert data['descricao'] == 'descricao'
    # qaundo a comparação é com True, False ou None, utiliza-se o "is"
    assert data['estado'] is False
```

:heavy_check_mark:

Importar o seguinte no início de todo.py

```python
from flask import request
```

```python
@app.route('/task', methods=['POST'])
def criar():
    titulo = request.json.get('titulo')
    descricao = request.json.get('descricao')
    tarefa = {
        'id': len(tarefas) + 1,
        'titulo': titulo,
        'descricao': descricao,
        'estado': False
    }
    return jsonify(tarefa)
```

:x:

```python
def test_criar_tarefa_codigo_de_status_retornado_deve_ser_201():
    with app.test_client() as cliente:
        resposta = cliente.post('/task', data=json.dumps({
            'titulo': 'titulo',
            'descricao': 'descricao'}),
            content_type='application/json')
        assert resposta.status_code == 201
```

:heavy_check_mark:

```python
@app.route('/task', methods=['POST'])
def criar():
    titulo = request.json.get('titulo')
    descricao = request.json.get('descricao')
    tarefa = {
        'id': len(tarefas) + 1,
        'titulo': titulo,
        'descricao': descricao,
        'estado': False
    }
    return jsonify(tarefa), 201
```

:x:

```python
def test_criar_tarefa_insere_elemento_no_banco():
    tarefas.clear()
    cliente = app.test_client()
    # realiza a requisição utilizando o verbo POST
    cliente.post('/task', data=json.dumps({
        'titulo': 'titulo',
        'descricao': 'descricao'}),
        content_type='application/json')
    assert len(tarefas) > 0
```

:heavy_check_mark:

```python
@app.route('/task', methods=['POST'])
def criar():
    titulo = request.json.get('titulo')
    descricao = request.json.get('descricao')
    tarefa = {
        'id': len(tarefas) + 1,
        'titulo': titulo,
        'descricao': descricao,
        'estado': False
    }
    tarefas.append(tarefa)
    return jsonify(tarefa), 201
```

:x:

```python
def test_criar_tarefa_sem_descricao():
    cliente = app.test_client()
    # o código de status deve ser 400 indicando um erro do cliente
    resposta = cliente.post('/task', data=json.dumps({'titulo': 'titulo'}),
                            content_type='application/json')
    assert resposta.status_code == 400
```

:heavy_check_mark:

```python
@app.route('/task', methods=['POST'])
def criar():
    titulo = request.json.get('titulo')
    descricao = request.json.get('descricao')
    if not descricao:
        abort(400)
    tarefa = {
        'id': len(tarefas) + 1,
        'titulo': titulo,
        'descricao': descricao,
        'estado': False
    }
    tarefas.append(tarefa)
    return jsonify(tarefa), 201
```

:x:

```python
def test_criar_tarefa_sem_titulo():
    cliente = app.test_client()
    # o código de status deve ser 400 indicando um erro do cliente
    resposta = cliente.post('/task', data=json.dumps(
        {'descricao': 'descricao'}),
        content_type='application/json')
    assert resposta.status_code == 400
```

:heavy_check_mark:

```python
@app.route('/task', methods=['POST'])
def criar():
    titulo = request.json.get('titulo')
    descricao = request.json.get('descricao')
    if not descricao or not titulo:
        abort(400)
    tarefa = {
        'id': len(tarefas) + 1,
        'titulo': titulo,
        'descricao': descricao,
        'estado': False
    }
    tarefas.append(tarefa)
    return jsonify(tarefa), 201
```

## Salvando a versão atual do código

Primeiro passo é checar o que foi feito até agora:

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   test_todo.py
	modified:   todo.py
```

Vamos adicionar as alterações nos arquivos.

`$ git add test_todo.py todo.py`

:floppy_disk: Agora vamos marcar esta versão como salva.

`git commit -m "criar tarefas"`

:octocat: Por fim envie ao github a versão atualizada do projeto.

`git push`

[Listando tarefas :arrow_right:](listar.md)

[:arrow_left: Mandando um foguete pro espaço](deploy.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
