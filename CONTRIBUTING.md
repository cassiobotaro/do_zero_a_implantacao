# Como contribuir

Primeiramente, muito obrigado pela disponibilidade em querer contribuir! 🫶

Estava lendo o repositório e teve uma nova ideia? Não entendeu alguma explicação, encontrou erros de grafia ou de código? Aqui você encontra um guia para você colaborar com a melhoria do material, indepedente do seu nível de conhecimento.

Entenda que não existem dúvidas simples demais e que toda contribuição é recebida com igual entusiasmo.

## Código de conduta

Trate todos igualmente com respeito e siga o nosso [código de conduta](CODE_OF_CONDUCT.md).

## Contribuições possíveis

Você pode ajudar o projeto das seguintes maneiras:

* Lendo o conteúdo e divulgando a seus conhecidos;
* Reportando erros de grafia encontrados no texto;
* Questionando explicações e solicitando uma melhoria no texto;
* Sugerindo melhorias do conteúdo;
* Adicionando novos materiais e tópicos.

## Sua primeira contribuição?

Caso queira apenas sugerir alguma modificação no conteúdo, vá em [issues](../../issues), certifique-se que alguém já não tenha feito a sugestão que você pretendia e tente descrver com maior riqueza de detalhes possíveis. Quando necessário adicione imagens (principalmente quando for um erro).

Uma outra maneira de contribuir, é editando você mesmo os arquivos através do github.

Acesse a pasta [`docs/`](docs) e escolha o arquivo que irá editar.

![image](https://user-images.githubusercontent.com/3127847/183785905-ee102868-b0e2-4f7d-ae1d-a105a74bb5f3.png)

Após escolher o arquivo, clique no lápis que aparece do lado direito para iniciar a edição do arquivo.

![image](https://user-images.githubusercontent.com/3127847/183786079-a8855609-db60-42b0-9972-54f48b370867.png)

Faça as alterações necessárias e e depois siga até o fim da página.

![image](https://user-images.githubusercontent.com/3127847/183786229-1581af1b-f74d-4a0a-a73f-3fdbc8ad9146.png)

Por fim, inicie a proposta de mudança.

![image](https://user-images.githubusercontent.com/3127847/183786943-cb3bdafb-b3d8-4db2-9af5-11f7f90c96e9.png)

Confira as alterações realizadas e através do botão `Create pull request`.

![image](https://user-images.githubusercontent.com/3127847/183790666-52b99bce-d777-4d26-a5a9-cfa9b4e726da.png)

Seu pedido de melhoria deve estar prenchido com o que preencheu anteriormente, mas caso precise, complemente com maiores detalhes.
Clique no botão `Create pull request` para finalizar a contribuição e aguarde.

![image](https://user-images.githubusercontent.com/3127847/183790791-3daefe6b-e4e7-4378-b645-fa5e29dd71c4.png)

Assim que a pessoa responsável analisar sua contribuição, suas alteraçês serão mescladas ao conteúdo.

![image](https://user-images.githubusercontent.com/3127847/183787281-c6947adb-eae1-4b67-8204-377f6766aff6.png)

🤖 Automaticamente, em poucos minutos uma nova versão do site já estará disponível!


## Desenvolvendo localmente

Crie um comando virtual utiliando o comando:

```
python -m venv .venv
```

Ative o ambiente através do comando:

```
source .venv/bin/activate
```

ou [equivalente em seu sistema operacional](https://cassiobotaro.dev/do_zero_a_implantacao/projeto/#o-ambiente-virtual).

Em seguida instale as dependências necesárias

```
python -m pip install -r requirements.txt
```

e para executar localmente:

```
python -m mkdocs serve
```

## Convenções utilizadas e dicas

* Não utilize emojis de forma textual `:emoji:`, copie do [emojipédia](https://emojipedia.org/pt) o invés;
* Todo título de seção é iniciado com um emoji;
* Novos capítulos devem ser adicionados também no menu de navegação que se encontra no arquivo `mkdocs.yml`;
