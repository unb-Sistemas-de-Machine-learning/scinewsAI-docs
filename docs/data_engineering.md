# Arquitetura e Engenharia de Dados

A arquitetura de dados do **ScinewsAI** foi projetada focando em robustez, rastreabilidade e autonomia. O sistema opera sob um paradigma de **ELT (Extract, Load, Transform)** modificado para fluxos de GenAI, onde a persistência dos dados brutos e enriquecidos ocorre no PostgreSQL antes da etapa de geração de conteúdo.

## 1. Estratégia de Coleta e Armazenamento

A ingestão de dados segue uma abordagem híbrida para garantir a qualidade e a relevância das informações:

* **Fonte Primária (Arxiv):** A coleta é realizada via API oficial do Arxiv, garantindo a autenticidade dos preprints. Buscamos integralmente os artigos das categorias selecionadas (`cs.AI`, `cs.LG`, `cs.CL`) publicados nos últimos 7 dias.
* **Enriquecimento de Metadados:** Diferente de uma coleta passiva, o sistema enriquece os dados brutos consultando o **Semantic Scholar**. Isso nos permite agregar métricas de impacto (citações, H-Index) que não existem na fonte primária.
* **Persistência (Single Source of Truth):** Utilizamos o **PostgreSQL** como repositório central. Sua capacidade de lidar com tipos complexos (`JSONB`, `ARRAY`) e a extensão **PGVector** eliminam a necessidade de bancos de dados vetoriais separados, simplificando a stack.

## 2. Escopo e Amostragem de Dados

Para o escopo atual (MVP e Produção), **não aplicamos técnicas de amostragem**. O volume semanal de publicações em Ciência da Computação no Arxiv, embora alto, é computacionalmente gerenciável. Processamos 100% dos artigos recuperados para garantir que nenhuma descoberta relevante seja descartada precocemente. A filtragem ocorre *a posteriori*, através do nosso algoritmo de **Relevância (Scoring)**, e não na coleta.

## 3. Paradigma de Machine Learning (Generative AI)

O núcleo de inteligência do projeto não se baseia em classificação tradicional, mas sim em **Geração de Texto (GenAI)**.

* **Abordagem Zero-Shot com RAG:** Não realizamos rotulação manual de dados nem treinamento supervisionado (*fine-tuning*). Utilizamos um LLM (OpenAI GPT) em um paradigma *Zero-Shot*, instruído via **Prompt Engineering**.
* **Contexto via RAG:** Para contornar alucinações e garantir fidelidade técnica, implementamos uma arquitetura **RAG (Retrieval-Augmented Generation)**. O "conhecimento" do modelo não vem de seus pesos internos, mas dos vetores (embeddings) gerados a partir do texto extraído do PDF do artigo.

## 4. Engenharia de Features e Pré-processamento

Embora não utilizemos *feature engineering* clássico (como *one-hot encoding*), aplicamos transformações críticas para o processamento de linguagem natural:

* **Tratamento de Outliers (Comprimento de Texto):** Artigos científicos variam drasticamente em tamanho. Para lidar com os limites de janela de contexto dos LLMs, aplicamos técnicas de **Chunking** (segmentação de texto) recursivo antes da vetorização.
* **Robustez a Falhas (Missing Values):** O pipeline de coleta é resiliente. Artigos com metadados corrompidos ou PDFs inacessíveis são sinalizados com status de erro no banco, impedindo que quebrem o fluxo de processamento, mas permitindo retentativas futuras.
* **Balanceamento de Relevância:** Como não há "classes" para balancear, nosso foco é o **balanceamento de ranking**. Utilizamos uma função logarítmica personalizada (vide seção de *Métricas*) para normalizar a disparidade entre autores "Superstars" e novos pesquisadores, garantindo uma curadoria justa.

## Histórico de Versões

| Versão | Data | Descrição | Autores | Revisores |
| --- | --- | --- | --- | --- |
| `1.0` | 19/10/2025 | Criação do documento de engenharia de dados | [Gustavo Melo](https://github.com/gusrberto) |  |
| `1.1` | 10/12/2025 | Refatoração do módulo | [Gustavo Melo](https://github.com/gusrberto) |  |