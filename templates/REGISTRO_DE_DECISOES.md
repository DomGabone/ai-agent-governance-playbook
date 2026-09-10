# Registro de decisões

> Status: canônico. Domínio: governança. Fonte viva obrigatória: lida no início de toda sessão.

## Como usar

- Numeração sequencial, nunca reutilizada.
- Nada é apagado. Reversão é uma entrada nova apontando para a antiga.
- O agente redige, a pessoa aprova. Sem aprovação é rascunho.
- Achado é decisão. Bug crítico encontrado no caminho vira entrada.

## Modelo

```markdown
## ADR-000 - Título curto

**Data:** AAAA-MM-DD
**Contexto:**
**Decisão:**
**Alternativas descartadas:**
**Consequências:**
**Verificação:** (ou "Não verificado")
**Relacionadas:**
```

---

## ADR-001 - Adotar este registro como fonte viva

**Data:** [ajustar]
**Contexto:** o projeto passa a ser construído com agente de IA como executor e precisa de memória compartilhada entre sessões.
**Decisão:** toda sessão começa pela leitura deste arquivo. Nenhuma mudança estrutural sem entrada aqui.
**Alternativas descartadas:** confiar no histórico de commits. Descartada porque não carrega o "por quê".
**Consequências:** o arquivo de instruções do agente referencia este registro como leitura obrigatória.
**Verificação:** a próxima sessão deve citar esta entrada antes de propor mudanças.
**Relacionadas:** nenhuma.
