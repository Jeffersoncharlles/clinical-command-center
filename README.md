# Clinical Command Center

> Protótipo front-end de alta fidelidade para explorar experiências digitais em operações de saúde.

[English version](README.en.md)

> [!IMPORTANT]
> Este é um projeto demonstrativo, construído exclusivamente com dados fictícios. Não se destina a uso clínico ou operacional.

**Deploy.**
[Deploy-crinical-command](https://crinical-command.vercel.app/)

> [!WARNING]
> Todas as rotas estão acessíveis livremente, pois este protótipo não possui autenticação, autorização ou verificação de papéis de acesso. Ao abrir a aplicação, o redirecionamento padrão leva à recepção (`/clinical-reception`).

| Rota | Área |
| --- | --- |
| [`/public`](https://crinical-command.vercel.app/public) | Painel público para acompanhar a chamada de pacientes. |
| [`/clinical-reception`](https://crinical-command.vercel.app/clinical-reception) | Painel da recepção e rota padrão da aplicação. |
| [`/clinical-nurses`](https://crinical-command.vercel.app/clinical-nurses) | Painel de triagem da enfermagem. |
| [`/clinical-doctor`](https://crinical-command.vercel.app/clinical-doctor) | Painel de atendimento médico. |

![Painel demonstrativo da recepção em tema escuro, com indicadores, salas e visão dos atendimentos](screen/clinical-reception.png)

## Visão geral

O **Clinical Command Center** investiga como interfaces densas e sensíveis ao contexto podem apoiar diferentes jornadas dentro de uma mesma experiência digital. O projeto combina visão operacional, acompanhamento público anonimizado e espaços de trabalho especializados em uma linguagem visual consistente.

Mais do que reproduzir um dashboard, a proposta trabalha desafios comuns em produtos complexos:

- transformar grande volume de informação em uma hierarquia visual compreensível;
- equilibrar densidade, legibilidade e velocidade de consulta;
- adaptar a experiência a diferentes contextos de uso;
- comunicar carregamento, conexão, erro e desatualização com transparência;
- preservar a privacidade entre experiências públicas e internas;
- manter consistência entre temas claro e escuro e diferentes tamanhos de tela.

## Destaques técnicos

- cinco experiências operacionais compartilhando o mesmo design system;
- organização por domínio e composição de páginas;
- dados remotos gerenciados com React Query;
- APIs e sincronização em tempo real simuladas com MSW;
- contratos públicos anonimizados na fronteira dos dados;
- carregamento sob demanda das principais experiências;
- estados de erro, reconexão e desatualização;
- testes comportamentais e acessibilidade orientada por semântica.

## Experiências demonstradas

| Experiência | Abordagem |
| --- | --- |
| **Acesso público** | Acompanhamento anonimizado com indicação de sincronização, conexão e última atualização. |
| **Recepção** | Visão operacional que reúne indicadores, ocupação, movimentação e contexto dos atendimentos. |
| **Pacientes** | Consulta demonstrativa com busca, filtros, seleção e informações fictícias organizadas. |
| **Enfermagem** | Espaço de trabalho informativo que prioriza contexto, registro explícito e continuidade visual. |
| **Médico** | Painel orientado à fila e ao atendimento atual, com ações demonstrativas e feedback imediato. |

As experiências utilizam dados locais e serviços simulados. Nenhuma alteração representa persistência clínica real.

## Galeria

### Acesso público

![Experiência pública em tema escuro, apresentando informações anonimizadas e estado de sincronização](screen/public-access.png)

Uma interface pública independente, desenhada para comunicar andamento e disponibilidade sem compartilhar informações identificáveis.

### Recepção

![Painel da recepção em tema escuro, com indicadores operacionais, salas e atendimentos](screen/clinical-reception.png)

Uma visão panorâmica para leitura rápida do ambiente, com detalhes apresentados sem interromper o contexto principal.

### Enfermagem

![Espaço de trabalho demonstrativo de enfermagem em tema escuro, com informações organizadas por contexto](screen/clinical-nurses.png)

Uma composição orientada à continuidade, com blocos independentes e uma hierarquia visual que reduz a competição entre informações.

### Médico

![Painel médico demonstrativo em tema escuro, com atendimento atual, indicadores e fila](screen/clinical-doctor.png)

Uma experiência focada no atendimento atual e no próximo passo, preservando a visão da fila e o acesso às ações principais.

> As capturas atuais apresentam o tema escuro. A galeria será ampliada com comparações em tema claro e diferentes tamanhos de tela.

## Abordagem de UX e UI

### Cockpit operacional

A interface adota uma linguagem de cockpit: informações essenciais permanecem visíveis, áreas secundárias complementam o contexto e ações recebem destaque proporcional à sua importância. O objetivo é oferecer densidade sem transformar todos os elementos em superfícies concorrentes.

### Hierarquia antes da decoração

Cor, tipografia, espaçamento, ícones e superfícies trabalham juntos para indicar prioridade. Estados nunca dependem somente de cor, e efeitos visuais são usados para estruturar o espaço, não apenas para ornamentação.

### Temas claro e escuro como um único sistema

Os temas compartilham componentes e semântica. A aparência é controlada por tokens, permitindo alterar contraste, superfícies, textos e estados sem duplicar a estrutura das telas.

### Responsividade orientada ao conteúdo

Os espaços de trabalho reorganizam navegação, grids, tabelas e painéis laterais conforme o espaço disponível. Em telas menores, a prioridade passa a ser leitura sequencial, controles acessíveis e preservação do contexto.

## Arquitetura conceitual

O projeto foi organizado em camadas de responsabilidade, mantendo a experiência visual separada do comportamento e das fronteiras de dados:

**Rotas → páginas de composição → domínios → componentes compartilhados → primitivas de interface → tema e infraestrutura**

Os principais princípios adotados foram:

- organização por domínio, mantendo cada jornada independente e compreensível;
- páginas pequenas, responsáveis apenas por compor a experiência;
- componentes com responsabilidade visual ou operacional bem definida;
- estado mantido próximo de quem realmente o utiliza;
- acesso a dados fora dos componentes de apresentação;
- primitivas reutilizáveis sem conhecimento do contexto clínico;
- uma única fonte de tokens para temas, espaçamento, tipografia e estados.

## Sincronização simulada

A experiência pública demonstra uma fronteira próxima de uma aplicação conectada:

- uma fotografia inicial é carregada por HTTP;
- eventos em tempo real sinalizam novas atualizações;
- versões evitam que uma informação anterior substitua uma mais recente;
- reconexão, indisponibilidade e dados potencialmente desatualizados são apresentados ao usuário;
- requisições e conexões são encerradas quando deixam de ser necessárias.

Toda essa camada é simulada com **Mock Service Worker (MSW)**. Ela existe para demonstrar estados e contratos de interface, não para representar uma infraestrutura hospitalar real.

## Qualidade e acessibilidade

- testes comportamentais para componentes, jornadas e serviços simulados;
- consultas e interações orientadas por nomes e papéis acessíveis;
- foco visível e navegação por teclado nos controles principais;
- anúncios para carregamento, sincronização e retorno de ações;
- alternativas textuais para visualizações de dados;
- suporte à preferência por movimento reduzido;
- estruturas de carregamento específicas para cada experiência;
- carregamento sob demanda das principais áreas;
- teste dedicado à anonimização da resposta pública.

Essas práticas demonstram uma abordagem consciente de acessibilidade, mas não equivalem a uma certificação formal de conformidade.

## Privacidade por design

A experiência pública não recebe o mesmo conjunto de informações usado nas áreas internas demonstrativas. A anonimização acontece na fronteira dos dados, e não apenas por ocultação visual.

As áreas internas utilizam somente dados fictícios e deixam explícito quando uma ação altera apenas o estado local da demonstração. O protótipo não possui autenticação, autorização, auditoria ou garantias de segurança de produção.

## Tecnologias

| Área | Tecnologias |
| --- | --- |
| Interface | React, TypeScript e React Router |
| Build | Vite |
| Estilos e temas | styled-components |
| Dados e cache | TanStack React Query |
| Visualização | Recharts |
| Ícones e primitivas | Lucide React e Base UI |
| Simulação de APIs | Mock Service Worker |
| Testes | Vitest e Testing Library |
| Qualidade | Biome e TypeScript |

## Estado atual

**Disponível na demonstração**

- cinco experiências visuais conectadas pelo mesmo design system;
- temas claro e escuro;
- busca, filtros, seleção e ações locais demonstrativas;
- carregamento progressivo e estados explícitos;
- sincronização pública simulada;
- cobertura comportamental das principais jornadas.

**Fora do escopo atual**

- backend e banco de dados reais;
- autenticação, autorização e controle de acesso;
- persistência de informações clínicas;
- prontuário eletrônico completo;
- trilha de auditoria;
- integração com sistemas hospitalares;
- validação para uso clínico ou produção.


## Sobre este repositório

Este repositório foi criado como uma apresentação técnica e visual do projeto, destacando sua arquitetura, experiência do usuário e decisões de design.

O código-fonte é mantido privado intencionalmente e não está disponível publicamente no momento.


## Demonstração

https://crinical-command.vercel.app/
