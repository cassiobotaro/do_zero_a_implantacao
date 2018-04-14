# :earth_americas: Um pouco sobre a web

<p align="center">
  <img style="float: right;" src="/imgs/web.jpg" alt="códigos html"/>
</p>

Antes de avançarmos com a criação da nossa aplicação, para nivelarmos a turma, vamos dar uma espiada em alguns conceitos de desenvolvimento web. Eles serão necessários o compreendimento dos tópicos a seguir.

Caso não seja novidade para você, tudo bem, pode pular este passo, mas se não se sentir confiante, dê uma olhada.

Aprenderemos um novo vocabulário com os tópicos a seguir, que são amplamente utilizados no desenvolvimento web, independente da linguagem. Iremos aprende-los de forma teórica e prática.

## URIs

### Conceito

Em português: Identificador de Recursos Universal, como diz o próprio nome, é o identificador do recurso. Pode ser uma imagem, uma página, etc, pois tudo o que está disponível na internet precisa de um identificador único para que não seja confundido.

### Prática

Abra um terminal e navegue até dentro do nosso projeto, digite `pipenv run http http://httpbin.org/anything`.

Nesse caso nosso recurso único acessado é um texto em formato json, com informações sobre a conexão.

Experimente também as seguintes URIs:

`pipenv run http http://httpbin.org/anything/resource`

`pipenv run http http://httpbin.org/anything/resource/42`

`pipenv run http http://httpbin.org/anything/resource/42?q=teste&a=b`

Na primeira e segunda URI, temos a mudança do nosso recurso, que na primeira URI é `/anything/resource` e a segunda é `/anything/resource/42`. A mudança nesta parte da URI que chamamos de `caminho` ou `path` é o que caracteriza como outro recurso diferente.

A terceira é o mesmo `caminho` da segunda porém a presença de parametros na URI pode afetar o retorno daquele recurso.

## Requisição (`request`) e Resposta (`response`)

### Conceito

A comunicação entre o servidor é `stateless`, o que significa que não há persistência de informações. Temos então dois instantes, que são, o momento que o pedido realizado pelo cliente chega ao servidor que referimos como requisição ou popularmente conhecido como `request` e este termo é adotado por vários frameorks e outro que é a resposta do servidor ao pedido por aquele recurso, que é conhecido como resposta ou `response`.

A requisição contém informação sobre o pedido de um recurso, pode ser um cabeçalho indicando o tipo daquele recurso ou os tipos de retorno aceitos como resposta. Pode conter dados de um formulário ou argumentos para filtragem de um recurso.

A resposta como o próprio nome diz, é o recurso pedido pelo cliente. Não necessariamente é texto, pode ser algum tipo de recurso binário como imagens.

### Prática

Experimentem estas uri's.

`pipenv run http http://httpbin.org/image/png`

`pipenv run http http://httpbin.org/encoding/utf8`

`pipenv run http http://httpbin.org/xml`

O primeiro recurso é uma imagem em formato png, caso queira ver esta imagem, abra um navegador e cole a url lá. Já o segundo recurso acessado é um texto em codificação utf-8. E por fim temos um texto em formato xml.

Prestem bastante atenção nos cabeçalhos.

## Código de status

### Conceito

A resposta de um servidor pode ser sucesso ou não, pode ser que o recurso pedido tenha sido movido de lugar. Quando há um erro, como saber se o erro foi com o cliente, ou com o servidor?

É pensando nestas respostas que o protocolo http, utiliza códigos que indicam o que ocorreu com a resposta.

Os mais famos deles são o `404 - Não encontrado`, que me diz que o recurso pedido não foi encontrado. O `200 - OK` que significa que a resposta obteve sucesso e também `500 - Erro interno do servidor`.

Alguns outros não tão famosos mas também importantes são o `201 - Criado`, `204 - Nenhum conteúdo`, `301 - Movido permanentemente`, `400 - Requisição inválida`e o `401 - Não autorizado`.

Uma lista com estes status pode ser encontrada [aqui](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status).

É importante saber que eles são divididos em categorias, aqueles iniciados com 1 são respostas informativas, com 2 são categoria de sucesso, com 3 significa uma redireção, com 4 erro do cliente e com 5 erro do servidor.


### Prática

Rode o seguinte comando.

`pipenv run http http://httpbin.org/status/418`

Experimente trocar o status na uri e veja as mensagens retornadas.

## Verbos HTTP

### Conceito

Os verbos indicam a ação executada sobre algum recurso. Os mais famosos são o `GET` e o `POST`, que são responsáveis respectivamente por solicitar uma representação de um recurso e submeter uma entidade a um recurso específico, às vezes causando uma mudança no estado do recurso.

:confused: Uma curiosidade, você sabe a diferença entre o verbo `PUT` e o `PATCH`?

O verbo PUT substitui todas as atuais representações de seu recurso alvo pela carga de dados da requisição, já o PATCH somente modifica parcialmente o recurso.

Veja a [lista](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods) para saber mais sobre os verbos http.

### Prática

Veja um exemplo de `GET`.

`pipenv run http GET http://httpbin.org/get`

Substitua o verbo e veja funcionando os outros verbos http. Fique atento que os verbos após o http devem ser escritos com letra maiúscula.

:smile: Bem legal não é? E agora, já vamos logo escrever código? Sim e não, vamos agora dar uma passada na linguagem Python.


[Primeiros passos com python :arrow_right:](python.md)

[:arrow_left: Iniciando o projeto](projeto.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
