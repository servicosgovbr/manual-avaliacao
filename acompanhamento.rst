Acompanhamento
**************

Os métodos de APIs necessitam estar logados para uso. Veja mais em `Login`_. 

Registro de Acompanhamento
---------------------------

Realizar o Registro de Acompanhamentos de um Serviços.

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
     "orgao": "57842",
     "protocolo": "0001AC.20171212",
     "servico": "12014",
     "situacaoEtapa": "Alguma descrição da situação."
   }

cpfCidadao
   Informe o CPF do cidadão que está executando o serviço.

dataEtapa
   Data da etapa que o serviço foi executado no formato "dd/mm/aaaa".

dataSituacaoEtapa
   Data da etapa que o situaçao foi criado/alterado no formato "dd/mm/aaaa".

etapa
   Descriçao da etapa que o serviço se encontra na dataEtapa.

orgao
   ID do órgão no `Portal de Serviços`_. Caso não saiba qual ID do órgão consulte pela `API do Portal de Serviços`_

Protocolo
   Protocolo interno do órgão referente ao serviço sendo executado.

servico
   ID do serviço no `Portal de Serviços`_. Caso não saiba qual ID do serviço consulte pela `API do Portal de Serviços`_.

situacaoEtapa
   Descrição da etapa do serviço.

Veja um exemplo de acesso utilizando o cURL_

.. code-block:: console

    $ curl -v -X POST --header 'Content-Type: application/json;charset=UTF-8' -k \
    --header 'Authorization: Basic YXBpQG1wLmdvdi5icjoxMjM0NTY3OA==' \ 
    --header 'Accept: application/json' -d '{ \ 
     "cpfCidadao": "08254631654", \ 
     "dataEtapa": "10/10/2017", \ 
     "dataSituacaoEtapa": "10/10/2017", \ 
     "etapa": "Em Processamento.", \ 
     "orgao": "57842", \ 
     "protocolo": "0001AC.20171212", \ 
     "servico": "12014", \ 
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


.. image:: _imagens/mylogo.svg
   :height: 100px
   :width: 200 px
   :scale: 50 %
   :alt: meu texto para a imagem


.. code-block:: python
   :emphasize-lines: 3,5

   def some_function():
       interesting = False
       print 'This line is highlighted.'
       print 'This one is not...'
       print '...but this one is.'


Python_.

.. _Python: http://www.python.org/

.. note::
    Apesar das instruções de instalação de bibliotecas e execução do :command:`virtualenv` sobre o Python da máquina,
    para menor complexidade do procedimento é recomendado o uso de uma nova instalação de Python 2.7,
    efetuando sobre ela esses procedimentos de instalação de bibliotecas e :command:`virtualenv`.


CPF
  CPF é isso aqui!

.. _cURl: https://curl.haxx.se/
.. _`Login`: login.html
.. _`Portal de Serviços`: http://servicos.gov.br
.. _`API do Portal de Serviços`: https://servicos.pre.nuvem.gov.br/api/v1/docs
.. _`verifique a documentação Swagger`: https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/swagger-ui.html
