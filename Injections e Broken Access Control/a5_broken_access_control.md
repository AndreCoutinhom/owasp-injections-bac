# A5 Broken Access Control

> Restrições sobre o que usuários autenticados têm permissão para fazer frequentemente não são aplicadas corretamente.
>
> Invasores podem explorar essas falhas para acessar funcionalidades e/ou dados não autorizados, como acessar contas de outros usuários, visualizar arquivos confidenciais, modificar dados de outros usuários, alterar direitos de acesso, etc.

Um exemplo bastante simples é quando consideramos dados de cadastro como entrada para páginas específicas. O código abaixo demonstra como esses dados podem ser organizados:

``` python
def perfil(numero):
        dados = carrega_do_banco(numero)
        return pagina_renderizada(dados)

```

No entanto, com o código escrito assim, qualquer um que tiver acesso a URI que carrega a página, poderá ter acesso à conta e aos dados do usuário referente. Portanto, é necessário que se apliquem condições para autenticar a veracidade do usuário que está tentando acessar a página. Um exemplo básico à partir do código acima é com uma função `if` e `else`. Se a condição não for cumprida, é gerado o erro `404`:

``` python
def perfil(numero):
    if meu_usuario_logado.pode_acessar_perfil(numero):
        dados = carrega_do_banco(numero)
        return pagina_renderizada(dados)
    else:
        abort(404)

```

Essas autenticações podem ser muito trabalhosas quando programadas manualmente. Por isso é muito comum que se encontrem brechas nos algoritmos. Essas brechas podem ser encontradas na URL, compartilhamento de contas, JSON Web Tokens (JWT), integração de APIs externas ([CORS](https://aws.amazon.com/pt/what-is/cross-origin-resource-sharing/#:~:text=O%20CORS%20define%20uma%20maneira,código%20no%20lado%20do%20cliente.)), etc.

## Prevenção

A forma mais clara de se previnir esse tipo de ataque é não oferecer controle de acesso para usuários. Tudo aquilo que envolve algoritmos e scripts referentes a controle de acesso, deve ser organizado e monitorado unicamente por desenvolvedores confiáveis. APIs, bibliotecas e frameworks a serem usados precisam ter como característica a impossibilidade de oferecer acesso a usuários externos. Caso não haja uso de microsserviços, é ideal que o sistema de controle de acesso seja um monolito.

A definição de quais arquivos podem ser vistos precisa ser definida manualmente. Isso exige bastante dedicação por parte dos desenvolvedores para deixar o bucket S3 totalmente fechado e controlar manualmente quais arquivos podem ser acessados pelos usuários.

Mesmo com alta criptografia e complexidade de digitação, buckets abertos (com acesso pela web) podem ser identificados por navegadores como o Google Chrome e disponibilizados abertamente. A menos que o bucket aberto seja totalmente seguro, não se recomenda deixar qualquer bucket aberto. É importante lembrar que buckets abertos podem ser mais práticos quando as tarefas precisam ser divididas em equipes remotas.

## Documentação OWASP Top 10 - 2017

Todas as informações destas anotações foram feitas à partir da documentação oficial da OWASP que pode ser acessada [aqui](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010-2017%20(en).pdf).

Informações específicas sobre o tópico **A5** estão na página 11.

---
