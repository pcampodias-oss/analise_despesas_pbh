

# 📊 Análise de Despesas da Prefeitura de Belo Horizonte
## 📋 Visão Geral
Projeto de **análise exploratória e inteligência de negócio** das despesas públicas da Prefeitura de Belo Horizonte, compreendendo o período de **2021 a 2026**. 

O projeto utiliza uma arquitetura de dados com:

- ✅ Modelagem dimensional (Star Schema)
- ✅ Pipeline ETL automatizado (Apache Hop)
- ✅ Análises avançadas com Machine Learning
- ✅ Dashboards executivos em Power BI


## 🎯 Objetivo do Projeto
 Prover análises detalhadas que facilitem a tomada de decisão em relação aos gastos públicos e alocação de recursos da Prefeitura de Belo Horizonte, considerando:
- **Evolução de despesas** ao longo dos anos
- **Distribuição por órgão** (Unidades Orçamentárias - UO) 
- **Análise por credor** (fornecedores/prestadores)
- **Detecção de anomalias** em padrões de despesas
- **Previsão de gastos** futuros
## Dimensões Analisadas
| Dimensão | Descrição |
|----------|-----------|
| **Temporal** | Análise por ano, mês e período |
| **Organizacional** | Despesas por UO e secretarias |
| **Credores** | Análise por fornecedor/prestador |
| **Natureza** | Classificação da despesa (empenho, liquidação, pagamento) |
| **Valores** | Evolução monetária das despesas |


## 👥 Público-Alvo 
### Gestores Estratégicos e Financeiros
- **Secretaria Municipal da Fazenda (SMF)** – Principal responsável pela saúde financeira
- **Prefeito e Secretários Municipais** – Decisões sobre alocação de recursos
- **Assessoria de Planejamento** – Definição de políticas públicas
###  Gestores Operacionais
- **Diretores de Unidades Orçamentárias (UOs)**
- **Ordenadores de Despesa** – Secretaria de Segurança, Educação, Saúde, etc.
- **Auditoria e Controle Interno**

## 📊 Conceitos de Despesa Pública
As despesas públicas no Brasil seguem um processo formal com **três fases principais**:
 1. **Empenho**: Ato administrativo que reserva parte do orçamento para uma despesa específica. É o compromisso de gastar.
 2. **Liquidação**: Fase em que o órgão público verifica se o bem foi entregue ou se o serviço foi prestado conforme o contratado.
 3. **Pagamento**: Quando o órgão público efetivamente transfere o dinheiro ao credor (prestador do serviço/fornecedor).

## 🗂️ Modelo de Dados


### Modelagem Dimensional

Foram elaborados **3 modelos dimensionais** (Star Schema):

1. **Fato Empenho** – Análise de comprometimento de recursos
2. **Fato Liquidação** – Análise de verificação de entrega/serviço
3. **Fato Pagamento** – Análise de transferência efetiva de recursos

#### Estrutura do Schema
**Nome do banco**: `despesaspbh`

**Tabelas Fato:**
- `fato_despesa_empenho` – Registros de empenho
- `fato_despesa_liquidacao` – Registros de liquidação
- `fato_despesa_pagamento` – Registros de pagamento

**Principais Tabelas Dimensões:**
- `dim_tempo` – Dimensão temporal
- `dim_unidade_orcamentaria` – Unidades Orçamentárias (UOs)
- `dim_credor` – Credores/Fornecedores
- `dim_natureza_despesa` – Classificação de despesas
- `dim_modalidade_empenho` – Modalidades de empenho

---


**Modelagem Dimensional Fato Despesa Empenho**

<img width="844" height="919" alt="image" src="https://github.com/user-attachments/assets/1470d4ab-94d1-4bcc-9ac0-d17815ef35fe" />


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


---

## 🔧 Tratamento e Integração de Dados (ETL)

### Ferramenta de ETL
**Apache Hop** 

### Processos de Limpeza e Transformação

#### 1️⃣ Carga das Dimensões


   1. Leitura do arquivo CSV (componente CSV_file_input)
   2. Configuração de formatação de colunas
   3. Remoção de duplicatas (Unique Rows)
   4. Tratamento de valores nulos (IF Null)
   - Strings nulas → "NÃO INFORMADO"
   - Números nulos → 0
   5. Seleção de colunas relevantes (Select Values)
   6. Limpeza de dados com Replace in String:
   - Remove números: [0-9]
   -  Remove pontos: .
   - Normaliza espaços: \s+
   - Remove caracteres especiais: [^a-zA-Z\sçÇáàâãéèêíïóôõöúçÁÀÂÃÉÈÊÍÏÓÔÕÖÚ]
   7. Padronização: maiúscula + trim (String Operations)
   8. Carga no banco de dados (Table Output com Dimension Lookup)


#### 2️⃣ Carga das Tabelas Fato


   1. Leitura do CSV (componente CSV_file_input)
   2. Seleção de campos necessários (Select Values)
   3. Limpeza de espaços em branco
   4. Busca de chaves estrangeiras (3 lookups em série):
   - Lookup Dimensão Tempo
   - Lookup Dimensão UO
   - Lookup Dimensão Credor
   5. Seleção de campos após lookups
   6. Ordenação e remoção de duplicatas
   7. Inserção no banco (Table Output)


#### 3️⃣ Workflow Automatizado
- Execução do script SQL (carga dimensão Tempo)
- Execução sequencial dos 3 pipelines de fato
- Logging de execução
- Notificação de sucesso/erro

**Workflow do processo ETL integrado**
<img width="945" height="390" alt="image" src="https://github.com/user-attachments/assets/e6e4641c-dff1-4ec4-8411-5b3a547e1b8f" />



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

#### 1. **Painel Estratégico** 
- **Visão Geral de Despesas 2021-2026**


<img width="930" height="522" alt="image" src="https://github.com/user-attachments/assets/963de770-3e91-4ba4-810e-cb7171844f95" />


#### 2. **Painel Tático** 
- **Visão Analítica das Despesas**


<img width="945" height="528" alt="image" src="https://github.com/user-attachments/assets/9daeb7b4-3650-41b4-90cc-613d82cd9f0c" />


#### 3. **Painel Operacional 1** 
- **Análise de Despesas por UO**
<img width="945" height="528" alt="image" src="https://github.com/user-attachments/assets/e05d97c7-63b5-451c-953a-139e9b1b1de6" />


#### 4. **Painel Operacional 2** 
- **Análise por Credor**
<img width="945" height="515" alt="image" src="https://github.com/user-attachments/assets/9508577a-cbe0-4b17-8ef5-b767e8492caf" />


---

## 🤖 Análises Avançadas

### 1. Detecção de Anomalias
Modelo de Machine Learning que identifica padrões anormais em despesas:
-  Despesas fora do padrão histórico
-  Picos anormais de gasto
-  Possíveis irregularidades
-  Alertas para auditoria

**Técnica**: Isolation Forest 
<img width="945" height="531" alt="image" src="https://github.com/user-attachments/assets/b1bbf5d6-0644-492a-a90a-ef8c06431ae0" />


### 2. Previsão de Despesas Futuras
Modelo preditivo para 2026:
- Estimativa de gastos futuros por UO
- Tendências de despesas
- Auxilia no planejamento orçamentário
- Suporta decisões de alocação

<img width="944" height="528" alt="image" src="https://github.com/user-attachments/assets/dfcaa3fe-2820-4c4f-b919-2a6d7109ebb3" />


### 🔄 Análise de Ciclo de Despesas
- ✅ Identificação do fluxo completo de despesas (Empenho → Liquidação → Pagamento)  
- ✅ Análise de gaps entre fases do ciclo  
- ✅ Identificação de gargalos operacionais

### 🔮 Previsões para 2026
- Valores aproximados com pequeno desvio da média  
- Crescimento esperado vs. períodos anteriores  
- Apoio à elaboração do orçamento

### ⚠️ Controle de Riscos (Anomalias)
-  Identificação de transações suspeitas  
-  Seleção de valores anormais para auditoria  
-  Redução de fraude e irregularidades

---

## 💻 Tecnologias Utilizadas

| Categoria | Tecnologia | Versão |
|-----------|-----------|---------|
| **Banco de Dados** | MySQL | 5.7+ |
| **Modelagem** | Star Schema / Data Warehouse | - |
| **ETL** | Apache Hop | 2.x |
| **BI & Visualização** | Microsoft Power BI | Desktop |
| **Machine Learning** | Python / Scikit-learn | - |
| **Consultas** | SQL | Avançado |
| **Fonte de Dados** | CSV | - |

---


## 📝 Conclusões e Lições Aprendidas

### Sobre os Dados
- Base com desafios significativos de modelagem
- Dados originários em planilha única sem estrutura
- Tratamento rigoroso necessário para qualidade

### Sobre o Desenvolvimento
- Migração de **Knime para Apache Hop** melhorou performance
- Machine Learning tem grande potencial para análises futuras

### Sobre o Negócio
- Conhecimento de despesa pública
- Compreensão das fases: Empenho → Liquidação → Pagamento
- Importância crítica da transparência e auditoria

### Sobre Habilidades Técnicas
-  Aprendizado de ferramentas desconhecidas
-  Gestão de problemas e pressão de cronograma
-  Desenvolvimento ágil em ambiente corporativo

---

## 🔗 Referências e Links

### Base de Dados
- 📊 [Portal Dados Abertos - Despesas PBH](https://dados.pbh.gov.br/dataset/despesa-consolidada-em-tempo-real)
- Nome do arquivo: Despesas 2021 até 2026

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

## 🛠️ Competências Aplicadas
- ✅ Modelagem de Dados (Star Schema / Data Warehouse)
- ✅ ETL com Apache Hop
- ✅ SQL Avançado (MySQL)
- ✅ Business Intelligence (Power BI)
- ✅ Machine Learning (Python / Scikit-learn)
- ✅ Análise de Dados e Inteligência de Negócio

---

## 👤 Contato e Redes
- 🔗 [LinkedIn](https://www.linkedin.com/in/patrícia-campos-dias-1b350822/)
- 🐙 [GitHub](https://github.com/pcampodias-oss/)
- 📧 Email: pcampodias@gmail.com

---

**Última atualização:** Setembro de 2026



