# A2 Broken Authentication

> Funções de aplicativo relacionadas à autenticação e gerenciamento de sessão geralmente são implementadas incorretamente, permitindo que invasores comprometam senhas, chaves ou tokens de sessão, ou explorem outras falhas de implementação para assumir identidades de outros usuários temporária ou permanentemente.

Uma das formas mais clássicas de se atacar um sistema dessa forma é experimentando senhas super comuns. Senhas como `senha`, `1234`, `qwerty` e muitas outras listadas pela própria OWASP em [10k worst passwords ](https://github.com/OWASP/passfault/blob/master/wordlists/wordlists/10k-worst-passwords.txt), são aquelas cujos sistemas podem ser facilmente acessados por usuários não autorizados.

Quebrar autenticações através de senhas não só é perigoso para um único sistema, mas para vários. O nome desse ataque é [credential stuffing](https://www.owasp.org/index.php/Credential_stuffing). Já que pessoas costumam utilizar a mesma senha para a maioria dos formulários (principalmente vinculado a um sistema de acesso variado como **Google** e **Microsoft**), a descoberta da senha em um sistema pode gerar uma geração de acessos violados em cadeia. 

## Prevenção

A [lista](https://github.com/OWASP/passfault/blob/master/wordlists/wordlists/10k-worst-passwords.txt) da OWASP pode ser utilizada no servidor como **senhas proibidas**, assim evitando que os clientes do sistema utilizem senhas facilmente decifráveis. A documentação do [NIST](https://pages.nist.gov/800-63-3/sp800-63b.html#memsecret) oferece sugestões de como melhorar as condições das senhas dos usuários.

Uma das formas de evitar isso é bloquear a possibilidade de um usuário realizar múltiplas tentativas de acesso através de rastreio de IP. Se um usuário consegue testar múltiplas senhas e nunca receber punição por isso, as chances de quebra de autenticação são muito altas. O [extraordinário caso do engenheiro social romeno Marcel Lehel Lazăr](https://www.youtube.com/watch?v=y9lAbV5l66Q&list=PLyRcl7Q37-DVwwoHbErNgTXOl1QICv_Kt&index=7) (mais conhecido como [Guccifer](https://en.wikipedia.org/wiki/Guccifer)), mostra o potencial que a paciência de testar múltiplas senhas de corromper a privacidade de pessoas extremamente poderosas.

Outra estratégia é a autenticação multi-fator. Uma forma interessante de trabalhar com fatores eficientes de autenticação é o exercício **O QUE EU SEI** `VS.` **O QUE EU TENHO** `VS.` **O QUE EU SOU**. Esse exercício permite que interpretemos três diferentes parâmetros para certificar se o usuário é quem diz ser:

| O QUE EU SEI       | O QUE EU TENHO      | O QUE EU SOU |
|--------------------|---------------------|--------------|
| Senhas             | Cartão de crédito   | Digitais     |
| Códigos            | Credenciais físicas | Íris         |
| Número de telefone | Passaporte          | Voz          |

Por padrão, é mais fácil para um atacante obter informações da coluna **O QUE EU SEI**. Portanto, é importante que um sistema de autenticação multi-fator seja capaz de tirar proveito de formas de autenticação que envolvem o mundo físico.

> "Nunca confie no cliente." *Guilherme Silveira*

## Documentação OWASP Top 10 - 2017

Todas as informações destas anotações foram feitas à partir da documentação oficial da OWASP que pode ser acessada [aqui](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010-2017%20(en).pdf).

Informações específicas sobre o tópico **A2** estão na página 8.

---
