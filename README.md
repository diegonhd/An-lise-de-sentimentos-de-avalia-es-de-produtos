# Análise de Sentimentos de Avaliações de Produtos (Olist)

Este projeto realiza uma análise de sentimentos sobre avaliações de produtos encontrados em um banco de datasets públicos da Olist. O objetivo é classificar os comentários dos clientes como positivos, negativos ou neutros e, a partir disso, identificar as categorias de produtos com os maiores e menores índices de satisfação.

O núcleo da análise é o uso de um modelo de linguagem pré-treinado (BERT) para interpretar o sentimento expresso nos textos das avaliações, comparando-o em seguida com a nota originalmente atribuída pelo cliente.

## 📂 Estrutura do Repositório
Markdown

# Análise de Sentimentos de Avaliações de Produtos (Olist)

Este projeto realiza uma análise de sentimentos sobre as avaliações de produtos de um grande marketplace brasileiro, utilizando o dataset público da Olist. O objetivo é classificar os comentários dos clientes como positivos, negativos ou neutros e, a partir disso, identificar as categorias de produtos com os maiores e menores índices de satisfação.

O núcleo da análise é o uso de um modelo de linguagem pré-treinado (BERT) para interpretar o sentimento expresso nos textos das avaliações, comparando-o em seguida com a nota originalmente atribuída pelo cliente.

## 📂 Estrutura do Repositório
```bash
/
├── archive/
│   ├── olist_order_items_dataset.csv
│   ├── olist_order_reviews_dataset.csv
│   ├── olist_orders_dataset.csv
│   ├── olist_products_dataset.csv
│   └── product_category_name_translation.csv
├── analise_sentimentos.ipynb
├── requirements.txt
└── README.md
```
-   **`archive/`**: Contém todos os arquivos `.csv` do dataset da Olist necessários para a análise.
-   **`analise_sentimentos.ipynb`**: O Jupyter Notebook com todo o código da análise, desde o pré-processamento até a visualização dos resultados.
-   **`requirements.txt`**: Arquivo com as bibliotecas Python necessárias para executar o projeto.

## 🛠️ Tecnologias Utilizadas

-   **Python 3**
-   **Pandas**: Para manipulação e análise dos dados.
-   **Transformers (Hugging Face)**: Para utilizar o modelo BERT pré-treinado em análise de sentimentos.
-   **Plotly**: Para a criação de gráficos interativos e visualizações de dados.
-   **TextBlob**: Biblioteca para processamento de texto.
-   **Jupyter Notebook**: Como ambiente de desenvolvimento para a análise.

## 🚀 Como Executar o Projeto

1.  **Clone o repositório:**
    ```bash
    git clone <url-do-seu-repositorio>
    cd <nome-do-repositorio>
    ```

2.  **Crie um ambiente virtual (recomendado):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    ```

3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Verifique os dados**: Certifique-se de que os arquivos CSV do dataset da Olist estão dentro da pasta `archive/`.

5.  **Execute o Jupyter Notebook:**
    ```bash
    jupyter notebook analise_sentimentos.ipynb
    ```

## 📝 Metodologia

A análise foi conduzida seguindo as etapas abaixo:

1.  **Carregamento e Mesclagem de Dados**: Os múltiplos arquivos CSV da Olist foram carregados e mesclados para criar um DataFrame unificado, contendo informações de pedidos, produtos e avaliações.

2.  **Análise de Sentimentos com BERT**:
    -   Foi utilizado o modelo pré-treinado `nlptown/bert-base-multilingual-uncased-sentiment` da Hugging Face, capaz de classificar textos em uma escala de 1 a 5 estrelas.
    -   Uma função foi criada para aplicar o modelo aos comentários das avaliações, extraindo uma "nota do comentário" (de 1 a 5).
    -   Essa nota foi então convertida em um sentimento categórico: **Positivo** (4 ou 5), **Neutro** (3) ou **Negativo** (1 ou 2).

3.  **Amostragem e Classificação**: Para otimizar o processamento, foi selecionada uma amostra aleatória de 1000 avaliações que continham comentários. Para cada avaliação na amostra, foram criadas duas colunas de sentimento:
    -   `sentimento_comentario`: Baseado na previsão do modelo BERT sobre o texto.
    -   `sentimento_nota`: Baseado na nota (de 1 a 5) que o cliente originalmente deu.

4.  **Avaliação de Acurácia**: A análise inicial comparou o `sentimento_comentario` com o `sentimento_nota`, atingindo uma acurácia de **73.20%**.

5.  **Análise Combinada (Aprimoramento)**: Para obter uma visão mais robusta, foi criada uma segunda métrica de análise (`analise_combinada2`) que calcula a média entre a nota do cliente (`review_score`) e a nota prevista pelo BERT (`comment_score`). Essa abordagem elevou a acurácia de compatibilidade para **81.80%**, mostrando-se mais alinhada com a avaliação original do cliente.
