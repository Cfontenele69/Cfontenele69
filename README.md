## Código Python para Gerenciamento de Bolo

```python
class Bolo:
    """Classe para representar um bolo com seus atributos e métodos."""

    def __init__(self, nome, preco, ingredientes, quantidade_estoque):
        """Inicializa um objeto Bolo com nome, preço, ingredientes e quantidade em estoque."""
        self.nome = nome
        self.preco = preco
        self.ingredientes = ingredientes
        self.quantidade_estoque = quantidade_estoque

    def vender(self, quantidade):
        """Vende uma quantidade de bolos, atualizando o estoque."""
        if quantidade <= self.quantidade_estoque:
            self.quantidade_estoque -= quantidade
            return True
        else:
            print(f"Estoque insuficiente para {self.nome}.")
            return False

    def __str__(self):
        """Retorna uma representação textual do bolo."""
        return f"Bolo {self.nome} - R$ {self.preco:.2f} - Estoque: {self.quantidade_estoque}"


class LojaBolos:
    """Classe para gerenciar a loja de bolos, com estoque, vendas e lucro."""

    def __init__(self):
        """Inicializa a loja com um dicionário de bolos e um histórico de vendas."""
        self.bolos = {}
        self.vendas_do_dia = {}

    def adicionar_bolo(self, bolo):
        """Adiciona um bolo ao estoque da loja."""
        self.bolos[bolo.nome] = bolo

    def vender_bolo(self, nome_bolo, quantidade):
        """Vende um bolo, atualizando o estoque e o histórico de vendas."""
        if nome_bolo in self.bolos:
            bolo = self.bolos[nome_bolo]
            if bolo.vender(quantidade):
                if nome_bolo in self.vendas_do_dia:
                    self.vendas_do_dia[nome_bolo] += quantidade
                else:
                    self.vendas_do_dia[nome_bolo] = quantidade
                print(f"{quantidade} {nome_bolo}(s) vendido(s) com sucesso!")
        else:
            print(f"Bolo {nome_bolo} não encontrado no estoque.")

    def calcular_lucro(self):
        """Calcula o lucro total do dia."""
        lucro_total = 0
        for nome_bolo, quantidade in self.vendas_do_dia.items():
            bolo = self.bolos[nome_bolo]
            lucro_total += (bolo.preco * quantidade) - (bolo.ingredientes * quantidade)
        return lucro_total

    def relatorio_vendas(self):
        """Exibe um relatório das vendas do dia."""
        print("Relatório de Vendas:")
        for nome_bolo, quantidade in self.vendas_do_dia.items():
            print(f"{nome_bolo}: {quantidade} unidades vendidas")
        print(f"Lucro total do dia: R$ {self.calcular_lucro():.2f}")

# Criando objetos Bolo
bolo_cenoura = Bolo("Cenoura", 15.00, 5.00, 10)
bolo_vulcao = Bolo("Vulcão", 18.00, 6.00, 8)

# Criando a loja
loja = LojaBolos()

# Adicionando os bolos ao estoque
loja.adicionar_bolo(bolo_cenoura)
loja.adicionar_bolo(bolo_vulcao)

# Simulando vendas
loja.vender_bolo("Cenoura", 3)
loja.vender_bolo("Vulcão", 2)

# Exibindo o relatório de vendas
loja.relatorio_vendas()
```

