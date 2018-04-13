# Iniciando o projeto

<p align="center">
  <img style="float: right;" src="/imgs/blueprint.jpg" alt="Blueprint do projeto"/>
</p>

Já temos as espátulas, facas, colheres e outros instrumentos na mesa, mas para prosseguirmos, precisamos escolher os melhores ingradientes.

Antes de instalar as bibliotecas que utilizaremos durante o nosso projeto, precisamos inicializá-lo.

## :arrow_forward: Começando a tirar do papel o projeto

O primeiro passo para desenvolvimento do nosso aplicativo web é criá-lo utilizando um controle de versão.Para este minicurso optei pelo controle de versão mais popular hoje em dia que se chama git.

Aproveitando esta escolha, como o Github é gratuito e também o mais conhecido, vamos hospedar o projeto lá(que irá ajudar com algumas integrações futuramente).

Aperte o botão novo_repositório.

![novo repositório](imgs/novo_repositorio.png " Novo repositório")

Preencha os campos como visto na imagem abaixo.

![novo repositório](imgs/novorepo.png "Novo repositório")

Agora faça um "clone" do seu repositório.

```bash
$ git clone https://github.com/cassiobotaro/todoapp.git
Cloning into 'todoapp'...
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 5 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (5/5), done.

```

Aproveite e já configure seu usuário git para este projeto, dentro do diretório recém clonado digite os seguintes comandos.

```bash
$ git config --local user.email emailutilizado@github.com

$ git config --local user.name usernamegithub
```

"Voilà", já temos o projeto iniciado.

Navegue até o diretório onde foi executado o comando de `clone` do projeto. Prossiga com a instalação das bilbiotecas de acordo com o seu sistema operacional.

:warning: Não se esqueça de entrar no diretório do projeto antes de continuar a instalação das bibliotecas.

## :books: Bibliotecas e utilitários

Chegou a hora de instalar algumas bibliotecas e utilitários que nos auxiliarão na criação do nosso sistema web, na realização de testes unitários e testes manuais.

Siga os passos de acordo com o seu sistema operacional para cada ferramenta. Tenha sempre certeza de que a ferramenta está instalada e funcionando.

### :dog: Flask

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

### :link: Httpie

**O que é?**

[HTTPie](https://github.com/jakubroztocil/httpie) é um cliente HTTP por linha de comando. Seu objetivo é transformar a interação com serviços web o mais humano possível.

**Para que serve?**

Diversos momentos do curso, teremos de testar manualmente se nosso sistema está funcionando, ainda que possua testes unitários.

Esta ferramenta ajuda a fazer estes testes de uma maneira mais simples.

**Como instalar**

:warning: Muita atenção, pois os comandos de instalação deste pacote terão o serão feitos com a opção `--dev` que indica que esta biblioteca é utilizada só para testar localmente, não sendo necessária para o programa rodar.

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

### :traffic_light: Pytest

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

Neste momento seu diretório deve estar assim:

```
.
├── LICENSE
├── Pipfile
├── Pipfile.lock
└── README.md
```

Vamos testar nossa instalção então?

```bash
$ python3
Python 3.6.2 (default, Jul 20 2017, 03:52:27)
[GCC 7.1.1 20170630] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import flask
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'flask'
>>>
```

:scream: Se entramos no python e tentamos importar a biblioteca flask, um erro é retornado dizendo que o módulo não foi encontrado.

Acontece que instalamos o flask somente no ambiente virtual. Para entrarmos no ambiente virtual digite `pipenv shell`.

```bash
$ python3
Python 3.6.2 (default, Jul 20 2017, 03:52:27)
[GCC 7.1.1 20170630] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import flask
>>>
```

Instalado as dependências, vamos salvar uma primeira versão do nosso projeto com o nosso andamento?

Primeiro passo é checar o que foi feito até agora:
```bash
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	Pipfile
	Pipfile.lock

nothing added to commit but untracked files present (use "git add" to track)
```

Vemos dois arquivos não rastreados, precisamos avisar ao controle de versão que monitore estes arquivos.

`$ git add Pipfile Pipfile.lock`

:floppy_disk: Agora vamos marcar esta versão como salva.

`git commit -m "adionando dependências do projeto"`

:octocat: Por fim, envie ao github a versão atualizada do projeto.

`git push`

:cake: Entusiasmados a começar a escrever sua aplicação? Agora que temos todo o ambiente configurado, já estamos bem próximo disso, faremos um nivelamento de conhecimento sobre web e python e em breve termos nossa aplicação no ar!

[Um pouco sobre a web :arrow_right:](web.md)

[:arrow_left: Escolhendo as melhores ferramentas](ferramentas.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
