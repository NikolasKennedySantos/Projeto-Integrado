# Projeto-Integrado
Programa de cadastramento de alunos
from datetime import datetime
import json
import os

# Coleta de dados
nome = input("Digite seu nome: ").strip().title()
cpf = input("Digite seu CPF: ").strip()
uf = input("Digite a UF (estado): ").strip().upper()
cidade = input("Digite a cidade: ").strip().title()

# Validação da data de nascimento
while True:
    data_nascimento = input("Digite sua data de nascimento (DD/MM/AAAA): ").strip()
    try:
        nascimento = datetime.strptime(data_nascimento, "%d/%m/%Y")
        break
    except ValueError:
        print("Formato inválido. Tente novamente usando DD/MM/AAAA.")

# Dados organizados em dicionário
dados_usuario = {
    "nome": nome,
    "cpf": cpf,
    "data_nascimento": data_nascimento,
    "uf": uf,
    "cidade": cidade
}

# Caminho do arquivo
arquivo_usuarios = "usuarios.json"

# Verifica se já existe o arquivo com usuários
if os.path.exists(arquivo_usuarios):
    with open(arquivo_usuarios, "r", encoding="utf8") as arquivo:
        try:
            lista_usuarios = json.load(arquivo)
        except json.JSONDecodeError:
            lista_usuarios = []
else:
    lista_usuarios = []

# Adiciona novo usuário à lista
lista_usuarios.append(dados_usuario)

# Salva todos os usuários no arquivo JSON
with open(arquivo_usuarios, "w", encoding="utf8") as arquivo:
    json.dump(lista_usuarios, arquivo, ensure_ascii=False, indent=4)

# Confirmação
print("\n✅ Usuário cadastrado com sucesso!")
