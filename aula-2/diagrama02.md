# Diagrama 2

```mermaid

graph TD
    vendedor([Vendedor])
    admin([Administrador])
    estoque([Time de Estoque])
    logistica[Sistema de Logística Externo]

    subgraph SVE_Boundary [Fronteira do Sistema SVE]
        subgraph APRESENTACAO [Camada de Apresentação]
            spa[Aplicação Web SPA <br/> React / TypeScript]
        end

        subgraph DOMINIO [Camada de Domínio / Negócio]
            api[API Backend <br/> Node.js ou Java]
        end

        subgraph DADOS [Camada de Dados]
            db[(Banco de Dados <br/> PostgreSQL)]
        end
    end

    %% Fluxos
    vendedor & admin & estoque -->|Acessa via navegador| spa
    spa -->|Requisições JSON/HTTPS| api
    api -->|Lê e grava SQL| db
    api -->|Notifica novos pedidos| logistica

    style spa fill:#438dd5,stroke:#2b659c,color:#fff
    style api fill:#1168bd,stroke:#0b4884,color:#fff
    style db fill:#7f7f7f,stroke:#595959,color:#fff
