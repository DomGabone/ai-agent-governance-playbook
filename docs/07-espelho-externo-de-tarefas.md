# 07. Espelho externo de tarefas

> Status: canônico. Domínio: governança e privacidade. Última revisão: 2026-09.

## O que é

Uma cópia superficial da lista de pendências em uma ferramenta externa de agenda, como um quadro ou banco de dados de tarefas, para acompanhamento fora do editor de código.

## A regra em uma frase

O espelho é agenda, não documentação. Ele recebe título, estado e prazo. Nunca recebe conteúdo.

## O que nunca sai do repositório

- Trecho de código, nome de função, nome de tabela, nome de rota.
- Achado de segurança, mesmo já corrigido.
- Credencial, URL de ambiente, identificador de projeto em provedor.
- Dado de usuário, inclusive de conta de teste.
- Descrição técnica de vulnerabilidade ou de plano de correção.
- Decisão de produto ainda não anunciada.

## O que pode sair

- Título curto da tarefa, escrito para quem não é técnico.
- Estado: aberta, em andamento, concluída, abandonada.
- Prazo e responsável.
- Marcador de domínio: segurança, produto, dados, comunicação.

## Duas visibilidades

- **Normal:** tarefas que qualquer pessoa da equipe pode ver.
- **Pessoal:** tarefas que dependem de ação humana exclusiva, como configurar painel de provedor, assinar contrato ou tomar decisão de produto. Estas aparecem só para quem decide.

## Como a promessa de não vazar se sustenta

1. O script de sincronização só lê a lista de pendências, nunca outros documentos.
2. Ele exporta campos fixos: título, estado, prazo, domínio, visibilidade.
3. Uma lista de termos proibidos é conferida antes do envio. Título com nome de tabela, de função ou de provedor é rejeitado.
4. A sincronização roda ao fim de toda sessão que alterou pendências, como regra permanente, não como pedido.

## Limites conhecidos

- O espelho não tem histórico. Quem precisa saber por que uma tarefa existe volta ao repositório.
- Uma tarefa abandonada no repositório precisa ser marcada como abandonada no espelho, nunca apagada, para não parecer que sumiu.
