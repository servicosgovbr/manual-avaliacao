Acesso as APIs de Acompanhamento e Avaliação de Serviços
********************************************************

Atualmente, há dois ambientes para o uso das APIs de Avaliação e Acompanhamento de Serviços Públicos:

1. Testes e homologação:
----------------------------
- Acompanhamento: https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/
- Avaliação:   https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/avaliacao/

2. Produção:
----------------------------
- Acompanhamento: https://acompanhamento.servicos.gov.br/api/acompanhamento/
- Avaliação:   https://avaliacao.servicos.gov.br/api/avaliacao/


As operações disponíveis estão descritas nos seguintes endereços abaixo:
____________________________________________________________________________
Swagger Acompanhamento:
- https://acompanhamento.servicos.gov.br/api/acompanhamento/swagger-ui.html


Avaliação: 
- https://avaliacao.servicos.gov.br/api/avaliacao/swagger-ui.html

.. important::
   Os métodos das APIs necessitam autenticação para uso. A solicitação das credenciais de acesso para uso das APIs deve ser enviada para apis@serviços.gov.br, contendo as informações: órgão, serviço, nome da aplicação, telefone do responsável, email a ser utilizado como usuário das APIs.

Deve-se usar o cabeçalho http **Authorization: Basic** em Base64 para passar as credenciais de autenticação nas chamadas das APIs. 

Caso deseje você pode utilizar a página https://www.base64decode.org/ para decodificar e codificar o login e senha em Base64.
 
.. code-block:: http
   
   Exemplo de login:senha `aladdin:opensesame` 
   Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l