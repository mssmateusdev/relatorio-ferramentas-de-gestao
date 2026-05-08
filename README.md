# OpenProject 

<img width="2599" height="1528" alt="Pasted image 20260507152232" src="https://github.com/user-attachments/assets/124dbd76-4869-45eb-b059-944fb50ebec0" />

## Relatório Técnico:

### Visão Geral

O OpenProject é um sistema de gestão de projetos de código aberto com forte apelo corporativo. Ele se diferencia por tentar unir o mundo do rastreamento de bugs técnico com a gestão de portfólio de projetos de alto nível.

| Tecnologia              | Descrição                                                                        |
| ----------------------- | -------------------------------------------------------------------------------- |
| **Backend**             | Desenvolvido em Ruby on Rails.                                                   |
| **Frontend**            | Construído em Angular.                                                           |
| **Banco de Dados**      | Requer exclusivamente **PostgreSQL**                                             |
| **Integrações Nativas** | Suporte robusto para integração via API REST (muito bem documentada) e Webhooks. |

### Capacidade de Bug Tracking

No OpenProject, tudo (bugs, tarefas, épicos, features) é tratado como um **Pacote de Trabalho (Work Package)**.

- **Rastreamento de Bugs:** pode criar um tipo específico de pacote chamado "Bug" e associar a fluxos de trabalho (workflows) restrito a ele. Por exemplo, um bug só pode ser movido "Em Teste" para "Fechado por um usuário com o papel de "QA".
- **Campos Personalizados e Relacionamentos:** é possível criar relações complexas entre bugs, como "Bloqueia", "Duplica", "Relacionado a" ou "Precede". Isso é vital em migrações de sistemas ou refatorações complexas onde um erro de banco de dados bloqueia uma tarefa de frontend.
- **Histórico e Auditoria:** cada pacote de trabalho possui uma trilha de auditoria imutável. Qualquer alteração de status, prioridade ou comentário fica registrada com data, hora e autor.
- **Controle de Versão**: integra-se com repositórios Git, permitindo que commits fechem bugs automaticamente se a sintaxe correta for usada na mensagem do commit.

### Gestão Visual e Produtividade

- **Gráficos de Gantt Interativos:** é um dos pontos mais fortes da ferramenta. O cronograma é gerado automaticamente com base nos _Work Packages_ e permite arrastar e soltar dependências diretamente na interface web.
- **Visões Ágeis (Kanban):** Permite a criação de quadros visuais para gerenciar o fluxo de correção de bugs. **Obs:** os quadros ágeis mais avançados (com múltiplos projetos no mesmo quadro) são limitados à versão paga (Enterprise).

### Eficiência, Consumo de Recursos e Infraestrutura

Considerando a otimização de infraestrutura, a OpenProject não é uma aplicação leve.
- **Consumo de RAM:** A combinação do servidor de aplicação Ruby (Puma) com os workers de background (Sidekiq) e o banco PostgreSQL exige uma quantidade considerável de memória. A recomendação mínima oficial é de **4 GB de RAM**, mas para um ambiente de produção estável, **8 GB de RAM** é o cenário ideal. Em máquinas locais ou servidores com recursos limitados, ele pode sofrer com gargalos de memória (_Out of Memory_).
- **Deploy:** A via mais eficiente e recomendada para deploy, inclusive para testes locais rodando sob o Windows 10 via terminal do **Ubuntu (WSL)**, é utilizando as imagens oficiais do **Docker**. Há um repositório oficial com o `docker-compose.yml` que provisiona o banco, a aplicação e o proxy reverso de forma automatizada.

### Modelo de Licenciamento

A versão _Community_ é 100% open-source e gratuita, mas o OpenProject utiliza um modelo de _open-core_. Isso significa que funcionalidades muito visadas por equipes de desenvolvimento estão restritas à versão _Enterprise_ (paga por usuário), tais como:
- Integração com Single Sign-On (SAML/OpenID).
- Quadros Ágeis (Boards) avançados.
- Campos personalizados de texto formatado e multiseleção avançada.
- Gráficos e relatórios de métricas avançadas.

### Veredito Técnico

> [!SUCCESS]  **Prós:**
> - Frontend moderno e responsivo.
> - Mecanismo de fluxo de trabalho (workflows) extremamente poderoso e customizável para controle de qualidade rigoroso.
> - Excelente para quem precisa de gráficos de Gantt e controle de dependências entre tarefas complexas.

>[!WARNING] **Contras:**
> - Alto consumo de memória RAM, não sendo ideal para servidores pequenos ou instâncias de baixo custo.
> - Alguns recursos ágeis essenciais bloqueados pelo licenciamento _Enterprise_.

[Site do OpenProject](https://www.openproject.org/)
[Documentação do OpenProject](https://www.openproject.org/docs/getting-started/)

___

# Bugzilla

<img width="614" height="391" alt="Pasted image 20260507155520" src="https://github.com/user-attachments/assets/a1d1d4c9-932d-48bd-9d11-ac500b62254c" />


## Relatório Técnico:

### Visão Geral

Criado originalmente pela Fundação Mozilla em 1998, o Bugzilla é o "avô" dos rastreadores de bugs modernos. Ele foi projetado para projetos de software de escala global (como o próprio Firefox e o Kernel do Linux) e seu foco é estrito e purista: relatar, rastrear e resolver falhas de software.

| Tecnologia         | Descrição                                                                                                                                                                                                    |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Backend**        | Desenvolvido inteiramente em **Perl**.                                                                                                                                                                       |
| **Frontend**       | Baseado em templates CGI clássicos (HTML puro, com pouquíssimo ou nenhum JavaScript moderno).                                                                                                                |
| **Banco de Dados** | Suporta nativamente MySQL/MariaDB (o mais utilizado e otimizado), PostgreSQL e até mesmo **Oracle** (o que o torna viável em ambientes de TI governamentais ou tribunais que possuem bases legadas pesadas). |
| **Arquitetura**    | Não é uma Single Page Application (SPA). Cada clique ou submissão de formulário recarrega a página.                                                                                                          |

### Capacidade de Bug Tracking

Se o OpenProject tenta ser um canivete suíço de gestão, o Bugzilla é um bisturi. Ele não trata "tarefas gerais", ele trata _bugs_.

- **Rastreamento Granular:** A ferramenta brilha para desenvolvedores que lidam com baixo nível, compilação de sistemas operacionais ou configurações de hardware. Campos nativos obrigatórios incluem "Hardware", "Sistema Operacional", "Versão", "Severidade" e "Prioridade".
- **Prevenção de Duplicatas:** Possui um dos melhores algoritmos nativos para sugerir bugs semelhantes enquanto o usuário digita o título do novo ticket, evitando a poluição do banco de dados com problemas repetidos.
- **Busca Avançada (Advanced Search):** É incomparável. Permite construir queries booleanas incrivelmente complexas (ex: "Mostre todos os bugs relacionados ao componente X, que bloquearam o componente Y, relatados nos últimos 30 dias, mas que não tiveram resposta do desenvolvedor Z").
- **Controle de Acesso por Módulo:** A segurança é levada ao extremo. Você pode configurar grupos para isolar completamente a visibilidade de determinados bugs confidenciais (por exemplo, falhas de segurança zero-day).

### Gestão Visual e Produtividade

- **Zero Foco em Ágil:** Não existem quadros Kanban, gráficos de Gantt, Sprints ou Épicos nativos. O Bugzilla é baseado estritamente em listas densas de texto e tabelas.
- **Interface Datada:** A interface web tem aparência dos anos 2000. Embora a navegação seja extremamente rápida devido à falta de scripts pesados, ela não é amigável para usuários não-técnicos.
- **Dependências entre Bugs:** Apesar da falta de visualização gráfica, a gestão de dependências ("Bug A depende do Bug B") é tratada de forma muito eficiente via links diretos nas tabelas, gerando árvores de dependência em formato de texto.

### Eficiência, Consumo de Recursos e Infraestrutura

- **Consumo de RAM:** Extremamente baixo. Ao contrário de stacks modernas em Java ou Ruby que exigem gigabytes de memória, um servidor Bugzilla pode rodar fluidamente com **1 GB ou 2 GB de RAM** para equipes médias. Os scripts CGI só consomem recursos ativamente durante o processamento da requisição HTTP.
- **Deploy e Configuração:** A instalação é o maior ponto de atrito. Por ser baseado em Perl, ele não possui a elegância de um binário único ou a mesma tração moderna em containers.
    - Em um ambiente Windows 10 rodando terminal **Ubuntu (WSL)**, você precisará usar o gerenciador do Perl (CPAN) para compilar dezenas de módulos nativos (como `Template-Toolkit`, `DBD::mysql` ou `DBD::Pg`), o que muitas vezes exige bibliotecas C/C++ instaladas no sistema (`build-essential`).
    - Existem imagens Docker, mas elas geralmente são mantidas pela comunidade e exigem mais ajustes manuais no arquivo `localconfig` do que soluções _plug-and-play_ modernas.


### O Modelo de Licenciamento

- **100% Open Source:** Licenciado sob a Mozilla Public License (MPL).
- **Sem Paywall:** Não existe versão "Enterprise" ou recursos bloqueados. Tudo o que a ferramenta oferece está disponível gratuitamente para toda a equipe.

### Veredito Técnico 

> [!SUCCESS] **Prós:**
> 
> - **Consumo de recursos minúsculo:** Ideal para servidores modestos ou para rodar localmente sem comprometer a memória da máquina.
> - **Motor de busca imbatível:** Ferramenta definitiva para rastrear milhares de tickets técnicos sem se perder.
> - **Estabilidade a longo prazo:** Uma vez configurado, raramente quebra.

> [!warning] **Contras:**
> 
> - **Instalação dolorosa:** A gestão de dependências Perl (CPAN) pode ser frustrante para quem está acostumado com ferramentas mais modernas.
> - **UX/UI obsoleta:** Afasta equipes multidisciplinares (designers, gerentes de produto, etc.), restringindo a adoção apenas a perfis altamente técnicos.
> - **Falta de recursos visuais:** Inviável se a equipe quiser adotar metodologias ágeis ou acompanhamento via quadros.

[Site do Bugzilla](https://www.bugzilla.org/)
[Documentação do Bugzilla](https://www.bugzilla.org/docs/)

___

# Linear

<img width="1408" height="719" alt="Pasted image 20260507163335" src="https://github.com/user-attachments/assets/afe04b89-d74d-40ed-97f3-e8a4aada90a3" />

## Relatório Técnico:

### Visão Geral e Arquitetura

O Linear não tenta ser uma ferramenta genérica para todas as áreas da empresa. Ele é **altamente opinativo** (tem um jeito "certo" de ser usado) e construído estritamente para equipes de engenharia de software e produto de alto desempenho.
- **Arquitetura Local-First (Sincronização):** Este é o grande diferencial técnico. O cliente (web ou desktop) baixa os dados e cria um banco de dados local na máquina. As alterações são feitas instantaneamente no cliente e sincronizadas em segundo plano via uma API **GraphQL** robusta. Isso significa que não há _loading screens_ ou esperas entre cliques.
- **Stack:** Construído com React, TypeScript e Node.js no backend.
- **Infraestrutura:** É estritamente **SaaS (Cloud)**. Diferente do Bugzilla ou OpenProject, você não pode baixar o código e hospedar no seu servidor.

### Capacidade de Bug Tracking

O Linear trata bugs e tarefas como **Issues**, mas remove toda a burocracia desnecessária.

- **Integração Profunda com Git:** A conexão com GitHub e GitLab é nativa e perfeita. Se você criar uma _branch_ baseada no ID da tarefa (ex: `LIN-123-fix-login`), o Linear rastreia os commits automaticamente. Quando o Pull Request é mesclado (_merged_), a tarefa é fechada automaticamente no quadro.
- **Editor Markdown Nativo:** As descrições de tarefas e comentários suportam Markdown avançado nativamente. É possível colar blocos de código formatados com facilidade, algo excelente para documentar logs de erro em Java ou Python sem quebrar a formatação.
- **Triagem (Triage):** Possui uma caixa de entrada (Inbox) dedicada. Bugs relatados por usuários externos (via integrações com Sentry ou Zendesk) ou criados rapidamente caem na Triagem, onde o líder técnico avalia, categoriza e coloca no fluxo de desenvolvimento.

### Gestão Visual e Produtividade

O Linear foi desenhado para que o desenvolvedor nunca precise usar o mouse se não quiser.
- **Menu de Comando (Ctrl+K):** Inspirado em editores de código modernos, você pressiona um atalho de teclado e digita o que quer fazer: "Criar bug", "Mudar para Em Progresso", "Atribuir a mim". A navegação é ultrarrápida.
- **Ciclos (Cycles) em vez de Sprints:** O Linear não usa o termo "Sprint" para evitar a bagagem burocrática do Scrum tradicional. Ele usa "Ciclos", que são períodos fixos (geralmente de 1 a 3 semanas) onde a equipe se compromete com um escopo de trabalho. O progresso gera gráficos de queima (burn-up/burn-down) automaticamente.
- **Design Minimalista:** A interface é predominantemente focada em um "Dark Mode" belíssimo e limpo. Não há poluição visual.

### Eficiência, Consumo de Recursos e Infraestrutura

Por ser um SaaS, a responsabilidade de infraestrutura é transferida para a empresa criadora da ferramenta.

- **Zero Manutenção:** Você não precisa se preocupar com consumo de RAM, instalação de dependências no WSL (Ubuntu), manutenção de banco de dados PostgreSQL ou atualizações de versão.
- **Aplicativo Desktop Leve:** Eles oferecem um aplicativo para Windows e macOS que roda muito bem e consome poucos recursos em comparação com ferramentas corporativas mais pesadas baseadas na web, operando de forma muito fluida no Windows 10.
- **API Preditiva e Webhooks:** Excelente para criar automações personalizadas. Se você precisar disparar scripts externos quando um bug crítico for reportado, os webhooks do Linear têm baixíssima latência.

### Modelo de Licensiamento (SaaS)

- **Plano Gratuito (Free Tier):** É bastante generoso para projetos pessoais, portfólios ou startups iniciais. Permite usuários ilimitados, mas limita o histórico a **250 _issues_ ativas** (tarefas não arquivadas).
- **Planos Pagos:** O modelo é baseado em assinatura mensal por usuário (em dólares), o que pode se tornar inviável financeiramente para o setor público ou projetos independentes sem orçamento em moeda estrangeira.

### Veredito Técnico

> [!SUCCESS] **Prós:**
> 
> - **Velocidade Absurda:** A sincronização _local-first_ faz com que seja a ferramenta mais rápida do mercado.
> - **Foco no Desenvolvedor:** Atalhos de teclado avançados e integrações automáticas com repositórios de código reduzem o atrito no dia a dia.
> - **Design e UX Impecáveis:** Estimula o uso da ferramenta ao invés de torná-la uma obrigação chata.

> [!warning] **Contras:**
> - **Dependência da Nuvem (SaaS):** Sem possibilidade de hospedagem própria, o que pode esbarrar em regras de conformidade de dados governamentais ou de segurança estrita.
> -  **Preço Escalonável:** O plano gratuito tem um teto rígido de tarefas, e as licenças pagas são cobradas em dólar.
> - **Pouca Flexibilidade Geral:** Se a equipe quiser usar uma metodologia que fuja dos padrões pré-definidos pelo Linear, a ferramenta simplesmente não se adapta; ela força você a trabalhar do jeito "deles".

[Site do Linear](https://linear.app/)
[Documentação do Linear](https://linear.app/docs)

___

# Comparação das Ferramentas de Gestão de Projetos


### Quadro Comparativo Direto

|**Recurso / Ferramenta**|**OpenProject**|**Bugzilla**|**Linear**|
|---|---|---|---|
|**Filosofia Principal**|Gestão de Projetos e Ágil Corporativo|Rastreamento de Bugs Purista|Engenharia de Alta Velocidade|
|**Hospedagem**|Self-hosted (Seu servidor) ou Cloud|Apenas Self-hosted|Apenas SaaS (Cloud)|
|**Stack Base**|Ruby on Rails + Angular + Postgres|Perl + CGI + MySQL/Oracle/Postgres|Node.js + React + GraphQL|
|**Consumo de Infra**|Alto (Requer ~4GB+ de RAM)|Muito Baixo (~1GB de RAM)|Zero (Nuvem / App nativo leve)|
|**Interface / UX**|Moderna e rica em gráficos|Datada (Anos 2000), baseada em texto|Minimalista, modo escuro, focada em teclado|
|**Integração com Código**|Boa (via commits e webhooks)|Básica / Manual|Excelente (Sincronização nativa Git)|
|**Custo**|Grátis (Core) / Pago (Enterprise)|100% Grátis|Grátis (Limitado) / Assinatura em Dólar|

