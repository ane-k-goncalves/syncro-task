# Product Requirements Document (PRD)

**Projeto:** Gerenciador de Projetos e Atividades
**Versão:** 1.0.0
**Última atualização:** 2026-09-20

> Este documento é a fonte da verdade sobre o que o produto faz. Tecnologia é
> assunto do `architecture.md`.

## 1. Visão Geral e Objetivo

**O problema:** Programadores, estudantes, professores e pesquisadores precisam
acompanhar vários projetos e atividades, mas podem perder informações e prazos
quando não têm um local centralizado para organizá-los.

**A solução:** Uma aplicação web que reúne projetos em um só lugar, permitindo
registrar atividades, organizar seus status em um quadro Kanban e acompanhar o
progresso e os prazos. Um plano pago libera métricas avançadas do projeto.

**Como saberemos que deu certo:** O usuário consegue localizar seus projetos,
visualizar as atividades por status no Kanban, identificar pendências e atrasos
 e acompanhar o progresso até a conclusão.

## 2. Glossário Ubíquo

| Termo | Significa | Não confundir com |
| :---- | :-------- | :---------------- |
| Projeto | Conjunto organizado que reúne atividades, checklists e o acompanhamento no Kanban. | Atividade individual, checklist ou coluna do Kanban. |
| Atividade | Tarefa independente que o usuário precisa realizar e que pode virar um card no Kanban. | Projeto ou coluna de status. |
| Checklist | Lista de coisas a fazer; neste sistema, seus itens são atividades independentes. | Projeto ou coluna do Kanban. |
| Kanban | Quadro visual que organiza as atividades por status. | Atividade ou projeto inteiro. |
| A fazer | Atividade ainda não iniciada. | Em andamento ou concluído. |
| Em andamento | Atividade que está sendo executada. | A fazer ou concluído. |
| Concluído | Atividade finalizada. | Atividade pendente. |

## 3. Atores e Permissões

| Ator | Quem é | Pode | Não pode |
| :--- | :----- | :--- | :------- |
| Usuário dono | Pessoa proprietária de um projeto. | Criar, editar e excluir projetos e atividades; gerenciar o Kanban; convidar pessoas e definir permissões. | Não possui restrições dentro dos próprios projetos. |
| Colaborador | Pessoa autorizada a colaborar em um projeto. | Criar e gerenciar atividades e alterar seus status no Kanban. | Criar, editar ou excluir projetos; gerenciar permissões. |
| Convidado | Pessoa autorizada apenas a acompanhar um projeto. | Visualizar projetos, atividades e status. | Criar, editar, excluir ou mover atividades. |

## 4. Escopo Funcional (User Stories)

> Toda story nasce `Draft`; só o aluno a promove para `Ready`. `Live` significa
> que o Pull Request da história foi mesclado.

### US01 — Criar conta · `Must Have` · `S` · Status: `⚪ Draft`

**Como** usuário, **eu quero** criar uma conta informando nome, e-mail e senha,
**para que** eu possa acessar a aplicação e organizar meus projetos e atividades.

**Critérios de aceite:**

- [ ] Dado que nome, e-mail e senha são válidos e o e-mail não está cadastrado, quando o usuário confirmar o cadastro, então a conta será criada e ele entrará automaticamente na aplicação.
- [ ] Dado que o e-mail já está cadastrado, quando o usuário tentar criar a conta, então o sistema exibirá uma mensagem de erro e não criará uma nova conta.
- [ ] Dado que algum dado obrigatório é inválido ou está ausente, quando o usuário tentar criar a conta, então o sistema exibirá uma mensagem de erro e não criará a conta.

**Regras relacionadas:** RN01, RN02, RN03

### US02 — Criar projeto · `Must Have` · `S` · Status: `⚪ Draft`

**Como** usuário dono, **eu quero** criar um projeto informando um nome,
**para que** eu possa reunir e organizar minhas atividades.

**Critérios de aceite:**

- [ ] Dado que o nome foi informado e ainda não existe outro projeto com esse nome para o usuário, quando ele confirmar, então o projeto será criado.
- [ ] Dado que o nome está vazio ou já existe para o usuário, quando ele tentar criar o projeto, então o sistema impedirá a criação e exibirá uma mensagem de erro.
- [ ] Dado que o usuário não possui permissão de criação, quando tentar criar um projeto, então o sistema impedirá a operação.

**Regras relacionadas:** RN04, RN05

### US03 — Criar quadro Kanban automaticamente · `Must Have` · `S` · Status: `⚪ Draft`

**Como** usuário dono, **eu quero** que um quadro Kanban seja criado automaticamente ao criar um projeto, **para que** eu possa organizar as atividades desde o início.

**Critérios de aceite:**

- [ ] Dado que o usuário cria um projeto com sucesso, quando o sistema concluir a criação, então um quadro Kanban será criado automaticamente.
- [ ] Dado que o quadro foi criado, então ele conterá as colunas A fazer, Em andamento e Concluído.
- [ ] Dado que a criação do projeto falhou, quando o sistema processar a operação, então não deverá criar um quadro Kanban incompleto ou sem projeto associado.

**Regras relacionadas:** RN05

### US04 — Criar atividade · `Should Have` · `L` · Status: `⚪ Draft`

**Como** usuário dono ou colaborador, **eu quero** criar uma atividade dentro de um projeto, informando título, descrição, prazo e responsável, **para que** eu possa organizar o trabalho do projeto.

**Critérios de aceite:**

- [ ] Dado que o usuário tem permissão no projeto e informa um título, descrição, prazo e responsável válido, quando confirmar, então a atividade será criada.
- [ ] Dado que o título está vazio ou o responsável não pertence ao projeto, quando tentar criar a atividade, então o sistema impedirá a criação e exibirá uma mensagem de erro.
- [ ] Dado que o usuário é convidado ou não participa do projeto, quando tentar criar uma atividade, então o sistema impedirá a operação.
- [ ] Dado que a atividade foi criada, então ela ficará disponível no quadro Kanban do projeto, inicialmente na coluna A fazer.

**Regras relacionadas:** RN06, RN07, RN08

### US05 — Visualizar projetos · `Must Have` · `S` · Status: `⚪ Draft`

**Como** usuário autenticado, **eu quero** visualizar os projetos dos quais sou dono, colaborador ou convidado, **para que** eu possa acessar rapidamente os projetos que acompanho.

**Critérios de aceite:**

- [ ] Dado que o usuário possui projetos associados, quando acessar sua lista de projetos, então verá apenas projetos em que é dono, colaborador ou convidado.
- [ ] Dado que o usuário não possui projetos associados, quando acessar a lista, então verá uma mensagem informando que ainda não há projetos disponíveis.
- [ ] Dado que existe um projeto ao qual o usuário não pertence, quando acessar a lista, então esse projeto não será exibido.

**Regras relacionadas:** RN03, RN19

### US06 — Gerenciar projeto · `Should Have` · `M` · Status: `⚪ Draft`

**Como** usuário dono, **eu quero** editar ou excluir meus projetos, **para que** eu possa manter meus projetos atualizados ou remover os que não utilizo mais.

**Critérios de aceite:**

- [ ] Dado que o usuário é dono do projeto, quando editar o nome ou a descrição e confirmar, então as alterações serão salvas.
- [ ] Dado que o usuário é dono do projeto, quando solicitar a exclusão e confirmar a ação, então o projeto será removido.
- [ ] Dado que o usuário é colaborador ou convidado, quando tentar editar ou excluir o projeto, então o sistema impedirá a operação e exibirá uma mensagem de erro.
- [ ] Dado que o usuário solicita exclusão mas cancela a confirmação, então o projeto permanecerá intacto.

**Regras relacionadas:** RN01, RN10

### US07 — Comprar plano com recursos avançados · `Must Have` · `L` · Status: `⚪ Draft`

**Como** usuário autenticado, **eu quero** comprar o plano de recursos avançados por R$ 14,99, **para que** eu possa acessar as métricas do projeto.

**Critérios de aceite:**

- [ ] Dado que o usuário escolhe o plano, quando iniciar a compra, então o servidor criará um pedido de pagamento de R$ 14,99 no Mercado Pago sandbox.
- [ ] Dado que o gateway retorna os dados de checkout, quando o usuário prosseguir, então ele será direcionado ao fluxo de pagamento do Mercado Pago.
- [ ] Dado que o pagamento for aprovado, quando o Mercado Pago enviar o webhook assinado, então o sistema validará a assinatura e atualizará o pagamento e o pedido para aprovados.
- [ ] Dado que o pagamento for recusado ou pendente, então o sistema manterá o pedido no estado correspondente e informará o usuário.
- [ ] Dado que o usuário fechar o checkout ou a notificação ainda não chegar, então o pedido permanecerá pendente e poderá ser consultado posteriormente.
- [ ] Dado que o usuário já possui uma compra aprovada do plano, quando tentar comprar novamente, então o sistema impedirá uma cobrança duplicada.

**Regras relacionadas:** RN13, RN14, RN15, RN16

### US08 — Gerenciar permissões · `Must Have` · `M` · Status: `⚪ Draft`

**Como** usuário dono, **eu quero** alterar o papel ou remover o acesso de pessoas do projeto, **para que** eu possa controlar quem pode colaborar ou apenas visualizar.

**Critérios de aceite:**

- [ ] Dado que o usuário é dono, quando alterar o papel de uma pessoa entre colaborador e convidado, então a nova permissão será aplicada.
- [ ] Dado que o usuário é dono, quando remover uma pessoa do projeto, então ela perderá acesso aos projetos e atividades.
- [ ] Dado que o usuário é colaborador ou convidado, quando tentar alterar permissões, então o sistema impedirá a operação e exibirá uma mensagem de erro.
- [ ] Dado que o usuário tenta alterar o papel de outro dono, então o sistema impedirá a operação.

**Regras relacionadas:** RN02, RN03

### US09 — Atualizar status da atividade · `Must Have` · `M` · Status: `⚪ Draft`

**Como** usuário dono ou colaborador, **eu quero** mover uma atividade entre as colunas do Kanban, **para que** eu possa acompanhar seu progresso.

**Critérios de aceite:**

- [ ] Dado que o usuário é dono ou colaborador do projeto, quando mover uma atividade, então o sistema atualizará o status para A fazer, Em andamento ou Concluído.
- [ ] Dado que o usuário é convidado, quando tentar mover uma atividade, então o sistema impedirá a operação e exibirá uma mensagem de erro.
- [ ] Dado que a atividade foi movida para Concluído, então ela será contabilizada como concluída nas métricas do projeto.
- [ ] Dado que o usuário mover uma atividade para outra coluna, então a alteração permanecerá salva ao recarregar o projeto.

**Regras relacionadas:** RN08, RN09, RN18

### US10 — Convidar participante · `Must Have` · `M` · Status: `⚪ Draft`

**Como** usuário dono, **eu quero** convidar uma pessoa por e-mail e escolher entre colaborador ou convidado, **para que** eu possa permitir sua participação no projeto.

**Critérios de aceite:**

- [ ] Dado que o usuário é dono, quando informar um e-mail e um papel válido, então o sistema enviará um convite por e-mail.
- [ ] Dado que a pessoa aceita o convite, quando ainda não possuir conta, então o sistema permitirá criar a conta e associará o papel escolhido ao projeto.
- [ ] Dado que a pessoa já possui conta, quando aceitar o convite, então será associada ao projeto com o papel escolhido.
- [ ] Dado que o usuário é colaborador ou convidado, quando tentar enviar convite, então o sistema impedirá a operação e exibirá uma mensagem de erro.
- [ ] Dado que o convite já foi enviado para o mesmo projeto e e-mail, quando o dono tentar reenviá-lo, então o sistema impedirá convites duplicados.

**Regras relacionadas:** RN02, RN03, RN11, RN12

### US11 — Visualizar métricas do projeto · `Must Have` · `M` · Status: `⚪ Draft`

**Como** usuário com o plano avançado aprovado, **eu quero** visualizar métricas do meu projeto, **para que** eu possa acompanhar seu progresso.

**Critérios de aceite:**

- [ ] Dado que o usuário possui o plano aprovado, quando acessar as métricas de um projeto, então verá a quantidade de atividades por status.
- [ ] Então também verá a quantidade de atividades concluídas, a quantidade de atividades atrasadas e o percentual geral de conclusão.
- [ ] Dado que o pagamento não foi aprovado, quando o usuário tentar acessar as métricas, então o sistema bloqueará o acesso e informará que o recurso exige o plano avançado.
- [ ] Dado que não existem atividades no projeto, quando o usuário acessar as métricas, então o sistema exibirá valores zerados e percentual de conclusão igual a 0%.

**Regras relacionadas:** RN17, RN18, RN19

## 5. Regras de Negócio (Constraints)

| ID | Regra |
| :-- | :---- |
| RN01 | Somente o usuário dono pode editar ou excluir um projeto. |
| RN02 | Somente o dono pode alterar permissões; colaboradores podem apenas gerenciar atividades. |
| RN03 | Convidados podem apenas visualizar projetos, atividades e status. |
| RN04 | O nome do projeto é obrigatório e não pode se repetir entre os projetos do mesmo dono. |
| RN05 | Ao criar um projeto com sucesso, o sistema deve criar automaticamente um Kanban com as colunas A fazer, Em andamento e Concluído. |
| RN06 | Dono e colaboradores podem criar e gerenciar atividades; convidados não podem alterá-las. |
| RN07 | O responsável por uma atividade deve ser o dono ou um colaborador do mesmo projeto. |
| RN08 | Toda atividade criada deve iniciar na coluna A fazer. |
| RN09 | Apenas dono e colaboradores podem mover atividades entre as colunas do Kanban. |
| RN10 | A exclusão de um projeto deve remover também suas atividades e seu quadro Kanban. |
| RN11 | Apenas o dono pode convidar pessoas e escolher entre os papéis colaborador e convidado. |
| RN12 | Um convite aceito por uma pessoa sem conta deve permitir a criação da conta durante o aceite. |
| RN13 | O plano avançado custa R$ 14,99 em compra única e é processado pelo Mercado Pago em sandbox. |
| RN14 | O pedido só pode ser marcado como aprovado após um webhook válido e assinado do Mercado Pago. |
| RN15 | Um pagamento pendente ou recusado não libera os recursos avançados. |
| RN16 | Um usuário que já possui uma compra aprovada do plano não pode gerar uma cobrança duplicada. |
| RN17 | As métricas avançadas só ficam disponíveis após a aprovação do pagamento. |
| RN18 | As métricas devem mostrar atividades por status, concluídas, atrasadas e percentual de conclusão. |
| RN19 | Se o projeto não possuir atividades, as métricas devem mostrar zero atividades e 0% de conclusão. |

## 6. Fora de Escopo (Non-goals)

- Aplicativo mobile, pois o projeto terá inicialmente apenas uma aplicação web.
- Integração com outros gateways além do Mercado Pago.
- Colaboração em tempo real.
- Notificações automáticas.

## 7. Requisitos Não Funcionais (Qualidade)

- **RNF01 — Segurança:** somente usuários autenticados poderão acessar seus projetos; cada ação deverá respeitar o papel do usuário.
- **RNF02 — Proteção de dados:** senhas e credenciais do Mercado Pago não poderão ser expostas ou armazenadas em texto aberto.
- **RNF03 — Responsividade:** a aplicação web deverá funcionar em telas de desktop e mobile pelo navegador.
- **RNF04 — Validação:** dados obrigatórios e inválidos deverão ser rejeitados com mensagens claras.
- **RNF05 — Consistência:** alterações em projetos, atividades, permissões e pagamentos deverão permanecer salvas após recarregar a aplicação.
- **RNF06 — Usabilidade:** o usuário deverá conseguir identificar facilmente o status das atividades e os prazos.
- **RNF07 — Acessibilidade:** as principais ações e mensagens deverão ser utilizáveis por teclado e compreensíveis por leitores de tela.
- **RNF08 — Privacidade:** um usuário não poderá consultar dados de projetos aos quais não pertence.

## 8. Histórico

| Data | Versão | O que mudou |
| :--- | :----- | :---------- |
| 2026-09-20 | 1.0.0 | Versão inicial definida na entrevista do `/utf-prd` |
