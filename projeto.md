# Iniciando o projeto

inicia projeto e instala libs python

## :dog: Flask

**O que é?**

O [flask](http://flask.pocoo.org/) é uma ferramenta para desenvolvimento web bastante conhecido por sua arquitetura minimalista.

**Para que serve?**

Serve para escrevermos nossa aplicação web de forma rápida e customisável.

Possui funções que auxiliam operações como roteamento, tratamento de requisições, renderização de conteúdo, gerenciamento de sessão e cookies, assim como várias outras que são típicas da web.

**Como instalar**

:warning: Preste atenção que os comandos serão executados dentro do diretório do projeto.

:computer: *windows*

Clique no botão iniciar, digite `cmd` e abra o programa `prompt de comandos`. Navegue ate o nosso projeto e agora digite `pipenv install flask`.

:package: *ubuntu*

Abra um terminal, navegue até a pasta do projeto e por fim digite `pipenv install flask`.

**Vamos verificar se deu tudo certo?**

:computer: *windows*

Clique no botão iniciar, digite `cmd` e abra o programa `prompt de comandos`. Agora digite `pipenv run python -m flask --version`.

:package: *ubuntu*

Abra um terminal e digite `pipenv run python -m flask --version`.

A saída para ambos os sistemas operacionais deverá ser similar a apresentada abaixo:

```bash
$ pipenv run python -m flask --version
Flask 0.12.2
Python 3.6.4 (default, Jan  5 2018, 02:35:40)
[GCC 7.2.1 20171224]
```

## :link: Httpie

**O que é?**

[HTTPie](https://github.com/jakubroztocil/httpie) é um cliente HTTP por linha de comando. Seu objetivo é transformar a interação com serviços web o mais humano possível.

**Para que serve?**

Diversos momentos do curso, teremos de testar manualmente se nosso sistema está funcionando, ainda que possua testes unitários.

Esta ferramenta ajuda a fazer estes testes de uma maneira mais simples.

**Como instalar**

:warning: Muita atenção pois os comandos de instalação deste pacote terão o serão feitos com a opção `--dev` que indica que esta biblioteca é utilizada só para testar localmente, não sendo necessária para o programa rodar.

:computer: *windows*

Clique no botão iniciar, digite `cmd` e abra o programa `prompt de comandos`. Navegue ate o nosso projeto e agora digite `pipenv install --dev httpie`.

:package: *ubuntu*

Abra um terminal, navegue até a pasta do projeto e por fim digite `pipenv install --dev httpie`.

**Vamos verificar se deu tudo certo?**

:computer: *windows*

Clique no botão iniciar, digite `cmd` e abra o programa `prompt de comandos`. Agora digite `pipenv run http --version`.

:package: *ubuntu*

Abra um terminal e digite `pipenv run http --version`.

:warning: Note que foi utilizado o comando http ao invés de httpie, este é o nome do executável do httpie depois de instalado no sistema.

A saída para ambos os sistemas operacionais deverá ser similar a apresentada abaixo:

```bash
$ pipenv run http --version
0.9.9
```

## :traffic_light: Pytest

**O que é?**

O framework [pytest](https://docs.pytest.org/en/latest/) é fácil para escrever teste simples, ainda escala para suportar testes funcionais complexos para aplicações e bibliotecas.

**Para que serve?**

Já dizia Michael C. Feathers, "Um código sem testes, é um código ruim. Não importa quão bem ele foi escrito".  Vamos então instalar o pytest, que é uma ferramenta que auxilia na execução de testes.

**Como instalar**

:warning: Muita atenção pois os comandos de instalação deste pacote terão o serão feitos com a opção `--dev` que indica que esta biblioteca é utilizada só para testar localmente, não sendo necessária para o programa rodar.

:computer: *windows*

Clique no botão iniciar, digite `cmd` e abra o programa `prompt de comandos`. Navegue ate o nosso projeto e agora digite `pipenv install --dev pytest`.

:package: *ubuntu*

Abra um terminal, navegue até a pasta do projeto e por fim digite `pipenv install --dev pytest`.

**Vamos verificar se deu tudo certo?**

:computer: *windows*

Clique no botão iniciar, digite `cmd` e abra o programa `prompt de comandos`. Agora digite `pipenv run python -m pytest --version`.

:package: *ubuntu*

Abra um terminal e digite `pipenv run python -m pytest --version`.

A saída para ambos os sistemas operacionais deverá ser similar a apresentada abaixo:

```bash
$ pipenv run python -m pytest --version
This is pytest version 3.4.2, imported from /home/cassiobotaro/.virtualenvs/todo.app-AIIv-fDj/lib/python3.6/site-packages/pytest.py
```

[Um pouco sobre a web :arrow_right:](web.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
