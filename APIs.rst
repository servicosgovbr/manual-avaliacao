APIs
=====

As APIs estão dividas entre:

Avaliação
**********

Acompanhamento
**************

Os métodos de APIs necessitam estar logados para uso.

Se deve usar o cabeçalho http **Authorization: Basic** em Base64
 
.. code-block:: http
   
   Exemplo de login:senha `aladdin:opensesame` 
   Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l

Método /
--------

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
   ID do órgão no `Portal de Serviços`_. Caso não saiba qual ID do órgão consulte pelo `Portal de Serviços`_

Protocolo
   Protocolo interno do órgão referente ao serviço sendo executado.

servico
   ID do serviço no `Portal de Serviços`_.

situacaoEtapa
   Descrição da etapa do serviço.

Parâmetros de Saída
++++++++++++++++++++++


Login
********

O login é o mesmo do editor de serviços e deve ser obtido da forma ....

Siga o manual de acesso ao portal disponível em ... :term:`API`

.. code-block:: json
 
   { "teste": "gesete" }

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

.. code-block:: console

    $ cd ~/portal.buildout
    $ virtualenv py27
    $ source py27/bin/activate

.. warning::
    **Não execute** o seu buildout com :command:`sudo`:
    dessa forma, seu virtualenv será `ignorado <http://askubuntu.com/a/478001>`_ e ocorrerá todo tipo de erro de dependências da sua instância com as do Python do sistema.

Python_.

.. _Python: http://www.python.org/

.. note::
    Apesar das instruções de instalação de bibliotecas e execução do :command:`virtualenv` sobre o Python da máquina,
    para menor complexidade do procedimento é recomendado o uso de uma nova instalação de Python 2.7,
    efetuando sobre ela esses procedimentos de instalação de bibliotecas e :command:`virtualenv`.


CPF
  CPF é isso aqui!


.. _`Portal de Serviços`: http://servicos.gov.br
