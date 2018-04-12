# :goat: Desenvolvimento guiado por testes (TDD)

Desenvolvimento guiado por testes(Test Driven Development) é uma técnica de desenvolvimento de software que baseia em um ciclo curto de repetições: Primeiramente o desenvolvedor escreve um caso de teste automatizado que define uma melhoria desejada ou uma nova funcionalidade. Então, é produzido código que possa ser validado pelo teste para posteriormente o código ser refatorado para um código sob padrões aceitáveis.

É um ciclo de desenvolvimento que segue os seguintes passos:

**1 - Adicione um teste**

Normalmente analisamos alguma funcionalidade que desejamos implementar ou validar e escrevemos um teste que será executado automaticamente relacionado aquela funcionalidade.
Ainda que uma funçãoi/classe não exista, devemos escrever o comportamento esperado da mesma.

**2 - Verifique se algum teste quebrou**

Neste ponto devemos verificar se os testes passam a falhar(os antigos e o que você acabou de escrever)

**3 - Escreva código**

Escreva código necessário para que seu teste seja contemplado, mas evite escrever muito além do que necessário.

**4 - Refatore seu código**

Com os testes passando, analise se é possível alguma refatoração.

**5 - Vá para o passo 1**

![Círculo do TDD](imgs/tdd.png "Ciclo do tdd")

[Vamos escrever código :arrow_right:](codigo.md)

[:arrow_left: Primeiros passos com python](python.md)

[:leftwards_arrow_with_hook: Voltar ao README ](README.md)
