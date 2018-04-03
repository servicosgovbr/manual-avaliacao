Concluir/reabrir uma prestação de serviço
**************

Após o registro das etapas na base de avaliação e tendo sido encerrrado a prestação do serviço, deve-se informar a conclusão utilizando o método Realizar a conclusão ou reabertura de uma prestação de serviço, disponível no endpoint https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/situcacao


Realizar a conclusão ou reabertura de uma prestação de serviço.
---------------------------

O método Realizar a conclusão ou reabertura de uma prestação de serviço, permite registrar a conclusão, ou reabertura de uma prestação de serviço de um protocolo já registrado.

.. note::
   Esse é um método **put** para registrar que um serviço foi concluído ou está sendo reaberto.


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
   CPF do cidadão sem formatação

orgao (string)
   Identificado do Orgão
protocolo (string)
   Protocolo para identificar o serviço

servico (string)
   Identificado do Serviço do Orgão
situacaoServico (string, optional)
   Situação atual do Serviço. 1 - Em Aberto, 2 - Concluído. = ['1', '2']


Veja um exemplo de acesso utilizando o cURL_


Cadu por favor inclua o exemplo!!!!!

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
