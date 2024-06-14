# Desafio-DIO-Python-Criando-conta-banc-ria
Abaixo está o código feito para o desafio da DIO onde eu criei um sistema bancário em python

class ContaBancaria:
    def __init__(self):
        self.saldo = 0.0
        self.movimentacoes = []
        self.saques_diarios = 0
        self.limite_saques_diarios = 3
        self.limite_saque = 500.0

    def depositar(self, valor):
        if valor > 0:
            self.saldo += valor
            self.movimentacoes.append(f"Depósito: R$ {valor:.2f}")
            print(f"Depósito de R$ {valor:.2f} realizado com sucesso.")
        else:
            print("Valor de depósito inválido.")

    def sacar(self, valor):
        if self.saques_diarios >= self.limite_saques_diarios:
            print("Limite de saques diários atingido.")
            return
        
        if valor > self.limite_saque:
            print(f"Não é possível sacar mais do que R$ {self.limite_saque:.2f} por operação.")
            return
        
        if valor <= 0:
            print("Valor de saque inválido.")
            return
        
        if valor > self.saldo:
            print("Saldo insuficiente para realizar o saque.")
            return
        
        self.saldo -= valor
        self.saques_diarios += 1
        self.movimentacoes.append(f"Saque: R$ {valor:.2f}")
        print(f"Saque de R$ {valor:.2f} realizado com sucesso.")

    def exibir_extrato(self):
        if not self.movimentacoes:
            print("Não foram realizadas movimentações.")
        else:
            for movimentacao in self.movimentacoes:
                print(movimentacao)
        print(f"Saldo atual: R$ {self.saldo:.2f}")

    def resetar_saques_diarios(self):
        self.saques_diarios = 0

# Exemplo de uso
conta = ContaBancaria()

# Realizando depósitos
conta.depositar(1000)
conta.depositar(500)

# Realizando saques
conta.sacar(300)
conta.sacar(200)
conta.sacar(100)

# Tentativa de saque além do limite diário
conta.sacar(50)

# Exibindo o extrato
conta.exibir_extrato()

Explicação do Código
Classe ContaBancaria: Define uma conta bancária com saldo, movimentações, limite de saques diários e limite por saque.
Método depositar: Permite adicionar dinheiro à conta, desde que o valor seja positivo.
Método sacar: Permite retirar dinheiro da conta, respeitando os limites de saques diários, o limite de valor por saque e verificando o saldo disponível.
Método exibir_extrato: Mostra todas as movimentações (depósitos e saques) e o saldo atual. Se não houver movimentações, exibe uma mensagem apropriada.
Método resetar_saques_diarios: Reseta o contador de saques diários, o que pode ser usado ao final de cada dia.
O exemplo de uso no final mostra como você pode interagir com a classe para realizar depósitos, saques e consultar o extrato.

Observações
Para um sistema em produção, você provavelmente precisaria de funções adicionais para gerenciamento de contas e persistência dos dados.
O método resetar_saques_diarios deveria ser chamado ao final de cada dia, possivelmente por meio de um processo agendado.
