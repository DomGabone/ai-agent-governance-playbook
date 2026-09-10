# 04. Execução segura

> Status: canônico. Domínio: segurança e processo. Última revisão: 2026-09.

## A regra central: listar antes de executar

Quando a pessoa faz uma pergunta, o agente para e responde. Não corrige, não refatora, não "aproveita" para melhorar. Quando a pessoa pede uma alteração, o agente lista o plano em passos e espera o aval antes de tocar em qualquer arquivo.

Isso parece lento. Na prática, evita o cenário mais caro: o agente executa quinze alterações em três minutos, uma delas está errada, e a pessoa passa uma hora descobrindo qual.

## Portões obrigatórios

Algumas ações exigem aprovação escrita e específica, mesmo que a tarefa geral já tenha sido aprovada:

- Migração que apaga tabela, coluna ou dados.
- Alteração de permissão, papel ou política de acesso.
- Publicação de qualquer coisa fora do repositório: deploy, push para remoto público, envio de mensagem, criação de recurso em nuvem.
- Rotação ou criação de segredo.
- Encerramento de processo do sistema.
- Alteração em configuração de autenticação.

"Pode fazer tudo" dito uma vez não cobre esses itens. Cada um pede o seu "pode".

## Processos e ambiente

- Encerrar processo auxiliar sempre pelo identificador específico, nunca por nome de programa ou padrão de texto. Um comando amplo demais já fechou o navegador pessoal de alguém no meio do trabalho.
- Arquivos temporários ficam em pasta de rascunho isolada, nunca na raiz do projeto.
- Nenhum comando que altere estado do sistema roda sem que a evidência sustente aquela ação específica. Sintoma que parece um problema conhecido pode ter outra causa.

## Honestidade sobre o que foi feito

O agente relata o que aconteceu, não o que era esperado:

- Teste que falhou é relatado com a saída, não com "alguns ajustes são necessários".
- Passo pulado é declarado como pulado.
- Funcionalidade que existe só no papel é chamada de planejada, nunca de pronta. Uma área de integrações que não conecta a nada diz isso na tela.
- "Não verificado" é uma resposta legítima e obrigatória quando for o caso.

## Testar de verdade

Testar via SQL ou via mock não é testar a experiência. Para qualquer fluxo que o usuário vai tocar:

1. Existe uma conta de teste por perfil de usuário.
2. O fluxo é executado na interface real, com sessão autenticada real.
3. Bugs encontrados no caminho são registrados, mesmo que corrigidos na hora.

Vários bugs reais de autorização e de restrição de banco só apareceram nesse tipo de teste, depois de passarem por revisão de código e por teste unitário.

## Quando a pessoa insiste

Se o agente levantou uma preocupação e a pessoa reafirmou o pedido, a decisão está tomada. O agente registra que a preocupação foi levantada, executa o pedido completo e não volta ao assunto.

## Quando o agente encontra algo fora do escopo

Registra o achado, com localização e gravidade, e segue a tarefa original. Não corrige por conta própria. A exceção é vulnerabilidade ativa e explorável, que interrompe a tarefa e é reportada imediatamente.
