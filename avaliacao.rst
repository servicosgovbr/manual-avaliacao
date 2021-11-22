Avaliação
**********

O registro da avaliação deve ser utilizada para geração do link de avaliação da prestação do serviço.

Obter Link do formulário de avaliação
---------------------

O método **Obter Link do formulário de avaliação** retorna um link para que o cidadão possa avaliar o serviço, registra na base as informações da avaliação e, se for o caso, faz o registro de uma manifestação junto à Ouvidoria.

.. attention::
   É obrigatório o registro de pelo menos uma etapa de acompanhamento para gerar um link do formulário de avaliação.


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

   
canalAvaliacao (string, optional)
    [1 - Formulário da plataforma, 2 - Formulário próprio, 3 - SMS, 4 - Pesquisa presencial e 5 - Whatsapp].
canalPrestacao (string,optional)
    [1 - Aplicativo Móvel, 2 - E-mail, 3 - Fax, 4 - Postal, 5 - Presencial, 6 - SMS, 7 - Telefone e 8 - Web].
cpfCidadao (string,optional)
   CPF do cidadão sem formatação.
etapa (string)
   Descrição da etapa do serviço.
orgao (string)
   Identificador do órgão.
protocolo (string)
   Protocolo para identificar o serviço. (O mesmo informado no registro de Acompanhamento!)
servico (string)
   Identificador do serviço.

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


Veja um exemplo de acesso utilizando Java

.. code-block:: java

    import org.apache.http.HttpHeaders;
    import org.apache.http.HttpResponse;
    import org.apache.http.client.methods.HttpPost;
    import org.apache.http.entity.ContentType;
    import org.apache.http.entity.StringEntity;
    import org.apache.http.impl.client.CloseableHttpClient;
    import org.apache.http.impl.client.HttpClients;

    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;

    public class Avaliacao {

        private final CloseableHttpClient httpClient = HttpClients.createDefault();

        public static void main(String[] args) throws Exception{
            Avaliacao avaliacao = new Avaliacao();
            try {
                avaliacao.obterLink();
            } finally {
                avaliacao.close();
            }
        }

        private void close() throws IOException {
            httpClient.close();
        }

        private void obterLink() throws Exception{
            String url = "https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/avaliacao/formulario?completo=false";
            String payload = "{" +
                    "\"canalAvaliacao\": \"4\", " +
                    "\"canalPrestacao\": \"4\", " +
                    "\"cpfCidadao\": \"99999999999\", " +
                    "\"etapa\": \"Em Processamento.\", " +
                    "\"orgao\": \"36802\", " +
                    "\"protocolo\": \"1234567\", " +
                    "\"servico\": \"47\"" +
                    "}";
            HttpPost request = new HttpPost(url);
            request.addHeader(HttpHeaders.AUTHORIZATION, "Basic " + "ZmFiaW8uZmVybmFuZGVzQGV");
            request.addHeader("Content-Type", "application/json;charset=UTF-8");
            request.addHeader("Accept", "application/json");
            StringEntity entity = new StringEntity(payload, ContentType.APPLICATION_JSON);
            request.setEntity(entity);
            HttpResponse response = httpClient.execute(request);
            BufferedReader reader = new BufferedReader(new InputStreamReader(response.getEntity().getContent(), "utf-8"), 8);
            String line = null;
            while ((line = reader.readLine()) != null) // Read line by line
                System.out.print(line);
        }
    }

Parâmetros de Saída
++++++++++++++++++++++

.. code-block:: json

    {
    "location": "https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/#/avaliacao/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJ7XCJzZXJ2aWNvXCI6XCI0N1wiLFwiY3BmQ2lkYWRhb1wiOlwiOTYyMjA2MjcxNzJcIixcInByb3RvY29sb1wiOlwiMDAwMUNBLjIwMTcxMjEyXCIsXCJvcmdhb1wiOlwiMzY4MDJcIixcImV0YXBhXCI6XCJFbSBQcm9jZXNzYW1lbnRvLlwiLFwiaWRcIjoyNTk4OTcsXCJjcml0ZXJpb3NcIjpbe1wiY29kaWdvXCI6MTAsXCJjb2RpZ29QZXJndW50YVwiOjl9LHtcImNvZGlnb1wiOjEsXCJjb2RpZ29QZXJndW50YVwiOjF9LHtcImNvZGlnb1wiOjksXCJjb2RpZ29QZXJndW50YVwiOjh9LHtcImNvZGlnb1wiOjIsXCJjb2RpZ29QZXJndW50YVwiOjN9LHtcImNvZGlnb1wiOjcsXCJjb2RpZ29QZXJndW50YVwiOjR9LHtcImNvZGlnb1wiOjgsXCJjb2RpZ29QZXJndW50YVwiOjZ9XSxcImF2YWxpYWNhb0NvbXBsZXRhXCI6ZmFsc2V9IiwiaXNzIjoiQVBJIFNlcnZpw6dvcyBEaWdpdGFpcyAtIEF2YWxpYcOnw6NvIiwiaWF0IjoxNjM1MTg0NTg4fQ.gr5QC_zl1dFqPIdK1o2fnO1sfUIcrpVeK4N2pVMTNi-agvxQSR3m-ez9YYZ0xZK7fRO6b6QCRiqmvNjcCcgAxg"
    }

location (string)
   URL de acesso ao formulário de avaliação.

.. warning::
    Para uma listagem completa da saída por favor `verifique a documentação Swagger`_.

