# :x: Removendo tarefas

:x:

```python
def test_deletar_tarefa_utiliza_verbo_delete():
    tarefas.clear()
    with app.test_client() as cliente:
        resposta = cliente.delete('/task/1')
        assert resposta.status_code != 405
```

:heavy_check_mark:

```python
@app.route('/task/<int:id_tarefa>', methods=['DELETE'])
def remover(id_tarefa):
    return ''
```
:x:

```python
def test_remover_tarefa_existente_retorna_204():
    tarefas.clear()
    tarefas.append({'id': 1, 'titulo': 'titulo',
                    'descricao': 'descricao', 'estado': False})
    cliente = app.test_client()
    resposta = cliente.delete('/task/1', content_type='application/json')
    assert resposta.status_code == 204
    assert resposta.data == b''
```

:heavy_check_mark:

```python
@app.route('/task/<int:id_tarefa>', methods=['DELETE'])
def remover(id_tarefa):
    return '', 204
```

:x:

```python
def test_remover_tarefa_existente_remove_tarefa_da_lista():
    tarefas.clear()
    tarefas.append({'id': 1, 'titulo': 'titulo',
                    'descricao': 'descricao', 'estado': False})
    cliente = app.test_client()
    cliente.delete('/task/1', content_type='application/json')
    assert len(tarefas) == 0
```

:heavy_check_mark:

```python
@app.route('/task/<int:id_tarefa>', methods=['DELETE'])
def remover(id_tarefa):
    tarefa = [tarefa for tarefa in tarefas if tarefa['id'] == id_tarefa]
    tarefas.remove(tarefa[0])
    return '', 204
```
:x:

```python
def test_remover_tarefa_nao_existente():
    tarefas.clear()
    cliente = app.test_client()
    resposta = cliente.delete('/task/1', content_type='application/json')
    assert resposta.status_code == 404
```

:heavy_check_mark:

```python
@app.route('/task/<int:id_tarefa>', methods=['DELETE'])
def remover(id_tarefa):
    tarefa = [tarefa for tarefa in tarefas if tarefa['id'] == id_tarefa]
    if not tarefa:
        abort(404)
    tarefas.remove(tarefa[0])
    return '', 204
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

`git commit -m "remover tarefas"`

:octocat: Por fim envie ao github a versão atualizada do projeto.

`git push`

[Listar tarefas :arrow_right:](listar.md)

[:arrow_left: Detalhando tarefas](detalhar.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
