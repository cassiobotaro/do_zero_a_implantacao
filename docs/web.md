# 🌎 Um pouco sobre a web

<figure markdown>
  ![Códigos HTML](imgs/web.jpg)
  <figcaption></figcaption>
</figure>

Antes de avançarmos com a criação da nossa aplicação, para nivelarmos a turma, vamos dar uma espiada em alguns conceitos de desenvolvimento web. Eles serão necessários para o compreendimento dos tópicos a seguir.

Caso não seja novidade para você, tudo bem, pode pular este passo, mas se não se sentir confiante, dê uma olhada.

Aprenderemos um novo vocabulário com os tópicos a seguir, que são amplamente utilizados no desenvolvimento web, independente da linguagem. Iremos aprende-los de forma teórica e prática.

## Cliente

### Conceito

Aquele que solicita algum serviço/recurso ao servidor.

### Prática

O seu navegador é um cliente de recursos. Quando acessamos um site, tipicamente o navegador recupera páginas no formato html, folhas de estilo que serão responsáveis por dar cores e estilos aos elementos da página. Também recupera javascripts que serão responsáveis por executar algumas funções e imagens, vídeos, aúdios, etc.

Mas cliente não se limita ao navegador, por exemplo, utilizaremos o httpie para fazer requisições http e solicitar recursos ao servidor.

Execute o comando abaixo e veja o cliente de linha de comando em ação.

```
http https://cassiobotaro.dev/do_zero_a_implantacao
```

## Servidor

### Conceito

Provê um serviço/recurso para o cliente conforme solicitado.

### Prática

O servidor é um processo que executa alguma tarefa, como um banco de dados, um servidor de arquivos, um servidor de e-mail, um servidor de aplicações, etc.

Utilizaremos o `uvicorn` como nosso servidor da aplicação.

Execute o comando abaixo e veja um servidor simples, que responde a requisições com o conteúdo do diretório atual.

```
python -m http.server
```

## Recurso

### Conceito

Um recurso é um mapeamento de alguma coisa do mundo real para um recurso da web.

### Prática

Um exemplo de recurso é o wttr.in que retorna uma previsão do tempo para um determinado local.

```
http wttr.in
```

Outro exemplo de recurso é o github.com que retorna o repositório do Cassio Botaro.

```
http https://api.github.com/users/cassiobotaro
```

## URIs

### Conceito

Em português: Identificador de Recursos Universal, como diz o próprio nome, é o identificador do recurso. Pode ser uma imagem, uma página etc., pois tudo o que está disponível na internet precisa de um identificador único para que não seja confundido.

### Prática

Abra um terminal e navegue até dentro do nosso projeto, digite `http http://httpbin.org/anything`.

Nesse caso nosso recurso único acessado é um texto em formato json, com informações sobre a conexão.

Experimente também as seguintes URIs:

`http https://swapi.dev/api/people/3/`

`http https://swapi.dev/api/starships/10/`

`http http://httpbin.org/anything`

`http http://httpbin.org/anything?argumento=valor`

Na primeira e segunda URI, temos a mudança do nosso recurso, que na primeira URI é `/api/people/3/` e a segunda é `/api/starships/10/`. A mudança nesta parte da URI que chamamos de `caminho` ou `path` é o que caracteriza como outro recurso diferente.

A terceira é o mesmo `caminho` da quarta porém a presença de parametros na URI pode afetar o retorno daquele recurso.

## Requisição (`request`) e Resposta (`response`)

### Conceito

A comunicação entre o servidor é `stateless`, o que significa que não há persistência de informações. Temos então dois instantes, que são, o momento que o pedido realizado pelo cliente chega ao servidor que referimos como requisição ou popularmente conhecido como `request` e este termo é adotado por vários frameworks e outro que é a resposta do servidor ao pedido por aquele recurso, que é conhecido como resposta ou `response`.

A requisição contém informação sobre o pedido de um recurso, pode ser um cabeçalho indicando o tipo daquele recurso ou os tipos de retorno aceitos como resposta. Pode conter dados de um formulário ou argumentos para filtragem de um recurso.

A resposta como o próprio nome diz, é o recurso pedido pelo cliente. Não necessariamente é texto, pode ser algum tipo de recurso binário como imagens.

### Prática

Experimentem estas uri's.

`http http://httpbin.org/image/png`

`http http://httpbin.org/encoding/utf8`

`http http://httpbin.org/xml`

O primeiro recurso é uma imagem em formato png, caso queira ver esta imagem, abra um navegador e cole a url lá. Já o segundo recurso acessado é um texto em codificação utf-8. E por fim temos um texto em formato xml.

Prestem bastante atenção nos cabeçalhos.

## Código de status

### Conceito

A resposta de um servidor pode ser sucesso ou não, pode ser que o recurso pedido tenha sido movido de lugar. Quando há um erro, como saber se o erro foi com o cliente, ou com o servidor?

É pensando nestas respostas que o protocolo http, utiliza códigos que indicam o que ocorreu com a resposta.

Os mais famosos deles são o `404 - Não encontrado`, que me diz que o recurso pedido não foi encontrado. O `200 - OK` que significa que a resposta obteve sucesso e também `500 - Erro interno do servidor`.

Alguns outros não tão famosos mas também importantes são o `201 - Criado`, `204 - Nenhum conteúdo`, `301 - Movido permanentemente`, `400 - Requisição inválida`e o `401 - Não autorizado`.

Uma lista com estes status pode ser encontrada [aqui](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status).

É importante saber que eles são divididos em categorias, aqueles iniciados com 1 são respostas informativas, com 2 são categoria de sucesso, com 3 significa uma redireção, com 4 erro do cliente e com 5 erro do servidor.


### Prática

Rode o seguinte comando.

`http http://httpbin.org/status/418`

Experimente trocar o status na uri e veja as mensagens retornadas.

## Verbos HTTP

### Conceito

Os verbos indicam a ação executada sobre algum recurso. Os mais famosos são o `GET` e o `POST`, que são responsáveis respectivamente por solicitar uma representação de um recurso e submeter uma entidade a um recurso específico, às vezes causando uma mudança no estado do recurso.

😕 Uma curiosidade, você sabe a diferença entre o verbo `PUT` e o `PATCH`?

O verbo PUT substitui todas as atuais representações de seu recurso alvo pela carga de dados da requisição, já o PATCH somente modifica parcialmente o recurso.

Veja a [lista](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods) para saber mais sobre os verbos http.

### Prática

Veja um exemplo de `GET`.

`http GET http://httpbin.org/get`

Um exemplo de post.

`http POST http://httpbin.org/post data=valor`

Substitua o verbo e veja funcionando os outros verbos http. Fique atento que os verbos após o http devem ser escritos com letra maiúscula.

Existem outros conceitos como sessões, cookies, cabeçalhos, etc. Recomendo a leitura do [documento de referência](https://developer.mozilla.org/pt-BR/docs/Web/HTTP) para saber mais sobre esses conceitos.

😊 Bem legal não é? E agora, já vamos logo escrever código? Sim e não, vamos agora dar uma passada na linguagem Python.
