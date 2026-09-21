# Diagrama 3

```mermaid

graph TD
    spa[Aplicação Web SPA]
    db[(Banco de Dados PostgreSQL)]
    logistica[Sistema de Logística Externo]

    subgraph API_Backend [Dentro da API Backend]
        auth[Componente de Autenticação / JWT]
        
        prod_ctrl[Controlador de Produtos]
        ped_ctrl[Controlador de Pedidos]
        est_ctrl[Controlador de Estoque]
        
        ped_serv[Serviço de Pedidos <br/> Regra de Negócio]
        est_serv[Serviço de Estoque <br/> Regra de Negócio]
    end

    %% Fluxos das requisições
    spa -->|Valida Token| auth
    spa -->|Gerencia Catálogo| prod_ctrl
    spa -->|Registra Vendas| ped_ctrl
    spa -->|Movimenta Estoque| est_ctrl

    %% Fluxos internos
    prod_ctrl -->|SQL| db
    est_ctrl --> est_serv
    ped_ctrl --> ped_serv
    
    ped_serv -->|Baixa automática| est_serv
    ped_serv -->|Notifica envio| logistica
    ped_serv -->|Salva Pedido SQL| db
    est_serv -->|Atualiza Saldo SQL| db

    style auth fill:#2b659c,color:#fff
    style prod_ctrl fill:#85bbf0,color:#000
    style ped_ctrl fill:#85bbf0,color:#000
    style est_ctrl fill:#85bbf0,color:#000
