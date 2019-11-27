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


[Containerizando sua aplicação :arrow_right:](docker.md)

[:arrow_left: Detalhando tarefas](detalhar.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
