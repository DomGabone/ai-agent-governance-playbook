# Playbook de governança para desenvolvimento com agentes de IA

Regras operacionais, modelos e rituais para construir software com agentes de IA como executores, mantendo o controle humano sobre o que importa: escopo, segurança, dados e decisões.

Este material foi consolidado ao longo de um produto real construído dessa forma e aparece aqui generalizado. Os exemplos usam um app fictício de agendamento para salões de beleza chamado Marcaí.

## Para quem é

Para quem dirige um agente de IA no dia a dia e percebeu que a ferramenta é rápida demais para ser deixada sem regras. O playbook parte de uma premissa: o agente escreve, a pessoa decide. Tudo aqui existe para que essa fronteira não se apague com o tempo.

## Os sete documentos

| Documento | O que resolve |
|---|---|
| [01 Fronteiras entre frontend e backend](docs/01-fronteiras-frontend-backend.md) | O que o agente nunca pode resolver no cliente, e como as integrações aparecem por capacidade de negócio em vez de por fornecedor. |
| [02 Registro de decisões](docs/02-registro-de-decisoes.md) | Um log vivo que substitui a memória da conversa. Modelo de entrada e três exemplos completos. |
| [03 Modelo de documentação](docs/03-modelo-de-documentacao.md) | Índice único, banner de status em cada arquivo, política de arquivar em vez de apagar. |
| [04 Execução segura](docs/04-execucao-segura.md) | Listar antes de executar, portões antes de operações irreversíveis, honestidade sobre o que foi ou não testado. |
| [05 Varredura contínua de segurança](docs/05-varredura-continua-de-seguranca.md) | O que roda a cada push, o que roda por sessão dedicada, e como se testa autorização de verdade. |
| [06 Modelo de maturidade](docs/06-modelo-de-maturidade.md) | Três eixos independentes para saber onde o produto está, sem confundir "lançável" com "completo". |
| [07 Espelho externo de tarefas](docs/07-espelho-externo-de-tarefas.md) | Como publicar a agenda em uma ferramenta externa sem vazar o que só o repositório pode conter. |

## Modelos prontos

- [templates/AGENTS.md](templates/AGENTS.md): arquivo de instruções para o agente, pronto para copiar para a raiz de um projeto.
- [templates/REGISTRO_DE_DECISOES.md](templates/REGISTRO_DE_DECISOES.md): esqueleto do log de decisões.
- [templates/ci-seguranca.yml](templates/ci-seguranca.yml): pipeline mínimo de segurança para GitHub Actions.

## Como adotar

1. Copie `templates/AGENTS.md` para a raiz do projeto e ajuste as seções marcadas.
2. Crie o registro de decisões a partir do modelo e escreva a primeira entrada: a decisão de adotar o registro.
3. Ative o pipeline de segurança. Ele falha em segredo commitado e em padrões perigosos no código do cliente.
4. Leia o documento 04 com o agente antes da primeira sessão de trabalho e cobre a regra de listar antes de executar.

## Princípios que atravessam tudo

- **O agente propõe, a pessoa aprova.** Nenhuma alteração de escopo, nenhuma operação irreversível e nenhum acesso novo sem confirmação explícita.
- **Verificar no código e no banco reais.** Afirmação de documento, de conversa anterior ou de outro agente é hipótese até ser confirmada.
- **Registrar tudo que mudou o rumo.** Se não está no registro de decisões, não aconteceu.
- **Dizer o que não foi feito.** Um item marcado como concluído sem teste real é pior do que um item aberto.
- **Segurança antes de conveniência.** Quando a solução rápida depende de confiar no cliente, ela está errada.

## Licença

MIT.
