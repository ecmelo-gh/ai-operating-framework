# CLAUDE.md — Squad Discovery / Overlabs

> Arquivo lido automaticamente no início de toda sessão. Mantenha-o curto, atual e sem dado de cliente.
> Dono deste arquivo: [supervisor responsável]. Alteração somente via PR.

---

## 1. Quem somos e o que entregamos

O **Discovery** é a etapa upstream do SDLC da Overlabs. Recebemos a demanda da área usuária e entregamos ao **Escritório de Projetos (PMO)** um pacote de devolutiva composto por:

1. **Entendimento da demanda** — interpretação estruturada do requisito de negócio
2. **Desenho de solução** — opções, trade-offs e decisão
3. **Definição de tecnologias** — stack e sistemas impactados
4. **Estimativa** — esforço e prazo, com premissas e riscos explícitos

Não escrevemos código de produto. Nosso produto é **decisão bem fundamentada**.

## 2. Composição

| Papel | Responsabilidade primária |
|---|---|
| Arquiteto de sistema | Desenho de solução, impacto sistêmico, decisão técnica |
| Especialista de desenvolvimento | Viabilidade, esforço, riscos de execução |
| Analista de negócio de TI (PO) | Interpretação do requisito, interface com a área usuária |

## 3. Fluxo padrão da demanda

```
Cerimônia com área usuária  →  Entendimento  →  Desenho de solução
                                                        ↓
              Devolutiva ao PMO   ←   Estimativa (esforço + prazo)
```

Cada etapa tem artefato próprio em `templates/`. Nenhuma etapa avança com a anterior em aberto.

## 4. Onde está o contexto

| Arquivo | Conteúdo |
|---|---|
| `contexto/mapa-sistemas.md` | Sistemas, integrações e donos técnicos |
| `contexto/stack-padrao.md` | Tecnologias aprovadas e restrições arquiteturais |
| `contexto/criterios-nfr.md` | Requisitos não funcionais obrigatórios por tipo de demanda |
| `contexto/glossario-negocio.md` | Termos de domínio e siglas da área usuária |
| `historico/demandas/` | Demandas anteriores com **estimado vs. realizado** |
| `templates/` | Formato padrão de cada artefato |

**Sempre consulte estes arquivos antes de responder.** Eles são a fonte da verdade — não use conhecimento genérico quando houver padrão definido aqui.

## 5. Regras invioláveis

1. **Rascunho, nunca decisão.** Toda saída gerada com apoio de IA é insumo. O artefato só é válido com dono humano nomeado e revisão registrada.
2. **Não inventar.** Se o requisito não diz, a saída deve registrar como **lacuna** ou **premissa**, jamais preencher por inferência silenciosa. Preferir "não informado" a plausibilidade.
3. **A estimativa não nasce da IA.** A sequência obrigatória é: decomposição → estimativa humana → comparação com `historico/`. Número gerado antes da análise humana produz ancoragem e corrompe o julgamento do time.
4. **Sem dado sensível no repositório.** Proibido: credenciais, bases de cliente, documentos sob NDA, dados pessoais. Glossário e mapa de sistemas em nível conceitual são permitidos.
5. **Rastreabilidade.** Todo artefato cita a origem: ata da cerimônia, documento de requisito ou demanda anterior.

## 6. Padrões de escrita

- Português do Brasil, tom executivo e direto
- Frase afirmativa; evitar hedging ("talvez", "possivelmente") — se há incerteza, ela vira **premissa** ou **risco** nomeado
- Toda afirmação técnica relevante deve ser rastreável a um item do requisito ou a um arquivo de `contexto/`
- Sem preâmbulo e sem resumo do que foi pedido

## 7. Skills disponíveis

| Comando | Uso |
|---|---|
| `/analise-demanda` | Transforma requisito de negócio + ata em entendimento estruturado |
| `/desenho-solucao` | Gera opções de solução com trade-offs (em implantação) |
| `/estimativa` | Decompõe e compara com histórico (em implantação) |
| `/devolutiva-pmo` | Consolida o pacote final (em implantação) |

Se uma skill necessária não estiver disponível na sessão, informe qual está faltando em vez de improvisar o formato.
