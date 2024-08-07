import sys

# Estrutura de dados para armazenar informações
clientes = {}
cardapio = {}
despesas = []
caixa = 0.0
marmitas_vendidas = 0
comandas = []
clientes_atendidos = set()

# Funções para o sistema
def cadastrar_cliente():
    nome = input("Nome do cliente: ")
    endereco = input("Endereço do cliente: ")
    telefone = input("Telefone do cliente: ")
    clientes[nome] = {"endereco": endereco, "telefone": telefone}
    print(f"Cliente {nome} cadastrado com sucesso.")

def cadastrar_cardapio():
    item = input("Nome do item: ")
    valor = float(input("Valor do item: "))
    cardapio[item] = valor
    print(f"Item {item} cadastrado com sucesso.")

def registrar_despesa():
    descricao = input("Descrição da despesa: ")
    valor = float(input("Valor da despesa: "))
    despesas.append({"descricao": descricao, "valor": valor})
    global caixa
    caixa -= valor
    print("Despesa registrada com sucesso.")

def registrar_venda():
    cliente = input("Nome do cliente: ")
    if cliente not in clientes:
        print("Cliente não cadastrado.")
        return
    item = input("Nome do item: ")
    if item not in cardapio:
        print("Item não cadastrado no cardápio.")
        return
    quantidade = int(input("Quantidade: "))
    valor_total = cardapio[item] * quantidade
    comandas.append({"cliente": cliente, "item": item, "quantidade": quantidade, "valor_total": valor_total})
    global caixa, marmitas_vendidas
    caixa += valor_total
    marmitas_vendidas += quantidade
    clientes_atendidos.add(cliente)
    print(f"Venda registrada com sucesso. Valor total: R$ {valor_total:.2f}")

def visualizar_caixa():
    print(f"Saldo em caixa: R$ {caixa:.2f}")
    print(f"Marmitas vendidas: {marmitas_vendidas}")
    print("Despesas registradas:")
    for despesa in despesas:
        print(f"  - {despesa['descricao']}: R$ {despesa['valor']:.2f}")

def visualizar_clientes_atendidos():
    print("Clientes atendidos:")
    for cliente in clientes_atendidos:
        print(f"  - {cliente}")

def menu():
    while True:
        print("\nMenu:")
        print("1. Cadastrar Cliente")
        print("2. Cadastrar Item no Cardápio")
        print("3. Registrar Despesa")
        print("4. Registrar Venda")
        print("5. Visualizar Caixa")
        print("6. Visualizar Clientes Atendidos")
        print("0. Sair")
        
        opcao = input("Escolha uma opção: ")
        
        if opcao == "1":
            cadastrar_cliente()
        elif opcao == "2":
            cadastrar_cardapio()
        elif opcao == "3":
            registrar_despesa()
        elif opcao == "4":
            registrar_venda()
        elif opcao == "5":
            visualizar_caixa()
        elif opcao == "6":
            visualizar_clientes_atendidos()
        elif opcao == "0":
            print("Saindo...")
            break
        else:
            print("Opção inválida. Tente novamente.")

# Execução do programa
if _name_ == "_main_":
    menu()
