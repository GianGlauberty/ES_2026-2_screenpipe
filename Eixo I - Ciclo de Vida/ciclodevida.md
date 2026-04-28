# Ciclo de Vida: Screenpipe

Este documento detalha o roadmap, o ritmo de entregas e a gestão de riscos do projeto **Screenpipe**, destacando sua abordagem ágil e foco em soberania de dados.

## Roadmap e Ritmo de Entregas

O Screenpipe não possui um documento único e estático de roadmap ou gestão explícita de riscos. Seu desenvolvimento é guiado por **Issues** com tags de prioridade e pelo ecossistema de **Pipes**, indicando a adoção de práticas ágeis com desenvolvimento incremental e iterativo.

As issues funcionam como um backlog dinâmico para:
* Registro de funcionalidades.
* Correções de bugs (hotfixes).
* Melhorias contínuas.

### Propostas Principais
1.  **Expansão dos "Pipes":** Transformar o projeto em uma "App Store" de IA para desktop, com agentes que automatizam tarefas (ex: sincronização com Obsidian, rastreadores de ideias).
2.  **Melhoria na Captura e Processamento:** Integração de OCR mais eficiente, suporte a múltiplos monitores e melhoria na diarização de áudio.
3.  **Privacidade e Segurança:** Implementação de *protected paths* e controles granulares de permissão via YAML.
4.  **Infraestrutura Local (MCP):** Suporte total ao *Model Context Protocol* (MCP) da Anthropic.

### Ritmo de Entrega
O ritmo é considerado **extremamente agressivo** e de alta frequência:
* **Frequência:** Modelo de Entrega Contínua (várias releases por dia ou semana).
* **Estilo de Versionamento:** Versionamento semântico (ex: v0.2.74 para v0.3.255).
* **Automação:** Fluxos de CI/CD (GitHub Actions) para macOS, Windows e Linux.
* **Feedback Loop:** Resposta a issues e implementação de sugestões em horas ou dias.

---

## Gestão de Riscos

A estratégia do Screenpipe é baseada em **desacoplamento e redundância** para lidar com a volatilidade da IA.

### Mitigação de Volatilidade
* **Soberania dos Dados:** Prioriza o uso de modelos locais para OCR e transcrição (como o Whisper local).
* **Independência de APIs:** Mitiga riscos de custos variáveis e mudanças nos termos de serviço das Big Techs.
* **Isolamento via Pipes:** Como os Pipes são baseados em scripts, o risco é isolado. Se um modelo externo (como o Claude) sofrer alterações (*drift*), apenas o Pipe específico exige ajuste, preservando o núcleo do sistema.

---
