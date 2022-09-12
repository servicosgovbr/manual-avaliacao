Exemplos
**************

Aqui você encontra as URL e métodos necessários para registrar acompanamentos e gerar o link da avaliação.
Com esse arquivo, será possivel obter todos os códigos exigidos na integração do seu serviço. Preencha corretamente seu usuário e senha no momento da execução.

Utilizamos Python para exemplificar e elucidar todas as dúuvidas:

.. code-block:: python

    import requests
	import base64

	siorg_orgao = " " #Informe o codigo SIORG do seu órgão

	usuario = " " #Email que foi cadastrado para acessar a API
	senha = " " #Senha liberada para o acesso a API

	url_acompanhamento_testes = "https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/"
	url_acompanhamento_situacao_testes = "https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/acompanhamento/situacao"
	url_avaliacao_teste = "https://api-acompanha-avalia-servicos.dev.nuvem.gov.br/api/avaliacao/formulario"

	url_acompanhamento_producao = "https://acompanhamento.servicos.gov.br/api/acompanhamento/"
	url_acompanhamento_situacao_producao = "https://acompanhamento.servicos.gov.br/api/acompanhamento/situacao"
	url_avaliacao_producao = "https://avaliacao.servicos.gov.br/api/avaliacao/formulario?completo=false"

	url_servico_teste = "https://servicos.treina.nuvem.gov.br/api/v1/servicos/orgao/"
	url_servico_producao = "https://servicos.gov.br/api/v1/servicos/orgao/"

	url_cod_orgao_api_teste = "https://servicos.treina.nuvem.gov.br/api/v1/orgao/"
	url_cod_orgao_api_producao = "https://servicos.gov.br/api/v1/orgao/"

	def create_session_pesquisar():
		sess = requests.Session()
		sess.headers.update({
			'Accept': 'application/json'
		})
		return sess

	def consultar_cod_orgao_api_teste():
		pesq = create_session_pesquisar()
		retorno = pesq.get(url=f'{url_cod_orgao_api_teste}{siorg_orgao}')
		print(retorno.json()["id"])
		pesq.close()

	def consultar_cod_orgao_api_producao():
		pesq = create_session_pesquisar()
		retorno = pesq.get(url=f'{url_cod_orgao_api_producao}{siorg_orgao}')
		print(retorno.json()["id"])
		pesq.close()

	def pesquisar_servicos_teste():
		pesq = create_session_pesquisar()
		retorno = pesq.get(url=f'{url_servico_teste}{siorg_orgao}')
		for aux in retorno.json()['resposta']:
			print(f'{aux["idDb"]} - {aux["nome"]}')
		pesq.close()

	def pesquisar_servicos_producao():
		pesq = create_session_pesquisar()
		retorno = pesq.get(url=f'{url_servico_producao}{siorg_orgao}')
		for aux in retorno.json()['resposta']:
			print(f'{(aux["id"]).split("https://servicos.gov.br/api/v1/servicos/")[1]} - {aux["nome"]}')
		pesq.close()

	def gerar_base64():
		encoded = base64.b64encode(f'{usuario}:{senha}'.encode('ascii'))
		return encoded.decode()

	def create_session():
		sess = requests.Session()
		sess.headers.update({
			'Content-Type': 'application/json;charset=UTF-8',
			'Accept': 'application/json',
			'Authorization': f'Basic {gerar_base64()}'
		})
		return sess

	def create_situacao_acompanhamento():
		body = {
			"cpfCidadao": "41333618069",
			"orgao": "36802",
			"protocolo": "Teste_125",
			"servico": "47",
			"situacaoServico": "2" #Situação atual do Serviço. 1 - Em Aberto, 2 - Concluído.
		}
		sess = create_session()
		response = sess.put(url=url_acompanhamento_situacao_testes, json=body)
		'''
			200 Registrado a conclusão/reabertura do serviço informado
			400 Erro nos dados enviados ao servidor
		'''
		print(response.status_code)
		print(response.content)
		sess.close()

	def create_acompanhamento():
		 body = {
			 "cpfCidadao": "41333618069",
			 "dataEtapa": "10/10/2017",
			 "dataSituacaoEtapa": "10/10/2017",
			 "etapa": "Em Processamento.",
			 "orgao": "36802",
			 "protocolo": "Teste_125",
			 "servico": "47",
			 "situacaoEtapa": "Alguma descrição da situação."
		 }
		 sess = create_session()
		 response = sess.post(url=url_acompanhamento_testes, json=body)
		 '''
			 201 Acompanhamento criado com sucesso
			 400 Erro nos dados enviados ao servidor
			 401 Não Autenticado
			 403 Autenticado sem autorização
			 404 Recurso não encontrado
			 500 Erro Interno do Servidor
		 '''
		 print(response.status_code)
		 print(response.content)
		 sess.close()

	def create_avaliacao():
		body = {
			"canalAvaliacao": "4",
			"canalPrestacao": "4",
			"cpfCidadao": "41333618069",
			"etapa": "Em Processamento.",
			"orgao": "36802",
			"protocolo": "Teste_125",
			"servico": "47"
		}
		sess = create_session()
		response = sess.post(url=url_avaliacao_teste, json=body)
		'''
			200 Link para o formulário
			400 Erro nos dados enviados ao servidor
		'''
		print(response.status_code)
		print(response.content)
		sess.close()

	def main():
		print("Serviços disponíveis no ambiente de testes:")
		pesquisar_servicos_teste()

		print("\nServiços no ambiente de produção:")
		pesquisar_servicos_producao()

		print("\nCodigo do orgão para ser usado na API de Avaliação (teste):")
		consultar_cod_orgao_api_teste()

		print("\nCodigo do orgão para ser usado na API de Avaliação (produção):")
		consultar_cod_orgao_api_producao()

		print("\nUse isto no Authorization da sua requisição (usuario e senha em Base64):")
		print(f'Basic {gerar_base64()}')

		create_acompanhamento()
		create_situacao_acompanhamento()
		create_avaliacao()

	if __name__ == '__main__':
		main()
