# A3 Sensitive Data Exposure

> Muitas aplicações web e APIs não protegem adequadamente dados confidenciais, como financeiros, médicos e PII. Os invasores podem roubar ou modificar esses dados mal protegidos para praticar fraude em cartão de crédito, roubo de identidade ou outros crimes. Dados confidenciais podem ser comprometidos sem proteção extra, como criptografia em repouso ou em trânsito, e requerem precauções especiais ao serem trocados com o navegador.

É importante lembrar que para cada saída e entrada de dados em um sistema, existe uma porta. É necessário construir sistemas que sejam rigorosos quanto a quais objetos podem adquirir esses dados e quais não podem. Os sistemas precisam, essencialmente, seguir padrões legislativos. No Brasil, a lei responsável pela proteção dos dados (LGPD) é a [LEI Nº 13.709, DE 14 DE AGOSTO DE 2018](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm), que deve ser usada não apenas para construir sistemas, mas para modelar as ameaças de acordo com as devidas punições no caso dos atacantes serem descobertos.

Ao mesmo tempo que tecnologias de segurança são desenvolvidas, tecnologias que quebram essas seguranças também são desenvolvidas. Por isso, TODOS os algoritmos devem ser sempre atualizados.

O HTTPS é acompanhado de um certificado. A validação do certificado é um compromisso do usuário. Qualquer um pode clicar no símbolo de fechadura (🔒) presente na URL de um site com HTTPS e checar a validade do certificado. Com isso é possível saber se a certificação de segurança do site é de confiança, ou se é falsa.

## Outros ataques

### Golpistas e informantes criminosos

Por mais que esse problema esteja bastante associado à exposição de senhas, que teoricamente são riscos que podem ser reduzidos com o uso do HTTPS, a exposição de dados é exatamente o utensílio de maior uso entre golpistas. Quando enganadores profissionais possuem acesso a dados, mesmo que não sensíveis como idade e sobrenome, abre-se uma porta de entrada para que sejam performandos golpes onde a vítima é confundida quando os enganadores apresentam dados que não deveriam pertencer a objetos de não confiança. 

Movimentos clássicos como mensagens no Whatsapp com fotos de parentes, mímicos de e-mail institucional, supostos telefonemas de bancos e falsos entregadores de comida, tiram proveito da apresentação de dados como nomes e fotos de parentes, endereço residencial e histórico acadêmico para ganhar a confiança das vítimas por um curto período de tempo.

As organizações de golpistas podem conseguir esses dados raqueando tráfego de dados de empresas, serviços de entrega, bancos, instituições e redes sociais ou obtendo informações de dentro. Por isso, o A3 representa um problema existente na burocracia e no rigor de contratação e confiança depositada em funcionários, além de problemas técnicos de cibersegurança.

### Algoritmos de senha padrão

Já foi falado no A2 que senhas comuns costumam ser vítimas fáceis de ataques. Quando falamos de criptografia, existem diversas tecnologias padrão que podem transformar o que foi digitado em uma string em uma sequência de dígitos totalmente diferente. O nome desse método é **hashing** e é explicado com exemplos de código [neste diretório](https://github.com/AndreCoutinhom/blockchain_bootcamp/tree/main/1%20-%20Fundamentos/Aula%203).

Existem, no entanto, algoritmos criados por atacantes que podem decifrar completamente a criptografia utilizada em um site. O exemplo demonstrado por [Guilherme Silveira](https://www.linkedin.com/in/guilhermeazevedosilveira/) combina a utilização de senhas comuns com a má prática de um sistema de colocar todas as senhas, mesmo que criptografadas, em um arquivo com criptografia fraca ou métodos de **hashing** ultrapassados. O atacante, ao conseguir acesso ao arquivo, testa o algoritmo de criptografia com uma senha comum e observa o resultado da senha criptografada. Assim, o atacante consegue interpretar semelhanças de sua senha com outras armazenadas no banco de dados. Não só o atacante será capaz de realizar o sequestro daquela conta, como obtém parâmetros para o **hash** do sistema, possibilitando que decifre outras senhas menos comuns.

Uma das formas de lidar com esse problema é através do Salt. 

> *"O Salt é uma sequência de dois caracteres (os 12 bits do Salt são usados para perturbar o algoritmo DES) escolhidos no conjunto de caracteres"A-Z", "a-z","0-9","."(ponto) e "/". O Salt é usado para variar o algoritmo de hashing, de modo que a mesma senha de texto não criptografado possa produzir 4.096 criptografias de senha possíveis. Uma modificação no algoritmo do DES, trocando bits i e i+24 na saída do DES E-Box quando o bit i é configurado no Salt, alcança isso enquanto também torna o hardware de criptografia DES inútil para adivinhação de senha."* [IBM](https://www.ibm.com/docs/pt-br/aix/7.3?topic=algorithm-traditional-password-crypt-function)

Basicamente, ele é capaz de criar um padrão que reforça a criptografia do método **hashing** para uma sequência mais complexa. Dessa forma, mesmo as senhas mais comuns recebem criptografia de um nível mais alto. Ainda assim, o Salt é apenas uma função. Há várias outras técnicas que podem ser complementadas como as disponibilizadas pela biblioteca python [Bcrypt](https://github.com/corydolphin/python-bcrypt).

## Proteção

Mais uma vez é reforçado que segurança de dados é um problema legislativo. Em cada país existem leis de proteção de dados digitais como a [LEI Nº 13.709, DE 14 DE AGOSTO DE 2018](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm) no Brasil. Classificações de dados podem ser feitas através da interpretação dessas leis.

A melhor de todas as precauções é **NUNCA ARMAZENE DADOS SENSÍVEIS**. Senhas, números de cartão de crédito, endereços residenciais e qualquer outro dado sensível que não precisa ser utilizado várias vezes, estão mais seguros se forem descartados do sistema depois que são utilizados. Isso inclui o método [**cache**](https://canaltech.com.br/software/cache-o-que-e/) para dados sensíveis.

### Recomendações de ferramentas 

* [Argon2](https://github.com/P-H-C/phc-winner-argon2);
* [Scrypt](https://github.com/Tarsnap/scrypt);
* [Bcrypt](https://github.com/corydolphin/python-bcrypt);
* [PBKDF2](https://www.php.net/manual/pt_BR/function.hash-pbkdf2.php).

## Documentação OWASP Top 10 - 2017

Todas as informações destas anotações foram feitas à partir da documentação oficial da OWASP que pode ser acessada [aqui](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010-2017%20(en).pdf).

Informações específicas sobre o tópico **A3** estão na página 9.

---
