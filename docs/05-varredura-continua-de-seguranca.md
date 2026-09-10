# 05. Varredura contínua de segurança

> Status: canônico. Domínio: segurança. Última revisão: 2026-09.

## Três camadas

A varredura acontece em três lugares, com frequências diferentes.

### Camada 1: a cada push, automática

Roda no CI e bloqueia o merge:

- **Varredura de segredos** no histórico completo do repositório.
- **Padrões perigosos** no código do cliente, por busca textual: referência a chave de serviço, cliente de banco fora da camada de dados, chamada direta a provedor externo.
- **Trava de arquivo de ambiente**: o pipeline falha se um arquivo de variáveis de ambiente estiver versionado.
- **Formatação, análise estática e testes.**

O modelo em `templates/ci-seguranca.yml` implementa essa camada.

### Camada 2: por sessão dedicada, semanal

Precisa de credencial de projeto e roda melhor em uma sessão só para isso:

- Relatório de segurança e desempenho do provedor de banco.
- Inventário de funções executáveis por cada papel, consultado no catálogo do banco e não nos scripts.
- Revisão de políticas de acesso por tabela: toda tabela tem política, toda política tem justificativa.
- Diferença entre o esquema real e as migrações versionadas.

### Camada 3: auditoria lógica, por rodada

Leitura de cada função exposta pela API com a pergunta: "o que acontece se quem chama for hostil". Verifica ordem das checagens de autorização, tratamento de nulo, escopo de dados devolvidos e efeitos colaterais.

Achados são classificados em P0 (explorável agora), P1 (explorável com condição), P2 (má prática sem exploração conhecida).

## Lições que viraram regra

- **Revogar de PUBLIC não revoga de um papel específico.** Só o catálogo do banco diz o que cada papel consegue executar.
- **Truncar tabela ignora política de linha.** Privilégio de tabela é a única defesa.
- **Nulo dentro de condição em função de banco passa em silêncio.** Toda asserção de autorização envolve o resultado em coalesce com falso.
- **Segurança por definer exige caminho de busca fixo** e nomes totalmente qualificados.
- **Trilha de auditoria imutável por permissão**, não por combinado.

## Testar autorização de verdade

Teste de política de acesso com mock não prova nada. O teste real:

1. Abre sessão com o papel e a identidade do usuário, do jeito que a API faria.
2. Tenta a operação proibida e espera a exceção de privilégio.
3. Tenta a operação permitida e confere que aconteceu.
4. Confere que a trilha de auditoria registrou quem fez.

Esses testes rodam contra um banco real no CI, em contêiner limpo, a cada push.

## Resposta a achado

1. Registrar no log de decisões com gravidade.
2. Se P0, corrigir antes de qualquer outra tarefa.
3. Escrever a asserção que teria pegado o problema, para que não volte.
4. Procurar o mesmo padrão no resto do código. Um achado raramente é único.
