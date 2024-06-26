# A6 Security Misconfiguration

> Configuração incorreta de segurança é o problema mais comum. Isso geralmente resulta de configurações padrão inseguras, configurações incompletas ou ad hoc, armazenamento em nuvem aberto, cabeçalhos HTTP mal configurados e mensagens de erro verbose contendo informações confidenciais. Não apenas todos os sistemas operacionais, frameworks, bibliotecas e aplicativos devem ser configurados com segurança, mas também devem ser corrigidos e atualizados em tempo hábil.

## Exemplos

É muito comum que alguns arquivos existam por padrão e acabam não sendo utilizados. Nesses casos, é sempre bom que um profissional de segurança cibernética verifique se os arquivos existentes em um projeto são de fato úteis; se forem, eles ficam, se não, eles vão embora.

Problemas de administração também são discutidos nesse tópico. Grandes acessos ilegais de contratados mal intencionados ocorrem por falhas na configuração de permissões do sistema. Esses problemas podem ainda resultar em falhas de acesso por pessoas autorizadas, quando problemas de configuração impedem que administradores acessem bancos de dados que precisam.

Usuários padrão são bastante comuns em sistemas operacionais para usar a maioria dos programas instalados no computador. O problema é que uma conta de usuário padrão possui login e senha padrão também. Lançar uma aplicação usando esse tipo de conta pode vulnerabilizar todo o seu sistema para ataques cibernéticos, considerando que seu login e senha são padrões de algum sistema operacional.

É comum que algumas lingugagens atribuam [stack trace](https://www.sentinelone.com/blog/javascript-stack-trace-understanding-it-and-using-it-to-debug/) em suas mensagens de erro. Isso também pode ser extremamente perigoso se usuários tiverem acesso ao histórico de ações de um software.

## Prevenção

Construir processos que aumentam a dificuldade de falhas de segurança. Quanto mais repetíveis forem os processos de aumento de segurança, mais fáceis são de se configurar e automatizar.

Limpeza de arquivos inúteis. Sempre se certifique que os arquivos presentes no projeto são absolutamente necessários. Isso ajuda a evitar lixo digital e manter o espaço disponível para atualizações frequentes em sistemas de segurança.

Confiar em [Security Headers](https://securityheaders.com) podem facilitar a padronização de segurança em protocolos web. Objetos padronizados facilitam a clareza na configuração.

## Documentação OWASP Top 10 - 2017

Todas as informações destas anotações foram feitas à partir da documentação oficial da OWASP que pode ser acessada [aqui](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010-2017%20(en).pdf).

Informações específicas sobre o tópico **A6** estão na página 12.

---
