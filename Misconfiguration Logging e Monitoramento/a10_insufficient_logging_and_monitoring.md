# A10 Insufficient logging and monitoring

> Registro e monitoramento insuficientes, juntamente com integração ausente ou ineficaz com resposta a incidentes, permitem que invasores ataquem further sistemas, mantenham persistência, pivoteiem para mais sistemas e adulterem, extraiam ou destruam dados. A maioria dos estudos de violação mostra que o tempo para detectar uma violação é superior a 200 dias, geralmente detectado por partes externas em vez de processos internos ou monitoramento.

O monitoramento de *logins* é extremamente necessário para que devidos usuários sejam devidamente autenticados. Pode inclusive detectar usuários que tentam entrar em um serviço diversas vezes.

Um exemplo é determinar um bloqueio em um limite de vezes que um usuário pode fazer um registro. Isso é importante não apenas para evitar clientes criminosos, mas previnir excesso de dados no servidor.

Os *pentests* são excelentes estratégias para detecção de vulnerabilidades e recursos de segurança insuficientes. Se um teste de penetração é realizado, espera-se que haja avisos e alertas relatados pelo pentester.

Monitoramento e logging insuficientes permitem que hackers ataquem facilmente e sem serem notados. Cada ação dentro de um sistema deve ser autenticada, registrada e observada para que qualquer ação maliciosa seja reportada.

## Prevenção

O logs devem ser condicionados a informações importantes dos usuários, de forma que tendências maliciosas possam ser evitadas desde o início.

Reforço de monitoramento pode evitar a tentativa de fugas de padrões. Todos os usuários devem ser submetidos aos mesmos testes e condições.

## Documentação OWASP Top 10 - 2017

Todas as informações destas anotações foram feitas à partir da documentação oficial da OWASP que pode ser acessada [aqui](https://github.com/OWASP/Top10/blob/master/2017/OWASP%20Top%2010-2017%20(en).pdf).

Informações específicas sobre o tópico **A10** estão na página 16.

---
