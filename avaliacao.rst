Avaliação
**********

A avaliação dos serviços prestados permitirá que o governo tenha uma visão da opinião do cidadão sobre os serviços disponíveis podendo assim melhora-los até que atendam, de fato, ao que a população espera.


O órgão quer avaliar seu serviço, deve, após cadastrar o acompanhamento da prestação do serviço, fazer a chamada ao método Obter Link do formulário de avaliação, o qual lhe fornecerá um endereço de um formulário que poderá ser embutido em seu sistema apresentando um botão "Avaliar" no seu sistema, ou encaminhar o link recebido diretamente ao cidadão, seja por e-mail, seja por SMS.


Formulário de Avaliação
---------------------

O método Obter Link do formulário de avaliação disponibiliza um link para que o cidadão possa avaliar um serviço recebido pelo governo e registra na base as informações da avaliação de um serviço e se for o caso, faz o registro de uma manifestação junto ao e-OUV.

.. note::
   Para obter um formulário de avaliação de serviço é necessário ter cadastrado previamente o acompanhamento da prestação do serviço.


Parâmetros de Entrada
++++++++++++++++++++++

.. code-block:: json

   {
  "canalAvaliacao": "1",
  "canalPrestacao": "8",
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
   Protocolo para identificar o serviço. (O mesmo informado no registro de Acompanhamento!)
servico (string)
   Identificador do serviço do órgão.

Veja um exemplo de acesso utilizando o cURL_

.. code-block:: console

    $ curl -v -X POST --header 'Content-Type: application/json;charset=UTF-8' -k \
    --header 'Authorization: Basic YXBpQG1wLmdvdi5icjoxMjM0NTY3OA==' \
    --header 'Accept: application/json' -d '{ \
     "canalAvaliacao": "1", \
     "canalPrestacao": "8", \     
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
					.setParameter("canalAvaliacao", "1")
                    .setParameter("canalPrestacao", "8")
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
