# Diagrama 2

```mermaid

classDiagram
    direction LR
    class Produto {
        +id
        +nome
        +preco
        +ativo
        +atualizarPreco()
    }

    class Pedido {
        +id
        +dataCriacao
        +status
        +vendedorResponsavel
        +adicionarItem()
        +fecharPedido()
    }

    class ItemPedido {
        +quantidade
        +precoUnitario
    }

    class MovimentacaoEstoque {
        +id
        +quantidade
        +tipoMovimentacao
        +data
        +justificativa
    }

    class EstoqueService {
        +consultarSaldo()
        +registrarEntrada()
        +registrarSaida()
    }

    Pedido "1" *-- "1..*" ItemPedido : possui
    ItemPedido "1" --> "1" Produto : referencia
    MovimentacaoEstoque "1" --> "1" Produto : altera saldo de
    EstoqueService ..> MovimentacaoEstoque : gerencia

