# CYBERFOOD --- FINALIZAÇÃO DO BACKEND, BANCO DE DADOS E AUTOMAÇÕES

## Claude Code \| Sonnet

Atue como um engenheiro de software sênior, especialista em arquitetura
Full Stack, Node.js, Express.js, TypeScript, MySQL, Prisma ORM, APIs
REST, n8n e deploy na Railway.

Sua missão é FINALIZAR A INFRAESTRUTURA do projeto CyberFood existente,
desenvolvendo o backend, o banco de dados e as automações necessárias
para transformar o protótipo em uma aplicação com arquitetura real e
preparada para produção.

**ATENÇÃO: O FRONTEND JÁ ESTÁ CONSTRUÍDO E NÃO DEVE SER MODIFICADO.**

------------------------------------------------------------------------

# 1. CONTEXTO DO PROJETO

O CyberFood é uma plataforma que conecta consumidores a food trucks,
permitindo descobrir estabelecimentos, visualizar cardápios, realizar
pedidos para retirada e oferecer aos proprietários ferramentas de
gerenciamento operacional.

O projeto possui dois tipos principais de usuários:

-   CLIENT: consumidor que utiliza a plataforma para encontrar food
    trucks e realizar pedidos.
-   OWNER: proprietário de um food truck, responsável pela administração
    do estabelecimento.

O projeto também possui funcionalidades de gerenciamento de produtos,
estoque, lotes, pedidos, clientes, promoções, avaliações, relatórios e
previsão de demanda.

Analise integralmente o projeto fornecido antes de começar.

Arquivos importantes:

-   `src/lib/types.ts`
-   `src/lib/storage.ts`
-   `src/lib/seed.ts`
-   `src/lib/validators.ts`
-   `src/context/AppContext.tsx`
-   `src/App.tsx`
-   `src/pages/`
-   `src/pages/client/`
-   `src/pages/manage/`
-   `src/imports/pasted_text/cyberfood-project-brief.md`

Utilize os tipos, funcionalidades e regras já existentes como referência
para construir a infraestrutura.

Não invente funcionalidades que não façam sentido para o produto.

# 2. REGRAS INEGOCIÁVEIS

## 2.1. Preservação do frontend

NÃO MODIFIQUE:

-   Componentes React.
-   Páginas.
-   Layouts.
-   CSS.
-   Tailwind.
-   Tipografia.
-   Cores.
-   Imagens.
-   Ícones.
-   Animações.
-   Responsividade.
-   Navegação.
-   Identidade visual.
-   Estrutura visual das telas.

Não redesenhe nenhuma página.

Não substitua componentes.

Não reconstrua a aplicação.

Não remova funcionalidades existentes.

Não altere a experiência visual ou comportamental do usuário.

O frontend deverá permanecer exatamente como foi entregue.

Desenvolva o backend em uma estrutura independente, preferencialmente:

`/backend`

Você poderá adicionar arquivos de configuração específicos para o
backend, documentação e arquivos de infraestrutura, sem modificar os
arquivos existentes do frontend.

Não altere o package.json da raiz para reorganizar o frontend.

## 2.2. Regras de negócio

1.  Não existe sistema de delivery.
2.  Todos os pedidos são para retirada no food truck.
3.  Um cliente pode realizar pedidos em diferentes food trucks.
4.  Cada pedido pertence a um único food truck.
5.  Cada proprietário somente pode acessar os dados do próprio
    estabelecimento.
6.  Um novo food truck deve começar completamente vazio.
7.  Dados demonstrativos devem permanecer separados dos dados reais.
8.  Os pedidos devem possuir histórico de alterações de status.
9.  As movimentações de estoque precisam manter consistência.
10. Nenhum proprietário pode acessar informações administrativas de
    outro estabelecimento.

# 3. BACKEND --- NODE.JS + EXPRESS.JS

Desenvolva o backend utilizando:

-   Node.js.
-   Express.js.
-   TypeScript.
-   API REST.
-   Prisma ORM.
-   Zod para validação.
-   bcrypt para hash de senhas.
-   JWT para autenticação.
-   Refresh tokens com armazenamento seguro e possibilidade de
    revogação.
-   CORS configurável.
-   Helmet.
-   Middleware de tratamento de erros.
-   Logs estruturados.

Organize o código em uma arquitetura modular.

Estrutura sugerida:

backend/ - src/ - config/ - controllers/ - services/ - repositories/ -
routes/ - middlewares/ - validators/ - utils/ - types/ - integrations/ -
n8n/ - app.ts - server.ts - prisma/ - schema.prisma - migrations/ -
seed.ts - tests/ - .env.example - package.json - tsconfig.json -
README.md

Separe responsabilidades:

-   Routes: definição dos endpoints.
-   Controllers: recebimento e resposta das requisições.
-   Services: regras de negócio.
-   Repositories: comunicação com o banco.
-   Middlewares: autenticação, autorização e validações.

Não concentre toda a lógica em um único arquivo.

# 4. AUTENTICAÇÃO E AUTORIZAÇÃO

Implemente autenticação real.

Funcionalidades:

-   Cadastro de clientes.
-   Cadastro de proprietários e seus food trucks.
-   Login.
-   Logout.
-   Renovação de sessão.
-   Recuperação de senha, com mecanismo seguro e configurável.
-   Consulta do usuário autenticado.
-   Alteração de informações pessoais.
-   Alteração de senha.

Utilize bcrypt para armazenar senhas criptografadas por hash.

Nunca armazene senhas em texto puro.

Implemente controle de acesso por perfil:

CLIENT: - Acessar informações públicas dos food trucks. - Consultar
cardápios. - Gerenciar favoritos. - Realizar pedidos. - Consultar seus
próprios pedidos. - Enviar avaliações e feedbacks.

OWNER: - Gerenciar seu próprio food truck. - Gerenciar produtos. -
Gerenciar estoque. - Gerenciar pedidos recebidos. - Consultar clientes
relacionados ao seu estabelecimento. - Gerenciar promoções. - Consultar
relatórios. - Consultar histórico e auditoria.

Todas as rotas privadas devem verificar autenticação e autorização.

A identificação do foodTruckId deve ser obtida a partir da sessão
autenticada e das relações de propriedade no banco, nunca confiando
exclusivamente em IDs enviados pelo frontend.

# 5. BANCO DE DADOS --- MYSQL

Utilize MySQL como banco de dados relacional.

Utilize Prisma ORM para modelagem e gerenciamento das migrations.

Crie relacionamentos reais com:

-   Primary Keys.
-   Foreign Keys.
-   Índices.
-   Restrições UNIQUE.
-   Restrições NOT NULL.
-   Regras de integridade referencial.
-   Timestamps.

Utilize nomes de tabelas consistentes e snake_case.

## 5.1. Estrutura de entidades

Desenvolva e relacione as seguintes tabelas:

### Usuários e planos

-   users
-   subscription_plans
-   plan_features

### Food trucks

-   food_trucks
-   food_truck_hours
-   food_truck_payment_methods

### Produtos

-   products
-   product_recipe_items
-   product_addons

### Estoque

-   inventory_items
-   inventory_batches
-   restocks
-   disposals

### Pedidos

-   carts
-   cart_items
-   cart_item_addons
-   orders
-   order_items
-   order_item_addons
-   order_status_history

### Relacionamento com clientes

-   favorites
-   reviews
-   feedback

### Gestão

-   promotions
-   audit_logs

Analise os tipos existentes em `src/lib/types.ts` e utilize-os como
referência para definir os atributos e relacionamentos.

Não crie tabelas sem finalidade dentro do projeto.

## 5.2. Relacionamentos importantes

Implemente corretamente:

-   Um usuário proprietário pode possuir um food truck, respeitando a
    regra de propriedade definida no projeto.
-   Um food truck possui vários produtos.
-   Um food truck possui vários itens de estoque.
-   Um item de estoque pode possuir vários lotes.
-   Um food truck recebe vários pedidos.
-   Um pedido pertence a um cliente.
-   Um pedido possui vários itens.
-   Um produto pode possuir vários adicionais.
-   Um produto pode possuir vários ingredientes vinculados ao estoque.
-   Um cliente pode favoritar vários food trucks.
-   Um food truck pode receber várias avaliações.
-   Um food truck pode possuir várias promoções.
-   Um food truck possui vários registros de auditoria.

Utilize tabelas associativas para relacionamentos N:N.

## 5.3. Isolamento de dados

Esta é uma das partes mais importantes da implementação.

Implemente isolamento por foodTruckId.

Um proprietário nunca poderá:

-   Consultar produtos de outro estabelecimento.
-   Alterar o estoque de outro estabelecimento.
-   Consultar pedidos de outro estabelecimento.
-   Excluir informações de outro estabelecimento.
-   Visualizar clientes pertencentes exclusivamente à gestão de outro
    food truck.
-   Consultar relatórios de outro food truck.

Implemente essa validação no backend, principalmente nos services e
repositories.

Não confie apenas nos filtros enviados pelo cliente.

# 6. REGRAS OPERACIONAIS DO BANCO

## 6.1. Cadastro de food trucks

Quando um proprietário cadastrar um novo estabelecimento:

-   Criar o usuário.
-   Criar o food truck.
-   Relacionar o proprietário ao food truck.
-   Registrar o evento de criação na auditoria.

O novo estabelecimento deve começar com:

-   Zero produtos.
-   Zero itens de estoque.
-   Zero pedidos.
-   Zero clientes relacionados.
-   Zero avaliações.
-   Zero promoções.
-   Zero vendas.

Não copie dados dos food trucks demonstrativos.

## 6.2. Pedidos

Implemente os seguintes status:

-   Novo.
-   Aceito.
-   Preparando.
-   Pronto para retirada.
-   Retirado.

Toda mudança de status deverá gerar um registro em order_status_history.

Utilize transações do banco para operações que alterem simultaneamente
pedidos e estoque.

Evite que um pedido seja criado parcialmente.

Cada pedido deve possuir:

-   Identificação do cliente.
-   Identificação do food truck.
-   Produtos.
-   Quantidades.
-   Adicionais.
-   Valores individuais.
-   Valor total.
-   Forma de pagamento.
-   Observações.
-   Data de criação.
-   Status atual.

As formas de pagamento são:

-   PIX.
-   Cartão de crédito.
-   Cartão de débito.
-   Dinheiro na retirada.

Não implemente gateways de pagamento ou processamento financeiro real.

## 6.3. Estoque

Implemente:

-   Cadastro de itens.
-   Edição.
-   Exclusão com validação de dependências.
-   Entrada de mercadorias.
-   Controle por lotes.
-   Data de validade.
-   Reposição.
-   Baixa de estoque.
-   Registro de desperdícios.
-   Histórico de movimentações.
-   Alertas de estoque mínimo.

Utilize transações para garantir consistência.

Implemente controle de concorrência para evitar que dois pedidos
simultâneos consumam quantidades inexistentes.

Quando houver receitas vinculadas aos produtos, calcule o consumo de
ingredientes de acordo com a quantidade vendida.

Não permita estoque negativo.

## 6.4. Promoções e avaliações

Implemente as operações CRUD de promoções.

Valide:

-   Datas de início e término.
-   Tipo de desconto.
-   Valor do desconto.
-   Produto associado.
-   Food truck proprietário.

Para avaliações:

-   Relacione a avaliação ao cliente.
-   Relacione ao food truck.
-   Relacione ao pedido correspondente.
-   Impedir avaliações duplicadas para o mesmo pedido, conforme a regra
    do produto.

# 7. API REST

Crie endpoints organizados por domínio.

Exemplo de organização:

/api/v1/auth /api/v1/users /api/v1/food-trucks /api/v1/products
/api/v1/inventory /api/v1/batches /api/v1/restocks /api/v1/disposals
/api/v1/orders /api/v1/carts /api/v1/favorites /api/v1/reviews
/api/v1/promotions /api/v1/customers /api/v1/analytics
/api/v1/forecasting /api/v1/feedback /api/v1/audit-logs
/api/v1/subscription-plans

Implemente:

-   GET para consultas.
-   POST para criação.
-   PUT/PATCH para alterações.
-   DELETE para exclusões.

Utilize respostas HTTP apropriadas.

Padronize os retornos JSON, erros e mensagens.

Implemente paginação, filtros e ordenação nos endpoints que retornam
coleções.

Disponibilize documentação interativa da API com Swagger / OpenAPI.

Crie também uma rota:

GET /api/v1/health

Ela deverá informar se a API está funcionando e se a conexão com o MySQL
está operacional.

# 8. INTEGRAÇÃO COM N8N --- AUTOMAÇÃO

Utilize n8n como ferramenta de automação.

O backend será responsável pelas regras de negócio e o n8n será
responsável pelos fluxos automatizados.

A integração deverá acontecer por webhooks HTTP autenticados.

Crie uma camada de integração em:

src/integrations/n8n/

Implemente os seguintes eventos:

## Automação 1 --- Novo pedido

Gatilho: criação de pedido.

Ações: - Notificar o food truck. - Informar número do pedido. - Informar
cliente. - Informar produtos. - Informar valor total. - Registrar o
evento.

## Automação 2 --- Atualização do pedido

Gatilho: mudança de status.

Ações: - Identificar o novo status. - Notificar o cliente. - Registrar
data e horário da atualização.

## Automação 3 --- Estoque baixo

Gatilho: quantidade de estoque inferior ao mínimo configurado.

Ações: - Identificar o food truck. - Identificar o ingrediente. -
Informar quantidade atual. - Informar quantidade mínima. - Enviar alerta
ao proprietário.

## Automação 4 --- Validade dos produtos

Gatilho: verificação periódica dos lotes.

Ações: - Identificar lotes próximos do vencimento. - Identificar
produtos vencidos. - Notificar o proprietário. - Registrar os alertas.

## Automação 5 --- Relatório de vendas

Gatilho: execução programada.

Ações: - Consultar vendas do período. - Calcular quantidade de
pedidos. - Calcular faturamento registrado. - Identificar produtos mais
vendidos. - Gerar resumo para o proprietário.

## Automação 6 --- Novo feedback

Gatilho: envio de feedback.

Ações: - Identificar tipo de feedback. - Registrar a mensagem. -
Notificar a equipe responsável.

## Requisitos técnicos do n8n

-   Criar os workflows.
-   Exportar os workflows em JSON.
-   Armazená-los em `backend/n8n/workflows/`.
-   Documentar como importá-los.
-   Configurar autenticação dos webhooks.
-   Implementar tratamento de erros.
-   Evitar execução duplicada.
-   Prever retentativas para falhas temporárias.
-   Não transmitir senhas, tokens ou dados sensíveis desnecessários.

Utilize variáveis de ambiente para os endereços dos webhooks.

Não faça o backend depender da disponibilidade do n8n para concluir uma
operação principal, como registrar um pedido.

# 9. SEGURANÇA

Implemente:

-   Hash de senhas com bcrypt.
-   JWT com expiração.
-   Refresh tokens revogáveis.
-   Validação de entradas com Zod.
-   Proteção contra SQL Injection por meio do ORM e consultas seguras.
-   Proteção contra acesso indevido a recursos.
-   Rate limiting nas rotas sensíveis.
-   CORS configurável.
-   Helmet.
-   Sanitização e validação dos dados.
-   Logs sem exposição de informações sensíveis.
-   Tratamento centralizado de exceções.

Não exponha variáveis de ambiente no frontend.

Não coloque credenciais reais nos arquivos versionados.

Crie `.env.example` com valores ilustrativos.

# 10. TESTES

Implemente testes automatizados.

Utilize Vitest ou Jest e Supertest.

Priorize:

-   Cadastro e login.
-   Autorização por perfil.
-   Isolamento entre food trucks.
-   Cadastro de produtos.
-   Movimentações de estoque.
-   Criação de pedidos.
-   Alteração de status.
-   Histórico de pedidos.
-   Transações.
-   Validação de dados.
-   Integração com webhooks.

Crie testes que comprovem que um proprietário não consegue acessar os
dados de outro.

Execute os testes e corrija os erros encontrados.

# 11. RAILWAY --- DEPLOY

Prepare o projeto para implantação na Railway.

A arquitetura de deploy deverá contemplar:

1.  Serviço do backend Node.js + Express.
2.  Serviço MySQL.
3.  Serviço n8n.

Configure:

-   Build e inicialização.
-   Variáveis de ambiente.
-   Conexão com MySQL.
-   Prisma migrations.
-   Health check.
-   Persistência necessária para o n8n.
-   Configuração de portas por variável de ambiente.
-   URLs públicas dos serviços.
-   CORS de acordo com a origem autorizada.

Crie os arquivos de configuração necessários, incluindo Dockerfile
quando apropriado e railway.json quando necessário.

Não utilize localhost nas configurações de produção.

Não invente credenciais ou URLs.

Documente quais serviços precisam ser criados manualmente no painel da
Railway.

Não declare que o deploy foi realizado se não houver autenticação e
execução efetiva na plataforma.

# 12. COMPATIBILIDADE COM O FRONTEND EXISTENTE

O frontend utiliza atualmente:

-   `src/lib/storage.ts`
-   `src/lib/seed.ts`
-   `src/context/AppContext.tsx`

Esses arquivos NÃO devem ser modificados.

Como o objetivo é preservar integralmente o frontend, implemente o
backend de forma independente e prepare uma documentação completa de
integração.

Crie:

`backend/docs/FRONTEND_INTEGRATION.md`

O documento deverá conter:

-   Mapeamento dos tipos TypeScript existentes para os modelos do banco.
-   Correspondência entre as operações do AppContext e os endpoints
    REST.
-   Exemplos de requisições e respostas.
-   Autenticação necessária.
-   Formato dos erros.
-   Variáveis de ambiente necessárias para uma futura conexão.
-   Estratégia de migração dos dados demonstrativos.
-   Estratégia para substituir futuramente o localStorage pela API sem
    alterar o design.

IMPORTANTE:

Não afirme que o frontend já está conectado ao banco de dados enquanto
ele continuar utilizando localStorage.

O backend deverá funcionar independentemente e estar pronto para uma
integração posterior.

# 13. DOCUMENTAÇÃO

Crie um README completo dentro de `/backend`.

Explique:

1.  Arquitetura.
2.  Tecnologias utilizadas.
3.  Estrutura de pastas.
4.  Instalação.
5.  Configuração do MySQL.
6.  Variáveis de ambiente.
7.  Execução das migrations.
8.  Criação dos dados iniciais.
9.  Inicialização do backend.
10. Execução dos testes.
11. Documentação Swagger.
12. Configuração do n8n.
13. Importação dos workflows.
14. Deploy na Railway.

Inclua comandos reais que possam ser executados no terminal.

# 14. ORDEM DE EXECUÇÃO

Execute o trabalho nesta sequência:

ETAPA 1 --- Análise - Inspecione todos os arquivos relevantes. -
Identifique as entidades. - Identifique as regras de negócio. -
Identifique os relacionamentos. - Identifique inconsistências. -
Apresente um plano de implementação.

ETAPA 2 --- Modelagem - Desenvolva o schema Prisma. - Defina
relacionamentos. - Configure índices e restrições. - Prepare migrations.

ETAPA 3 --- Backend - Configure Node.js e Express. - Implemente
autenticação. - Implemente autorização. - Desenvolva os módulos. -
Desenvolva os endpoints. - Implemente as regras de negócio.

ETAPA 4 --- Banco de dados - Configure conexão. - Execute migrations. -
Desenvolva seed controlado. - Teste integridade e isolamento.

ETAPA 5 --- n8n - Desenvolva os workflows. - Configure webhooks. -
Implemente comunicação com a API. - Exporte os arquivos JSON.

ETAPA 6 --- Testes - Execute testes automatizados. - Corrija erros. -
Verifique segurança. - Teste operações críticas.

ETAPA 7 --- Railway - Prepare configurações. - Documente variáveis. -
Prepare os serviços. - Documente o procedimento de deploy.

ETAPA 8 --- Entrega - Verifique se o frontend permanece inalterado. -
Verifique se o backend inicia corretamente. - Verifique se as migrations
funcionam. - Verifique se os workflows estão exportados. - Finalize a
documentação.

# 15. CRITÉRIOS DE CONCLUSÃO

O trabalho somente poderá ser considerado concluído quando:

\[ \] Backend Node.js + Express implementado.

\[ \] API REST funcional.

\[ \] Autenticação e autorização implementadas.

\[ \] Banco MySQL modelado.

\[ \] Prisma configurado.

\[ \] Migrations criadas.

\[ \] Isolamento de dados entre food trucks testado.

\[ \] Cadastro de novos food trucks iniciando vazio.

\[ \] Gerenciamento de pedidos implementado.

\[ \] Controle de estoque implementado.

\[ \] Transações implementadas nas operações críticas.

\[ \] Workflows n8n criados e exportados.

\[ \] Integração por webhooks documentada.

\[ \] Testes automatizados executados.

\[ \] Swagger disponível.

\[ \] Configuração Railway preparada.

\[ \] README completo.

\[ \] Documentação de integração com o frontend criada.

\[ \] Nenhum arquivo visual do frontend modificado.

# 16. INSTRUÇÃO FINAL

Trabalhe diretamente no projeto fornecido.

Não entregue apenas exemplos de código ou explicações teóricas.

Implemente efetivamente os arquivos, estruturas, serviços, modelos,
rotas, migrations, testes, workflows e documentações.

Priorize código limpo, modular, seguro, escalável e compatível com as
funcionalidades já existentes.

Não crie funcionalidades desnecessárias.

Não remova funcionalidades existentes.

Não altere o frontend.

Não simule integrações que não foram realmente executadas.

Se alguma etapa depender de credenciais, serviços externos ou
configurações que não estão disponíveis, prepare toda a implementação
possível e explique exatamente o que falta configurar manualmente.

Ao finalizar, apresente um relatório contendo:

1.  Arquivos criados.
2.  Arquivos modificados.
3.  Funcionalidades implementadas.
4.  Estrutura do banco de dados.
5.  Endpoints disponíveis.
6.  Automações desenvolvidas.
7.  Testes executados e resultados.
8.  Instruções para iniciar o projeto.
9.  Instruções para configurar a Railway.
10. Pendências necessárias para conectar o frontend ao backend.

**OBJETIVO FINAL: TRANSFORMAR A INFRAESTRUTURA DO CYBERFOOD EM UM
SISTEMA REAL, COM BACKEND, BANCO DE DADOS E AUTOMAÇÕES, PRESERVANDO
INTEGRALMENTE O FRONTEND EXISTENTE.**
