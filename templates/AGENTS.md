# Instruções para o agente

> Copie este arquivo para a raiz do projeto. Ajuste as seções marcadas com [ajustar].

## Leitura obrigatória no início de toda sessão

1. `docs/REGISTRO_DE_DECISOES.md`, do fim para o início, até a última entrada que você já conhece.
2. `docs/MAPA.md`, para saber quais documentos estão valendo.
3. `docs/PENDENCIAS.md`, para saber o que está aberto e o que depende de quê.

## Regras permanentes

- Pergunta da pessoa responsável é um sinal de parada. Responda e espere.
- Pedido de alteração começa com um plano em passos. Execute só depois do aval.
- Nunca resolva no cliente o que é papel do servidor. Ver `docs/01-fronteiras-frontend-backend.md`.
- Nunca execute migração destrutiva, alteração de permissão, publicação externa ou criação de segredo sem aprovação específica para aquela ação.
- Encerre processos pelo identificador, nunca por nome ou padrão.
- Registre no log de decisões tudo que mudou o rumo, inclusive achados.
- Relate o que aconteceu, não o que era esperado. Teste que falhou é relatado com a saída.
- Texto visível ao usuário, documentação e mensagens de commit em [ajustar: idioma e norma].

## Fronteiras deste projeto

- Camada de dados: [ajustar: pasta ou pacote que pode falar com o backend].
- Cliente de backend permitido apenas em: [ajustar].
- Segredos vivem em: [ajustar: gerenciador de segredos do provedor ou cofre cifrado do banco]. Nunca no repositório, nunca no código do cliente, nunca alcançáveis por papel que o cliente consiga assumir.
- Ambientes: [ajustar: nomes, sem URLs].

## Contas de teste

Uma por perfil de usuário. Credenciais fora do repositório, em [ajustar]. Todo fluxo tocado pelo usuário é testado na interface real, com sessão autenticada real, antes de ser marcado como concluído.

## Fim de sessão

1. Atualizar banners dos documentos tocados.
2. Conferir o mapa.
3. Registrar decisões.
4. Atualizar pendências.
5. Sincronizar o espelho externo de tarefas, se existir.
