Avaliação
**********

A avaliação dos serviços prestados permitirá que o governo tenha uma visão da opinião do cidadão sobre os serviços disponíveis podendo assim melhora-los até que atendam, de fato, ao que a população espera.

Duas formas estão disponíveis para o registro da opinião do cidadão. 

Na primeira, um órgão de governo implementa o formulário de avaliação em seu próprio sistema e faz a chamada ao método Registrar Avaliação, o qual se encarregará em registrar o resultado da avaliação na base nacional de serviços e registrará a informação no e-OUV. 

Na segunda, o órgão quer avaliar seu serviço, mas não quer desenvolver uma interface de avaliação, nesse caso ele deverá fazer a chamada ao método Obter Link do formulário de avaliação, que lhe fornecerá um endereço de um formulário que poderá ser embutido em seu sistema, usando um <iframe>, ou encaminhar o link recebido diretamente ao cidadão, seja por e-mail, seja por SMS.



Registrar Avaliação
---------------------

O método Registrar Avaliação permite que sejam registradas as informações da avaliação de um serviço prestado ao cidadão e o registro de uma manifestação junto ao e-OUV.

.. note::
   Para registrar uma avaliação é necessário ter cadastrado previamente o acompanhamento da prestação do serviço.


Parâmetros de Entrada
++++++++++++++++++++++

.. code-block:: json
   
   {
    "avaliacao": {
    "cpfCidadao": "08254631654",
    "etapa": "Análise Documental",
    "orgao": "57842",
    "protocolo": "0001AC.20171212",
    "servico": "12014"
  },
  "avaliarComoAnonimo": "false",
  "comentarioAvaliacao": "Atendimento rápido, pessoa qualificada e prestativa.",
  "criteriosAvaliados": [
    "1"
  ],
  "emailUsuario": "jose.silva@email.com.br",
  "nomeUsuario": "José da Silva",
  "outroCriterio": "Pontualidade",
  "tipoAvaliacao": "4",
  "tipoNota": "4"
   }


cpfCidadao (string)
   CPF do cidadão sem formatação.

etapa (string)
   Descrição da etapa do Serviço.

orgao (string)
   Identificador do Orgão.

protocolo (string)
   Protocolo para identificar o serviço.

servico (string)
   Identificador do Serviço do Órgão.

avaliarComoAnonimo (string)
   Informar se a avaliação deve ser anônimo, true ou false. Caso false, o usuário não terá uma resposta do e-OUV. = ['true', 'false'],

comentarioAvaliacao (string, optional)
   Descrição de 500 caracteres com comentário do usuário sobre o serviço prestado.

criteriosAvaliados (Array[string])
   Códigos dos critérios selecionados pelo usuário na Avaliação. Quando Retornado na Consulta, vem com a Descrição e não com ID.

emailUsuario (string, optional)
   Email do usuário. Utilizado para enviar ao sistema e-OUV. Não armazenado na API.

nomeUsuario (string, optional)
   Nome do usuário. Utilizado para enviar ao sistema e-OUV. Não armazenado na API.

outroCriterio (string, optional)
   Descrição de 30 caracteres quando o usuário seleciona o Critério 'Outro'.

tipoAvaliacao (string)
   Tipo de Avaliação. = ['2 - Avaliar', '3 - Não Avaliar', '4 - Avaliar Depois']

tipoNota (string)
   Nota do usuário.1 a 5, quanto maior melhor. = ['1', '2', '3', '4', '5']


.. note::
   Para registrar as informações da avaliação o Tipo de Avaliação dever ser  2! As outras opções serão para implementações futuras de melhorias.


Veja um exemplo de acesso utilizando o cURL_

.. code-block:: console

    $ curl -v -X POST --header 'Content-Type: application/json;charset=UTF-8' -k \
    --header 'Authorization: Basic YWxhZGluQGRpc25leS5jb206b3BlbnNlc2FtZQ==' \ 
    --header 'Accept: application/json' -d '{ \ 
     "cpfCidadao": "08254631654", \ 
     "etapa": "Em Processamento.", \ 
     "orgao": "57842", \ 
     "protocolo": "0001AC.20171212", \ 
     "servico": "12014" \ 
     }' 'https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/avaliacao/'



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



Formulário de Avaliação
---------------------

O método Obter Link do formulário de avaliação disponibiliza um link para que o cidadão possa avaliar um serviço recebido pelo governo e registra na base as informações da avaliação de um serviço e se for o caso, faz o registro de uma manifestação junto ao e-OUV.

.. note::
   Para obter um formulário de avaliação de serviço é necessário ter cadastrado previamente o acompanhamento da prestação do serviço.


Parâmetros de Entrada
++++++++++++++++++++++

.. code-block:: json
   
   {
  "cpfCidadao": "08254631654",
  "etapa": "Em Processamento.",
  "orgao": "57842",
  "protocolo": "0001AC.20171212",
  "servico": "12014"
   }

cpfCidadao (string)
   CPF do cidadão sem formatação.
etapa (string)
   Descrição da etapa do serviço.
orgao (string)
   Identificador do órgão.
protocolo (string)
   Protocolo para identificar o serviço.
servico (string)
   Identificador do serviço do órgão.

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


Veja um exemplo mínimo de acesso na linguagem Java utilizando o HTTPClient Apache.

.. code-block:: java

    import org.apache.http.Header;
    import org.apache.http.HeaderElement;
    import org.apache.http.auth.AuthScope;
    import org.apache.http.client.utils.URIBuilder;
    import org.apache.http.auth.UsernamePasswordCredentials;
    import org.apache.http.client.CredentialsProvider;
    import org.apache.http.client.methods.CloseableHttpResponse;
    import org.apache.http.client.methods.HttpPost;
    import org.apache.http.impl.client.BasicCredentialsProvider;
    import org.apache.http.impl.client.CloseableHttpClient;
    import org.apache.http.impl.client.HttpClients;
    import org.apache.http.util.EntityUtils;
    import java.util.List;
    import java.util.Arrays;
    import java.net.URI;

    public class BuscaAvaliacao {

        public static void main(String[] args) throws Exception {
            CredentialsProvider credsProvider = new BasicCredentialsProvider();
            credsProvider.setCredentials(
                    AuthScope.ANY,
                    new UsernamePasswordCredentials("aladin@disney.com", "opensesame"));
            CloseableHttpClient httpclient = HttpClients.custom()
                    .setDefaultCredentialsProvider(credsProvider)
                    .build();
            try {
                URIBuilder builder = new URIBuilder();
                builder.setScheme("https").setHost("avaliacao.servicos.gov.br")
                    .setPath("/api/avaliacao/formulario")
                    .setParameter("servico", "47")
                    .setParameter("cpfCidadao", "08254631654")
                    .setParameter("protocolo", "0001AC.20171212")
                    .setParameter("orgao", "36802") 
                    .setParameter("etapa", "Em Processamento.");

                URI uri = builder.build();
                HttpPost httpPost = new HttpPost(uri);
                System.out.println("----------------------------------------");
                System.out.println("Executando request " + httppost.getRequestLine());
                CloseableHttpResponse response = httpclient.execute(httppost);
                try {
                    System.out.println("----------------------------------------");
                    System.out.println(response.getStatusLine());
                    System.out.println(EntityUtils.toString(response.getEntity()));
                } finally {
                    response.close();
                }
            } finally {
                httpclient.close();
            }
        }
    }

.. attention:: 
   **Não** está sendo considerado nesse exemplo questões como armazenar no código o login e senha de acesso as APIs. Por favor **utilize as melhores práticas de segurança** para armazenar e gerenciar as senhas.


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


O link da avaliação levará o cidadão para um formuláro de avaliação como o exibido abaixo:

.. image:: _imagens/formulario.PNG
   :scale: 100 %
   :alt: Formulário de Avaliação de Serviços
   :align: center

.. _`Portal de Serviços`: http://servicos.gov.br
