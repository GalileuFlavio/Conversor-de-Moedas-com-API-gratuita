# Conversor-de-Moedas-com-API-gratuita
Preenchimento: adicione sua API key na linha 15 (obtenha em exchangerate-api.com)
"""
Conversor de Moedas com API gratuita
Preenchimento: adicione sua API key na linha 15 (obtenha em exchangerate-api.com)
"""
import requests

class ConversorMoedas:
    API_URL = "https://v6.exchangerate-api.com/v6/{api_key}/latest/{moeda_base}"
    
    def __init__(self, api_key):
        self.api_key = api_key  # ← PREENCHA AQUI: sua API key
    
    def converter(self, valor, de_moeda, para_moeda):
        """Converte valor entre moedas (ex: USD, BRL, EUR)"""
        try:
            url = self.API_URL.format(api_key=self.api_key, moeda_base=de_moeda.upper())
            resposta = requests.get(url, timeout=10)
            dados = resposta.json()
            
            if dados["result"] == "success":
                taxa = dados["conversion_rates"][para_moeda.upper()]
                resultado = valor * taxa
                return f"{valor} {de_moeda.upper()} = {resultado:.2f} {para_moeda.upper()}"
            return "Erro: Moeda não encontrada"
        except Exception as e:
            return f"Erro: {e}"

# === COMO CONFIGURAR ===
# 1. Acesse: https://www.exchangerate-api.com/ (gratuito)
# 2. Copie sua API key e cole abaixo:
API_KEY = "SUA_API_KEY_AQUI"  # ← PREENCHA ESTA LINHA

# === COMO USAR ===
# Execute e siga as instruções no terminal

if __name__ == "__main__":
    conversor = ConversorMoedas(API_KEY)
    
    print("💱 Conversor de Moedas")
    valor = float(input("Valor: "))
    de = input("De (ex: USD): ")
    para = input("Para (ex: BRL): ")
    
    print(conversor.converter(valor, de, para))
