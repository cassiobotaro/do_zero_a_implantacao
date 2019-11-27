# :memo: Criando uma tarefa

:x:

```python
def test_recurso_tarefas_deve_aceitar_o_verbo_post(cliente):
    resposta = cliente.post("/tarefas")
    assert resposta.status_code != 405
```

:heavy_check_mark:

```python
@app.post('/tarefas')
def criar():
    pass
```

TODO: mudar teste para verificar presença de titulo no corpo
:x:

```python
def test_quando_titulo_da_tarefa_for_invalido_retorne_codigo_de_status_422(cliente):
    resposta = cliente.post("/tarefas", {})
    assert resposta.status_code == 422
```

:heavy_check_mark:

```python
from fastapi import FastAPI
from pydantic import BaseModel


app = FastAPI()


class Tarefa(BaseModel):
    titulo: str


TAREFAS = []


@app.get('/tarefas')
def listar():
    return TAREFAS


@app.post('/tarefas')
def criar(tarefa: Tarefa):
    pass
```

:x:

```python
def test_titulo_da_tarefa_pode_contar_entre_3_e_50_caracteres(cliente):
    resposta = cliente.post("/tarefas", {"titulo": 2 * "*"})
    assert resposta.status_code == 422
    resposta = cliente.post("/tarefas", {"titulo": 51 * "*"})
    assert resposta.status_code == 422
```
:heavy_check_mark:

TODO: solução para o teste acima


:x:

TODO: teste que checa descriçao com até 140 caracteres

:heavy_check_mark:

TODO: adiciona descrição ao modelo


:x:

TODO: deve retornar uma tarefa

:heavy_check_mark:

TODO: modifica para retornar a tarefa

:x:

TODO: tarefa deve ter id unico


:heavy_check_mark:

TODO: adiciona duas tarefas e os ids devem ser diferentes

:x:

TODO: O estado deve ser concluido por padrão

:heavy_check_mark:

TODO: adiciona estado ao modelo com valor default, deve ser um enum.
:x:

TODO: Código de estatus retornado deve ser 201

:heavy_check_mark:

TODO: modifica resposta da função

:x:

TODO: a tarefa deve ser persistida(checa se len(tarefas) foi modificado)

:heavy_check_mark:

TODO: append da tarefa em TAREFAS

## Salvando a versão atual do código

TODO: reescrever esta parte

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
