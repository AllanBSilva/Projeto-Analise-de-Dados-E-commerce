# 🚀 Projeto de Análise de Dados de E-commerce

## 📌 Descrição
Este projeto tem como objetivo analisar um conjunto de dados históricos de vendas de um e-commerce brasileiro, com foco na extração de insights estratégicos, segmentação de clientes e previsão de atrasos nas entregas. Através de técnicas de **Machine Learning** e **análises exploratórias**, buscamos identificar padrões de comportamento e otimizar o desempenho do e-commerce. As principais etapas incluem:

- ✅ **Preparação e limpeza dos dados**
- 📊 **Análise exploratória** (sazonalidade, tempo de entrega, categorias de produtos, etc.)
- 🤖 **Modelagem com Machine Learning** para prever atrasos na entrega
- 🧠 **Segmentação de clientes** e análise de retenção
- 📈 **Criação de dashboards interativos** para análise de vendas, satisfação do cliente e logística

---

## 🗂️ Estrutura do Projeto

A estrutura do projeto está organizada da seguinte forma:

- `data/`  
  - `raw/` - Dados brutos extraídos do Kaggle  
  - `processed/` - Dados tratados e prontos para análise  

- `notebooks/` - Notebooks com todas as etapas do projeto  
  - `01_preparacao_dados.ipynb` - Importação e limpeza de dados  
  - `02_analise_exploratoria.ipynb` - Visualizações e padrões nos dados  
  - `03_solucao_problemas.ipynb` - Modelagem de predição de atrasos  
  - `04_dashboards_visualizacoes.ipynb` - Geração de dashboards e relatórios  

- `requirements.txt` - Lista de bibliotecas necessárias  
- `README.md` - Documentação do projeto

---

## 🔍 Etapas do Projeto

### 1. Preparação dos Dados (`01_preparacao_dados.ipynb`) 🔄
Esta etapa é crucial para garantir que os dados estejam prontos para análises mais profundas e modelagens subsequentes. As principais atividades incluem:

- **Importação de Dados**: Carregamento dos dados brutos em formatos como CSV ou Excel.
- **Tratamento de Dados**: Limpeza de dados ausentes, valores inconsistentes, duplicatas e valores errôneos.
- **Transformação de Dados**: Modificação dos dados para o formato necessário para análise e modelagem.
- **Criação de Features**: Geração de novas variáveis úteis para a análise e modelagem (ex: extração de informações de datas, cálculo de métricas).
- **Criação de Banco de Dados SQLite**: O código cria um banco de dados SQLite (em memória ou arquivo) e armazena os DataFrames como tabelas dentro dele, incluindo informações sobre pedidos, produtos, vendedores, itens, reviews, geolocalização, clientes, pagamentos e categorias.
- **Cálculo de Distâncias**: Utilizando a biblioteca geopy, calcula a distância entre os vendedores e os clientes com base nas suas coordenadas geográficas. Esses dados de distância são então salvos em um arquivo CSV e também carregados de volta ao banco de dados para futuras consultas.

O código nesta etapa garante que os dados sejam limpos e consistentes, permitindo análises e modelagens eficazes.

### 2. Análise Exploratória (`02_analise_exploratoria.ipynb`) 📊
Neste notebook são realizadas consultas SQL no banco de dados SQLite para gerar insights a partir dos dados processados. As análises incluem:

- **Variação mensal de pedidos**: identifica picos e quedas de vendas com base na média histórica mensal, avaliando possíveis tendências sazonais.
- **Tempo de entrega dos pedidos**: classifica os pedidos entregues em faixas de tempo entre aprovação e entrega.
- **Relação entre valor do frete e distância**: agrupa os pedidos por faixas de distância e calcula o frete médio em cada faixa.
- **Faturamento por categoria de produto**: soma do faturamento por categoria com base nos itens vendidos.
- **Ticket médio por estado**: calcula o valor médio dos pedidos em cada estado brasileiro.

Cada uma dessas análises é feita por meio de consultas SQL organizadas em um dicionário Python e executadas diretamente no banco de dados ecommerce_olist.db. Além disso, são exibidos os principais resultados e há uma análise textual específica para identificar padrões de sazonalidade nas vendas.

### 3. Modelagem de Predição de Atrasos (`03_solucao_problemas.ipynb`) 🤖
Neste notebook, foram respondidas diretamente as questões de negócio propostas, sem a realização de tratamento adicional dos dados. Cada item foi abordado separadamente, com análises e modelos simples, conforme exigido:

- **Análise de Retenção**: 
  - Calculada a taxa de clientes recorrentes, considerando como recorrente o cliente que realizou mais de um pedido no período analisado.
  - Foram extraídos insights sobre o comportamento de recompra e possíveis estratégias de fidelização.

- **Predição de Atraso na Entrega**:
  - Definido como "pedido atrasado" aquele entregue após a data estimada (`order_estimated_delivery_date < order_delivered_customer_date`).
  - Criadas variáveis (features) relevantes a partir dos dados disponíveis.
  - Conjunto de dados dividido entre treino e teste.
  - Implementado um modelo de classificação simples (Regressão Logística).
  - Avaliado o desempenho do modelo com métricas apropriadas (como acurácia e matriz de confusão), com explicações sobre os resultados.

- **Segmentação de Clientes (Clustering)**:
  - Aplicada técnica de clustering (KMeans) para segmentar os clientes com base em características de compra.
  - Analisado o perfil de cada grupo identificado.
  - Sugeridas estratégias de marketing personalizadas para cada segmento.

- **Análise de Satisfação**:
  - Investigada a relação entre a nota de avaliação (`review_score`) e variáveis como: categoria do produto, tempo de entrega e valor total do pedido.
  - Identificados os fatores que mais influenciam a satisfação dos clientes, com destaque para o tempo de entrega.


### 4. Dashboards e Visualizações (`04_dashboards_visualizacoes.ipynb`) 📈
Este notebook é dedicado à criação de dashboards interativos e visualizações para explorar os dados da Olist. Utiliza bibliotecas como `plotly`, `seaborn`, `matplotlib` e `ipywidgets` para gerar gráficos interativos e insights visuais.

### 📈 Evolução de Vendas ao Longo do Tempo

Foi criado um dashboard com filtros por **estado do cliente** e **categoria do produto**, permitindo a análise da evolução das vendas ao longo do tempo.

- Dados utilizados:
  - `pedidos.csv`
  - `itens.csv`
  - `produtos.csv`
  - `clientes.csv`

- Tecnologias:
  - `plotly.express` para visualizações interativas
  - `ipywidgets` para criação de filtros dinâmicos

### 🗺️ Mapa de Calor: Vendas por Estado

Foi desenvolvido um **mapa interativo** que mostra a concentração de vendas por estado brasileiro.

- O total de vendas é agregado por estado e visualizado em um **mapa coroplético**.
- Utiliza um arquivo `GeoJSON` de estados do Brasil hospedado no GitHub.
- Ferramentas: `plotly.express`, `requests`, `pandas`

### 📦 Avaliação x Tempo de Entrega

Análise da relação entre o tempo de entrega e a nota de avaliação dada pelos clientes.

- Dados utilizados:
  - `pedidos.csv`
  - `reviews.csv`

- Visualizações:
  - **Boxplot** para mostrar a dispersão do tempo de entrega por nota
  - **Barplot** com média de tempo de entrega por nota
  - **Gráfico de dispersão (stripplot)** para análise granular

- Tecnologias: `seaborn`, `matplotlib`

### 🏆 Análise dos Top Vendedores

Análise dos **10 vendedores com maior faturamento**.

- Métricas por vendedor:
  - Total de pedidos
  - Total de itens vendidos
  - Faturamento total
  - Média de avaliação dos clientes
  - Tempo médio de entrega
  - Cidade e estado de origem

- Gráficos:
  - Faturamento
  - Satisfação média dos clientes
  - Tempo médio de entrega

- Bibliotecas: `plotly.express`, `pandas`

---

Essas visualizações oferecem insights essenciais sobre o comportamento de vendas, qualidade logística e desempenho de vendedores na plataforma da Olist.

---

## 💻 Como Executar
1. Clone este repositório:
   ```bash
   git clone https://github.com/seu-usuario/triggo_ai_trainee_project.git
    ```

2. Crie um ambiente virtual:
- Linux/macOS:
    ```bash
    python -m venv venv
    source venv/bin/activate
    ```
- Windows:
    ```bash
    python -m venv venv
    venv\Scripts\activate
    ```

3. Instale as dependências:
    ```bash
    pip install -r requirements.txt
    ```

4. Execute os notebooks com Jupyter:
    ```bash
    jupyter notebook notebooks/02_analise_exploratoria.ipynb
    ```

 ---

## 📚 Tecnologias Utilizadas

- Python (pandas, scikit-learn, matplotlib, seaborn, Plotly, Dash)
- Jupyter Notebook
- Kaggle (para obtenção dos dados)
- Machine Learning (Modelos de Regressão, Árvores de Decisão, Random Forest)
- SQLAlchemy (para gerenciamento de banco de dados, caso necessário)

 ---

## 📋 Licença

Este projeto está licenciado sob a licença MIT. Consulte o arquivo LICENSE para mais detalhes.