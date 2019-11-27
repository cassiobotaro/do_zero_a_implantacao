# :scroll: Detalhando tarefas

:x:

```python
def test_detalhar_tarefa_existente():
    tarefas.clear()
    tarefas.append({'id': 1, 'titulo': 'titulo',
                    'descricao': 'descricao', 'entregue': False})
    cliente = app.test_client()
    resposta = cliente.get('/task/1', content_type='application/json')
    data = json.loads(resposta.data.decode('utf-8'))
    assert resposta.status_code == 200
    assert data['id'] == 1
    assert data['titulo'] == 'titulo'
    assert data['descricao'] == 'descricao'
    assert data['entregue'] is False
```
:heavy_check_mark:

```python
@app.route('/task/<int:id_tarefa>', methods=['GET'])
def detalhar(id_tarefa):
    tarefa = [tarefa for tarefa in tarefas if tarefa['id'] == id_tarefa]
    return jsonify(tarefa[0])
```
:x:

```python
def test_detalhar_tarefa_nao_existente():
    tarefas.clear()
    cliente = app.test_client()
    resposta = cliente.get('/task/1', content_type='application/json')
    assert resposta.status_code == 404
```

:heavy_check_mark:

```python
@app.route('/task/<int:id_tarefa>', methods=['GET'])
def detalhar(id_tarefa):
    tarefa = [tarefa for tarefa in tarefas if tarefa['id'] == id_tarefa]
    if not tarefa:
        abort(404)
    return jsonify(tarefa[0])
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

`git commit -m "detalhar tarefas"`

:octocat: Por fim envie ao github a versão atualizada do projeto.

`git push`

[Entregando tarefas :arrow_right:](entregar.md)

[:arrow_left: Removendo tarefas](remover.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
