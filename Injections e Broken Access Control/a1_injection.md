# A1 Injection

> "Falhas de injeção, como injeção de SQL, NoSQL, SO e LDAP, ocorrem quando dados não confiáveis são enviados a um interpretador como parte de um comando ou consulta. Os dados hostis do atacante podem induzir o interpretador a executar comandos não intencionais ou acessar dados sem a devida autorização." *OWASP Top 10 - 2017*

Os ataques de injeção são executados por pessoas que tentam adivinhar a estrutura dos arquivos de gerenciamento de banco de dados. A inserção de um comando SQL em um formulário, por exemplo, pode corromper a interpretação do servidor a ponto de conceder ao usuário acesso a recursos web que precisariam de autenticação.

No exemplo de injeção SQL abaixo, o uso do comando de comentário `#` é usado para desvalidar a autenticação pela senha. Além disso, o input `or admin=true` implementa um comando no sistema que pode permitir que o atacante acesse a conta de um administrador.

``` python
var sql = """
select * from Usuarios where email='""" + email + """'
and senha='""" + senha + """'
or admin=true#
select * from Usuarios where email='' or admin=true#'
and senha='243897879234324'
"""

```

O código acima se torna um ataque em potencial porque os dados informados pelos usuários não são validados. Além disso, a concatenação está sendo feita em `string` o que possibilita a entrada de dados no servidor pelo input da interface.

Tradicionalmente, esse problema seria evitado utilizando um conjunto de métodos chamado **sanitização de string**, que basicamente oferece meios de validação de `string`. No entanto, é um método extremamente trabalhoso e muito fácil de ser contornado.

Para isso há algumas bibliotecas que realizam esse processo automaticamente. [Hibernate](https://hibernate.org) é uma delas. A recomendação geral, tanto para linguagens de programação quanto para drivers, é sempre criar um escape para concatenação. Se for possível para um usuário inserir dígitos que interferem nas strings de um código presente no servidor, essa é uma grande porta de entrada para **Injection**.

> "Uma aplicação é vulnerável a ataques quando:
> 
> • Dados fornecidos pelo usuário não são validados, filtrados ou sanitizados pela aplicação.
> 
> • Consultas dinâmicas ou chamadas não parametrizadas sem escape com reconhecimento de contexto são usadas diretamente no interpretador.
> 
> • Dados hostis são usados em parâmetros de pesquisa de mapeamento objeto-relacional (ORM) para extrair registros adicionais confidenciais.
> 
> • Dados hostis são usados diretamente ou concatenados, de forma que o SQL ou comando contenha tanto estrutura quanto dados hostis em consultas dinâmicas, comandos ou procedimentos armazenados."
> 
> *OWASP Top 10 - 2017*

Não importa em qual linguagem seja. Toda e qualquer informação enviada pelos usuários finais para o servidor, precisa ser validada e sanitizada.

Ferramentas de auxílio podem ser encontradas na documentação da OWASP em relação a [ferramentas de análise de código fonte](https://owasp.org/www-community/Source_Code_Analysis_Tools) e [ferramentas de escaneamento de vulnerabilidades](https://owasp.org/www-community/Vulnerability_Scanning_Tools).

---
