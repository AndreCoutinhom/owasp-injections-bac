# A4 XML External Entities

> Muitos processadores XML antigos ou mal configurados avaliam referências de entidade externa em documentos XML. Entidades externas podem ser usadas para divulgar arquivos internos usando o manipulador de URI de arquivo, compartilhamentos de arquivos internos, varredura de porta interna, execução remota de código e ataques de negação de serviço.

XML é um tipo de linguagem de marcação da W3C, derivada da linguagem SGML, utilizada para compartilhamento fácil de informações por intermédio da internet.

A XML oferece suporte ao intercâmbio de informações entre sistemas de computador, como sites, bancos de dados e aplicações de terceiros.

``` xml
<contato>
  <nome>Guilherme</nome>
  <telefone>3217372</telefone>
</contato>

```

O risco na estrutura do XML é quando um arquivo utiliza entidades para declarar valores não típicos. Se usarmos uma entidade para definir o nome no exemplo acima, ficaria desse jeito:

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<!ENTITY meunome TEXT "Guilherme">
<!DOCTYPE Contato

<contato>
  <nome>&meunome; </nome>
  <nome-oficial>&meunome;</nome-oficial>
  <telefone tipo="residencial">3217372</telefone>  
  <telefone tipo="comercial">3217372</telefone>
  <telefone tipo="celular">3217372</telefone>

</contato>
```

Dessa forma o sistema não precisa ler o nome `Guilherme` todas as vezes. Mas há um problema quando o arquivo XML não está preparado para bloquear entidades externas, porque se sim isso pode acontecer:

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<!ENTITY meunome SYSTEM "file:///etc/passwd">
<!DOCTYPE Contato

<contato>
  <nome>&meunome; </nome>
  <nome-oficial>&meunome;</nome-oficial>
  <telefone tipo="residencial">3217372</telefone>  
  <telefone tipo="comercial">3217372</telefone>
  <telefone tipo="celular">3217372</telefone>

</contato>
```

Assim, o nome do contato atribuído se torna a lista de senhas dos usuários gravados no servidor e elas são expostas para o cliente que fez a requisição. Mais uma vez, é reforçada a necessidade de não armazenar senhas em um arquivo desprotegido como discutido no A3.

Essa estratégia pode tirar proveito de sistemas mau organizados. Dependendo da requisição, requisições em XML podem extrair informações do sistema e até embutir malwares.

## Prevenção

O método mais simples de prevenção, além de não serializar dados sensíveis como já falado no A3, é utilizar o JSON para formatar os dados. O JSON não é tão propenso a sistemas complexos como o XML, mas ele não é vulnerável a entidades externas.

Mesmo assim, no XML existem [métodos para nunca processar entidades externas](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html). Tais métodos podem inclusive prevenir ataques de injeção vistos no A1.

## Documentação OWASP Top 10 - 2017

Todas as informações destas anotações foram feitas à partir da documentação oficial da OWASP que pode ser acessada [aqui](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010-2017%20(en).pdf).

Informações específicas sobre o tópico **A4** estão na página 10.

---
