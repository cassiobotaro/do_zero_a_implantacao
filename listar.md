# :book: Listando tarefas

:x:

```python
def test_listar_tarefas_deve_apresentar_tarefas_nao_finalizadas_primeiro():
    tarefas.clear()
    tarefas.append({'titulo': 'tarefa 1', 'descricao': 'tarefa de numero 1',
                    'estado': True})
    tarefas.append({'titulo': 'tarefa 2', 'descricao': 'tarefa de numero 2',
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

`git commit -m "listar tarefas"`

:octocat: Por fim envie ao github a versão atualizada do projeto.

`git push`

[Removendo tarefas :arrow_right:](remover.md)

[:arrow_left: Criando uma tarefa](criar.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
