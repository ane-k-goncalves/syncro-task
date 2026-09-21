# Tokens de Design

**Projeto:** Gerenciador de Projetos e Atividades
**Versão:** 1.0.0
**Última atualização:** 2026-09-20

> Este documento define os papéis visuais mínimos para manter consistência entre
> as telas do produto.

## Paleta

| Token | Valor | Onde se usa |
| --- | --- | --- |
| `primaria` | `#0F766E` | ações principais |
| `superficie` | `#F8FAFC` | fundo de cards e painéis |
| `texto` | `#17202A` | texto padrão |
| `texto-suave` | `#64748B` | legendas e apoio |
| `perigo` | `#E11D48` | erro e exclusão |
| `sucesso` | `#15803D` | confirmação e conclusão |
| `desabilitado` | `#CBD5E1` | controle inativo |

## Escala de espaçamento

| Token | Valor |
| --- | --- |
| `xs` | `4px` |
| `sm` | `8px` |
| `md` | `16px` |
| `lg` | `24px` |
| `xl` | `32px` |

## Tipografia

| Token | Família · tamanho · peso | Papel |
| --- | --- | --- |
| `titulo-pagina` | Plus Jakarta Sans · `32px` · `700` | título principal |
| `titulo-secao` | Plus Jakarta Sans · `24px` · `700` | títulos de seções |
| `titulo-card` | Plus Jakarta Sans · `18px` · `600` | títulos de projetos e cards |
| `corpo` | Plus Jakarta Sans · `16px` · `400` | texto padrão |
| `legenda` | Plus Jakarta Sans · `14px` · `400` | apoio e metadados |

## Estados de botão

| Estado | Aparência |
| --- | --- |
| normal | Fundo `primaria`, texto branco e contraste alto. |
| hover | Fundo `#0B5F59`, mantendo o texto branco. |
| foco (teclado) | Contorno visível de `3px` em `#F59E0B`, sem remover o indicador padrão. |
| desabilitado | Fundo `desabilitado`, texto `texto-suave` e sem interação. |
| carregando | Fundo `primaria`, texto ou ícone de carregamento e cliques bloqueados. |

## Protótipo

**Link:** Pendente — ainda não existe protótipo em Figma, Stitch ou ferramenta equivalente.

**Telas previstas:**

- Lista de projetos;
- Detalhes do projeto com quadro Kanban;
- Criação de atividade;
- Área de compra do plano avançado;
- Métricas do projeto.
