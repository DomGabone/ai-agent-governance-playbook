# 01. Fronteiras entre frontend e backend

> Status: canônico. Domínio: arquitetura. Última revisão: 2026-09.

## Por que isso é a primeira regra

Um agente de IA resolve o problema que está na frente dele com o que tem à mão. Se a tela precisa saber se o usuário pode editar um registro, o agente vai verificar isso na tela. Funciona no teste, passa na revisão superficial e cria uma vulnerabilidade que só aparece quando alguém chama a API sem passar pela tela.

A fronteira existe para tirar essa decisão do agente. Ela não é uma preferência de arquitetura. É uma regra de segurança.

## O que pertence a cada lado

O frontend existe para:

- interface e experiência;
- estado local e cache local;
- roteamento;
- validação leve, que melhora a experiência mas nunca é a única barreira;
- consumo de contratos seguros;
- apresentação de resultados prontos.

O backend existe para:

- autenticação e autorização reais;
- políticas de acesso por linha;
- regras críticas de negócio;
- transações e escrita em múltiplas tabelas;
- pagamentos, webhooks e notificações transacionais;
- limites de uso e antifraude;
- segredos e chaves, em gerenciador do provedor ou em cofre cifrado do banco, lidos apenas por código de servidor;
- observabilidade e auditoria.

## O que nunca pode depender do cliente

- Criação de conta de negócio ou de qualquer estrutura que envolva mais de uma tabela.
- Atribuição de papéis e permissões.
- Decisão de pagamento, cálculo de valor final, aplicação de desconto.
- Processamento de webhook.
- Envio de e-mail ou de qualquer mensagem transacional.
- Chamada direta a provedor externo crítico.
- Qualquer verificação de segurança.

Se o agente propuser resolver um item dessa lista no cliente, a resposta é não, mesmo que a alternativa demore mais.

## Contratos por capacidade, não por fornecedor

No frontend, as integrações aparecem pelo que fazem para o negócio, e não por quem as fornece. Exemplos de capacidades:

- `identity`
- `catalog`
- `orders`
- `payments`
- `subscriptions`
- `notifications`
- `analytics`
- `export`

Cada capacidade tem uma interface no domínio e uma implementação na camada de dados. A tela conhece a interface. Trocar o fornecedor de pagamento, de push ou de banco não toca em nenhuma tela.

Isso também permite uma implementação falsa por capacidade, o que torna os testes de widget independentes de canal de plataforma e de rede.

## Exemplo no Marcaí

A tela de confirmação de agendamento mostra o valor do serviço. O valor que aparece vem de um snapshot calculado pelo backend no momento da reserva, não de uma multiplicação feita no app. Se o salão mudar o preço depois, o agendamento já feito mantém o valor combinado, e ninguém consegue alterar o total editando o estado local.

## Como o agente deve agir

1. Antes de implementar, classificar cada regra nova como "cliente" ou "servidor" usando as listas acima.
2. Se houver dúvida, é servidor.
3. Nunca criar uma rota, função ou política sem dizer explicitamente qual papel pode chamá-la.
4. Se encontrar lógica crítica no cliente durante outra tarefa, registrar o achado e não corrigir em silêncio. A correção é uma decisão da pessoa.
