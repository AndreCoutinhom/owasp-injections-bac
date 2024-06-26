# A8 Insecure Deserialization

> Desserialização insegura frequentemente leva à execução remota de código. Mesmo que falhas de desserialização não resultem em execução remota de código, elas podem ser usadas para realizar ataques, incluindo ataques de replay, ataques de injeção e ataques de escalação de privilégios.

Desserialização acontece quando informações contidas em um arquivo JSON, por exemplo, se tornam parte do banco de dados de um sistema. É extremamente comum em requisições HTTP.

Mudanças nessa estrutura como a implantação de malwares ou scripts, podem significar vulnerabilidades.

O pesquisador em segurança cibernética [Alvaro Muñoz](https://github.com/pwntester) publicou [um relato](https://www.pwntester.com/blog/2013/12/23/rce-via-xstream-object-deserialization38/) de como scripts de desserialização podem performar em documentos XML.

``` xml
<dynamic-proxy>
<interface>com.company.model.Contact</interface>
<handler class="java.beans.EventHandler">
    <target class="java.lang.ProcessBuilder">
	<command><string>/Applications/Calculator.app/Contents/MacOS/Calculator</string></command>
    </target>
    <action>start</action>
</handler>
</dynamic-proxy>
```

Este código está configurado para que, ao invocar um método na interface `com.company.model.Contact`, o proxy criado pelo `java.beans.EventHandler` execute o comando definido no `ProcessBuilder`, que, neste caso, abre a Calculadora do macOS.

Usando o `java.beans.EventHandler` e o `ProcessBuilder`, é possível executar qualquer comando no sistema operacional. Se o processo JVM estiver sendo executado com altos privilégios (por exemplo, como root ou administrador), o código pode executar comandos que alteram o sistema, desabilitam proteções de segurança, ou comprometem outros usuários no sistema.

## Prevenção

Por padrão, a serialização nunca pode ser feita por qualquer fonte totalmente conhecida. 

É recomendado que estruturas de dados em JSON ou XML não devem serializar dados sensíveis. Há outros processos mais seguros do que requisições HTTP para que dados importantes sejam serializados.

Autenticação de requisições e postagens através HTTPS também podem servir como boas formas de prevenção.

## Documentação OWASP Top 10 - 2017

Todas as informações destas anotações foram feitas à partir da documentação oficial da OWASP que pode ser acessada [aqui](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010-2017%20(en).pdf).

Informações específicas sobre o tópico **A8** estão na página 14.

---
