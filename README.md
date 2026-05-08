# OpenProject

## Relatório Técnico

### Visão Geral

O OpenProject é um sistema de gestão de projetos de código aberto com forte apelo corporativo. Ele se diferencia por tentar unir o mundo do rastreamento de bugs técnico com a gestão de portfólio de projetos de alto nível.

|**Tecnologia**|**Descrição**|
|---|---|
|**Backend**|Desenvolvido em Ruby on Rails.|
|**Frontend**|Construído em Angular.|
|**Banco de Dados**|Requer exclusivamente **PostgreSQL**.|
|**Integrações Nativas**|Suporte robusto para integração via API REST e Webhooks.|

### Capacidade de Bug Tracking

No OpenProject, tudo (bugs, tarefas, épicos, features) é tratado como um **Pacote de Trabalho (Work Package)**.

- **Rastreamento de Bugs:** Permite criar fluxos de trabalho (workflows) restritos, como exigir que um bug seja fechado apenas por usuários com papel de "QA".
    
- **Campos Personalizados e Relacionamentos:** Possibilidade de criar relações complexas como "Bloqueia", "Duplica" ou "Precede".
    
- **Histórico e Auditoria:** Possui uma trilha imutável com registro de data, hora e autor para cada alteração.
    
- **Controle de Versão:** Integração com Git para fechamento automático de bugs via mensagens de commit.
    

### Eficiência e Infraestrutura

- **Consumo de RAM:** Exige no mínimo **4 GB de RAM**, sendo **8 GB** o ideal para produção.
    
- **Deploy:** Recomendado via **Docker**, funcionando bem no Windows 10 via **WSL (Ubuntu)**.
    

### Veredito Técnico

> [!TIP]
> 
> **Prós:**
> 
> - Frontend moderno e responsivo.
>     
> - Mecanismo de fluxo de trabalho (workflows) extremamente poderoso e customizável.
>     
> - Excelente para gráficos de Gantt e controle de dependências complexas.
>     

> [!WARNING]
> 
> **Contras:**
> 
> - Alto consumo de memória RAM.
>     
> - Recursos ágeis avançados (como quadros multiplataforma) restritos ao licenciamento _Enterprise_.
>     

---

# Bugzilla

## Relatório Técnico

### Visão Geral

Criado pela Fundação Mozilla, o Bugzilla é focado estritamente em relatar, rastrear e resolver falhas de software.

|**Tecnologia**|**Descrição**|
|---|---|
|**Backend**|Desenvolvido inteiramente em **Perl**.|
|**Frontend**|Baseado em templates CGI clássicos (HTML puro).|
|**Banco de Dados**|Suporta MySQL/MariaDB, PostgreSQL e **Oracle**.|
|**Arquitetura**|Não é uma SPA; cada clique recarrega a página.|

### Capacidade de Bug Tracking

- **Rastreamento Granular:** Campos nativos para Hardware, Sistema Operacional e Severidade.
    
- **Prevenção de Duplicatas:** Algoritmo nativo que sugere bugs semelhantes durante a digitação do título.
    
- **Busca Avançada:** Permite construções booleanas complexas para encontrar tickets específicos.
    

### Eficiência e Infraestrutura

- **Consumo de RAM:** Extremamente baixo, rodando com **1 GB ou 2 GB de RAM**.
    
- **Deploy:** Instalação manual complexa via CPAN (Perl), especialmente no **WSL**.
    

### Veredito Técnico

> [!TIP]
> 
> **Prós:**
> 
> - Consumo de recursos minúsculo.
>     
> - Motor de busca imbatível para milhares de tickets.
>     
> - Alta estabilidade a longo prazo.
>     

> [!WARNING]
> 
> **Contras:**
> 
> - Instalação e gestão de dependências Perl (CPAN) trabalhosa.
>     
> - UX/UI obsoleta que pode afastar membros não-técnicos da equipe.
>     
> - Falta total de recursos visuais como quadros Kanban nativos.
>     

---

# Linear

## Relatório Técnico

### Visão Geral

Ferramenta **SaaS (Cloud)** altamente opinativa, construída para equipes de engenharia de alta performance. Utiliza uma arquitetura **Local-First**, onde os dados são sincronizados em segundo plano via **GraphQL**.

### Capacidade de Bug Tracking

- **Integração com Git:** Rastreamento automático de commits e fechamento de issues via Pull Requests.
    
- **Editor Markdown:** Suporte nativo para blocos de código formatados.
    
- **Triagem (Triage):** Caixa de entrada dedicada para avaliar e categorizar bugs rapidamente.
    

### Gestão Visual e Produtividade

- **Menu de Comando (Ctrl+K):** Navegação e execução de ações inteiramente via teclado.
    
- **Ciclos (Cycles):** Alternativa aos Sprints tradicionais com foco em escopo fixo e fluidez.
    

### Veredito Técnico

> [!TIP]
> 
> **Prós:**
> 
> - Velocidade absurda devido à sincronização local.
>     
> - Foco total na experiência do desenvolvedor (DX).
>     
> - Design e UX minimalistas e impecáveis.
>     

> [!WARNING]
> 
> **Contras:**
> 
> - Dependência total da nuvem (sem opção de self-hosting).
>     
> - Preço escalonável em dólar e teto rígido de issues no plano gratuito.
>     
> - Pouca flexibilidade para metodologias que fogem do padrão da ferramenta.
>     

---

### Quadro Comparativo Direto

|**Recurso**|**OpenProject**|**Bugzilla**|**Linear**|
|---|---|---|---|
|**Hospedagem**|Self-hosted ou Cloud|Apenas Self-hosted|Apenas SaaS|
|**RAM**|Alta (~4GB+)|Muito Baixa (~1GB)|Zero (Nuvem)|
|**Interface**|Moderna/Rica|Datada/Texto|Minimalista/Dark|
|**Custo**|Grátis/Pago|100% Grátis|Grátis/Assinatura ($)|
