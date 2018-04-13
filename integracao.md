# :heavy_check_mark: Integração contínua

<p align="center">
  <img style="float: right;" src="/imgs/ci.jpg" alt="continous integration"/>
</p>

## Conceito

O desenvolvedor integra o código alterado e/ou desenvolvido ao projeto principal na mesma frequência com que as funcionalidades são desenvolvidas, sendo feito muitas vezes.

Todo o nosso projeto será contruído utilizando testes automatizados, e sempre rodaremos os testes localmente.

Mas como garantir que minha alteração não impacta com o restante do projeto, ter isto de forma simples e automatizada?
Como garantir que a qualidade do código foi mantida?

Utilizaremos o serviço [travis](https://travis-ci.org/) para checar que nosso código não quebra a "build", ou seja, quando integrado o novo código ao sistema, todo o sistema continua funcional.

Basicamente, a grande vantagem da integração contínua está no feedback instantâneo. Isso funciona da seguinte forma: a cada commit no repositório, o build é feito automáticamente, com todos os testes sendo executados de forma automática e falhas sendo detectadas. Se algum commit não compilar ou quebrar qualquer um dos testes, a equipe toma conhecimento instantâneamente (através de email, por exemplo, indicando as falhas e o commit causador das mesmas). A equipe pode então corrigir o problema o mais rápido possível, o que é fundamental para não introduzir erros ao criar novas funcionalidades, refatorar, etc. Integração contínua é mais uma forma de trazer segurança em relação a mudanças: você pode fazer modificações sem medo, pois será avisado caso algo saia do esperado.

## Passo a passo

Utilize sua conta do github para cadastrar no travis.

![Cadastro no travis](imgs/cadastro_travis.png "Cadastro no travis")

Seus projetos estarão listados da seguinte maneira

![listagem projetos](imgs/projetos_travis.png "projetos travis")

Escolha o projeto todoapp e habilite a integração contínua.

![habilita projeto](imgs/habilitar_travis.png "habilitar travis")

No seu projeto crie um arquivo chamado `.travis.yml` com o seguinte conteúdo.

```yaml
language: python
python:
    - 3.6
install:
  - pip install -U pipenv
  - pipenv install --dev
script:
  - pytest
```

:tada: Pronto, a partir de agora, o travis irá rodar todos os testes do seu projeto de forma automatizada e indicara se a construção do mesmo está com problemas.

Isto será extremamente útil nos póximos passos.

:floppy_disk: Para terminar a integração com travis, salve a versão atual do projeto e veja a primeira contrução sendo realizada.

`git commit -m "integração contínua"`

:octocat: Por fim envie ao github a versão atualizada do projeto.

`git push`

[Mandando um foguete pro espaço :arrow_right:](deploy.md)

[:arrow_left: Hello Flask](hello_flask.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
