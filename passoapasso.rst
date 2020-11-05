Passo a passo para avaliar um serviço
*************************************

Para avaliar com sucesso uma execução de um serviço pelo o cidadão é necessário executar alguns passos:


1. Cadastre seu serviço no Portal de Serviços:
----------------------------------------------
Um requisito para avaliação é ter o serviço público cadastrado no portal de serviços.

**Como fazer:**
Solicite para o representante do órgão no Portal de Serviços que cadastre e mantenha atualizado o seu serviço.
Acesse https://servicos.gov.br/editar para editar o serviço.

.. note::
   É necessário ter as credenciais no Portal de Serviços para poder editar um serviço. Caso não possua `siga o procedimento para obter as credenciais`_.

2. Descubra o código do órgão e o código dos seus serviços
----------------------------------------------------------
A API de avaliação precisa do código do órgão e do serviço para poder ser utilizada.

**Como fazer:**
Acesse a API do Portal de Serviços para obter os códigos. 

**a) Descubra o ID do seu órgão no SIORG:** https://siorg.planejamento.gov.br/siorg-cidadao-webapp/pages/listar_orgaos_estruturas/listar_orgaos_estruturas.jsf

**b) Descubra o código dos serviços:**
https://servicos.gov.br/api/v1/servicos/orgao/"substitua código do órgão no SIORG"

Exemplo: https://servicos.gov.br/api/v1/servicos/orgao/235874

**c) Descubra o código do órgão para a API:**
https://servicos.gov.br/api/v1/orgao/"substitua código do órgão no SIORG" 

Exemplo: https://servicos.gov.br/api/v1/orgao/235874

.. important::
   Esse código é específico para cada órgão e cada serviço. Não utilize códigos de outros órgãos e serviços.
   Para ambiente de teste, substitua "servicos.gov.br" por "servicos.treina.nuvem.gov.br"

3. Obtenha as credenciais para usar as APIs de avaliação
--------------------------------------------------------

**Como fazer:**
Os métodos das APIs necessitam autenticação para uso.
A solicitação das credenciais de acesso para uso das APIs deve ser enviada para apis@servicos.gov.br, contendo as informações: órgão, serviço, nome da aplicação, telefone do responsável, email a ser utilizado como usuário das APIs.

.. caution::
   Essa credencial não é a mesma para edição dos serviços no Portal de Servicos.


4. Envie os acompanhamentos durante a execução do serviço
---------------------------------------------------------

Para a avaliação final da execução do serviço é necessário ter um acompanhamento prévio.

**Como fazer:**
Utilize o endpoint de acompanhamento. Acesse o manual em `Acompanhamento`_ para verificar como utilizar o endpoint.

5. Envie o pedido de geração de link ou formulário para avaliação ao final da execução do serviço
--------------------------------------------------------------------------------------------------

**Como fazer:**
Utilize o endpoint de avaliação.  Acesse o manual em `Avaliação`_ para verificar como utilizar o endpoint.

6. Envie o link ou o formulário para o cidadão
----------------------------------------------

**Como fazer:**
Pode-se usar qualquer meio de contato com o cidadão que deseje. O meio sugerido é enviar por email.
Verifique a `Apresentação`_ para outras sugestões.

7. O cidadão preenche a avaliação
---------------------------------

O cidadão irá preencher o formulário de avaliação relacionado ao serviço prestado.

8. Acompanhe as avaliações do cidadão
-------------------------------------

Caso o orgão tenha interesse é possível acessar os dados da avaliação dos cidadãos.
Acesse as consultas disponíveis na API de `Avaliação`_ para obter os dados e poder analisá-los em seu õrgão.

.. important::
   Uma avaliação pode gerar uma manifestação na ouvidoria caso o cidadão tenha optado.
   O órgão pode ter que tratar uma avaliação via ouvidoria.



.. _`Acompanhamento`: acompanhamento.html
.. _`Avaliação`: avaliacao.html
.. _`Apresentação`: apresentacao.html#fluxo-simplificado-para-o-cidadao
.. _`siga o procedimento para obter as credenciais`: https://www.servicos.gov.br/pagina-tematica/outras-duvidas-editores
