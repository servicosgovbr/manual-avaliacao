Acompanhamento
**************

Devem ser encaminhados cada etapa e situação que ocorreram na prestação do serviço e ao final informar que a prestação foi concluída.

Registro de Acompanhamento
---------------------------

O método Realizar o Registro de Acompanhamentos de um Serviços permite que sejam registradas na base as informações de acompanhamento do serviço como as etapas e suas situações. Após a execução da última etapa da prestação, o método Concluir/Reabrir Acompanhamento deve ser utilizado, para sinalizar a conclusão da prestação.

Realizar o Registro de Acompanhamentos de um Serviços 

.. note::
   Esse é um método **POST** para envio de acompanhamentos dos serviços sendo executados.

Parâmetros de Entrada
++++++++++++++++++++++

.. code-block:: json
   
   {
     "cpfCidadao": "08254631654",
     "dataEtapa": "10/10/2017",
     "dataSituacaoEtapa": "10/10/2017",
     "etapa": "Em Processamento.",
     "orgao": "36802",
     "protocolo": "0001AC.20171212",
     "servico": "47",
     "situacaoEtapa": "Alguma descrição da situação."
   }

cpfCidadao
   Informe o CPF do cidadão que está executando o serviço. Esse CPF vai ser validado na base 11.

dataEtapa
   Data da etapa que o serviço foi executado no formato "dd/mm/aaaa".

dataSituacaoEtapa
   Data da etapa que o situação foi criado/alterado no formato "dd/mm/aaaa".

etapa
   Descrição da etapa que o serviço se encontra na dataEtapa.

orgao
   ID do órgão no `Portal de Serviços`_. Caso não saiba qual ID do órgão consulte pela `API do Portal de Serviços`_

.. attention::
   Esse é o código do Portal de Serviços e **não** o do SIORG.

Protocolo
   Protocolo interno do órgão referente ao serviço sendo executado.

servico
   ID do serviço no `Portal de Serviços`_. Caso não saiba qual ID do serviço consulte pela `API do Portal de Serviços`_.

situacaoEtapa
   Descrição da etapa do serviço.

Veja um exemplo de acesso utilizando o cURL_

.. code-block:: console

    $ curl -v -X POST --header 'Content-Type: application/json;charset=UTF-8' -k \
    --header 'Authorization: Basic YWxhZGluQGRpc25leS5jb206b3BlbnNlc2FtZQ==' \ 
    --header 'Accept: application/json' -d '{ \ 
     "cpfCidadao": "08254631654", \ 
     "dataEtapa": "10/10/2017", \ 
     "dataSituacaoEtapa": "10/10/2017", \ 
     "etapa": "Em Processamento.", \ 
     "orgao": "36802", \ 
     "protocolo": "0001AC.20171212", \ 
     "servico": "47", \ 
     "situacaoEtapa": "Alguma descrição da situação." \ 
     }' 'https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/'

Parâmetros de Saída
++++++++++++++++++++++

.. code-block:: json

    { 
      "message": "Operação realizada com sucessos!",
      "status": "OK"
    }

messagem
   Mensagem que descreve o status da operação.

status
   Status final da operação. Pode ser **OK** ou **ERROR** 

.. warning::
    Há outras saídas possíveis dependendo se foi feito com sucesso o login ou mesmo se o serviço já existe no `Portal de Serviços`_. Para uma listagem completa da saída por favor `verifique a documentação Swagger`_.

﻿Concluir/reabrir uma prestação de serviço
-----------------------------------------

Após o registro das etapas na base de avaliação e tendo sido encerrado a prestação do serviço, deve-se informar a conclusão utilizando o método Realizar a conclusão ou reabertura de uma prestação de serviço, disponível no endpoint https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/situcacao

Esse método permite registrar a conclusão ou reabertura de uma prestação de serviço de um protocolo já registrado.

.. note::
   Esse é um método **PUT** para registrar que um serviço foi concluído ou está sendo reaberto.


Parâmetros de Entrada
++++++++++++++++++++++

.. code-block:: json
   
   {
  "cpfCidadao": "08254631654",
  "orgao": "57842",
  "protocolo": "0001AC.20171212",
  "servico": "12014",
  "situacaoServico": "2"
   }

cpfCidadao (string)
   CPF do cidadão sem formatação.

orgao (string)
   Identificador do Órgão.
protocolo (string)
   Protocolo para identificar o serviço.

servico (string)
   Identificador do Serviço do Órgão.
situacaoServico (string, optional)
   Situação atual do Serviço. 1 - Em Aberto, 2 - Concluído. = ['1', '2']


Veja um exemplo de acesso utilizando o cURL_

.. code-block:: console

    $ curl -v -X PUT --header 'Content-Type: application/json;charset=UTF-8' -k \
    --header 'Authorization: Basic YWxhZGluQGRpc25leS5jb206b3BlbnNlc2FtZQ==' \ 
    --header 'Accept: application/json' -d '{ \ 
    "cpfCidadao": "08254631654", \ 
    "orgao": "57842", \ 
    "protocolo": "0001AC.20171212", \ 
    "servico": "12014", \ 
    "situacaoServico": "2" \ 
    }' 'https://acompanhamento.servicos.gov.br/api/acompanhamento/situacao'

Parâmetros de Saída
++++++++++++++++++++++

.. code-block:: json

    { 
      "message": "Operação realizada com sucessos!",
      "status": "OK"
    }

messagem
   Mensagem que descreve o status da operação.

status
   Status final da operação. Pode ser **OK** ou **ERROR** 

.. warning::
    Há outras saídas possíveis dependendo se foi feito com sucesso o login ou mesmo se o serviço já existe no `Portal de Serviços`_. Para uma listagem completa da saída por favor `verifique a documentação Swagger`_.

.. _cURl: https://curl.haxx.se/
.. _`Login`: login.html
.. _`Portal de Serviços`: http://servicos.gov.br
.. _`API do Portal de Serviços`: https://servicos.pre.nuvem.gov.br/api/v1/docs
.. _`verifique a documentação Swagger`: https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/swagger-ui.html
