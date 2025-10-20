# Arquitetura / Engenharia de Dados

## Coleta e Armazenamento dos Dados

**1**. A coleta é feita diretamente da fonte primária (arXiv), garantindo autenticidade. O armazenamento em um banco de dados PostgreSQL é ideal por ser robusto, confiável e ter excelente suporte para tipos de dados como `Text` e `ARRAY`, que são necessários para o seu schema.

**2**. O processo é projetado para ser 100% automatizado. Um orquestrador de tarefas (como **Celery** ou **Airflow** (ainda a decidir) com agendamento) executará o script de coleta semanalmente.

## Aplicou alguma técnica de amostragem?

**Não**. Para este caso de uso, nenhuma amostragem é necessária. O objetivo é processar todos os artigos de ciência da computação da última semana. O volume de publicações no arXiv é gerenciável e não exige amostragem para o MVP.

## Precisou rotular? Como lidou com a rotulação dos dados? Que tipo de modelo esta usando para resolver esse problema?

* **Não**, nenhuma rotulação de dados é necessária.

* **Como Lidamos**: Usamos um LLM pré-treinado (Google Gemini) em um paradigma zero-shot. Isso significa que o modelo já possui um conhecimento vasto sobre linguagem, ciência e a tarefa de resumir/simplificar, e podemos instruí-lo através de um prompt bem elaborado (a parte de "Geração" no RAG) sem precisar de exemplos rotulados.

* **Tipo de Modelo**: Modelo generativo de texto, especificamente para uma tarefa de simplificação e sumarização abstrativa do conteúdo.

## O projeto lida com balanceamento de classes?

**Não**. O balanceamento de classes é uma técnica para problemas de classificação, onde há um número desigual de exemplos para cada classe. Nosso problema é de geração de texto, portanto, este conceito não se aplica.

## Devido a falta de dados, como os times lideram ou criaram data augmentation?

* Este conceito também não se aplica diretamente aqui. O *data augmentation* é usado para aumentar artificialmente um conjunto de dados de treinamento quando ele é pequeno. Como não estamos treinando (ou mesmo fine-tuning no MVP), não precisamos de dados de treinamento e, consequentemente, de augmentation. O "dado" é o próprio artigo que queremos simplificar, e ele já existe.

## Da parte de feature engineering, como vocês lidam com:

* **Missing values**: O script de coleta deve ser robusto. Se a API do arXiv retornar um artigo sem um campo essencial (ex: `abstract`), podemos decidir pular o artigo ou registrá-lo com um status de `failed_preprocessing`.

* **Outliers**: Em texto, um "outlier" poderia ser um artigo extremamente longo ou curto. O modelo de linguagem geralmente lida bem com variações de comprimento, mas pode haver limites de tokens na API. O `full_text` pode precisar ser truncado ou processado em partes (**chunks**) se exceder o limite de contexto do modelo.

* **Enriquecimento dos dados**: Para o MVP, não é necessário. Futuramente, poderíamos enriquecer os dados buscando o número de citações do artigo, a afiliação dos autores, ou links para implementações no GitHub.

* **Excluir variáveis inúteis**: Não há variáveis inúteis no schema; todas têm um propósito (para exibição, para o modelo ou para metadados).

* **Normalização e padronização dos dados / One hot encoding**: Essas técnicas são para dados numéricos e categóricos usados em modelos de ML tradicionais. Elas não são aplicáveis aqui, pois a entrada do nosso modelo é texto bruto.

## Histórico de Versões

| Versão | Data | Descrição | Autores | Revisores |
| --- | --- | --- | --- | --- |
| `1.0` | 19/10/2025 | Criação do documento de engenharia de dados | [Gustavo Melo](https://github.com/gusrberto) |  |