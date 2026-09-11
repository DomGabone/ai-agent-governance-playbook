# 06. Modelo de maturidade em três eixos

> Status: canônico. Domínio: produto e arquitetura. Última revisão: 2026-09.

## Por que três eixos e não uma nota

"Está pronto?" é uma pergunta sem resposta útil. Um produto pode estar pronto para a loja de aplicativos e longe de ser completo. Pode ser completo e não aguentar cem usuários simultâneos. Os três eixos são independentes de propósito, para que ninguém confunda um com o outro.

## Eixo A: prontidão de lançamento

Mede se o produto pode ser publicado e usado por estranhos sem constrangimento.

| Nível | Critério |
|---|---|
| A0 | Roda só na máquina de quem desenvolve. |
| A1 | Build de release assinado com chave de produção nas plataformas alvo. |
| A2 | Termos, privacidade e permissões de sistema declarados e coerentes com o que o app faz. |
| A3 | Contas de loja criadas, fichas preenchidas, revisão de loja aprovada. |
| A4 | Publicado, com canal de suporte e processo de atualização. |

Armadilha comum: build de release assinado com chave de depuração. Passa em todo teste e falha na loja.

## Eixo B: completude de produto

Mede se o produto faz tudo que promete para cada perfil de usuário.

| Nível | Critério |
|---|---|
| B0 | Telas existem, mas os dados são estáticos ou simulados. |
| B1 | Fluxo principal de cada perfil funciona de ponta a ponta com dados reais. |
| B2 | Nenhuma tela promete o que não entrega. Tudo que é "em breve" está oculto ou rotulado. |
| B3 | Estatísticas, exportações e integrações reais para cada perfil. |
| B4 | O produto substitui a ferramenta anterior do usuário no dia a dia. |

Armadilha comum: contar como concluído o que só existe no banco. Se o usuário não alcança pela interface, não existe.

## Eixo C: escala e confiabilidade

Mede se o produto sobrevive a uso real e a falhas.

| Nível | Critério |
|---|---|
| C0 | Sem observabilidade. Erro em produção é descoberto pelo usuário. |
| C1 | Logs estruturados e alertas de erro. |
| C2 | Backup verificado por restauração, não só por existência. |
| C3 | Limites de uso, proteção contra abuso, custo por usuário conhecido. |
| C4 | Teste de carga com meta declarada e plano de resposta a incidente. |

Armadilha comum: confundir "o provedor faz backup" com "eu consigo restaurar".

## Como usar

- Registrar o retrato atual nos três eixos com data, em um documento canônico.
- Toda rodada de trabalho declara qual eixo pretende mover.
- Nunca vender um nível de um eixo como se fosse de outro.
- Reavaliar a cada marco, não a cada sessão.

## Exemplo de retrato

```text
Marcaí, 2026-06
Eixo A: A1  (assinado, mas sem contas de loja)
Eixo B: B2  (nenhuma promessa falsa; integrações reais só para notificação)
Eixo C: C1  (logs e alertas; backup nunca restaurado)
Próximo movimento: C2, porque lançar sem restauração testada é irresponsável.
```
