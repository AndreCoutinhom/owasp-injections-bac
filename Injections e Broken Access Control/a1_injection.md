# A1 Injection

> Falhas de injeção, como injeção de SQL, NoSQL, SO e LDAP, ocorrem quando dados não confiáveis são enviados a um interpretador como parte de um comando ou consulta. Os dados hostis do atacante podem induzir o interpretador a executar comandos não intencionais ou acessar dados sem a devida autorização.

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

> Uma aplicação é vulnerável a ataques quando:
> 
> * Dados fornecidos pelo usuário não são validados, filtrados ou sanitizados pela aplicação.
> 
> * Consultas dinâmicas ou chamadas não parametrizadas sem escape com reconhecimento de contexto são usadas diretamente no interpretador.
> 
> * Dados hostis são usados em parâmetros de pesquisa de mapeamento objeto-relacional (ORM) para extrair registros adicionais confidenciais.
> 
> * Dados hostis são usados diretamente ou concatenados, de forma que o SQL ou comando contenha tanto estrutura quanto dados hostis em consultas dinâmicas, comandos ou procedimentos armazenados.

Apesar de ser mais comum em SQL, Injection não é exclusivo dessa lingugagem. Não importa em qual linguagem seja. Toda e qualquer informação enviada pelos usuários finais para o servidor, precisa ser validada e sanitizada.

Ferramentas de auxílio podem ser encontradas na documentação da OWASP em relação a [ferramentas de análise de código fonte](https://owasp.org/www-community/Source_Code_Analysis_Tools) e [ferramentas de escaneamento de vulnerabilidades](https://owasp.org/www-community/Vulnerability_Scanning_Tools).

## Prevenção

> Prevenir injeção de SQL requer manter os dados separados de comandos e consultas.
> 
> * A opção preferida é usar uma API segura, que evita o uso completo do interpretador ou fornece uma interface parametrizada, ou migrar para o uso de ferramentas de mapeamento relacional de objeto (ORMs). Observação: Mesmo quando parametrizados, procedimentos armazenados ainda podem introduzir injeção de SQL se PL/SQL ou T-SQL concatenar consultas e dados, ou executar dados hostis com EXECUTE IMMEDIATE ou exec().
>   
> * Use validação de entrada do lado do servidor positiva ou "lista de permissões". Esta não é uma defesa completa, pois muitos aplicativos requerem caracteres especiais, como áreas de texto ou APIs para aplicativos móveis.
>   
> * Para qualquer consulta dinâmica residual, escape caracteres especiais usando a sintaxe de escape específica para aquele interpretador. Observação: A estrutura SQL, como nomes de tabelas, nomes de colunas e assim por diante, não pode ser escapada e, portanto, nomes de estrutura fornecidos pelo usuário são perigosos. Esse é um problema comum em softwares de criação de relatórios.
>   
> * Use LIMIT e outros controles SQL dentro das consultas para evitar a divulgação em massa de registros em caso de injeção de SQL.

No exemplo abaixo, a API Java [Prepared Statement](https://docs.oracle.com/javase/8/docs/api/java/sql/PreparedStatement.html) recebe os parâmetros de input do usuário separadamente, e importa essas informações com escapes de concatenação. 

``` java
PreparedStatement pstmt = con.prepareStatement("UPDATE EMPLOYEES
                                     SET SALARY = ? WHERE ID = ?");
   pstmt.setBigDecimal(1, 153833.00)
   pstmt.setInt(2, 110592)
```

Portanto, não é necessário realizar a sanitização das strings à mão, a própria API realiza esse procedimento. Ferramentas de mapeamento relacional de objetos (ORMs) como o [Hibernate](https://hibernate.org) também conseguem realizar esse procedimento.

Mesmo assim, o cuidado é necessário. Aplicações externas também podem ter possíveis quebras de segurança. É sempre importante executar o maior número de escapes de concatenação possíveis. Isso pode ser feito criando listas de parâmetros aceitos, adicionando caracteres de escape e acionando limitadores de uso. 

Em SQL, o escape pode ser feito utilizando `\` e o limitador de uso pode ser acionado com `limit 1` para limitar os parâmetros a um único usuário.

> "SEMPRE use `limit`" *Guilherme Silveira*.

## Testes

Não se pode realizar testes de injections aleatoriamente. Isso provavelmente será reconhecido como um ataque. Os testes precisam acontecer dentro de aplicações próprias ou em empresas nas quais possuímos autorização.

Esse tipo de teste só pode ser feito em ambientes em que se possua permissão de acesso e utilizando senhas e usuários fictícios feitos para os testes.

## Documentação OWASP Top 10 - 2017

Todas as informações destas anotações foram feitas à partir da documentação oficial da OWASP que pode ser acessada [aqui](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010-2017%20(en).pdf).

Informações específicas sobre o tópico **A1**, estão entre as páginas 6 e 7.

---
