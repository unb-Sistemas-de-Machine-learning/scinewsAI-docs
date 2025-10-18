# Requisitos de Machine Learning

## Requisitos Funcionais (ML)

1. RF-ML01 - Entrada do Modelo: O modelo deve aceitar como entrada o texto completo (full_text) ou uma concatenação do título, resumo e texto completo de um artigo científico.
2. RF-ML02 - Saída do Modelo: O modelo deve gerar um texto em português que seja uma versão simplificada do artigo original, explicando os conceitos chave, a metodologia e os resultados de forma clara e acessível para não especialistas.
3. RF-ML03 - Consistência Factual: A simplificação gerada deve ser factualmente correta e não introduzir informações que não estejam presentes no artigo original.
4. RF-ML04 - Controle de Jargão: O modelo deve identificar e explicar jargões técnicos ou substituí-los por termos mais simples, quando possível.

---

## Requisitos Não Funcionais (ML)

1. RNF-ML01 - Latência de Inferência: Como o processo rodará em background semanalmente, a latência por artigo não é crítica, mas o lote de artigos da semana deve ser processado em menos de 12 horas para garantir a publicação atempada.
2. RNF-ML02 - Robustez: O modelo deve ser capaz de lidar com diferentes formatações de texto extraído de PDFs, incluindo notações matemáticas e referências, sem gerar erros.
3. RNF-ML03 - Reprodutibilidade: Para um mesmo artigo de entrada, o processo de simplificação deve gerar resultados consistentes, mesmo que não sejam idênticos (devido à natureza estocástica de alguns modelos).
4. RNF-ML04 - Custo de Inferência: O custo por artigo simplificado deve ser monitorado. Por exemplo, manter o custo abaixo de $0.05 por artigo.

---

## Métricas de Avaliação do Modelo (ML)

Esta seção define as métricas quantitativas e qualitativas que serão utilizadas para avaliar o desempenho e a qualidade do modelo de simplificação (RAG + LLM) do SciNewsAI, bem como o comportamento operacional do pipeline de ML em produção.

---

### **Métricas Funcionais (Qualidade e Factualidade)**

O modelo deve ser avaliado periodicamente com base em métricas padronizadas de qualidade textual e consistência factual:

| Categoria    | Métrica                     | Descrição                                                                                                                | Valor Esperado | Ferramenta                 |
| ------------ | --------------------------- | ------------------------------------------------------------------------------------------------------------------------ | -------------- | -------------------------- |
| Semântica    | BERTScore                   | Mede a similaridade semântica entre o artigo original e o texto simplificado, avaliando se o significado foi preservado. | `≥ 0.80`       | `bert_score` (HuggingFace) |
| Factualidade | RAGAS - Faithfulness        | Mede o quanto o texto gerado é fiel às evidências recuperadas no RAG, evitando alucinações.                              | `≥ 0.70`       | `ragas` (LangChain)        |
| Relevância   | RAGAS - Context Precision   | Mede se o modelo está utilizando apenas contextos relevantes e não redundantes.                                          | `≥ 0.70`       | `ragas`                    |
| Cobertura    | ROUGE-L                     | Mede o grau de sobreposição entre o texto simplificado e o original, garantindo manutenção das principais ideias.        | `≥ 0.60`       | `evaluate`                 |
| Legibilidade | Flesch Reading Ease (PT-BR) | Mede o quão fácil é compreender o texto simplificado.                                                                    | `≥ 60`         | `textstat`                 |

---

### **Métricas Operacionais (MLOps e Desempenho)**

As métricas operacionais monitoram a performance da pipeline e confiabilidade das execuções automatizadas.

| Categoria       | Métrica                      | Descrição                                                                            | Valor Esperado      | Ferramenta                   |
| --------------- | ---------------------------- | ------------------------------------------------------------------------------------ | ------------------- | ---------------------------- |
| Desempenho      | Latência média por artigo    | Tempo total para processar e simplificar um artigo, incluindo coleta, RAG e geração. | `≤ 60 s/artigo`     | Prefect Metrics / Prometheus |
| Throughput      | Artigos processados por hora | Quantidade média de artigos processados automaticamente.                             | `≥ 20 artigos/hora` | Prefect Metrics              |
| Disponibilidade | Uptime da pipeline           | Percentual de execuções agendadas concluídas com sucesso.                            | `≥ 99%`             | Prefect / Grafana            |

---

### **Métricas de Experiência do Usuário (Feedback Loop)**

Após a publicação dos textos simplificados, métricas de experiência serão coletadas para medir clareza, confiança e engajamento dos usuários.

| Categoria           | Métrica                         | Descrição                                                                                                  | Valor Esperado | Coleta                               |
| ------------------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------- | -------------- | ------------------------------------ |
| Clareza             | Nota média de clareza (_1–5_)   | Usuários avaliam a facilidade de compreensão do texto.                                                     | `≥ 4.0`        | Formulário / UI feedback             |
| Confiança percebida | Nota média de confiança (_1–5_) | Mede se o usuário percebe o texto como coerente, lógico e confiável, mesmo sem conhecer o artigo original. | `≥ 4.0`        | Feedback simples (positivo/negativo) |
| Engajamento         | Taxa de leitura completa (_%_)  | Percentual de usuários que leem o artigo até o final.                                                      | `≥ 70%`        | Google Analytics / Web stats         |

---

### **Métricas de Qualidade e Ética (Incremental/Futuro)**

Para garantir transparência e confiabilidade do sistema, métricas adicionais podem ser implementadas nas próximas fases.

| Categoria      | Métrica                                | Descrição                                                                   | Ferramenta           |
| -------------- | -------------------------------------- | --------------------------------------------------------------------------- | -------------------- |
| Alucinação     | Alucinação Detectada (LlamaIndex Eval) | Mede se o modelo introduz informações não presentes nas fontes originais.   | `LlamaIndex evals`   |
| Auditabilidade | Explicabilidade (Prompt Trace)         | Registra e rastreia prompts e respostas para auditoria e análise posterior. | `LangSmith / MLflow` |

---

## Histórico de Versões

| Versão | Data       | Descrição                                  | Autor(es)                                        | Revisor(es)                                  |
| ------ | ---------- | ------------------------------------------ | ------------------------------------------------ | -------------------------------------------- |
| `1.0`  | 18/10/2025 | Adiciona documentação de requisitos da IA. | [Matheus Henrique](https://github.com/mathonaut) | [Gustavo Melo](https://github.com/gusrberto) |
