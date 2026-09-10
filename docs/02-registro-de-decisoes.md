# 02. Registro de decisões

> Status: canônico. Domínio: governança. Última revisão: 2026-09.

## O problema que ele resolve

Uma conversa com um agente de IA não tem memória entre sessões. O que foi decidido na terça não existe na quinta, e o agente vai propor de novo a solução que já foi recusada. Pior: várias sessões podem trabalhar em paralelo sem saber uma da outra.

O registro de decisões é a memória compartilhada. Ele é obrigatório, é lido no início de toda sessão e é a única fonte que vale quando dois documentos discordam.

## Regras

- **Toda decisão que muda o rumo entra aqui.** Escopo, arquitetura, segurança, remoção de funcionalidade, adiamento consciente.
- **Achado também é decisão.** Um bug crítico descoberto no caminho vira entrada, mesmo que a correção tenha sido imediata.
- **Numeração sequencial e nunca reutilizada.** Se duas sessões colidirem no mesmo número, a segunda renumera e registra a colisão.
- **Nada é apagado.** Decisão revertida ganha uma entrada nova que aponta para a antiga.
- **O agente escreve a entrada, a pessoa aprova o texto.** Uma decisão registrada pelo agente sem aprovação é um rascunho.

## Modelo de entrada

```markdown
## ADR-000 - Título curto no infinitivo ou no substantivo

**Data:** AAAA-MM-DD
**Contexto:** o que estava acontecendo e por que a questão surgiu.
**Decisão:** o que foi decidido, em uma ou duas frases.
**Alternativas descartadas:** o que foi considerado e por que perdeu.
**Consequências:** o que muda no código, nos dados, no processo. O que precisa ser feito depois.
**Verificação:** como se confirmou que a decisão foi aplicada. "Não verificado" é uma resposta válida e obrigatória quando for o caso.
**Relacionadas:** ADR-xxx, ADR-yyy.
```

## Três exemplos completos, no Marcaí

### ADR-001 - Adotar o registro de decisões como fonte viva

**Data:** 2026-03-02
**Contexto:** duas sessões de trabalho em dias seguidos propuseram a mesma refatoração de roteamento, e a segunda desfez parte da primeira sem perceber.
**Decisão:** todo início de sessão começa pela leitura deste arquivo. Nenhuma refatoração estrutural sem entrada aqui.
**Alternativas descartadas:** manter o histórico só nos commits. Descartada porque o agente não lê o histórico do git por conta própria e a mensagem de commit não carrega o "por quê".
**Consequências:** o arquivo de instruções do agente ganha a regra de leitura obrigatória. O modelo de entrada acima passa a ser exigido.
**Verificação:** a sessão seguinte abriu com a leitura do registro e citou a ADR-001 antes de propor mudanças.
**Relacionadas:** nenhuma.

### ADR-014 - O valor do agendamento é congelado pelo backend na reserva

**Data:** 2026-04-18
**Contexto:** durante a revisão da tela de confirmação, o agente encontrou o cálculo do total sendo feito no app, a partir do preço atual do serviço. Uma mudança de preço no salão alterava agendamentos já feitos.
**Decisão:** o backend grava um snapshot do valor no momento da reserva. O app só exibe.
**Alternativas descartadas:** manter o cálculo no app e adicionar validação no envio. Descartada porque a validação no cliente não é barreira.
**Consequências:** nova coluna de valor congelado na tabela de agendamentos, migração de dados para os registros existentes, remoção do cálculo no app. Achado registrado como vulnerabilidade de integridade, não só como bug.
**Verificação:** teste manual na interface real com dois usuários: alteração de preço depois da reserva não muda o total exibido nem o total cobrado.
**Relacionadas:** ADR-002 (fronteiras), ADR-015 (auditoria de integridade de preço).

### ADR-031 - Remoção do módulo de fidelidade por pontos

**Data:** 2026-06-09
**Contexto:** o módulo existia desde o início, nunca foi ativado por nenhum salão e mantinha quatro tabelas, seis funções e duas telas. A remoção envolvia apagar dados irreversivelmente.
**Decisão:** remover o módulo por completo, com portão de aprovação explícita antes de executar a migração destrutiva.
**Alternativas descartadas:** desativar por flag e manter o código. Descartada porque código morto com acesso a dados é superfície de ataque sem benefício.
**Consequências:** migração destrutiva escrita e revisada antes de ser executada. Backup do banco confirmado. Documentação do módulo arquivada, não apagada.
**Verificação:** a migração foi executada só depois do "pode executar" escrito pela pessoa responsável. Dois efeitos não previstos no script original foram encontrados no caminho e corrigidos antes da execução.
**Relacionadas:** ADR-004 (arquivar em vez de apagar), ADR-030 (inventário de código morto).

## Sinais de que o registro está funcionando

- O agente cita entradas pelo número ao justificar uma proposta.
- Uma sessão nova consegue continuar o trabalho de outra sem repetir perguntas.
- Quando algo dá errado, a pergunta "por que fizemos isso" tem resposta em menos de um minuto.
