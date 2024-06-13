# A7 Cross Site Scripting

> Falhas de XSS ocorrem sempre que um aplicativo inclui dados não confiáveis em uma nova página da web sem validação ou escape apropriados, ou atualiza uma página da web existente com dados fornecidos pelo usuário usando uma API do navegador que pode criar HTML ou JavaScript. O XSS permite que invasores executem scripts no navegador da vítima, o que pode sequestrar sessões do usuário, desfigurar sites da web ou redirecionar o usuário para sites maliciosos.

Dados de um usuário final devem sempre ser analisados, principalmente se esses dados irão retornar ao usuário de alguma forma. Usuários atacantes podem implantar dados ou scripts de malware através de links para outras páginas.

## Prevenção

O uso de frameworks e linguagens que escapam de XSS por padrão, melhoram a personalização do sistema. O uso das ferramentas em padrões de segurança não é obrigatório, mas é altamente recomendado.

Protocolos HTTP possuem cabeçalhos para evitar a entrada de links maliciosos por clientes.

## Documentação OWASP Top 10 - 2017

Todas as informações destas anotações foram feitas à partir da documentação oficial da OWASP que pode ser acessada [aqui](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010-2017%20(en).pdf).

Informações específicas sobre o tópico **A7** estão na página 13.

---
