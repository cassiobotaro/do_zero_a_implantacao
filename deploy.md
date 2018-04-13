# :rocket: Mandando um foguete para o espaço

<p align="center">
  <img style="float: right;" src="/imgs/python_rocket.png" alt="snake in a rocket"/>
</p>

# Hora do deploy

Neste passo iremos colocar no ar a aplicação utilizando a plataforma [heroku](https://www.heroku.com/home).

A heroku é uma plataforma de nuvem como serviço, suportando várias linguagens de programação que é utilizada como modelo de implementação de aplicativos web.

Em termos simples, a plataforma recebe a sua base de código, identifica a linnguagem de programação e ferramentas utilizadas e coloca no ar sua aplicação, sem precisar se preocupar com configuração complexa de infraestrutura.

Quando utilizamos o termo `deploy`, estamos falando da implementação da nossa aplicação web, ou seja, colocar a nossa aplicação no ar.

Primeiro passo para fazermos deploy da versão atual do nosso software é se registrar na plataforma.

É uma plataforma grátis para aplicativos de pequeno porte e uma opção também para aplicativos maiores.

Acesse https://signup.heroku.com/ e preencha o formulário.

![formulário heroku](imgs/form-heroku.png)

Em um terminal faça login em sua conta recém criada através do comando `heroku login`.

Crie uma aplicação no Heroku, preparando a heroku para receber seu código-fonte.

```bash
$ heroku create
Creating app... done, ⬢ warm-springs-22819
https://warm-springs-22819.herokuapp.com/ | https://git.heroku.com/warm-springs-22819.git
```

Com este comando um repositório remoto é vinculado ao seu repositório local e cada vez que quiser modificar a versão do código rodando, basta enviar seu código para este repositório remoto. Esta ação desencadeia toda uma nova implementação da sua aplicação.

Antes de enviar pela primeira vez nosso código, vamos fazer as últimas configurações necessárias.

O Heroku utiliza um arquivo chamado `Procfile` que contém informações de como rodar sua aplicação. Crie este arquivo com o seguinte conteúdo.

`web: FLASK_APP=todo.py flask run --host=0.0.0.0 --port=$PORT`

Agora vamos a implantação do sistema.

É simples como `git push heroku master`.

```bash
$ git push heroku master
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (10/10), 3.11 KiB | 1.04 MiB/s, done.
Total 10 (delta 1), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote: 
remote: -----> Python app detected
remote: -----> Installing python-3.6.4
remote: -----> Installing pip
remote: -----> Installing dependencies with Pipenv 11.8.2…
remote:        Installing dependencies from Pipfile.lock (816422)…
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote: 
remote: -----> Compressing...
remote:        Done: 53.4M
remote: -----> Launching...
remote:        Released v3
remote:        https://warm-springs-22819.herokuapp.com/ deployed to Heroku
remote: 
remote: Verifying deploy... done.
To https://git.heroku.com/warm-springs-22819.git
 * [new branch]      master -> master
```

# Deu certo?

Para verificarmos se a implantação deu certo, digite `heroku open` e lembre-se que o recurso está em `/task` ou copie a url retornada no comando de implantação acrescentando `/task` e utilize o httpie para testar assim como foi feito localmente.

No nosso exemplo seria `pipenv run http https://warm-springs-22819.herokuapp.com/task`.

Verifique se uma resposta 200 OK foi obtida.

:trollface: Acabou, é isso pessoal! Já temos uma aplicação no ar e podemos ir embora.

Brincadeira, foi legal ter a nossa primeira versão da aplicação no ar, mas agora precisamos evolui-la.

[Criando uma tarefa :arrow_right:](criar.md)

[:arrow_left: Integração contínua](integracao.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
