# CLAUDE.md

## O que é este repositório

Este repositório é o programa **AI Adoption** da área de Desenvolvimento da Overlabs.
Concentra estratégia, governança, frentes de execução, artefatos, pesquisa e playbooks
da adoção de IA na área.

## Kairós

O **Kairós** é a frente que automatiza a esteira de projetos, de **MP01 a MP10**.
Tudo o que é específico do Kairós fica em `02-frentes/kairos/`.

## Mapa das pastas

```
.
├── CLAUDE.md              # Instruções para o Claude (este arquivo)
├── README.md              # Visão geral do repositório
├── DOUTRINA.md            # Princípios que regem a criação de skills
├── .claude/skills/        # Skills do Claude Code
├── 01-programa/
│   ├── estrategia/        # Visão, objetivos e direção do programa
│   ├── roadmap/           # Roadmap do programa
│   ├── equipe/            # Papéis e pessoas
│   └── governanca/        # Ritos, decisões e controles
├── 02-frentes/
│   └── kairos/            # Frente Kairós (esteira MP01–MP10)
│       ├── contexto/      # Contexto e escopo da frente
│       ├── roadmap/       # Roadmap da frente
│       ├── historico/     # Decisões e evolução
│       ├── templates/     # Templates de artefatos da frente
│       ├── CLAUDE-kairos.md  # Referência da frente (origem: system-development)
│       └── docs/<ID>/     # Uma pasta por demanda (<ID> = NN.NNNN) — NÃO versionada
├── 03-artefatos/
│   ├── apresentacoes/
│   ├── diagramas/
│   └── documentos/
├── 04-pesquisa/           # Pesquisas e referências
└── 05-playbooks/          # Playbooks operacionais
```

## Regras

1. **Skills:** toda skill nova é criada pela meta-skill `kairos-skill`, seguindo a
   `DOUTRINA.md`. Não crie skills manualmente nem fora desse fluxo.

   As skills extrair-demanda e analise-demanda são anteriores à DOUTRINA.md.
   Foram calibradas contra caso real (demanda 25.0167) em três rodadas, mas ainda
   não passaram pela kairos-skill nem têm evals. Serão revalidadas quando a
   DOUTRINA.md e a kairos-skill existirem. Até lá, não servem de modelo para
   skills novas.
2. **Dados de cliente:** `02-frentes/kairos/docs/` contém demandas reais de cliente.
   Nunca versione, copie para outras pastas ou cite seu conteúdo em artefatos
   versionados.
