# 03. Modelo de documentação

> Status: canônico. Domínio: governança. Última revisão: 2026-09.

## O problema

Projetos com agentes de IA produzem documentação em volume. Planos, auditorias, relatórios e listas de pendências se acumulam, e em poucas semanas ninguém sabe qual arquivo está valendo. O agente lê um plano de dois meses atrás e executa o que já foi descartado.

## As quatro regras

### 1. Um índice único

Existe um único arquivo de mapa da documentação. Todo documento está listado nele, com uma linha de descrição e o status. Um documento que não está no mapa não existe para o agente.

### 2. Banner de status em todo arquivo

Toda primeira linha útil de um documento declara:

- **Status:** canônico, em revisão, superado ou arquivado.
- **Domínio:** segurança, arquitetura, produto, dados, usabilidade, pendências, comunicação.
- **Última revisão:** ano e mês.

O agente é instruído a ignorar documentos superados e arquivados, a menos que a tarefa seja explicitamente histórica.

### 3. Arquivar, nunca apagar

Documento superado vai para uma pasta de arquivo, com o status trocado no banner e uma linha no topo apontando para o que o substituiu. O histórico de por que algo foi pensado de certa forma é parte do produto.

### 4. Pendências em um lugar só

Pode haver vários documentos de análise, mas a lista do que falta fazer é uma. Cada item tem identificador, dependência declarada e estado. Estados possíveis: aberta, em andamento, concluída, abandonada. "Abandonada" existe para que uma tarefa possa ser descartada conscientemente em vez de ficar aberta para sempre.

## Estrutura sugerida

```
docs/
  MAPA.md                     índice único
  REGISTRO_DE_DECISOES.md     ver documento 02
  PENDENCIAS.md               lista única
  arquitetura/
  seguranca/
  produto/
  arquivo/                    superados, com banner e ponteiro
```

## O que a documentação não é

- Não é o lugar de segredos, credenciais ou URLs de ambientes internos.
- Não é o lugar de dados pessoais de usuários de teste.
- Não substitui o registro de decisões. Um plano diz o que se pretende; o registro diz o que foi decidido.

## Ritual de fim de sessão

Antes de encerrar qualquer sessão de trabalho que tenha produzido ou alterado documentos:

1. Atualizar o banner dos arquivos tocados.
2. Conferir que todos estão no mapa.
3. Registrar no log de decisões o que mudou de rumo.
4. Atualizar a lista única de pendências.
