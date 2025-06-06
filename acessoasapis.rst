Acesso as APIs de Acompanhamento e Avaliação de Serviços
********************************************************

Há dois ambientes para o uso da API de Avaliação de Serviços Públicos:

Testes e homologação
----------------------------
- **Acompanhamento:** https://h-acompanhamento-govbrapi.np.estaleiro.serpro.gov.br/api/acompanhamento/
- **Avaliação:** https://h-avaliacao-govbrapi.np.estaleiro.serpro.gov.br/api/avaliacao/

Produção
----------------------------
- **Acompanhamento:** https://acompanhamento.servicos.gov.br/api/acompanhamento/
- **Avaliação:** https://avaliacao.servicos.gov.br/api/avaliacao/

Ambiente web para desenvolvedores
---------------------------------

Caso necessite, é disponibilizado um Swagger para teste de chamadas aos métodos da API:

Swagger de testes
___________________________
- **Acompanhamento:** https://h-acompanhamento-govbrapi.np.estaleiro.serpro.gov.br/api/acompanhamento/swagger-ui.html

- **Avaliação:** https://h-avaliacao-govbrapi.np.estaleiro.serpro.gov.br/api/avaliacao/swagger-ui.html

Swagger de produção
___________________________
- **Acompanhamento:**   https://acompanhamento.servicos.gov.br/api/acompanhamento/swagger-ui.html

- **Avaliação:**   https://avaliacao.servicos.gov.br/api/avaliacao/swagger-ui.html

Deve-se usar o cabeçalho http **Authorization: Basic** em Base64 para passar as credenciais de autenticação nas chamadas das APIs. 

.. note::
   
   Lembre-se de informar usuário e senha no formato (login:senha) em Base64 para utilizar os métodos.
   
   Exemplo prático:

   Nosso usuário é **aladdin** e a senha é **opensesame**. Então temos o formato **aladdin:opensesame**

   Codificamos essa string (aladdin:opensesame) em Basic64 e obtemos o senguinte código: **YWxhZGRpbjpvcGVuc2VzYW1l**

   Agora é só colocar essa informação no header das nossas chamadas aos métodos da API de avaliação

   Reultado final fica: **Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l**

Você pode utilizar a página https://www.base64encode.org/ para codificar a string do login e senha em Base64.
