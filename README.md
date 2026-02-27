# 💸 PoupAI Finance — Aplicativo Financeiro Conversacional

O **PoupAI** é um aplicativo de organização financeira baseado em *interações por conversa com linguagem natural*. O usuário envia mensagens como “gastei 45 uber” ou “salário 1200”, e o sistema interpreta automaticamente a operação, classificando categorias, atualizando saldo, organizando ciclos financeiros e gerando relatórios completos (incluindo relatório anual).

O objetivo é tornar o controle financeiro simples, natural e livre de planilhas e formulários.

---

## 📌 1. Prompt Final (PRD refinado com Copilot Web)

> **Este é o PRD final enviado ao Lovable para gerar todo o app.**

```markdown
# PoupAI — App Financeiro Conversacional

O PoupAI é um aplicativo de organização financeira baseado inteiramente em conversas. O usuário descreve gastos, receitas e consultas em linguagem natural, e o sistema registra tudo automaticamente em ciclos financeiros personalizados. O app deve ser simples, intuitivo, com design roxo/lilás e respostas leves e descontraídas enviadas pela IA.

1. DESIGN E INTERFACE

## Paleta obrigatória
- Roxo escuro (primário)
- Lilás (secundário)
- Branco (fundo)
- Preto suave (texto)

Aplicação:
- cabeçalhos
- botões
- cards
- gráfico
- sidebar
- gradientes

## Telas obrigatórias
1. Tela de Chat (principal)
2. Sidebar com lista de ciclos
3. Página de resumo do ciclo (gráficos e totais)
4. Histórico filtrado por ciclo
5. Relatório anual
6. Tela de seleção de moeda (primeiro acesso)
7. Configurações do usuário
8. Página de renomear/excluir ciclo


2. AUTENTICAÇÃO E PERFIL

## Requisitos
- Login com e-mail/senha.
- No cadastro por e-mail/senha, o app deve solicitar o campo “Nome” (obrigatório).
- Exibir o nome do usuário no header/sidebar e na mensagem inicial do chat.


3. SELEÇÃO DE MOEDA

Ao entrar no app pela primeira vez:

1. Exibir modal obrigatório: "Qual moeda você deseja usar?"
2. Opções:
   - BRL (R$)
   - EUR (€)
   - USD ($)
3. Toda a lógica financeira usa essa moeda.
4. O usuário pode alterar depois em “Configurações”.
5. Se o usuário digitar valor com outra moeda, pedir confirmação antes de registrar.


4. CICLOS FINANCEIROS 

## Conceito
Ciclos são períodos financeiros personalizados (não seguem calendário).

Exemplos:
- "Março"
- "Pós-férias"
- "Ciclo 3"
- "13º salário"

## Comportamento ao registrar receita
Quando o usuário envia uma receita pela IA:

Fluxo obrigatório:
- Abrir modal:
  - "Criar novo ciclo"
  - "Manter ciclo atual"
  - Campo de nome para novo ciclo (obrigatório)
- Se criar novo ciclo:
  1. Criar registro do ciclo no banco.
  2. Definir como ciclo ativo.
  3. Registrar a receita **no novo ciclo** (não no antigo).
  4. Atualizar sidebar, resumo do ciclo e saldo.
  5. Enviar mensagem no chat:
     "Novo ciclo iniciado: <nome>"
     Em seguida, confirmar a receita com o template padrão.
- Se manter ciclo atual:
  - Registrar receita no ciclo ativo.
  - Atualizar UI normalmente.

## Comportamento ao registrar categorias/gastos
- Gastos sempre entram no ciclo ativo.
- Se nenhum ciclo existir, criar automaticamente:
  "Ciclo Inicial"
  e notificar no chat:
  "Iniciei seu primeiro ciclo automaticamente."


5. RENOMEAR E EXCLUIR CICLOS

## Renomear ciclo
- Sidebar e página de ciclo devem ter ação “Renomear ciclo”.
- Ao renomear:
  - Atualizar sidebar
  - Atualizar cabeçalho
  - Atualizar filtros e relatórios
  - Persistir alteração no banco

## Excluir ciclo
- Modal de confirmação:
  "Deseja excluir este ciclo?"

Modal deve ter duas opções:
1. Excluir ciclo e todas as transações dentro dele.
2. Reatribuir transações para outro ciclo (dropdown list).

Após excluir ou mover:
- Recalcular saldo
- Recarregar sidebar
- Atualizar relatório e histórico


6. LÓGICA DE INTERPRETAÇÃO DA IA

IA deve identificar:
- gastos
- receitas
- consultas de saldo
- pedidos de relatório
- pedidos de dicas financeiras
- categorias
- moeda mencionada
- intenção de criar novo ciclo (explícita ou implícita)

Exemplos de mensagens válidas:
- "gastei 45 uber"
- "paguei 35 no cabelo"
- "comprei uma cama por 547"
- "salário 1200"
- "recebi 300"
- "saldo"
- "quanto tenho"
- "mostra meu relatório"
- "qual meu maior gasto?"

## Estrutura das respostas da IA
A IA deve sempre responder com:

Mensagem personalizada  
- Valor  
- Categoria  
- Descrição  
- Data  

Exemplo gasto:
"Espero que a viagem tenha sido boa 🚗"
- Valor: 20
- Categoria: Transporte
- Descrição: Uber
- Data: <data>

Exemplo receita:
"Ufa, parecia que não ia cair nunca, né? 🤑"
- Valor: 1200
- Categoria: Receita
- Descrição: Salário
- Data: <data>

## Quando não entender:
Responder:
"Pode me explicar melhor?"


7. CATEGORIZAÇÃO AUTOMÁTICA

Regras obrigatórias:
- comida → supermercado
- almoço, jantar, lanche → restaurante
- cabelo, barba → beleza
- uber, taxi, 99 → transporte
- gasolina, combustível → combustível
- netflix, prime, disney → streaming
- médico, dentista → saúde
- academia → academia
- cama, sofá, armário → casa/móveis
- delivery → delivery
- presentes → presentes
- cursos, estudos → educação
- viagem → viagem
- roupas → vestuário

8. FUNCIONALIDADES OBRIGATÓRIAS

1. Chat conversacional 100% funcional
2. Registro automático de gastos e receitas
3. Sistema completo de ciclos financeiros
4. Renomear e excluir ciclos
5. Histórico filtrado por ciclo
6. Resumo do ciclo com gráfico de pizza
7. Sidebar com todos os ciclos do usuário
8. Seleção de moeda no primeiro acesso
9. Relatórios anuais
10. Mensagem automática no início do ano
11. Dicas financeiras automáticas
12. Persistência completa via banco de dados


9. RELATÓRIO ANUAL

## Geração do relatório
O sistema deve consolidar:
- total de receitas do ano
- total de gastos do ano
- maiores categorias do ano
- top transações do ano
- mês com maior gasto
- média mensal
- ciclo com maior gasto
- comparação com ano anterior

## Quando gerar
- No primeiro login do novo ano
- Quando o usuário pedir: "relatório anual"
- Ao fechar um ciclo que cruza a virada do ano

## Mensagem obrigatória
"Seu relatório anual está pronto. Quer ver o resumo do ano anterior?"


10. BANCO DE DADOS

Tabelas necessárias:
- users / profiles
- settings
- cycles
- transactions
- chat_messages

## RLS
Todas as tabelas devem estar em modo PERMISSIVE.

## Constraints obrigatórias:
- transactions.cycle_id é obrigatório para gastos e receitas
- cycles.user_id obrigatório
- currency em profiles (BRL, EUR, USD)

## Índices
- user_id
- cycle_id
- occurred_at

11. CRITÉRIOS DE ACEITE / QA

O sistema é aceito somente se:
1. Receita registrada em “novo ciclo” for associada ao novo ciclo (não ao antigo).
2. Sidebar atualizar imediatamente após criar, renomear ou excluir ciclos.
3. Saldo nunca ficar negativo indevidamente.
4. Nome do usuário aparecer no header e nas mensagens apropriadas.
5. Seleção de moeda funcionar no onboarding.
6. A IA nunca assumir BRL sem escolha do usuário.
7. Relatório anual gerar com dados reais do usuário.
8. Nenhum erro causado por RLS.

````

### Interações com o Lovable

> Crie um App Financeiro de acordo com o PRD (Product Requirements Document) abaixo: {PRD}  

> No side bar a parte de ciclos não está atualizando mesmo após a criação de novos ciclos  

> Personalize as mensagens de gastos

**Aplicação final:** <https://poupai-finance.lovable.app>

***

## 🖼️ 2. Vídeo das Interações

https://github.com/user-attachments/assets/6f6a7b53-575a-4957-a4e4-d91752984ee4

***

## 📘 3. Resumo das Funcionalidades do PoupAI

### Registro de gastos e receitas via chat

O usuário digita mensagens como:

*   gastei 50 no mercado
*   paguei 20 uber
*   comprei uma cama por 547
*   recebi 2000 de salário

A IA interpreta automaticamente:

*   tipo da operação (gasto ou receita)
*   valor
*   descrição
*   categoria
*   moeda
*   associação ao ciclo financeiro ativo

A confirmação aparece no chat contendo valor, categoria, descrição e data.

### Ciclos financeiros personalizados

Em vez de meses fixos, o PoupAI usa ciclos definidos pelo usuário.

*   Ao registrar uma receita, o app pergunta se deseja criar um novo ciclo ou manter o ciclo atual.
*   Cada ciclo pode ser nomeado livremente (por exemplo: abril, férias, viagem, fevereiro).
*   Gastos sempre entram no ciclo ativo.
*   É possível renomear ou excluir ciclos.
*   Ao excluir, o usuário pode escolher entre remover as transações do ciclo ou reatribuí-las para outro ciclo.
*   A sidebar lista todos os ciclos com o saldo de cada um e permite navegação rápida.

### Resumo do ciclo com insights

Cada ciclo possui um painel com:

*   saldo do ciclo
*   total de receitas e total de gastos
*   gráfico de gastos por categoria
*   observações analíticas da IA sobre variações e tendências
*   comparação entre ciclo atual e ciclo anterior

***

## 💭 4. Reflexão Sobre o Processo

### O que funcionou bem

*   O Lovable interpretou bem PRDs longos e estruturados.
*   A geração automática de UI acelerou bastante o processo.
*   A integração entre chat, ciclos e banco funcionou bem após configurar RLS PERMISSIVE.
*   O design roxo/lilás saiu consistente.

### O que não funcionou como esperado

*   O Lovable inicialmente associou receitas ao ciclo errado.
*   RLS restritivo impedia inserções após login.
*   Criar novo ciclo não registrava a receita nele.
*   A moeda foi assumida como BRL antes de implementarmos a escolha inicial.

### O que aprendi sobre conversar com IAs

*   Quanto mais detalhado o PRD, menos correções são necessárias.
*   Especificar fluxos linha a linha evita bugs lógicos.
*   É melhor ser extremamente explícito com regras que parecem óbvias.

