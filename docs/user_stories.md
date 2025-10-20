# User Stories

## Personas

**Usuário**: Representa o público geral da plataforma — qualquer pessoa interessada em acessar e aprender com os resumos simplificados dos artigos científicos. Busca ter uma experiência personalizada conforme seu perfil (Estudante, Educador ou Entusiasta), com acesso fácil a conteúdo atualizado e compreensível.

**Estudante**: Aluno de graduação ou pós-graduação em ciência da computação (ou áreas relacionadas) que busca compreender tendências atuais sem enfrentar barreiras técnicas excessivas. Procura entender o essencial das pesquisas recentes e ampliar seu conhecimento de forma prática e acessível.

**Educador**: Professor universitário ou instrutor que deseja incorporar novidades da pesquisa científica em suas aulas e manter-se atualizado sobre o estado da arte. Deseja encontrar rapidamente resumos confiáveis e relevantes para utilizar em suas práticas de ensino.

**Entusiasta (Leigo)**: Pessoa curiosa e interessada em ciência e tecnologia, mas sem formação técnica formal na área. Quer aprender de forma acessível e confiável, buscando compreender os avanços da computação sem precisar enfrentar jargões técnicos ou paywalls.

---

### US1 — Cadastro e seleção de perfil

**Persona:** Usuário

**Descrição:** Como novo usuário, quero me cadastrar na plataforma e escolher meu perfil de interesse (Estudante, Educador ou Leigo/Entusiasta), para que o conteúdo seja apresentado de forma adequada às minhas necessidades.

**Critérios de Aceitação:**

* Há um botão claro “Cadastrar” em qualquer página.
* No formulário de cadastro, o usuário escolhe seu perfil ("Estudante", "Educador" ou "Entusiasta").
* A plataforma exibe uma mensagem de boas-vindas e mostra resumos conforme o perfil escolhido.
* O usuário pode alterar o perfil a qualquer momento em “Meu Perfil”.

---

### US2 — Resumos em linguagem simples (Estudante)

**Persona:** Estudante

**Descrição:** Como estudante de computação, quero ler resumos de artigos recentes em linguagem simples, para entender tendências atuais da minha área sem me sentir sobrecarregado.

**Critérios de Aceitação:**

* Na página inicial, o usuário vê uma lista de artigos da última semana.
* Ao abrir um artigo, o texto utiliza analogias e explica termos complexos.
* Após ler o resumo, o usuário consegue explicar a ideia principal a um colega.

---

### US3 — Acesso rápido para Educadores

**Persona:** Educador

**Descrição:** Como professor, quero ter acesso rápido a resumos de pesquisas de ponta, para incorporar novidades em minhas aulas.

**Critérios de Aceitação:**

* No resumo há um link visível para o artigo original em PDF no arXiv.
* É possível buscar artigos por tópico (ex.: “redes neurais convolucionais”).

---

### US4 — Fonte confiável para Entusiastas

**Persona:** Entusiasta (Leigo)

**Descrição:** Como entusiasta, quero uma fonte confiável para aprender sobre avanços da computação, para satisfazer minha curiosidade sem depender de mídias superficiais.

**Critérios de Aceitação:**

* Ao ler um artigo, o usuário compreende o “porquê” e o “como” da tecnologia, não apenas “o que” ela faz.
* Após terminar o resumo, o usuário tem contexto suficiente para decidir se quer ler o artigo completo.

---

### US5 — Busca por título/autor/palavra-chave

**Persona:** Usuário

**Descrição:** Como usuário, quero poder buscar artigos por título, autor ou palavra-chave, para encontrar rapidamente os temas que me interessam.

**Critérios de Aceitação:**

* Há um campo de busca na página inicial.
* Ao digitar um termo, aparecem resultados relevantes com título, autores e resumo simplificado.
* Se não houver resultados, o sistema exibe “Nenhum artigo encontrado”.

---

### US6 — Página de detalhe do artigo

**Persona:** Usuário

**Descrição:** Como usuário, quero acessar uma página de detalhes de um artigo, para ler o texto simplificado completo e visitar a fonte original no arXiv.

**Critérios de Aceitação:**

* Ao clicar em um artigo da lista, o usuário é levado à página de detalhe.
* A página mostra o texto completo, autores, data e link para o artigo original.
* É fácil voltar para a lista de artigos.

---

### US7 — Newsletter semanal por e-mail

**Persona:** Usuário

**Descrição:** Como usuário, quero receber um e-mail semanal com os principais artigos simplificados, para me manter atualizado mesmo sem visitar o site.

**Critérios de Aceitação:**

* Usuário logado pode ativar/desativar a newsletter nas configurações.
* O usuário recebe o e-mail semanal com títulos, resumos e links.
* O e-mail é legível e responsivo em dispositivos móveis.

---

### US8 — Ajuste do nível de simplificação

**Persona:** Estudante / Entusiasta

**Descrição:** Como leitor, quero ajustar o nível de simplificação dos textos (básico, intermediário), para que o conteúdo seja adequado ao meu conhecimento.

**Critérios de Aceitação:**

* Em cada artigo há uma opção para alterar o nível de explicação.
* Ao alterar o nível, o texto se adapta automaticamente.
* A plataforma lembra a preferência do usuário para acessos futuros.


## Histórico de Versões

| Versão | Data | Descrição | Autores | Revisores |
| --- | --- | --- | --- | --- |
| `1.0`  | 19/10/2025 | Criação do documento de histórias de usuário | [Gustavo Melo](https://github.com/gusrberto) |  |
| `1.1` | 20/10/2025 | Organiza arquivos de USs e Backlog | [Bruno Martins](https://github.com/brunomartins03) |  