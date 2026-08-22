---
status: raw input
date: 2026-08-16
version: 1.0
language: pt-BR
note: Raw research input, kept verbatim. Not project documentation.
      English synthesis: docs/discovery/market-pain-research.md
---

# Pesquisa de Mercado: Dores, Pedidos de Feature e Bugs Recorrentes em Softwares de PKMS

**Objetivo:** mapear as maiores frustrações dos usuários de ferramentas de Personal Knowledge Management (PKMS), as features mais pedidas e os bugs/erros mais recorrentes, como insumo para o desenvolvimento de um novo aplicativo nesse espaço.

**Metodologia e nota sobre fontes:** a pesquisa combinou buscas na web, fóruns oficiais (Obsidian, Logseq, RemNote), GitHub Issues de projetos open-source (Joplin, AppFlowy, Logseq), sites de review agregados (G2, Capterra, TrustPilot, Product Hunt, AlternativeTo, Shopify App Store quando aplicável) e artigos/blogs que sintetizam discussões do Reddit e comunidades de PKM. O acesso direto e em massa a threads do Reddit foi tecnicamente limitado neste ambiente (o motor de busca disponível não indexa bem URLs de reddit.com/r/.../comments no momento desta pesquisa), então o material foi triangulado com fóruns oficiais e issue trackers — que na prática contêm o mesmo tipo de reclamação, de forma mais estruturada e rastreável. Onde relevante, sinalizo a origem específica.

---

## 1. Panorama do mercado

O espaço de PKMS hoje é dividido em algumas famílias de produto, e isso já é a primeira fonte de frustração: **não existe consenso sobre o que uma ferramenta de PKM deveria ser**, e os usuários migram entre paradigmas constantemente.

| Categoria | Exemplos | Modelo mental |
|---|---|---|
| Markdown local-first / arquivos em disco | Obsidian, Logseq, Zettlr | "Meus dados são meus arquivos" |
| All-in-one workspace (blocos + banco de dados) | Notion, AppFlowy, Anytype | "Um Lego para organizar a vida" |
| Outliner / bullets diários | Logseq, Roam Research, Workflowy | "Penso em tópicos e blocos, não em páginas" |
| Estruturado por objetos/tags (não-hierárquico) | Tana, Anytype | "Supertags" e relações tipo banco de dados |
| Canvas espacial / visual | Heptabase, Capacities, Muse, Milanote | "Penso espacialmente, em quadros" |
| Aprendizado com repetição espaçada | RemNote, Anki-adjacent | "Notas viram flashcards" |
| Clássicos corporativos/legado | Evernote, OneNote | "Confiança histórica, mas estagnados" |
| Self-hosted / hierárquico clássico | Trilium/TriliumNext, Joplin | "Controle total, sem vendor lock-in" |

Essa fragmentação é, ela mesma, uma dor relatada constantemente: usuários descrevem um ciclo de "shiny object syndrome" — testar um app novo a cada poucos meses, nunca consolidar um sistema, e acabar com notas espalhadas em 5–10 ferramentas diferentes ao longo dos anos. Um usuário resumiu bem esse padrão dizendo que sua lista de apps testados incluía diário físico, rascunhos de e-mail, Word, Notas do Google, Apple Notes, Evernote, Notion e Roam Research — e que o resultado eram centenas de notas distribuídas em dezenas de lugares. Esse comportamento de troca constante é tão comum que virou tema recorrente em blogs de PKM ("Pick one, and stick to it", "PKM and dealing with 'ooh, shiny'").

---

## 2. Análise por ferramenta

### 2.1 Obsidian

**Perfil:** app proprietário, mas com dados em Markdown local; ~1 milhão de usuários estimados, comunidade no Reddit com ~94.600 membros (top 5% do Reddit em tamanho), ecossistema de mais de 2.000 plugins.

**Frustrações principais:**
- **Sincronização não é nativa e gratuita.** Obsidian Sync custa ~US$ 10/mês só para sincronizar arquivos de texto, o que gera revolta recorrente ("é só um monte de arquivos .md, por que pagar assinatura para isso?"). Isso gerou uma indústria paralela de soluções alternativas (Syncthing, plugins de sync via Google Drive, iCloud, OneDrive), cada uma com seus próprios problemas.
- **Conflito entre sync nativo e serviços de armazenamento em nuvem "sob demanda".** A própria documentação da Obsidian alerta que usar múltiplos serviços de sync ao mesmo tempo (ex.: Obsidian Sync + Dropbox) pode causar perda de dados e corrupção. Serviços como OneDrive com "Files On-Demand" fazem o Obsidian achar que arquivos foram deletados quando na verdade só foram removidos do cache local.
- **Plugins não-oficiais de sync são explicitamente instáveis.** O plugin de sync via Google Drive mais popular (usado como alternativa gratuita) traz avisos formais de "pode haver perda de dados, faça backup antes de instalar" em sua própria documentação — e ainda assim tem mais de 1.000 estrelas no GitHub, sinal de que a demanda por sync gratuito supera o medo do risco.
- **Falta de app mobile "de verdade" no passado** — resolvida parcialmente, mas ainda é citada como ponto fraco em comparações recentes de mercado.
- **Graph view não escala.** Vaults com milhares de notas (ex.: 6.000+) tornam a visualização em grafo lenta e "uma tarefa frustrante" — o recurso mais icônico do app (a visualização de conexões) para de funcionar bem exatamente quando o usuário mais precisaria dele (bases de conhecimento grandes e maduras).
- **Dependência de plugins da comunidade para funcionalidade básica.** Tabelas avançadas, bancos de dados dentro de notas (Dataview), templates dinâmicos (Templater) — tudo isso é plugin de terceiros, não nativo. Isso cria risco de abandono: um plugin crítico para o workflow de alguém pode parar de ser mantido a qualquer momento.

**Features mais pedidas:**
- Sync nativo, confiável e sem custo adicional (ou parte de um plano único razoável).
- Bancos de dados/tabelas relacionais nativos (hoje via Dataview, mas os usuários pedem isso "de fábrica").
- Melhor performance em vaults grandes (graph view, busca, indexação).
- Colaboração em tempo real (multiplayer) — ausente por design (app local-first single-user).

**Bugs/erros recorrentes:**
- Perda de anexos/renomeação inesperada de arquivos durante sync via plugins não-oficiais.
- Notas indo parar na pasta de "conflitos" sem motivo aparente após updates.
- Editor perdendo foco ao editar tabelas ou expressões LaTeX (bug conhecido e documentado em plugins de terceiros).

---

### 2.2 Notion

**Perfil:** all-in-one workspace, blocos + bancos de dados, cloud-first, +30 milhões de usuários.

**Frustrações principais (o tema nº 1, disparado, é performance/lentidão):**
- **Lentidão crônica**, especialmente em páginas grandes ou com muitos bancos de dados vinculados. A causa raiz, segundo análises técnicas, é que cada linha de conteúdo é um "bloco" separado com seus próprios metadados — uma página longa vira literalmente milhares de registros que o app precisa buscar e renderizar a cada carregamento.
- Limites técnicos duros e pouco visíveis: 250.000 linhas por banco de dados, 500 propriedades por banco, 2.5 MB de dados de propriedade por página — passado isso, novas alterações simplesmente **param de salvar**, sem aviso claro ao usuário até que ele perceba que perdeu trabalho.
- **App mobile inferior ao desktop** — citado repetidamente em reviews como "não tão fluido quanto a versão desktop", frustrante para quem quer fazer updates rápidos.
- **Modo offline muito limitado** — Notion depende fortemente de conexão com a internet; sem rede, a experiência degrada muito.
- Curva de aprendizado alta para montar um sistema "do jeito certo" — muitos usuários relatam meses configurando templates antes de sentir que o sistema "funciona".

**Features mais pedidas:**
- Performance real em workspaces grandes (não apenas otimizações incrementais).
- Modo offline completo e confiável.
- Paridade mobile-desktop.
- Transparência sobre limites técnicos antes que o usuário bata neles e perca conteúdo.

**Bugs/erros recorrentes:**
- Erros de "request body too large" no Notion AI mesmo com parágrafos curtos, travando a geração e fazendo o conteúdo gerado desaparecer.
- Lag perceptível ao rolar páginas com muitas imagens, embeds e bancos de dados vinculados em coluna.

---

### 2.3 Logseq

**Perfil:** outliner open-source, local-first, blocos como unidade central, referências bidirecionais em nível de bloco (não só de página).

**Frustrações principais:**
- **Degradação de performance conforme o grafo cresce** — é talvez o padrão mais bem documentado desta pesquisa (múltiplas threads longas no fórum oficial). Um usuário com apenas ~2.000 páginas e ~430 entradas de diário relatou 4 minutos para abrir o app num MacBook com SSD, e **10+ minutos** num iMac com HD tradicional — a ponto do app simplesmente parar de responder.
- **A "versão DB" (nova arquitetura em SQLite) está em beta/alpha e traz risco real de perda de dados** — a própria documentação oficial recomenda fazer backups automáticos ou manuais regulares porque "a perda de dados é possível". Isso é dito abertamente pelo próprio time, o que gera ansiedade em quem depende do app para conhecimento acumulado ao longo de anos.
- Ecossistema de plugins muito menor que o do Obsidian (~200 vs. 2.000+), e desenvolvimento considerado lento por usuários de longa data, com "muitas reclamações de bugs" segundo comparações de terceiros.
- App mobile ainda em desenvolvimento/imaturo comparado ao desktop.
- Uso intensivo de recursos do sistema (CPU/memória), principalmente no graph view com datasets grandes.

**Features mais pedidas:**
- Sync robusto de verdade (RTC — Real-Time Collaboration — está em alpha, ainda não é confiável para produção).
- Query builder mais maduro (equivalente ao Dataview do Obsidian).
- Estabilidade de longo prazo antes de features novas.

**Bugs/erros recorrentes:**
- Colapsar/expandir itens na barra lateral levando 10+ segundos em grafos grandes.
- Corrupção de conteúdo em "file graphs" quando não se usa backup via Git (aviso oficial do projeto).

---

### 2.4 Roam Research

**Perfil:** pioneiro do modelo "outliner com backlinks", cultuado no Twitter/PKM circles, mas hoje considerado por muitos analistas como tendo perdido tração frente a Obsidian/Logseq/Tana.

**Frustrações principais:**
- Preço historicamente alto frente a alternativas gratuitas (Logseq nasceu, em parte, como resposta open-source a essa insatisfação).
- Percepção de estagnação: comparações recentes descrevem o Roam como tendo "praticamente saído da conversa" de PKM que antes dominava, sinal de erosão de confiança da base de usuários early-adopter.
- Falta de app mobile nativo robusto por muito tempo foi um ponto de fricção clássico da comunidade.

---

### 2.5 Anytype

**Perfil:** open-source, local-first, P2P encriptado ponta-a-ponta, "objetos" em vez de páginas/blocos simples — tenta unir o melhor de Notion (bancos de dados) com o melhor de Obsidian (privacidade/dados locais).

**Frustrações principais:**
- **Curva de aprendizado íngreme** em torno de "objetos, relações e configuração inicial", especialmente para usuários não-técnicos — é o ponto fraco nº 1 citado.
- **Paridade mobile fraca**: o app Android é descrito como "às vezes com bugs ao criar novos objetos".
- **Recursos ainda incompletos ou "rough"**: onboarding, colaboração, busca, e polimento de exportação aparecem repetidamente como gaps em reviews agregadas.
- Bugs gerais esperados de um produto ainda em maturação.

**Features mais pedidas:**
- Templates mais robustos.
- Lembretes/reminders nativos.
- Fórmulas (equivalentes às do Notion).
- Colaboração mais suave (multiplayer ainda recente).

---

### 2.6 Tana

**Perfil:** estruturado por "supertags" (tags que funcionam como schemas de banco de dados), outliner de blocos, forte foco em automação e "Command Nodes"; captou US$ 25 milhões em 2025.

**Frustrações principais:**
- **Curva de aprendizado com custo real e antecipado**: análises apontam de 3 a 5 horas de configuração inicial antes do sistema "compensar" — quem começa a usar em período corrido do trabalho tende a montar um sistema pela metade, ter resultados inconsistentes, e concluir erroneamente que "a ferramenta não funciona".
- **App mobile é considerado fraco a ponto de reviewers da App Store chamarem de "gravador de voz glorificado"** — não é um workspace completo no celular, o que frustra quem espera continuidade entre desktop e mobile.
- **Modo offline só funciona para workspaces pessoais**; workspaces compartilhados exigem internet — inutilizável em avião/trem sem wifi, por exemplo.
- Camada visual limitada (cores e banners básicos) comparado à profundidade estrutural do produto — para quem organiza visualmente, é uma limitação real.
- Risco de precificação: por ser financiado por VC com metas de crescimento agressivas, analistas de mercado já sinalizam "vale ficar de olho" quanto a aumentos de preço futuros.
- Migração para fora do Tana é difícil na prática: embora haja exportação para JSON/Markdown, os "supertag schemas" e "Command Nodes" — o cerne do valor do produto — **não são transferíveis** para outras ferramentas. Isso é lock-in funcional, mesmo com exportação de dados brutos disponível.

---

### 2.7 RemNote

**Perfil:** nota + flashcard + repetição espaçada integrados, forte em nichos acadêmicos/médicos.

**Frustrações principais:**
- **App visto como "muito, muito bugado"** por usuários de longa data mesmo gostando do conceito (citação direta de fórum oficial: usuário com um mês de uso descreve a experiência assim, apesar de "amar a ideia").
- **Apps iOS/iPad têm reputação de instabilidade**: congelamentos, crashes, atraso em relação à versão desktop — a própria RemNote reconheceu publicamente esse problema em resposta a usuários (abril de 2026) e lançou correções, mas o veredito da comunidade sobre se resolveu ainda estava indefinido.
- **Ordem de revisão dos flashcards é ilógica para uso acadêmico real**: usuários relatam que cartões aparecem fora de ordem lógica (ex.: pedindo tópicos avançados antes dos fundamentos), e mesmo pagando pelo plano Pro para destravar "aprender em ordem", a experiência de revisão continua limitada a três respostas (pular/errei/lembrei) em vez de opções mais granulares.
- **Perda de formatação ao copiar/colar conteúdo entre documentos** — um usuário relatou ter perdido dias de trabalho criando flashcards porque a formatação quebrou ao tentar reorganizar por capítulos.
- Uso "gratuito" é percebido como muito limitado, e a adição de features de IA "por créditos" é vista por parte da base como uma mudança de posicionamento chata/agressiva.

---

### 2.8 Evernote

**Perfil:** o pioneiro histórico da categoria (fundado em 2007, chegou a ter 100+ milhões de usuários), hoje sob a Bending Spoons (adquirido em 2022/2023).

**Frustrações principais — e aqui o padrão muda de "bugs de produto jovem" para "erosão de confiança em produto legado":**
- **Corte agressivo do plano gratuito**: de "notas ilimitadas por mais de uma década" para um limite de **50 notas editáveis** no plano free — um dos cortes de produto mais citados negativamente em toda a categoria.
- **Layoffs e reestruturação após aquisição**: a Bending Spoons demitiu os 129 funcionários da equipe nos EUA pouco depois da compra, formalmente citando que o modelo anterior era "insustentável no longo prazo" — o que reforçou a narrativa de "empresa sugando valor de uma base cativa" entre usuários antigos.
- **Updates que quebram funcionalidade básica**: usuários relatam que é possível pesquisar literalmente a palavra "update" na comunidade do Evernote e achar dezenas de threads sobre atualizações que quebraram partes do app — inclusive formatação de bullet points travando durante ligações/reuniões.
- **Cancelamento de assinatura deliberadamente difícil**: um review recente descreve terem aumentado o preço "na véspera de Natal, no meio da assinatura", com limites de exportação, links legados quebrados e botão de cancelamento "enterrado" na interface.
- **Push agressivo de recursos de IA** enquanto bugs básicos de sincronização entre pessoas editando a mesma nota continuam existindo (sync às vezes trava quando duas pessoas editam a mesma nota ao mesmo tempo).
- Narrativa de "por que eu larguei o Evernote depois de 13 anos": o motivo central citado não é mais uma feature técnica específica, e sim **perda de confiança** na empresa — "broken trust = broken user experience", nas palavras de um blogueiro de longa data que documentou sua saída.

**O que isso ensina para um novo produto:** no segmento de PKM, confiança de longo prazo (nunca restringir retroativamente o que já foi prometido, nunca dificultar exportação/cancelamento) pesa tanto quanto qualquer feature.

---

### 2.9 Craft

**Perfil:** editor de blocos com forte foco em design/estética, nativo em Apple, tentando ser "Notion mais bonito e mais rápido para começar".

**Frustrações principais:**
- **Excesso de features empilhadas na interface** — um review técnico detalhado descreve isso como o motivo de não conseguir adotar o Craft no dia a dia apesar de achá-lo "literalmente a ferramenta de notas mais bem desenvolvida" que já testou: a UI fica "lotada", com navegação confusa, animações demais, e elementos escondidos atrás de múltiplos painéis deslizantes.
- **Suporte a Android e confiabilidade de conta** citados como "lacunas notáveis" em análises de mercado — histórico do produto é mais forte em iOS/Mac.
- Pedidos recorrentes por: formatação mais rápida, melhor comportamento de blocos de código, Markdown mais completo, backup local, e recursos mais avançados de linking/templates.

---

### 2.10 Joplin (open-source)

**Perfil:** app de notas open-source, Markdown, criptografia ponta-a-ponta, múltiplos backends de sincronização (Nextcloud, WebDAV, Dropbox, OneDrive, Joplin Cloud).

**Frustrações principais — aqui o padrão dominante e cristalino é: sincronização e conflitos de sync.** Uma varredura nas issues mais recentes do repositório oficial no GitHub mostra que é, de longe, a categoria de bug mais reportada:
- Android extremamente lento após deletar muitos conflitos acumulados (issue com 23 comentários).
- Conflitos de sync gerados mesmo quando o conteúdo local e remoto são **idênticos**, por causa de um atributo interno (`sync_time`) sendo tratado como diferença real — um bug puramente técnico que gera ruído e desconfiança no usuário.
- Notas inteiras movidas para a pasta "Conflicts" sem motivo aparente após updates do cliente, inclusive em casos de conta desabilitada no Joplin Cloud, apagando o entendimento do usuário sobre o que era "verdade" nos seus dados.
- Pasta de conflitos fica **enterrada no fim da lista de notebooks**, especialmente ruim em mobile, então usuários nem percebem que um conflito ocorreu até muito tempo depois.
- Recursos duplicados (anexos) permanecem "orfãos" no servidor de sync após um conflito de recurso, inflando espaço de armazenamento silenciosamente.

**Features mais pedidas:**
- Opção de sync unidirecional/seletivo por dispositivo (ex.: "no celular eu só quero ler, não sincronizar mudanças automaticamente").
- Indicação visual clara e imediata quando um conflito acontece, independente de quantos notebooks o usuário tenha.

---

### 2.11 Trilium / TriliumNext

**Perfil:** app hierárquico de notas com "clonagem" (a mesma nota pode aparecer em múltiplos lugares da árvore), scripting avançado, SQLite local — muito popular entre desenvolvedores/power users que hospedam a própria instância.

**Frustrações principais:**
- Curva de aprendizado alta (scripting, atributos, estrutura de árvore) — não é para o usuário casual.
- Depois da saída do mantenedor original (zadam), o projeto passou por uma fase de incerteza de continuidade antes de ser assumido pela comunidade como "TriliumNext" — esse tipo de evento (mudança de mantenedor em projeto open-source crítico para os dados de alguém) é citado como fator de ansiedade recorrente nesse nicho.
- Não tem sync backend dedicado tão simples quanto concorrentes — depende de rodar servidor próprio.

---

### 2.12 AppFlowy (open-source, "Notion aberto")

**Perfil:** alternativa open-source ao Notion, Rust + Flutter, promete "as features do Notion com 100% de controle dos dados"; 66-72 mil estrelas no GitHub.

**Frustrações principais — aqui o gap entre marketing e realidade técnica é o tema central:**
- Uma análise que cruzou métricas do GitHub (66,5 mil estrelas, **974 issues abertas**) resume o padrão: o produto é descrito como estando em **"beta perpétuo"**, com instabilidade real — o oposto do que se espera de uma "segunda mente" confiável.
- **Bugs críticos de sync com relatos de corrupção e perda parcial de dados** — apontado como "o verdadeiro fator eliminatório" para uso sério.
- **Problemas de performance extremos**: relatos no GitHub de **5 a 10 minutos de tempo de inicialização** e **mais de 90% de uso de CPU** para workspaces de apenas 44 KB de dados — um sinal claro de dívida técnica na arquitetura.
- Cobertura de funcionalidades de banco de dados estimada em ~70% do que o Notion oferece — faltam relações entre bancos de dados, rollups e a profundidade de fórmulas do Notion.
- Discussão pública dos próprios mantenedores/comunidade questionando se o AppFlowy "é de fato" um substituto do Notion, já que originalmente nem seguia atalhos de Markdown básicos (`-` para lista, ``` para bloco de código, `#` para heading) — só foram sendo adicionados com o tempo por pressão de usuários.
- Mesmo assim, autohospedar o AppFlowy (via Docker) é citado como forma de resolver a maior queixa de quem usa Notion (ausência de posse real sobre os arquivos) — ou seja, o público disposto a tolerar a instabilidade em troca de soberania de dados existe e é vocal.

---

### 2.13 Heptabase

**Perfil:** "cards em whiteboard infinito" — nicho de pensamento visual/espacial, forte entre pesquisadores, estudantes de pós-graduação e escritores de livros.

**Frustrações principais:**
- **Sem plano gratuito permanente** (só trial limitado) — citado como a barreira de entrada nº 1 em múltiplas reviews independentes.
- Preço no patamar médio-alto da categoria (US$ 8,99–11,99/mês conforme o plano e o momento).
- **Performance degrada em whiteboards muito grandes** (centenas de cards): o app fica mais lento e o usuário "pode perder a visão geral" — ironicamente, o próprio recurso central (organização espacial) sofre em escala, o mesmo padrão de falha visto no graph view do Obsidian.
- Não serve bem quem só quer notas lineares simples — usuários desse perfil relatam sensação de "ferramenta pesada demais" para necessidades básicas.

---

### 2.14 Capacities

**Perfil:** organização por "tipos de objeto" (pessoas, livros, artigos, projetos) em vez de páginas soltas — comparável em espírito ao Anytype/Tana, mas com forte ênfase em daily notes e um design mais opinativo.

Não foi possível obter reviews tão granulares quanto para as demais ferramentas nesta rodada de pesquisa (produto mais novo, menos volume de discussão pública ainda), mas o padrão de posicionamento no mercado é claramente o mesmo cluster de dores: usuários migrando de Notion/Obsidian em busca de "estrutura sem rigidez", e citando como principais hesitações (a) tamanho pequeno da comunidade/ecossistema de plugins comparado a Obsidian, e (b) dependência de estar sempre atualizando o app para acompanhar features novas, o que gera a mesma fadiga de "app em beta permanente" vista no Anytype e no AppFlowy.

---

## 3. Padrões transversais (as dores que atravessam TODAS as ferramentas)

Esta é provavelmente a seção mais importante para orientar o desenho de um novo produto — são dores estruturais da categoria, não bugs pontuais de um app específico.

### 3.1 Sincronização é o ponto de fricção nº 1, universalmente
Em praticamente toda ferramenta analisada — proprietária ou open-source, paga ou gratuita — sync aparece como fonte principal de bugs, ansiedade e churn: Obsidian (sync pago vs. soluções caseiras arriscadas), Logseq (RTC ainda em alpha), Joplin (conflitos falso-positivos), AppFlowy (corrupção/perda de dados), Anytype (bugs mobile ao sincronizar objetos), Notion (lentidão que se agrava com dados sincronizados). Isso sugere que **sync confiável, rápido e sem surpresas é possivelmente o maior espaço de diferenciação competitiva possível** nessa categoria — é a dor mais universal e menos resolvida.

### 3.2 Paridade mobile é sistematicamente pior que desktop
Obsidian (histórico), Notion, Tana ("gravador de voz glorificado"), Anytype (bugs Android), RemNote (crashes em iOS/iPad), Craft (Android como "lacuna notável"), Logseq (app mobile "ainda em desenvolvimento"), AppFlowy (mobile secundário). Nenhuma ferramenta analisada tem paridade completa e estável entre desktop e mobile. Para um novo entrante, tratar mobile como **cidadão de primeira classe desde o dia 1** (não como "versão light depois") é uma oportunidade clara.

### 3.3 Ferramentas de visualização (graph view / whiteboard) não escalam
Obsidian (grafo trava em vaults de milhares de notas), Heptabase (whiteboards com centenas de cards ficam lentos e "perde-se a visão geral"), Logseq (uso pesado de CPU/memória no graph view). O recurso mais usado em marketing ("veja suas ideias conectadas!") é frequentemente o primeiro a quebrar quando o usuário de fato acumula conhecimento por anos — que é o próprio objetivo declarado da categoria.

### 3.4 Ansiedade de lock-in e portabilidade de dados
Mesmo ferramentas que "exportam dados" (Tana, Heptabase, AppFlowy) deixam claro que a estrutura real de valor (schemas, supertags, relações) não é portável — só o conteúdo bruto. Isso gera hesitação de adoção mesmo entre usuários interessados, e é citado explicitamente como critério de avaliação em quase toda comparação de mercado ("dá pra sair depois, sem perder tudo?").

### 3.5 "Shiny object syndrome" / fadiga de troca de ferramenta
Documentado de forma consistente em blogs de PKM independentes: o próprio ato de "otimizar o sistema de notas" vira uma forma de procrastinação. Isso não é bug de nenhum app específico — é uma dor psicológica/comportamental da categoria inteira, e sugere que **onboarding que produz valor rápido, sem exigir uma configuração perfeita antes de começar**, é diferencial forte (ex.: Tana falha exatamente aqui, exigindo 3-5h de setup antes do "aha moment").

### 3.6 IA "empurrada" gera desconfiança quando bugs básicos continuam sem solução
Padrão visto em Evernote (push de IA com sync básico ainda quebrado), RemNote ("mais um app gritando sobre IA" — citação direta de review), Tana (créditos de IA cobrados à parte). Usuários dessa categoria tendem a ser tecnicamente exigentes e percebem rapidamente quando IA é usada como cortina de fumaça para dívida técnica não resolvida.

### 3.7 Aumentos de preço / mudanças de modelo de negócio retroativas quebram confiança de forma desproporcional
Evernote (corte de plano gratuito de "ilimitado" para 50 notas) é o caso mais extremo, mas o padrão de "ansiedade sobre precificação futura" aparece também em análises sobre Tana (financiado por VC, "vale ficar de olho") e é citado como razão histórica da migração em massa Roam → Logseq/Obsidian.

### 3.8 Curva de aprendizado alta é tolerada — mas só se o valor for visível rápido
Anytype, Tana, Logseq, Trilium: todos têm curva de aprendizado íngreme reconhecida pelos próprios usuários fiéis. A diferença entre "curva de aprendizado que vale a pena" e "abandono" parece estar em **quanto tempo até o primeiro resultado tangível** — Tana é criticado especificamente por atrasar esse momento (3-5h de setup).

### 3.9 Busca de qualidade real é surpreendentemente rara
Apesar de "encontrar o que preciso depois" ser o objetivo central de qualquer PKM, poucas ferramentas são elogiadas especificamente pela busca — é mais citada como algo que "funciona bem o suficiente" (RemNote, Obsidian com plugins) do que como um diferencial forte de qualquer produto. Isso sugere espaço de oportunidade pouco explorado (busca semântica/local de alta qualidade, sem depender de nuvem).

---

## 4. Síntese: matriz de dor → oportunidade de produto

| Dor recorrente | Presente em | Oportunidade para um novo app |
|---|---|---|
| Sync não-confiável / pago à parte / gera conflitos falsos | Obsidian, Logseq, Joplin, AppFlowy, Anytype | Sync nativo, gratuito ou embutido no preço base, com resolução de conflito automática e transparente (nunca "sumiço silencioso") |
| Mobile de segunda classe | Quase todas | Mobile-first real desde o MVP, não "porta depois" |
| Visualização (graph/canvas) não escala | Obsidian, Heptabase, Logseq | Arquitetura de renderização pensada para 10k+ notas desde o início (virtualização, clustering, lazy load) |
| Lock-in funcional disfarçado de "exporta seus dados" | Tana, Heptabase, AppFlowy | Exportação que preserva estrutura/relações, não só texto bruto |
| Setup inicial longo antes de gerar valor | Tana, Anytype | Onboarding com valor em minutos, estrutura opcional e incremental |
| IA como cortina de fumaça para bugs básicos | Evernote, RemNote, Tana | IA opcional, nunca em troca de estabilidade core; transparência sobre custo/créditos |
| Mudança retroativa de modelo de negócio | Evernote | Compromisso público e contratual sobre o que não muda no plano gratuito existente |
| Plugins críticos podem ser abandonados | Obsidian, ecossistemas de plugin em geral | Funcionalidades essenciais nativas; plugins para o "extra", não para o "básico" |
| Fadiga de troca de ferramenta / paradoxo da escolha | Categoria inteira | Migração de entrada facilitada (importadores robustos de Notion/Obsidian/Evernote/Roam) para reduzir o custo de "só mais uma tentativa" |
| Falta de transparência sobre limites técnicos (linhas, tamanho) | Notion | Avisos proativos antes do usuário perder trabalho, nunca "falha silenciosa ao salvar" |

---

## 5. Limitações desta pesquisa

- O acesso direto e em volume a threads específicas do Reddit foi tecnicamente restrito no momento da coleta (o buscador disponível não indexou URLs de `reddit.com/r/.../comments/` de forma consistente); a triangulação foi feita via fóruns oficiais, GitHub Issues e agregadores de review (G2, Capterra, TrustPilot, Product Hunt), que no geral refletem os mesmos padrões de queixa que aparecem no Reddit, com a vantagem de serem mais estruturados e datados.
- Capacities e alguns players menores (Mem, Reflect, Notesnook, Obsidian-likes recentes) têm volume de discussão pública ainda pequeno, então a cobertura deles é mais rasa que a de Obsidian/Notion/Evernote.
- Muitas fontes citadas são de 2025–2026, refletindo o estado mais recente do mercado; onde há mudança de versão relevante (ex.: Logseq DB version, RemNote fix de abril/2026), isso foi sinalizado no texto.

---

## 6. Principais fontes consultadas

- Fórum oficial Logseq (discuss.logseq.com) — threads sobre performance e escala
- Fórum oficial RemNote (forum.remnote.io)
- GitHub Issues: laurent22/joplin, AppFlowy-IO/AppFlowy, stravo1/obsidian-gdrive-sync
- Documentação oficial Obsidian (Sync, conflitos)
- Product Hunt Reviews: Anytype, Craft.do
- G2, Capterra, TrustPilot: Notion, Evernote, RemNote, Tana
- AlternativeTo, SaaSHub, StackShare: comparativos e listas de prós/contras
- Artigos e reviews independentes 2025–2026: tl;dv (RemNote), aishortcutlab (Tana), toolchase/makerstack/storyflow (Heptabase), opentechhub e xda-developers (AppFlowy), falconer.com (Notion performance)
- Blogs de PKM independentes sobre comportamento de troca de ferramentas ("shiny object syndrome")
- Wikipedia (dados de contexto: base de usuários Obsidian, histórico Evernote)
