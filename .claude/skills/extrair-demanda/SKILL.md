---
name: extrair-demanda
description: Converte a demanda recebida em .pptx, .xlsx, .docx ou .pdf para markdown normalizado em 02-frentes/kairos/docs/<ID>/, preservando o texto original sem interpretar. Use como primeiro passo, antes de /analise-demanda, sempre que a demanda chegar em formato Office.
argument-hint: [caminho do arquivo original]
allowed-tools: Bash, Read, Write, Glob
---

# Extração de Demanda — Discovery

## Objetivo

Transformar o arquivo original da área usuária em um **artefato textual fiel**, que sirva de entrada para `/analise-demanda`.

Esta skill **não interpreta, não resume, não corrige e não organiza**. Ela transporta conteúdo de um formato para outro. Qualquer melhoria de redação aqui destrói o objeto de análise da etapa seguinte: a ambiguidade do texto original é justamente o que precisa ser detectado depois.

## Pasta da demanda

Cada demanda tem uma pasta própria, `02-frentes/kairos/docs/<ID>/`, onde `<ID>` é o código do projeto no padrão `NN.NNNN`. O arquivo original e todos os derivados ficam nela. Se o `<ID>` não puder ser identificado pelo caminho ou pelo arquivo, pergunte; não invente.

## Procedimento

1. **Verificar o arquivo de entrada.** Se `$ARGUMENTS` estiver vazio, liste as pastas `02-frentes/kairos/docs/<ID>/` e os arquivos originais dentro delas, e pergunte qual processar. Não invente conteúdo.

2. **Converter.** Para `.pptx`, o método principal é **`python-pptx`**, que dá controle sobre notas, tabelas e formas agrupadas. Para `.xlsx`, use **`openpyxl`**, percorrendo **todas as abas, inclusive as ocultas**. `markitdown` serve como alternativa quando as bibliotecas não estiverem disponíveis. Informe ao usuário qual caminho foi usado.

   Saída em `02-frentes/kairos/docs/<ID>/bruto.md`, gravada em UTF-8.

3. **Recuperar o que a conversão costuma perder.** Esta etapa é obrigatória e é onde está o valor real da skill:

   | Formato | Verificar sempre |
   |---|---|
   | `.pptx` | **Notas de slide** (contêm a explicação falada, frequentemente mais rica que o slide), caixas de texto soltas, comentários, texto dentro de imagens/diagramas |
   | `.xlsx` | Todas as abas (não só a primeira), abas ocultas, comentários de célula, fórmulas que revelam regra de negócio, linhas abaixo da área visível |
   | `.docx` | Comentários, alterações controladas, notas de rodapé, cabeçalhos |
   | `.pdf` | Se for digitalizado, avisar que o texto pode estar incompleto |

4. **Sinalizar conteúdo não textual.** Diagramas, fluxogramas, prints de tela e gráficos não sobrevivem à conversão. Registre um marcador explícito no ponto correspondente:
   ```
   > [!] CONTEÚDO VISUAL NÃO EXTRAÍDO — slide 4: diagrama de fluxo.
   > Requer leitura manual ou captura como imagem.
   ```
   Nunca descreva por inferência o que o diagrama provavelmente mostra.

5. **Sinalizar ordem de leitura não confiável.** Quando o texto vier de formas soltas, agrupadas ou livres — linhas do tempo, cronogramas, quadros de marcos, infográficos — a sequência extraída **não corresponde à leitura visual**. Rotule o bloco inteiro:
   ```
   > [!] ORDEM DE LEITURA NÃO CONFIÁVEL — slide 2: bloco montado com formas
   > agrupadas. Os fragmentos abaixo estão fora da ordem original; não associe
   > datas a marcos, nem rótulos a valores, sem conferência visual.
   ```
   Este marcador é obrigatório sempre que o slide tiver formas agrupadas ou livres em quantidade relevante. Texto de tabela e de caixa de texto isolada não precisa dele.

6. **Gravar** em `02-frentes/kairos/docs/<ID>/bruto.md` no formato de saída abaixo.

7. **Reportar** ao usuário: origem, quantidade de slides/abas processados, o que foi recuperado além do texto principal e o que não pôde ser extraído.

## Formato de saída

```markdown
# Demanda <ID> — material bruto

**Arquivo de origem:** <nome e formato>
**Convertido em:** <data>
**Método:** <ferramenta usada>
**Integridade:** COMPLETA / PARCIAL
<Se PARCIAL, liste o que faltou.>

---

## [Slide 1 / Aba "Nome"] <título original>

<texto exatamente como está no original>

### Notas do slide
<conteúdo das notas, se houver>

---

## [Slide 2] ...
```

Preserve a ordem e a segmentação do original. Cada slide ou aba vira uma seção identificada — isso permite que a análise seguinte cite a origem exata de cada requisito.

## Regras

- **Transcrição, não redação.** Erro de português, frase incompleta, bullet solto e contradição interna devem ser preservados como estão.
- **Não unifique** informação repetida em slides diferentes. Repetição com variação é sinal de ambiguidade e é dado relevante para a análise.
- **Não classifique nem priorize** o conteúdo. Isso é trabalho de `/analise-demanda`.
- **Não produza análise.** Ao terminar, informe o caminho do arquivo e sugira executar `/analise-demanda 02-frentes/kairos/docs/<ID>/bruto.md`. Não emende as duas etapas.
- **Integridade PARCIAL é resultado válido.** Declarar o que não foi extraído vale mais que uma saída aparentemente completa.
