---
name: analise-demanda
description: Avalia se o CPA atualizado após a reunião de Discovery está pronto para o Desenho de Solução. Produz uma ficha de prontidão com bloqueadores, ficha por requisito, fronteiras não declaradas e pauta sugerida. Use após a cerimônia, sobre o deck já atualizado pelo Escritório de Projetos.
argument-hint: [caminho do markdown extraído do CPA]
allowed-tools: Read, Grep, Glob, Write
---

# Prontidão para Desenho de Solução

## Objetivo

Responder a **uma** pergunta: *o que saiu da reunião de Discovery sustenta o Desenho de Solução e a decomposição?*

Esta skill não interpreta a necessidade do negócio — isso foi resolvido ao vivo, com o PO na sala, e foi resolvido bem. Ela verifica se o **registro** dessa decisão está completo o suficiente para as duas etapas seguintes, que são as mais caras do processo.

Roda **depois** da cerimônia, sobre o deck atualizado. O deck é a fonte da verdade; esta ficha é um checkpoint, não um substituto.

## Entrada

Markdown produzido por `/extrair-demanda` a partir do CPA. Se `$ARGUMENTS` estiver vazio, liste os arquivos em `docs/` e pergunte qual avaliar. Nunca invente conteúdo.

## Localização das seções — âncoras semânticas

**Nunca localize conteúdo por número de slide.** A posição varia entre versões do template, e a master story list transborda para dois ou mais slides quando a demanda passa de ~8 requisitos. Localize por **título de seção**; o template numera as seções (`01.` a `11.`), e essa numeração é estável enquanto a posição não é.

| Âncora primária (título) | Assinatura estrutural (fallback) | Uso na avaliação |
|---|---|---|
| `01. Discurso de elevador` | blocos "Qual a necessidade / Proposta / Porque investir" | Objetivo e driver |
| `02. Jornada do cliente/usuário` | rótulos `As-Is` e `To be` | Verificar preenchimento real |
| `03. Quadro master story list` | tabela com IDs `R1..Rn` | **Ficha por requisito** |
| `04. Itens fora do escopo` | tabela com IDs `N1..Nn` | **Fronteira** |
| `05. Temas relacionados à áreas vizinhas` | tabela com IDs `M1..Mn` | Dependência organizacional |
| `06. Validação nome do projeto` | — | Ignorar |
| `07. Desenho simplificado…`, `08. Estimativa…`, `8.1…`, `09. Quadro resumo…` | divisor `CPA 2` | **Bloco CPA 2 — ignorar quando vazio** |
| `10. ATA CPA` | tabela com Data / Horário / participantes | **Ler sempre.** Decisões e pendências |
| `11. Lista de action items` | tabela com IDs `A1..An` | Pendências formais |
| Capa e identificação | código no padrão `NN.NNNN.XX-…`, VP, PO, marcos | Identificação. **Estimativas em branco na v1 são esperadas** |

**Regras de robustez:**

1. **Agregue, não assuma slide único.** Se os IDs `R` continuarem em outro slide (R9, R10…), trate como continuação da mesma seção. O mesmo vale para `N`, `M` e `A`.
2. **Se o título não existir, use a assinatura estrutural** — o prefixo do ID e os cabeçalhos da tabela são mais estáveis que o texto do título.
3. **Se nem assim localizar uma seção**, não infira por posição: registre na ficha que a seção não foi encontrada e siga. Seção ausente é achado, não erro de leitura.
4. Números de slide servem apenas como **referência de rastreabilidade na saída** — cite o slide onde encontrou, nunca use o número para procurar.

## Descarte obrigatório de boilerplate

O template traz texto de exemplo que **não pertence à demanda**. Descartar sempre, sem exceção:

- Frases iniciadas por `Exemplo:` e o texto entre aspas que as segue — no discurso de elevador, os exemplos do template falam de fatura, Icare Parceiro e 2ª via, e **não têm relação com nenhuma demanda específica**
- `Owner: PO`, `Owner: Arquiteto`, `Owner: Escritório Projetos`, `Preenchimento mandatório`
- Marcadores de edição: `- Alterado`, `- X`, `Observações`
- Placeholders: `dd/mm/aaaa`, `R$ XXX.XXX`, `(1 mês)`, `[    ]`
- Rodapé de copyright
- Linhas de tabela inteiramente vazias (N1–N10 em branco significam *nada declarado*, não dez itens)

**Confundir boilerplate com conteúdo é a falha mais grave desta skill.** Na dúvida sobre um trecho, trate-o como conteúdo e sinalize a dúvida na ficha.

## Verificações

### Bloqueadores — impedem o Desenho de Solução

| Verificação | Condição |
|---|---|
| Fronteira não declarada | Seção `04` sem nenhum item `N` preenchido |
| Requisito que não sustenta decomposição | Redação genérica, sem objeto identificável ou sem sistema |
| Requisito que é regra, não funcionalidade | Descreve restrição de negócio sem entregável associado |
| Jornada ausente | Seção `02` vazia ou com uma frase por lado |
| Pendência aberta na ata | Seção `10` registra ação não concluída que condiciona o entendimento |

### Pontos de atenção — não impedem, mas devem ir à pauta

- Esteira TI não preenchida na master story list
- Requisito marcado como atendido por outro projeto (é dependência, não requisito deste)
- Área vizinha listada na seção `05` sem requisito correspondente, ou o inverso
- Classificação MVP/Backlog sem critério registrado
- Requisito que cita sistema ausente de `contexto/mapa-sistemas.md`
- Requisito com esteira operacional (ex.: SAP) — declarar que não gera esforço de desenvolvimento
- Volumetria, janela de processamento ou NFR ausentes quando o requisito os pressupõe
- Campos de identificação não preenchidos (esteira de entrada, requisito para BI, driver principal)
- Ata ausente ou anterior aos marcos registrados — indica que a cerimônia não foi documentada

### Marcos e datas — tratar com desconfiança

O bloco de marcos vem de layout livre, sem ordem de leitura confiável: em alguns pares a data precede o rótulo, em outros o sucede. **Nunca afirme que um marco específico ocorreu em uma data específica com base nesse bloco.** É permitido observar que existem marcos registrados e comparar o conjunto das datas com a data da ata; não é permitido vincular data a marco.

O **BIT (Brainstorm com TI)** é etapa opcional do processo — ocorre quando a área usuária precisa de apoio da TI para escrever os requisitos. **Sua ausência não é achado** e não deve ser reportada.

### Risco estrutural

Procure **dependências entre projetos** (padrão `NN.NNNN`) em qualquer lugar do deck, inclusive em colunas onde não deveriam estar, como *Complexidade* ou *Observações*. Dependência registrada em campo errado não aparece em controle de risco e é fonte recorrente de atraso não previsto. Conte quantos requisitos dependem do mesmo projeto e reporte a proporção.

## Contexto a consultar

Leia antes de avaliar, quando existirem: `contexto/mapa-sistemas.md`, `contexto/criterios-nfr.md`, `contexto/glossario-negocio.md`, `contexto/racional-estimativa.md`. Se estiverem vazios, prossiga e **declare no rodapé** que a avaliação foi feita sem base de contexto.

Busque também em `docs/` outras demandas que citem os mesmos sistemas ou projetos relacionados.

## Formato de saída

Grave em `docs/<ID>/prontidao.md`. Deve caber em **uma tela** — se não couber, corte pontos de atenção, nunca bloqueadores.

```markdown
# Prontidão para Desenho de Solução — <ID> <nome>

**Veredito: PRONTO | PRONTO COM RESSALVAS | NÃO PRONTO**
<N bloqueadores, N pontos de atenção>
Base: CPA <versão> · reunião de <data da ata>

## Bloqueadores — resolver antes de agendar o Desenho
| # | O quê | Onde | Para quem |
|---|---|---|---|

## Ficha por requisito
| ID | Sustenta decomposição? | Esteira | Dependência | Veredito |
|---|---|---|---|---|

## Fronteira de escopo — o que não está dito
- <lacuna de fronteira>

## Pontos de atenção
| # | O quê | Onde | Para quem |
|---|---|---|---|
<Tudo que não é bloqueador vai aqui — campos de identificação não preenchidos,
área vizinha sem requisito correspondente, requisito operacional, classificação
sem critério. Nunca deixe ponto de atenção vazar para o rodapé ou para a pauta.>

## Risco estrutural
<Somente se houver. Seja específico e quantifique.>

## Pauta sugerida para o Desenho de Solução
<No máximo 5 itens, em ordem de precedência. Pauta longa não é lida antes da reunião.
Se sobrar item relevante, ele já está registrado em bloqueadores ou pontos de atenção.>
1. <ponto a fechar>

---
Gerado com apoio de IA — rascunho. Revisor: _______ | Data: _____
<Uma linha, apenas sobre a base de contexto utilizada. Nada além disso.>
```

**Coluna "Para quem":** PMO quando a correção é no deck; PO quando exige decisão de negócio; TI quando é pendência interna.

**Coluna "Sustenta decomposição?":** Sim / Parcial / Não. O critério é operacional — um especialista conseguiria, a partir desta redação, listar sistemas e componentes afetados?

## Regras

- **Não estimar.** Nenhum número de esforço, prazo ou faixa. Nem ordem de grandeza.
- **Não desenhar solução.** Não sugerir tecnologia, arquitetura ou abordagem técnica. Apontar que um requisito não indica sistema é verificação; dizer qual sistema usar é a etapa seguinte.
- **Não reescrever requisito.** Apontar que a redação não sustenta decomposição, sem propor o texto corrigido — isso se decide com o PO.
- **NÃO PRONTO é resultado valioso.** Um veredito negativo bem fundamentado economiza uma reunião de arquitetos.
- **Campo vazio é achado, não ausência de informação.** Fora de escopo em branco após a cerimônia é o achado mais importante que esta skill pode produzir.
- **Rastreabilidade:** todo bloqueador cita a seção de origem pelo título (ex.: `04. Itens fora do escopo`) e, entre parênteses, o slide onde foi encontrada nesta versão do deck.
- **Seção não localizada** deve ser reportada explicitamente na ficha, com a âncora que foi procurada. Silêncio sobre seção ausente é falha grave.
- **Nada de achado no rodapé.** O rodapé contém uma linha sobre a base de contexto e nada mais. Todo achado pertence a bloqueadores, pontos de atenção, fronteira ou risco.
- **Não afirmar o que a extração não garante.** Quando a informação vier de bloco com ordem de leitura não confiável, ou estiver marcada como não extraída, descreva a limitação em vez de preencher a lacuna com a leitura mais plausível.
- Ao terminar, informe o caminho do arquivo e o veredito em uma linha. Não emende para a etapa seguinte.
