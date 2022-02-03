Acompanhamento
**************

O registro de um acompanhamento deve ser enviado a cada etapa da prestação do serviço.

1. Registrar Acompanhamentos
----------------------------

O método **Registrar Acompanhamentos** permite que seja registrada informações de acompanhamento do serviço.

Para mais informações, `verifique a documentação Swagger`_.

.. attention::
   Vale lembrar que a geração do **formulário de avaliação** está condicionada ao registro de **pelo menos um** acompanhamento.

Endpoint de homologação 
++++++++++++++++++++++

.. code-block:: html

   https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/

Endpoint de produção 
++++++++++++++++++++++

.. code-block:: html

   https://acompanhamento.servicos.gov.br/api/acompanhamento/
   
Parâmetros de Entrada
++++++++++++++++++++++

.. code-block:: json

   {
     "cpfCidadao": "08254631654",
     "dataEtapa": "10/10/2017",
     "dataSituacaoEtapa": "10/10/2017",
     "etapa": "Inicial",
     "orgao": "36802",
     "protocolo": "0001AC.20171212",
     "servico": "47",
     "situacaoEtapa": "Alguma descrição da situação."
   }

cpfCidadao (string, optional)
   Informe o CPF do cidadão que está executando o serviço. Esse CPF vai ser validado com 11 dígitos.

dataEtapa (string)
   Data da etapa que o serviço foi executado no formato "dd/mm/aaaa".

dataSituacaoEtapa (string)
   Data da etapa que o situação foi criado/alterado no formato "dd/mm/aaaa".

etapa (string)
   Descrição da etapa que o serviço se encontra na dataEtapa.

orgao (string)
   ID do órgão, caso não saiba qual ID do órgão consulte a `API do Portal de Serviços`_

.. attention::
   Esse é o código do órgão na `API do Portal de Serviços`_ e **não** o código SIORG do órgão.

protocolo (string)
   Protocolo interno do órgão referente ao serviço sendo executado. Geralmente é utilizado uma identificação única do sistema.

servico (string)
   ID do serviço, caso não saiba qual ID do serviço consulte a `API do Portal de Serviços`_.

situacaoEtapa (string)
   Descrição da etapa do serviço.

Veja um exemplo de acesso utilizando o cURL_

.. code-block:: console

    $ curl -v -X POST --header 'Content-Type: application/json;charset=UTF-8' -k \
    --header 'Authorization: Basic YWxhZGluQGRpc25leS5jb206b3BlbnNlc2FtZQ==' \
    --header 'Accept-Language: pt-br' \
    --header 'Accept: application/json' -d '{ \
     "cpfCidadao": "08254631654", \
     "dataEtapa": "10/10/2017", \
     "dataSituacaoEtapa": "10/10/2017", \
     "etapa": Final", \
     "orgao": "36802", \
     "protocolo": "0001AC.20171212", \
     "servico": "47", \
     "situacaoEtapa": "Alguma descrição da situação." \
     }' 'https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/'

Veja um exemplo de acesso utilizando Java

.. code-block:: java

    import org.apache.http.HttpHeaders;
    import org.apache.http.HttpResponse;
    import org.apache.http.client.methods.HttpPost;
    import org.apache.http.client.methods.HttpPut;
    import org.apache.http.entity.ContentType;
    import org.apache.http.entity.StringEntity;
    import org.apache.http.impl.client.CloseableHttpClient;
    import org.apache.http.impl.client.HttpClients;

    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;

    public class Acompanhamento {

        private final CloseableHttpClient httpClient = HttpClients.createDefault();

        public static void main(String[] args) throws Exception {
            Acompanhamento acompanhamento = new Acompanhamento();
            try {
                acompanhamento.enviarAcompanhamento();
            } finally {
                acompanhamento.close();
            }
        }

        private void close() throws IOException {
            httpClient.close();
        }

        private void enviarAcompanhamento() throws Exception {
            String url = "https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/";
            String payload = "{" +
                    "\"cpfCidadao\": \"99999999999\", " +
                    "\"dataEtapa\": \"10/10/2020\", " +
                    "\"dataSituacaoEtapa\": \"10/10/2020\", " +
                    "\"etapa\": \"Inicial\", " +
                    "\"orgao\": \"123\", " +
                    "\"protocolo\": \"001\", " +
                    "\"servico\": \"02\", " +
                    "\"situacaoEtapa\": \"Texto.\"" +
                    "}";
            HttpPost request = new HttpPost(url);
            request.addHeader(HttpHeaders.AUTHORIZATION, "Basic " + "ZmFiaW8uZmVybmFuZGV");
            request.addHeader("Content-Type", "application/json;charset=UTF-8");
            request.addHeader("Accept-Language", "pt-br");
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
      "message": "Acompanhamento registrado com sucesso.",
      "status": "CREATED"
    }

messagem
   Mensagem que descreve o status da operação.

status
   Status final da operação. Pode ser **CREATED**, **BAD REQUEST** ou **INTERNAL_SERVER_ERROR**

.. warning::
    Para uma listagem completa da saída por favor `verifique a documentação Swagger`_.

2. Solicitar Conclusão/Reabertura de uma prestação de serviço
-------------------------------------------------------------

Esse método permite registrar a conclusão ou reabertura de uma prestação de serviço de um protocolo já registrado.

Após os registros dos acompanhamentos e encerrada a prestação do serviço, poderá ser informada a conclusão da prestação do serviço utilizando o método **Realizar a conclusão ou reabertura de uma prestação de serviço**. Contudo, para gerar o link do **formulário de avaliação** não é necessário que o atendimento esteja concluído.

Para mais informações, `verifique a documentação Swagger`_.

Endpoint de homologação 
++++++++++++++++++++++

.. code-block:: html

   https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/situacao

Endpoint de produção 
++++++++++++++++++++++

.. code-block:: html

   https://acompanhamento.servicos.gov.br/api/acompanhamento/situacao

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

cpfCidadao (string, optional)
   CPF do cidadão sem formatação.

orgao (string)
   Identificador do Órgão.
   
protocolo (string)
   Protocolo para identificar o serviço.

servico (string)
   Identificador do serviço.
   
situacaoServico (string, optional)
   Situação atual do serviço. 1 - Em Aberto, 2 - Concluído. = ['1', '2']


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

Veja um exemplo de acesso utilizando Java

.. code-block:: java

    import org.apache.http.HttpHeaders;
    import org.apache.http.HttpResponse;
    import org.apache.http.client.methods.HttpPost;
    import org.apache.http.client.methods.HttpPut;
    import org.apache.http.entity.ContentType;
    import org.apache.http.entity.StringEntity;
    import org.apache.http.impl.client.CloseableHttpClient;
    import org.apache.http.impl.client.HttpClients;

    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;

    public class Acompanhamento {

        private final CloseableHttpClient httpClient = HttpClients.createDefault();

        public static void main(String[] args) throws Exception {
            Acompanhamento acompanhamento = new Acompanhamento();
            try {
                acompanhamento.enviarFechamentoReabertura();
            } finally {
                acompanhamento.close();
            }
        }

        private void close() throws IOException {
            httpClient.close();
        }

        private void enviarFechamentoReabertura() throws Exception {
            String url = "https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/situacao";

            String payload = "{" +
                    "\"cpfCidadao\": \"99999999999\", " +
                    "\"orgao\": \"123\", " +
                    "\"protocolo\": \"001\", " +
                    "\"servico\": \"01\", " +
                    "\"situacaoServico\": \"Texto\"" +
                    "}";
            HttpPut put = new HttpPut(url);
            put.addHeader(HttpHeaders.AUTHORIZATION, "Basic " + "ZmFiaW8uZmVybmFuZGVzQGV");
            put.addHeader("Content-Type", "application/json;charset=UTF-8");
            put.addHeader("Accept", "application/json");
            StringEntity entity = new StringEntity(payload, ContentType.APPLICATION_JSON);
            put.setEntity(entity);
            HttpResponse response = httpClient.execute(put);
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
      "message": "Registrada a conclusão do serviço informado.",
      "status": "OK"
    }

messagem
   Mensagem que descreve o status da operação.

status
   Status final da operação. Pode ser **OK**, **ERROR** ou **INTERNAL_SERVER_ERROR**

.. warning::
    Para uma listagem completa da saída por favor `verifique a documentação Swagger`_.

.. _cURl: https://curl.haxx.se/
.. _`Login`: login.html
.. _`API do Portal de Serviços`: https://www.servicos.gov.br/api/v1/docs
.. _`verifique a documentação Swagger`: https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/swagger-ui.html
