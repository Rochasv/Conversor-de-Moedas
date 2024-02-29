import requests

def converter_moeda(valor, moeda_origem, moeda_destino):
    # Substui 'YOUR_API_KEY' pela sua chave de API
    api_key = 'YOUR_API_KEY'
    base_url = 'https://open.er-api.com/v6/latest'

    parametros = {'base': moeda_origem, 'symbols': moeda_destino}

    if api_key:
        parametros['apikey'] = api_key

    try:
        response = requests.get(base_url, params=parametros)
        dados = response.json()

        taxa_cambio = dados['rates'][moeda_destino]
        valor_convertido = valor * taxa_cambio

        return valor_convertido

    except requests.exceptions.RequestException as e:
        print(f"Erro na requisição: {e}")
        return None

# Exemplo de uso:
valor_em_usd = 170  # Valor em dólares
moeda_destino = 'EUR'  # Converter para Euros

resultado = converter_moeda(valor_em_usd, 'USD', moeda_destino)

if resultado is not None:
    print(f"{valor_em_usd} USD é equivalente a {resultado:.2f} {moeda_destino}")
else:
    print("Conversão falhou.")
