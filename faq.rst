FAQ - Perguntas frequentes
**********

Principais dúvidas sobre integração com a API de avaliação.

O CPF do cidadão é obrigatório?
-------------------------------

O CPF não é obrigatório. A API foi projetada para receber avaliações anônimas e não exige a passagem desse parâmetro.

Não acho meu serviço na lista de serviços para meu órgão. O que devo fazer?
-------------------------------

Procure o ponto focal no órgão pela digitalização de serviços. Essa pessoa terá acesso irrestrito a edição de serviços no órgão (tanto para o ambiente de produção quanto para homologação). 

Os códigos dos órgãos e serviços são os mesmos em teste/homologação e em produção?
----------------------------------------------------------------------------------

Não necessariamente. Os códigos podem mudar dependendo do ambiente utilizado. É sempre recomendado que o desenvolvedor verifique os códigos antes de qualquer mudança de ambiente. Mais informações no `Passo a Passo a passo para avaliar um serviço`_ 

Para registrar o acompanhamento é necessário enviar o número do protocolo? Esse número possui um formato específico? Qual seu tamanho mínimo e máximo?
------------------------------------------------------------------------------------------------------------------------------------------------------

Mesmo que seu serviço não gere um número de protocolo é necessário passar um número no parâmetro de protocolo que pode , por exemplo, ser a chave primária que identifique um atendimento. Não existe um formato padrão pré estabelecido. Cada órgão estabelece seu número/formato de protocolo. Ele deve ter no mínimo 1 caractere e no máximo 60 (incluídos os numerais e símbolos).

Posso encadear acompanhamento, finalização e obtenção de link numa mesma ação do usuário (clique único)?
--------------------------------------------------------------------------------------------------------

O desenvolvedor pode, em uma única ação do usuário, gerar um acompanhamento, finalizar o serviço e gerar o link do formulário. Basta implementar uma rotina em sequência na aplicação com a criação do acompanhamento e geração do link.

Pode ser gerado acompanhamento sem finalização?
-----------------------------------------------

Sim, o acompanhamento pode ser gerado em qualquer etapa do serviço (etapa inicial, intermediária ou final).

Quais os passos para o cancelamento de um acompanhamento?
---------------------------------------------------------

Não há como cancelar um acompanhamento já registrado.

Existe algum mecanismo do módulo de avaliação para submeter e-mail/SMS para solicitar avaliação diretamente ao usuário?
-----------------------------------------------------------------------------------------------------------------------------------------------------

Não há suporte ao envio de e-mail/SMS pela API de Avaliação, somente a geração do link do formulário de avaliação. A forma de exibição do formulário de avaliação fica a critério do órgão que está implementando a integração. A forma mais indicada de exibir o formulário para o cidadão é utilizando a própria interface do serviço (utilizando modal, iframe ou pop-up).

Existe alguma interface web onde conseguimos consultar os acompanhamentos abertos e avaliações?
-----------------------------------------------------------------------------------------------

Não foi implementada interface web para consultar os acompanhamentos e avaliações. Entretanto há endpoints na API que permitem a consulta aos acompanhamentos, são eles, porCidadao, porOrgao, porProtocolo e porServico. Para mais informações, `verifique a documentação Swagger de Acompanhamento`_. E para avaliação, são eles, porCidadao, porOrgao e porServico. Para mais informações, `verifique a documentação Swagger de Avaliação`_.

Há a possibilidade de gerar a avaliação sem que seja necessário a criação do acompanhamento?
--------------------------------------------------------------------------------------------

Não é possível obter o link do formulário de avaliação sem ter feito, ao menos, um registro de acompanhamento.

É preciso finalizar o atendimento para gerar o link de avaliação?
-----------------------------------------------------------------

Não. Independente do status do atendimento (1 - Em Aberto ou 2 - Concluído) é possível gerar o link do formulário de avaliação.

Há algum ícone padrão para ser usado no link da avaliação?
----------------------------------------------------------

Não, a respeito das características de design, o desenvolvedor pode consultar o design system para obter alguma referência `gov.br/ds`_.

Os campos do formulário de avaliação são fixos ou parametrizados? Quem define esses campos?
------------------------------------------------------------------------------

Os campos são fixos.

Onde é feito o acompanhamento das avaliações enviadas pelos cidadãos?
------------------------------------------------------

O acompanhamento é feito no gov.br/gestor.

.. _`Passo a Passo a passo para avaliar um serviço`: passoapasso.html
.. _`verifique a documentação Swagger de Acompanhamento`: https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/swagger-ui.html
.. _`verifique a documentação Swagger de Avaliação`: https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/avaliacao/swagger-ui.html
.. _`gov.br/ds`: http://gov.br/ds



