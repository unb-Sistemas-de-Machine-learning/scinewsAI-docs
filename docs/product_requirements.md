# Backlog

## Requisitos Funcionais (RF)

| **ID**  | **Nome**                              | **Descrição**                                                                                                                                                           |
|----------|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <a name="RF01"></a>**RF01** | Coleta Automática de Artigos          | O sistema deve se conectar à API do arXiv semanalmente para buscar novos artigos de ciência da computação.                                                               |
| <a name="RF02"></a>**RF02** | Armazenamento de Artigos              | O sistema deve persistir os dados dos artigos coletados (ID, título, autores, data, abstract, etc.) no banco de dados PostgreSQL, conforme o schema definido.            |
| <a name="RF03"></a>**RF03** | Processamento e Simplificação de Artigos | Cada novo artigo coletado deve ser submetido a um processo de simplificação usando um modelo de linguagem (via RAG), e o texto resultante deve ser armazenado no campo `simplified_text`. |
| <a name="RF04"></a>**RF04** | Exibição de Artigos Simplificados      | A plataforma web (blog) deve exibir uma lista de artigos com seus títulos, autores e a versão simplificada do texto.                                                     |
| <a name="RF05"></a>**RF05** | Visualização de Artigo Completo        | Ao clicar em um artigo na lista, o usuário deve ser levado a uma página de detalhe que mostra o texto simplificado completo e um link para o artigo original no arXiv (`source_url`). |
| <a name="RF06"></a>**RF06** | Busca de Artigos                      | A plataforma deve oferecer uma funcionalidade de busca que permita aos usuários procurar artigos por título, autor ou palavras-chave.                                    |
| <a name="RF07"></a>**RF07** | Envio de Newsletter                   | O sistema deve compilar os artigos simplificados da semana em um formato de e-mail e enviá-lo para uma lista de assinantes.                                              |
| <a name="RF08"></a>**RF08** | Cadastro e Gerenciamento de Usuários | O sistema deve permitir que novos usuários se cadastrem, selecionem um perfil de interesse (**Estudante**, **Educador** ou **Entusiasta**) e gerenciem suas informações pessoais. O perfil deve influenciar a forma como o conteúdo é exibido e ser editável a qualquer momento. |


## Requisitos Não Funcionais (RNF)

| **ID**   | **Nome**           | **Descrição**                                                                                                                                                                                                 |
|-----------|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RNF01** | Desempenho         | A página inicial e as páginas de artigos devem carregar em menos de 3 segundos. O processo de simplificação (que roda em background) deve ser concluído em tempo razoável para não atrasar a publicação semanal. |
| **RNF02** | Disponibilidade    | A plataforma web deve ter uma disponibilidade mínima de 99,5% (uptime).                                                                                                                                    |
| **RNF03** | Usabilidade        | A interface deve ser limpa, intuitiva e otimizada para leitura, garantindo boa legibilidade em dispositivos móveis e desktops.                                                                              |
| **RNF04** | Manutenibilidade   | O código deve ser bem documentado e modular, facilitando futuras atualizações e a adição de novas funcionalidades (como a personalização da simplificação).                                                 |
| **RNF05** | Escalabilidade     | A arquitetura deve ser capaz de suportar aumento gradual no número de artigos processados por semana e no número de usuários acessando o site.                                                               |
| **RNF06** | Custo              | O custo de infraestrutura e de chamadas de API para o modelo de ML deve ser monitorado e mantido dentro de um orçamento predefinido.                                                                        |

## Histórico de Versões

| Versão | Data | Descrição | Autores | Revisores |
| --- | --- | --- | --- | --- |
| `1.0` | 19/10/2025 | Criação do documento de requisitos de produto | [Gustavo Melo](https://github.com/gusrberto) |  |