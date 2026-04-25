# 📊 Olist | Executive Strategic Intelligence

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![Reflex](https://img.shields.io/badge/Reflex-Web_Framework-black.svg)
![DuckDB](https://img.shields.io/badge/DuckDB-Data_Warehouse-yellow.svg)
![dbt](https://img.shields.io/badge/dbt_Core-Data_Transformation-orange.svg)

Uma aplicação web analítica completa (Business Intelligence) desenvolvida em Python, focada em fornecer visibilidade estratégica para o corpo executivo (C-Level) do E-commerce brasileiro **Olist**. 

O projeto consolida dados operacionais, financeiros, de experiência do cliente e de marketplace em um único painel de alta performance, construído sobre uma Modern Data Stack (DuckDB + dbt).

---

## 🚀 Como rodar o projeto localmente (Quickstart)

Para executar este projeto na sua máquina, certifique-se de ter o Python 3.9+ instalado.

**1. Clone o repositório:**
```bash
git clone [https://github.com/seu-usuario/olist-executive-dashboard.git](https://github.com/seu-usuario/olist-executive-dashboard.git)
cd olist-executive-dashboard
2. Crie e ative um ambiente virtual:

Bash
python -m venv venv
# No Windows:
venv\Scripts\activate
# No Mac/Linux:
source venv/bin/activate
3. Instale as dependências:

Bash
pip install -r requirements.txt
4. Execute as transformações de dados (dbt Core):
Nota: Este passo compila os Data Marts no banco de dados DuckDB.

Bash
cd olist_project
dbt run
cd ..
5. Inicie a aplicação Reflex (Dashboard):

Bash
reflex run
Acesse o painel no seu navegador através de http://localhost:3000.

📑 Functional Requirements Document (FRD)
Este documento detalha o propósito de negócios, a arquitetura e as métricas que guiaram o desenvolvimento deste produto de dados.

🎯 1. The Goal (O Objetivo)
O objetivo principal deste dashboard é quebrar os silos de informação entre os diferentes departamentos da Olist. Ele visa fornecer uma "Fonte Única de Verdade" (Single Source of Truth) para a alta gestão, permitindo o acompanhamento rápido da saúde financeira, eficiência logística, satisfação do cliente e ecossistema de vendedores (sellers) no período consolidado de Janeiro de 2017 a Agosto de 2018.

📈 2. Key Metrics (Principais Métricas e o "Porquê")
As métricas foram selecionadas e divididas em abas dedicadas aos principais stakeholders:

CFO (Financeiro): Receita Mensal, Ticket Médio e Faturamento por Estado.

Por quê? Para rastrear o fluxo de caixa histórico, o valor vitalício extraído por transação e identificar quais regiões garantem o maior ROI (Retorno sobre Investimento).

COO (Operações): SLA de Entrega (Gargalos e Eficiência), Categorias Mais/Menos Vendidas e Taxa de Pontualidade.

Por quê? A logística é o maior centro de custos de um E-commerce. Monitorar o SLA por estado e o volume de atrasos é crucial para dimensionar a malha logística e trocar de transportadoras se necessário.

CX (Customer Experience): Evolução da Nota de Review, Distribuição de Estrelas e Ranking de Categorias (Melhores/Piores).

Por quê? Clientes insatisfeitos geram custos de SAC e churn. Monitorar categorias críticas (como "Fraldas e Higiene" com notas baixas) permite ações corretivas imediatas na curadoria de produtos.

Head of Marketplace: Concentração de Lojistas, Receita gerada por Estado (Seller) e Competitividade de Frete.

Por quê? Entender onde os sellers estão localizados e o impacto disso no custo do frete é essencial para focar campanhas de aquisição de novos lojistas em estados estratégicos.

🛠️ 3. Actions (Ações e Tomada de Decisão)
Como o time executivo utilizará este painel na prática:

Alocação de Verba: O CFO pode usar o gráfico de "Receita por Estado" para aprovar orçamentos de marketing maiores para regiões com alta conversão (ex: SP e RJ).

Gestão de Crise Logística: O COO pode investigar imediatamente por que Roraima (RR) possui um SLA de quase 30 dias e renegociar contratos de frete rodoviário/aéreo para a região Norte.

Auditoria de Catálogo: O Head de CX pode suspender produtos da categoria "Móveis para Escritório" até que os lojistas melhorem a qualidade, visto que estão derrubando o NPS médio da empresa.

Expansão de Sellers: O Head de Marketplace pode notar um custo alto de frete gerado por lojistas do Sul/Sudeste vendendo para o Nordeste, iniciando uma campanha agressiva para cadastrar lojistas locais na região Nordeste.

🗄️ 4. Data Sources & Architecture (Fontes e Arquitetura)
O projeto segue as melhores práticas de uma Modern Data Stack:

Data Source: Base de dados pública da Olist E-commerce (Kaggle).

Data Warehouse (Motor Analítico): DuckDB - Escolhido por ser um banco de dados relacional colunar in-process, otimizado para cargas de trabalho analíticas rápidas localmente (OLAP).

Data Transformation: dbt Core - Utilizado para limpar as strings, padronizar nomes, unir tabelas e criar os Data Marts finais consumidos pela aplicação.

Frontend (BI): Reflex - Framework Python utilizado para construir a interface de usuário reativa, gerando os componentes visuais e os gráficos (via Recharts) sem necessidade de código Javascript.

🔮 5. Next Steps (Próximos Passos: O que faria com mais 10 horas)
Se o projeto dispusesse de mais 10 horas de desenvolvimento, as seguintes melhorias seriam priorizadas:

Testes de Qualidade de Dados (dbt Tests): Implementar testes granulares no dbt (ex: not_null, unique, accepted_values na coluna de review_score) para garantir a integridade dos Data Marts antes do dashboard ser atualizado.

Filtros Globais Dinâmicos (UI): Adicionar componentes de Dropdown e Date Picker no topo do painel Reflex, permitindo que a diretoria filtre todos os gráficos do dashboard por um mês específico ou por um Estado (UF) em tempo real.

Pipeline CI/CD: Configurar GitHub Actions para rodar automaticamente o dbt run e verificar falhas de código Python sempre que um novo Pull Request for aberto.

Cloud Deployment: Conteinerizar a aplicação (Docker) e realizar o deploy do front-end na Vercel ou AWS, trocando o DuckDB local por um banco na nuvem (como MotherDuck ou BigQuery).
