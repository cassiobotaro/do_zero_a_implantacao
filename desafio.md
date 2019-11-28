# :trophy: O desafio

TODO: descrever o desafio e modificar daqui pra baixo para conter somente dicas sobre cada tarefa ainda não concluida.

# :book: Listando tarefas

:x:

```python
def test_listar_tarefas_deve_apresentar_tarefas_nao_finalizadas_primeiro():
    tarefas.clear()
    tarefas.append({'id': 1, 'titulo': 'tarefa 1', 'descricao': 'tarefa de numero 1',
                    'estado': True})
    tarefas.append({'id': 2, 'titulo': 'tarefa 2', 'descricao': 'tarefa de numero 2',
                    'estado': False})
    with app.test_client() as cliente:
        resposta = cliente.get('/task')
        data = json.loads(resposta.data.decode('utf-8'))
        primeira_task, segunda_task = data
        assert primeira_task['titulo'] == 'tarefa 2'
        assert segunda_task['titulo'] == 'tarefa 1'
```


:heavy_check_mark:

```python
@app.route('/task')
def listar():
    return jsonify(sorted(tarefas, key=itemgetter('estado')))
```

:warning: `itemgetter` pode ser obtido através do pacote operator.`from operator import itemgetter`

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

# :ballot_box_with_check: Entregando tarefas

:x:

```python
def test_atualizando_uma_tarefa_existente():
    tarefas.clear()
    tarefas.append({'id': 1, 'titulo': 'titulo',
                    'descricao': 'descricao', 'estado': False})
    cliente = app.test_client()
    resposta = cliente.put('/task/1', data=json.dumps(
        {'titulo': 'titulo atualizado',
         'descricao': 'descricao atualizada', 'estado': True}
    ),
        content_type='application/json')
    data = json.loads(resposta.data.decode('utf-8'))
    assert resposta.status_code == 200
    assert data['id'] == 1
    assert data['titulo'] == 'titulo atualizado'
    assert data['descricao'] == 'descricao atualizada'
    assert data['estado'] is True
```


:heavy_check_mark:

```python
@app.route('/tarefa/<int:id_tarefa>', methods=['PUT'])
def atualizar(id_tarefa):
    tarefa = [tarefa for tarefa in tarefas if tarefa['id'] == id_tarefa]
    titulo = request.json.get('titulo')
    descricao = request.json.get('descricao')
    estado = request.json.get('estado')
    tarefa_escolhida = tarefa[0]
    tarefa_escolhida['titulo'] = titulo or tarefa_escolhida['titulo']
    tarefa_escolhida['descricao'] = descricao or tarefa_escolhida['descricao']
    tarefa_escolhida['estado'] = estado or tarefa_escolhida['estado']
    return jsonify(tarefa_escolhida)
```



:x:

```python
def test_atualizando_uma_tarefa_nao_existente():
    tarefas.clear()
    cliente = app.test_client()
    resposta = cliente.put('/tarefa/1', data=json.dumps(
        {'titulo': 'titulo atualizado',
         'decricao': 'descricao atualizada', 'estado': True}
    ),
        content_type='application/json')
    assert resposta.status_code == 404
```

:heavy_check_mark:

```python
@app.route('/tarefa/<int:id_tarefa>', methods=['PUT'])
def atualizar(id_tarefa):
    tarefa = [tarefa for tarefa in tarefas if tarefa['id'] == id_tarefa]
    titulo = request.json.get('titulo')
    descricao = request.json.get('descricao')
    entregue = request.json.get('entregue')
    if not tarefa:
        abort(404)
    tarefa_escolhida = tarefa[0]
    tarefa_escolhida['titulo'] = titulo or tarefa_escolhida['titulo']
    tarefa_escolhida['descricao'] = descricao or tarefa_escolhida['descricao']
    tarefa_escolhida['entregue'] = entregue or tarefa_escolhida['entregue']
    return jsonify(tarefa_escolhida)
```

:x:

```python
def test_atualizando_uma_tarefa_com_campos_invalidos():
    tarefas.clear()
    tarefas.append({'id': 1, 'titulo': 'titulo',
                    'descricao': 'descricao', 'estado': False})
    cliente = app.test_client()
    # sem estado
    resposta = cliente.put('/tarefa/1', data=json.dumps(
        {'titulo': 'titulo atualizado',
         'decricao': 'descricao atualizada'}
    ),
        content_type='application/json')
    assert resposta.status_code == 400
    # sem descrição
    resposta = cliente.put('/tarefa/1', data=json.dumps(
        {'titulo': 'titulo atualizado',
         'estado': False}
    ),
        content_type='application/json')
    assert resposta.status_code == 400
    # sem titulo
    resposta = cliente.put('/tarefa/1', data=json.dumps(
        {'descricao': 'descricao atualizado',
         'estado': False}
    ),
        content_type='application/json')
    assert resposta.status_code == 400
```

:heavy_check_mark:

```python
@app.route('/tarefa/<int:id_tarefa>', methods=['PUT'])
def atualizar(id_tarefa):
    tarefa = [tarefa for tarefa in tarefas if tarefa['id'] == id_tarefa]
    titulo = request.json.get('titulo')
    descricao = request.json.get('descricao')
    estado = request.json.get('estado')
    if not tarefa:
        abort(404)
    if not descricao or not titulo or estado is None:
        abort(400)
    tarefa_escolhida = tarefa[0]
    tarefa_escolhida['titulo'] = titulo or tarefa_escolhida['titulo']
    tarefa_escolhida['descricao'] = descricao or tarefa_escolhida['descricao']
    tarefa_escolhida['estado'] = estado or tarefa_escolhida['estado']
    return jsonify(tarefa_escolhida)
```
[Containerizando sua aplicação :arrow_right:](integracao.md)

[:arrow_left: Criando uma tarefa](testes.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
