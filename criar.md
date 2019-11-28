# :memo: Criando uma tarefa

Vamos a mais uma das funcionalidades:

- [x] listar as tarefas
- [x] adicionar tarefa
- [ ] remover tarefa
- [ ] ordenar a listagem por estado
- [ ] finalizar uma tarefa
- [ ] exibir uma tarefa de forma detlhada

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

:x:

```python
def test_quando_uma_tarefa_e_submetida_deve_possuir_um_titulo(cliente):
    resposta = cliente.post("/tarefas", json={})
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
def test_titulo_da_tarefa_deve_conter_entre_3_e_50_caracteres(cliente):
    resposta = cliente.post("/tarefas", json={"titulo": 2 * "*"})
    assert resposta.status_code == 422
    resposta = cliente.post("/tarefas", json={"titulo": 51 * "*"})
    assert resposta.status_code == 422
```
:heavy_check_mark:

```python
from pydantic import BaseModel, constr



class Tarefa(BaseModel):
    titulo: constr(min_length=3, max_length=50)
```

:x:

```python
def test_quando_uma_tarefa_e_submetida_deve_possuir_uma_descricao(cliente):
    resposta = cliente.post("/tarefas", json={"titulo": "titulo"})
    assert resposta.status_code == 422
```

:heavy_check_mark:

```python
class Tarefa(BaseModel):
    titulo: constr(min_length=3, max_length=50)
    descricao: str
```


:x:

```python
def test_descricao_da_tarefa_pode_conter_no_maximo_140_caracteres(cliente):
    resposta = cliente.post("/tarefas", json={"titulo": "titulo", "descricao": "*" * 141})
    assert resposta.status_code == 422
```

:heavy_check_mark:

```python
class Tarefa(BaseModel):
    titulo: constr(min_length=3, max_length=50)
    descricao: constr(max_length=140)
```

:x:

```python
def test_quando_criar_uma_tarefa_a_mesma_deve_ser_retornada(cliente):
    tarefa = {"titulo": "titulo", "descricao": "descricao"}
    resposta = cliente.post("/tarefas", json=tarefa)
    assert resposta.json() == tarefa
```

:heavy_check_mark:

```
@app.post('/tarefas')
def criar(tarefa: Tarefa):
    return tarefa
```

:x:

```python
def test_quando_criar_uma_tarefa_seu_id_deve_ser_unico(cliente):
    tarefa1 = {"titulo": "titulo1", "descricao": "descricao1"}
    tarefa2 = {"titulo": "titulo2", "descricao": "descricao1"}
    resposta1 = cliente.post("/tarefas", json=tarefa1)
    resposta2 = cliente.post("/tarefas", json=tarefa2)
    assert resposta1.json()["id"] != resposta2.json["id"]
```

:heavy_check_mark:

```python
from uuid import UUID, uuid4


class TarefaEntrada(BaseModel):
    titulo: constr(min_length=3, max_length=50)
    descricao: constr(max_length=140)


class Tarefa(TarefaEntrada):
    id: UUID


@app.post('/tarefas', response_model=Tarefa)
def criar(tarefa: TarefaEntrada):
    nova_tarefa = tarefa.dict()
    nova_tarefa.update({"id": uuid4()})

:x:

```python
def test_quando_criar_uma_tarefa_seu_estado_padrao_e_nao_finalizado(cliente):
    tarefa = {"titulo": "titulo", "descricao": "descricao"}
    resposta = cliente.post("/tarefas", json=tarefa)
    assert resposta.json()["estado"] ==  "não finalizado"
```

:heavy_check_mark:

```
from enum import Enum


class EstadosPossiveis(str, Enum):
    finalizado = "finalizado"
    nao_finalizado = "não finalizado"


class TarefaEntrada(BaseModel):
    titulo: constr(min_length=3, max_length=50)
    descricao: constr(max_length=140)
    estado: EstadosPossiveis = EstadosPossiveis.nao_finalizado
```

:x:

```python
def test_quando_criar_uma_tarefa_seu_estado_padrao_e_nao_finalizado(cliente):
    tarefa = {"titulo": "titulo", "descricao": "descricao"}
    resposta = cliente.post("/tarefas", json=tarefa)
    assert resposta.status_code == 202
```

:heavy_check_mark:

```python
@app.post('/tarefas', response_model=Tarefa, status_code=201)
def criar(tarefa: TarefaEntrada):
    nova_tarefa = tarefa.dict()
    nova_tarefa.update({"id": uuid4()})
    return nova_tarefa
```

:x:

```
def test_quando_criar_uma_tarefa_esta_deve_ser_persistida(cliente):
    tarefa = {"titulo": "titulo", "descricao": "descricao"}
    cliente.post("/tarefas", json=tarefa)
    assert resposta.status_code == 201
    assert len(TAREFAS) == 1
    TAREFAS.clear()
```

:heavy_check_mark:

```python
@app.post('/tarefas', response_model=Tarefa, status_code=201)
def criar(tarefa: TarefaEntrada):
    nova_tarefa = tarefa.dict()
    nova_tarefa.update({"id": uuid4()})
    TAREFAS.append(nova_tarefa)
    return nova_tarefa
```

Volte em todos os testes de sucesso acrescentando `TAREFAS.clear()`.

## Testando manualmente

`http localhost:8000 titulo="titulo" descricao="uma descrição qualquer"`

ou através da nossa interface (docs)

## Salvando a versão atual do código

Primeiro passo é checar o que foi feito até agora:

```bash
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gerenciador_tarefas/gerenciador.py
        modified:   tests/test_gerenciador.py

no changes added to commit (use "git add" and/or "git commit -a")
```

Vamos adicionar as alterações nos arquivos.

`$ git add gerenciador_tarefas/gerenciador.py tests/test_gerenciador.py`

:floppy_disk: Agora vamos marcar esta versão como salva.

`git commit -m "adicionando funcionalidade de criar tarefas"`

:octocat: Por fim envie ao github a versão atualizada do projeto.

`git push`

:cloud: E coloque no ar a nova versão

`git push heroku master`

:tada: Estamos ficando bons nisto. Vamos então nos desafiar agora nos proximos pasos!

[Listando tarefas :arrow_right:](listar.md)

[:arrow_left: Mandando um foguete pro espaço](deploy.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
