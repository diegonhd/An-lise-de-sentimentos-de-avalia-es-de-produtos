# Análise de Sentimentos — Olist

Este repositório contém um notebook Jupyter (`analisefinal.ipynb`) que realiza uma análise exploratória e de sentimentos em avaliações de clientes usando os datasets públicos da **Olist**. O objetivo principal é comparar o sentimento extraído dos comentários (via modelo BERT) com as notas numéricas (`review_score`) e analisar padrões por categoria de produto.

---

## Sumário

* **Descrição:** que faz o notebook
* **Arquivos esperados:** quais CSVs são usados
* **Dependências:** bibliotecas necessárias
* **Como executar:** passos para reproduzir
* **Descrição das etapas do notebook:** resumo das células e análises realizadas
* **Resultados principais & próximos passos**

---

## Arquivos principais

* `analisefinal.ipynb` — Notebook com todo o fluxo de análise.

**Datasets esperados (coloque na pasta `data/` ou adapte caminhos no notebook):**

```
olist_order_items_dataset.csv
olist_order_reviews_dataset.csv
olist_orders_dataset.csv
olist_products_dataset.csv
product_category_name_translation.csv
```

---

## Dependências

Recomendado criar um ambiente virtual e instalar dependências com:

```bash
pip install -r requirements.txt
```

Exemplo mínimo de `requirements.txt`:

```
pandas
matplotlib
plotly
textblob
transformers
jupyter
```

> Observação: o notebook usa um modelo BERT via `transformers` — é necessário acesso à internet para baixar o modelo (`nlptown/bert-base-multilingual-uncased-sentiment`) na primeira execução. GPU é opcional, porém acelera o processamento de inferência.

---

## Como executar (passo a passo)

```bash
# clonar o repositório
git clone https://github.com/seu-usuario/seu-repo.git
cd seu-repo

# criar e ativar ambiente virtual (opcional)
python -m venv venv
# Linux / macOS
source venv/bin/activate
# Windows
venv\Scripts\activate

# instalar dependências
pip install -r requirements.txt

# abrir o notebook
jupyter notebook analisefinal.ipynb
```

---

## Descrição das etapas no notebook

1. **Carregamento das bibliotecas e dos datasets** — import das bibliotecas e leitura dos CSVs da Olist.
2. **Pré-processamento / Merge** — união das tabelas (`order_items`, `orders`, `order_reviews`, `products`) por `order_id` e `product_id` para compor o dataset final de análise.
3. **Amostragem** — seleção de uma amostra de avaliações com texto (por exemplo, 1000 comentários) para acelerar a inferência inicial e permitir visualizações rápidas.
4. **Análise de Sentimento com BERT** — aplicação do modelo `nlptown/bert-base-multilingual-uncased-sentiment` para classificar cada comentário como *Positivo*, *Neutro* ou *Negativo*.
5. **Comparação sentimento vs. nota** — criação de uma métrica de compatibilidade entre o sentimento detectado e a nota `review_score` (1–5) e cálculo de acurácia da correspondência.
6. **Análises por categoria de produto** — cálculo de proporções de avaliações baixas (1–2), neutras e altas (4–5) por categoria; filtra categorias com número mínimo de avaliações para evitar vieses.
7. **Visualizações interativas (Plotly)** — histogramas, rankings por categoria e gráficos que facilitam a interpretação dos padrões de satisfação.

---

## Resultados principais (resumo)

* **Taxa de concordância** entre sentimento textual e nota numérica: o notebook calcula uma acurácia percentual indicando o quanto comentário e nota estão alinhados.
* **Categorias com melhor/worse percepção**: ranking de categorias por proporção de avaliações positivas/negativas.
* **Visualizações interativas** que permitem inspecionar distribuições e comparar sentimento por nota e por categoria.

> Nota: valores numéricos concretos (ex.: acurácia em %) e gráficos gerados estão disponíveis dentro do próprio notebook — revise as células de saída para ver os números obtidos na sua execução local.

---

## Observações e cuidados

* O modelo BERT usado é multilíngue e funciona razoavelmente bem em português, porém existem modelos especificamente treinados para português (ex.: BERTimbau) que podem melhorar a acurácia.
* Avaliações curtas ou com ironia/sarcasmo podem gerar classificações equivocadas — considere rotular uma amostra manualmente para avaliar a performance real.
