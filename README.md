# import requests
# resposta = requests.get("http://jsonplaceholder.typicode.com/users")
# usuarios = resposta.json()

# contatos = {
#     "Amanda Melo": "amanda.melo@email.com",
# }
# print(contatos["Amanda Melo"])  

# 14-05-2025
# 
# # Exercício 1
# import requests
# resposta = requests.get("https://jsonplaceholder.typicode.com/users")
# usuarios = resposta.json()
# dicionario_usuarios = {usuario['name']:usuario['email'] for usuario in usuarios}
# print(dicionario_usuarios)
# Exercicio 2
# import requests
# def contar_tarefas_concluidas():
   
#     resposta = requests.get("https://jsonplaceholder.typicode.com/todos")
#     tarefas = resposta.json()
   
#     tarefas_concluidas = {}
   
#     for tarefa in tarefas:
#         user_id = tarefa['userId']
#         if tarefa['completed']:
#             if user_id in tarefas_concluidas:
#                 tarefas_concluidas[user_id] += 1
#             else:
#                 tarefas_concluidas[user_id] = 1
#         else:
#             if user_id not in tarefas_concluidas:
#                 tarefas_concluidas[user_id] = 0
               
#     return tarefas_concluidas
# resultado = contar_tarefas_concluidas()
# print(resultado)
# Exercício 3
# import requests
# def listar_posts_por_usuario():
#     resposta = requests.get("https://jsonplaceholder.typicode.com/posts")
#     posts = resposta.json()
   
#     resultado = {}
   
#     for post in posts:
#         user_id = post['userId']
#         if user_id not in resultado:
#             resultado[user_id] = []
#         resultado[user_id].append(post['title'])
   
#     return resultado
# posts = listar_posts_por_usuario()
# print(posts[1])  
# Exercício 4
# import requests
# usuarios = requests.get("https://jsonplaceholder.typicode.com/users").json()
# posts = requests.get("https://jsonplaceholder.typicode.com/posts").json()
# contagem_posts = {}
# for post in posts:
#     user_id = post['userId']
#     contagem_posts[user_id] = contagem_posts.get(user_id, 0) + 1
# resultado = {}
# for usuario in usuarios:
#     user_id = usuario['id']
#     resultado[usuario['name']] = contagem_posts.get(user_id, 0)
# print(resultado) 

# 19-05-2025

# Exercício 1:

# import requests

# def consulta_cep():
    
#     while True:  # Loop principal
#         print("\n=== CONSULTA DE CEP ===")
        
#         # Passo 1: Pedir ao usuário que digite um CEP
#         cep = input("Digite o CEP (apenas números) ou 'sair' para encerrar: ").strip()
        
#         # Opção para sair do programa
#         if cep.lower() == 'sair':
#             print("Encerrando o programa...")
#             break
        
#         # Verificar se o CEP é válido (apenas números e 8 dígitos)
#         if not cep.isdigit() or len(cep) != 8:
#             print("Erro: CEP inválido. Deve conter exatamente 8 dígitos numéricos.")
#             continue
        
#         # Passo 2: Consultar a API BrasilAPI
#         url = f"https://brasilapi.com.br/api/cep/v2/{cep}"
        
#         try:
#             response = requests.get(url)
#             response.raise_for_status()  # Levanta exceção para erros HTTP
            
#             # Passo 3: Exibir as informações organizadas
#             dados = response.json()
            
#             print("\n=== INFORMAÇÕES DO ENDEREÇO ===")
#             print(f"CEP: {dados.get('cep', 'Não informado')}")
#             print(f"Rua: {dados.get('street', 'Não informado')}")
#             print(f"Bairro: {dados.get('neighborhood', 'Não informado')}")
#             print(f"Cidade: {dados.get('city', 'Não informado')}")
#             print(f"Estado: {dados.get('state', 'Não informado')}")
            
#         except requests.exceptions.HTTPError as e:
#             if response.status_code == 404:
#                 print("Erro: CEP não encontrado.")
#             else:
#                 print(f"Erro na consulta: {e}")
#         except requests.exceptions.ConnectionError:
#             print("Erro: Problema de conexão. Verifique sua internet.")
#         except Exception as e:
#             print(f"Erro inesperado: {e}")
        
#         # Perguntar se deseja continuar (com verificação mais robusta)
#         while True:
#             continuar = input("\nDeseja fazer outra consulta? (sim/não): ").strip().lower()
#             if continuar in ('sim', 'Sim'):
#                 break  # Continua o loop principal
#             elif continuar in ('não', 'nao', 'Não'):
#                 print("Encerrando o programa...")
#                 return  # Sai da função completamente
#             else:
#                 print("Por favor, responda com 'sim' ou 'não'.")

# # Executar a função
# if __name__ == "__main__":
#     consulta_cep()

# Exercício 2:

# import requests

# def consulta_genero():
#     """
#     Função que consulta o gênero mais provável para um nome usando a API Genderize.
#     Oferece a opção de sair quando o usuário digitar o nome.
#     """
#     while True:  # Loop principal para múltiplas consultas
#         print("\n=== CONSULTA DE GÊNERO POR NOME ===")
        
#         # Passo 1: Solicitar o nome ao usuário
#         nome = input("Digite um nome ou 'sair' para encerrar: ").strip()
        
#         # Opção para sair do programa
#         if nome.lower() == 'sair':
#             print("Encerrando o programa...")
#             break
        
#         # Verificar se o nome não está vazio
#         if not nome:
#             print("Erro: Nome não pode estar vazio.")
#             continue
        
#         # Passo 2: Consultar a API Genderize
#         url = f"https://api.genderize.io/?name={nome}"
        
#         try:
#             response = requests.get(url)
#             response.raise_for_status()  # Levanta exceção para erros HTTP
            
#             dados = response.json()
            
#             # Passo 3: Exibir os resultados
#             print("\n=== RESULTADO ===")
#             print(f"Nome consultado: {dados.get('name', 'Não disponível')}")
            
#             genero = dados.get('gender')
#             probabilidade = dados.get('probability', 0)
            
#             if genero:
#                 # Traduzindo o gênero para português
#                 genero_pt = 'masculino' if genero == 'male' else 'feminino'
#                 print(f"Gênero estimado: {genero_pt}")
#                 print(f"Probabilidade: {probabilidade * 100:.2f}%")
#             else:
#                 print("Não foi possível determinar o gênero para este nome.")
            
#             # Mostrar quantidade de amostras (quando disponível)
#             if 'count' in dados:
#                 print(f"Baseado em {dados['count']} ocorrências na base de dados.")
        
#         except requests.exceptions.HTTPError as e:
#             print(f"Erro na consulta à API: {e}")
#         except requests.exceptions.ConnectionError:
#             print("Erro: Problema de conexão. Verifique sua internet.")
#         except Exception as e:
#             print(f"Erro inesperado: {e}")
        
#         # Perguntar se deseja continuar
#         while True:
#             continuar = input("\nDeseja fazer outra consulta? (sim/não): ").strip().lower()
#             if continuar == 'sim':
#                 break  # Continua o loop principal
#             elif continuar in ('não', 'nao', 'Não'):
#                 print("Encerrando o programa...")
#                 return  # Sai da função completamente
#             else:
#                 print("Por favor, responda com 'sim' ou 'não'.")

# # Executar a função
# if __name__ == "__main__":
#     consulta_genero() 
