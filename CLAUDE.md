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
│       └── docs/          # Demandas reais de cliente — NÃO versionada (.gitignore)
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
2. **Dados de cliente:** `02-frentes/kairos/docs/` contém demandas reais de cliente.
   Nunca versione, copie para outras pastas ou cite seu conteúdo em artefatos
   versionados.
