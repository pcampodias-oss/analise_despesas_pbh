# 📊 Análise de Despesas da Prefeitura de Belo Horizonte

    ![Badge](https://img.shields.io/badge/Status-Completo-brightgreen) 
    ![Badge](https://img.shields.io/badge/Período-2021%20a%202026-blue)
    ![Badge](https://img.shields.io/badge/Linguagem-SQL%2FPower%20BI-orange)
    ![Badge](https://img.shields.io/badge/Banco%20de%20Dados-MySQL-blueviolet)

    ---

    ## 📋 Visão Geral

    Projeto de **análise exploratória e inteligência de negócio** das despesas públicas da Prefeitura de Belo Horizonte, compreendendo o período de **2021 a 2026**. 

    O projeto utiliza uma arquitetura moderna de dados com:
    - ✅ Modelagem dimensional (Star Schema)
    - ✅ Pipeline ETL automatizado (Apache Hop)
    - ✅ Análises avançadas com Machine Learning
    - ✅ Dashboards executivos em Power BI

    **Objetivo**: Facilitar a tomada de decisão dos gestores públicos sobre alocação de recursos e controle de despesas.

    ---

    ## 🎯 Objetivos do Projeto

    ### Objetivo Principal
    Prover análises detalhadas que facilitem a tomada de decisão em relação aos gastos públicos da Prefeitura de Belo Horizonte, considerando:

    - 💰 **Evolução de despesas** ao longo dos anos
    - 🏛️ **Distribuição por órgão** (Unidades Orçamentárias - UO)
    - 👥 **Análise por credor** (fornecedores/prestadores)
    - 🔍 **Detecção de anomalias** em padrões de despesas
    - 📈 **Previsão de gastos** futuros

    ### Dimensões Analisadas
    | Dimensão | Descrição |
    |----------|-----------|
    | **Temporal** | Análise por ano, mês e período |
    | **Organizacional** | Despesas por UO e secretarias |
    | **Credores** | Análise por fornecedor/prestador |
    | **Natureza** | Classificação da despesa (empenho, liquidação, pagamento) |
    | **Valores** | Evolução monetária das despesas |

    ---

    ## 👥 Público-Alvo

    ### 1️⃣ Gestores Estratégicos e Financeiros
    - **Secretaria Municipal da Fazenda (SMF)** – Principal responsável pela saúde financeira
    - **Prefeito e Secretários Municipais** – Decisões sobre alocação de recursos
    - **Assessoria de Planejamento** – Definição de políticas públicas

    ### 2️⃣ Gestores Operacionais
    - **Diretores de Unidades Orçamentárias (UOs)**
    - **Ordenadores de Despesa** – Secretaria de Segurança, Educação, Saúde, etc.
    - **Auditoria e Controle Interno**


    ---

    ## 📊 Conceitos de Despesa Pública

    As despesas públicas no Brasil seguem um processo formal com **três fases principais**:

    ### 1. **Empenho** 🎯
    Ato administrativo que **reserva parte do orçamento** para uma despesa específica. É o compromisso de gastar.

    ### 2. **Liquidação** ✅
    Fase em que o órgão público **verifica se o bem foi entregue** ou se o **serviço foi prestado** conforme o contratado.

    ### 3. **Pagamento** 💳
    Quando o órgão público **efetivamente transfere o dinheiro** ao credor (prestador do serviço/fornecedor).

    ---

    ## 🗂️ Modelo de Dados

    ### Arquitetura
    O projeto utiliza uma **Arquitetura em Camadas**:

    ```
    ┌─────────────────────────────────────┐
    │   Camada de Apresentação            │
    │   (Dashboards - Power BI)           │
    └────────────────┬────────────────────┘
                     │
    ┌────────────────▼────────────────────┐
    │   Camada de Análise                 │
    │   (MySQL + Machine Learning)        │
    └────────────────┬────────────────────┘
                     │
    ┌────────────────▼────────────────────┐
    │   Camada de Dados                   │
    │   (Modelo Dimensional - Star Schema)│
    └────────────────┬────────────────────┘
                     │
    ┌────────────────▼────────────────────┐
    │   Camada de Integração (ETL)        │
    │   (Apache Hop - Pipelines)          │
    └────────────────┬────────────────────┘
                     │
    ┌────────────────▼────────────────────┐
    │   Camada de Origem                  │
    │   (CSV - Dados Abertos PBH)         │
    └─────────────────────────────────────┘
    ```

    ### Modelagem Dimensional

    Foram elaborados **3 modelos dimensionais** (Star Schema):

    1. **Fato Empenho** – Análise de comprometimento de recursos
    2. **Fato Liquidação** – Análise de verificação de entrega/serviço
    3. **Fato Pagamento** – Análise de transferência efetiva de recursos

    #### Estrutura do Schema
    **Nome do banco**: `despesaspbh`

    **Tabelas Fato:**
    - `fact_empenho` – Registros de empenho
    - `fact_liquidacao` – Registros de liquidação
    - `fact_pagamento` – Registros de pagamento

    **Tabelas Dimensões:**
    - `dim_tempo` – Dimensão temporal
    - `dim_unidade_orcamentaria` – Unidades Orçamentárias (UOs)
    - `dim_credor` – Credores/Fornecedores
    - `dim_natureza_despesa` – Classificação de despesas
    - `dim_modalidade_empenho` – Modalidades de empenho

    ---

    ## 📥 Dados

    ### Fonte de Dados

    | Atributo | Detalhes |
    |----------|----------|
    | **Origem** | [Portal de Dados Abertos - Prefeitura de Belo Horizonte](https://dados.pbh.gov.br/dataset/despesa-consolidada-em-tempo-real) |
    | **Dataset** | Despesas 2021 até 2026 |
    | **Formato** | CSV |
    | **Linhas** | 737.594 registros |
    | **Colunas** | 63 campos |
    | **Período** | 2021 a 2026 |
    | **Frequência** | Consolidado em tempo real |

    ### Características dos Dados
    - ✅ Dados públicos e auditáveis
    - ✅ Atualização em tempo real
    - ✅ Cobertura completa das despesas municipais
    - ⚠️ Requer limpeza e transformação (tratamento de nulos, duplicatas, formatação)

    ---

    ## 🔧 Tratamento e Integração de Dados (ETL)

    ### Ferramenta de ETL
    **Apache Hop** 
    ### Processos de Limpeza e Transformação

    #### 1️⃣ Carga das Dimensões
    ```
    1. Leitura do arquivo CSV (componente CSV_file_input)
    2. Configuração de formatação de colunas
    3. Remoção de duplicatas (Unique Rows)
    4. Tratamento de valores nulos (IF Null)
       └─ Strings nulas → "NÃO INFORMADO"
       └─ Números nulos → 0
    5. Seleção de colunas relevantes (Select Values)
    6. Limpeza de dados com Replace in String:
       └─ Remove números: [0-9]
       └─ Remove pontos: \.
       └─ Normaliza espaços: \s+
       └─ Remove caracteres especiais: [^a-zA-Z\sçÇáàâãéèêíïóôõöúçÁÀÂÃÉÈÊÍÏÓÔÕÖÚ]
    7. Padronização: maiúscula + trim (String Operations)
    8. Carga no banco de dados (Table Output com Dimension Lookup)
    ```

    #### 2️⃣ Carga das Tabelas Fato
    ```
    1. Leitura do CSV (componente CSV_file_input)
    2. Seleção de campos necessários (Select Values)
    3. Limpeza de espaços em branco
    4. Busca de chaves estrangeiras (3 lookups em série):
       └─ Lookup Dimensão Tempo
       └─ Lookup Dimensão UO
       └─ Lookup Dimensão Credor
    5. Seleção de campos após lookups
    6. Ordenação e remoção de duplicatas
    7. Inserção no banco (Table Output)
    ```

    #### 3️⃣ Workflow Automatizado
    - Execução do script SQL (carga dimensão Tempo)
    - Execução sequencial dos 3 pipelines de fato
    - Logging de execução
    - Notificação de sucesso/erro

    ### Expressões Regulares Utilizadas

    | Padrão | Descrição | Exemplo |
    |--------|-----------|---------|
    | `[0-9]` | Remove todos os números | `123ABC` → `ABC` |
    | `\.` | Remove pontos | `A.B.C` → `ABC` |
    | `\s+` | Espaços duplos em um só | `A  B` → `A B` |
    | `[^a-zA-Z\s...]` | Remove caracteres especiais | `A@B!` → `AB` |

    ---

    ## 📈 Camada de Apresentação

    ### Dashboards Executivos (Power BI)

    Foram desenvolvidos **4 painéis principais**:

    #### 1. **Painel Estratégico** 🎯
    - **Visão Geral de Despesas 2021-2026**
    - KPIs: Total gasto, média anual, evolução temporal
    - Análise de tendências gerais
    - Público: Prefeito, Secretários, SMF

    #### 2. **Painel Tático** 📊
    - **Visão Analítica das Despesas**
    - Despesas por UO (órgão)
    - Distribuição por modalidade
    - Análise comparativa entre períodos
    - Público: Gestores estratégicos

    #### 3. **Painel Operacional 1** 🏢
    - **Análise de Despesas por UO**
    - Drill-down por Unidade Orçamentária
    - Detalhamento de gastos por secretaria
    - Evolução histórica
    - Público: Diretores de UOs

    #### 4. **Painel Operacional 2** 👥
    - **Análise por Credor**
    - Principais fornecedores/prestadores
    - Volume de transações
    - Valores pagos por credor
    - Público: Auditoria, Controle Interno

    ---

    ## 🤖 Análises Avançadas

    ### 1. Detecção de Anomalias
    Modelo de Machine Learning que identifica padrões anormais em despesas:
    - 🔴 Despesas fora do padrão histórico
    - 🔴 Picos anormais de gasto
    - 🔴 Possíveis irregularidades
    - 🔴 Alertas para auditoria

    **Técnica**: Isolation Forest / Z-Score

    ### 2. Previsão de Despesas Futuras
    Modelo preditivo para 2026:
    - 📈 Estimativa de gastos futuros por UO
    - 📈 Tendências de despesas
    - 📈 Auxilia no planejamento orçamentário
    - 📈 Suporta decisões de alocação



    ---


    ### Análise de Ciclo de Despesas
    ✅ Identificação do fluxo completo de despesas (Empenho → Liquidação → Pagamento)  
    ✅ Análise de gaps entre fases do ciclo  
    ✅ Identificação de gargalos operacionais

    ### Previsões para 2026
    📊 Valores aproximados com pequeno desvio da média  
    📊 Crescimento esperado vs. períodos anteriores  
    📊 Apoio à elaboração do orçamento

    ### Detecção de Anomalias
    ⚠️ Identificação de transações suspeitas  
    ⚠️ Seleção de valores anormais para auditoria  
    ⚠️ Redução de fraude e irregularidades

    ---

    ## 💻 Tecnologias Utilizadas

    | Categoria | Tecnologia | Versão |
    |-----------|-----------|---------|
    | **Banco de Dados** | MySQL | 5.7+ |
    | **Modelagem** | Star Schema / Data Warehouse | - |
    | **ETL** | Apache Hop | 2.x |
    | **BI & Visualização** | Microsoft Power BI | Desktop |
    | **Machine Learning** | Python/Scikit-learn | - |
    | **Consultas** | SQL 
    | **Fonte de Dados** | CSV | - |

    ---

    ## 📁 Estrutura do Projeto

    ```
    analise-despesas-pbh/
    │
    ├── README.md                          # Este arquivo
    ├── LICENSE                            # Licença do projeto
    │
    ├── dados/
    │   ├── despesas_2021_2026.csv         # Dataset original
    │   ├── dicionario_dados.md            # Descrição das colunas
    │   └── qualidade_dados.md             # Relatório de qualidade
    │
    ├── sql/
    │   ├── schema/
    │   │   ├── criacao_schema.sql         # Criação do banco
    │   │   ├── tabelas_dimensoes.sql      # Criação dimensões
    │   │   └── tabelas_fatos.sql          # Criação fatos
    │   │
    │   ├── consultas/
    │   │   ├── kpi_estrategicos.sql       # KPIs principais
    │   │   ├── analise_uos.sql            # Análise por UO
    │   │   ├── analise_credores.sql       # Análise por credor
    │   │   └── deteccao_anomalias.sql     # Queries de anomalias
    │   │
    │   └── manutencao/
    │       ├── carga_inicial.sql          # Carga de dados
    │       └── indices.sql                # Otimizações
    │
    ├── etl/
    │   ├── pipelines/
    │   │   ├── pipeline_dimensoes.hop     # Pipeline ETL dimensões
    │   │   ├── pipeline_empenho.hop       # Pipeline fato empenho
    │   │   ├── pipeline_liquidacao.hop    # Pipeline fato liquidação
    │   │   └── pipeline_pagamento.hop     # Pipeline fato pagamento
    │   │
    │   ├── workflows/
    │   │   └── workflow_automatizado.hop  # Orquestração automática
    │   │
    │   └── logs/
    │       ├── etl_execucoes.log          # Log de execuções
    │       └── erros_tratamento.log       # Log de erros
    │
    ├── powerbi/
    │   ├── relatorio_executivo.pbix       # Arquivo Power BI
    │   │
    │   ├── dashboards/
    │   │   ├── painel_estrategico.md      # Documentação painel 1
    │   │   ├── painel_tatico.md           # Documentação painel 2
    │   │   ├── painel_operacional_uo.md   # Documentação painel 3
    │   │   └── painel_operacional_credor.md # Documentação painel 4
    │   │
    │   └── screenshots/
    │       ├── painel_1.png
    │       ├── painel_2.png
    │       ├── painel_3.png
    │       └── painel_4.png
    │
    ├── analise_ml/
    │   ├── deteccao_anomalias.py          # Modelo de anomalias
    │   ├── previsao_despesas.py           # Modelo preditivo
    │   ├── treinamento_modelos.py         # Script de treino
    │   └── resultados.md                  # Resultados ML
    │
    ├── documentacao/
    │   ├── arquitetura.md                 # Visão geral arquitetura
    │   ├── modelo_conceitual.md           # Conceitos de negócio
    │   ├── guia_usuario.md                # Manual para usuários
    │   ├── guia_manutencao.md             # Guia técnico
    │   └── licoes_aprendidas.md           # Reflexões do projeto
    │
    └── imagens/
        ├── diagrama_etl.png
        ├── diagrama_modelo.png
        └── fluxo_despesas.png
    ```

   


    ## 📝 Conclusões e Lições Aprendidas

    ### Sobre os Dados
    - 🔍 Base com desafios significativos de modelagem
    - 🔍 Dados originários em planilha única sem estrutura
    - 🔍 Tratamento rigoroso necessário para qualidade

    ### Sobre o Desenvolvimento
    - 🛠️ Migração de **Knime para Apache Hop** melhorou performance
    - 🛠️ Testes de inserção após carga validaram integridade
    - 🛠️ Machine Learning tem grande potencial para análises futuras

    ### Sobre o Negócio
    - 💡 Conhecimento aprofundado de despesa pública
    - 💡 Compreensão das fases: Empenho → Liquidação → Pagamento
    - 💡 Importância crítica da transparência e auditoria

    ### Sobre Habilidades Técnicas
    - 🎓 Aprendizado de ferramentas desconhecidas
    - 🎓 Gestão de problemas e pressão de cronograma
    - 🎓 Desenvolvimento ágil em ambiente corporativo

    ---

    ## 🔗 Referências e Links

    ### Base de Dados
    - 📊 [Portal Dados Abertos - Despesas PBH](https://dados.pbh.gov.br/dataset/despesa-consolidada-em-tempo-real)

    ### Conceitos e Regulamentação
    - 📚 [Glossário - Prefeitura de BH](https://prefeitura.pbh.gov.br/transparencia/contas-publicas/glossario)
    - 📚 [Portal da Transparência Federal](https://portaldatransparencia.gov.br)
    - 📚 [Portal de Transparência BH](https://prefeitura.pbh.gov.br/transparencia?form=despesas)
    - 📚 [Orçamento Fácil - Senado Federal](https://www12.senado.leg.br/orcamentofacil)

    ### Capacitação
    - 🎓 [Escola Virtual - Governo Federal](https://www.escolavirtual.gov.br/curso/115)

    ### Artigos Técnicos
    - 📄 [Detecção e Análise de Anomalias em Séries Temporais de Despesas Municipais](https://sol.sbc.org.br/index.php/wcge/article/view/36325/36112)

    ---


    ### Habilidades Aplicadas
    - ✅ Modelagem de Dados (Star Schema / Data Warehouse)
    - ✅ ETL com Apache Hop
    - ✅ SQL Avançado (MySQL)
    - ✅ Business Intelligence (Power BI)
    - ✅ Machine Learning (Python / Scikit-learn)
    - ✅ Análise de Dados e Inteligência de Negócio

    ### Redes
    - 🔗 [LinkedIn](https://linkedin.com/in/patrícia-campos-dias-1b350822)
    - 🐙 [GitHub](https://github.com/pcampodias-oss)
    - 📧 Email: pcampodias@gmail.com

    ---

   

    **Última atualização:** Setembro de 2026  


    ---


    