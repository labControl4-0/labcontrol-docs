# LabControl 4.0 - Normas, Acordos de Equipe e Obrigações Operacionais

**Identificador da Entrega:** `[S4][GP-06]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/gestao/acordos-equipe.md`  
**Disciplina / Área:** Gestão de Projetos  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#6](https://github.com/labControl4-0/labcontrol-docs/issues/6)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Propósito e Vigência dos Acordos

Este documento estabelece os **Acordos de Trabalho (Working Agreements)**, normas de conduta técnica, padrões de engenharia e obrigações operacionais formalizadas pelo time de desenvolvimento do **LabControl 4.0** para o 4º Semestre do Projeto Integrador (PI-IV).

Todos os membros da equipe (@giovanimiamotob, @victorgeroto, @ceduardooliveira, @AndreFernandes9010, @GustavoSilveira1012) submetem-se a estes critérios como base de colaboração, avaliação mútua e qualidade de software.

---

## 2. Acordos de Comunicação e Ritos Ágeis

### 2.1 Canais de Comunicação
- **GitHub Issues e Discussions (Oficial Assíncrono):** Todas as discussões técnicas, decisões de arquitetura, dúvidas de requisitos e bloqueios de dependência devem ficar documentados na issue pertinente no GitHub. Nenhuma decisão de escopo pode permanecer exclusivamente em chats informais.
- **Canal de Voz / Mensagens Rápidas (Discord/WhatsApp):** Utilizado exclusivamente para avisos urgentes (ex: "PR aberto precisando de revisão", agendamento de reuniões, testes integrados síncronos).

### 2.2 Ritos Operacionais
1. **Alinhamento Semanal (Weekly Sync):** Reunião síncrona semanal de 30 a 45 minutos para inspeção do quadro Kanban, replanejamento de prioridades e identificação antecipada de impedimentos.
2. **Standup Assíncrono (Check-in Diário/Bi-diário):** Cada membro atualiza o status do seu card no GitHub Project (o que foi feito, o que fará a seguir, eventuais bloqueios).
3. **SLA Interno de Code Review:** Todo Pull Request submetido deve ser revisado por pelo menos um colega em no máximo **24 horas úteis**, evitando que tarefas fiquem represadas na coluna *In Review*.

---

## 3. Padrões de Engenharia e Controle de Versão

### 3.1 Política de Branches e Commits
- **Branch Protection:** É expressamente proibido fazer `git push --force` ou commits diretos na branch `main`. Todo código entra por Pull Request a partir de branch de feature/fix.
- **Padrão de Commits:** Utilização do padrão **Conventional Commits**:
  - `feat(...)`: nova funcionalidade
  - `fix(...)`: correção de bug
  - `docs(...)`: alteração ou adição de documentação
  - `test(...)`: adição ou correção de testes automatizados
  - `refactor(...)`: refatoração sem alteração comportamental
  - `ci(...)` / `chore(...)`: alterações em automações, build ou dependências

### 3.2 Higiene de Código e Segurança
- **Proibição Absoluta de Segredos Versionados:** Tokens de API, credenciais de banco de dados, chaves JWT e senhas do Mosquitto **jamais** devem ser incluídos em commits ou arquivos rastreados. Utilizar variáveis de ambiente (`.env.example`) e segredos de repositório no GitHub Actions.
- **Sanitização de Evidências:** Em relatórios, logs e capturas de tela anexadas em issues, dados sensíveis (IPs reais, senhas, tokens de autorização) devem ser mascarados ou substituídos por valores sintéticos de exemplo.

---

## 4. Definição de Pronto (DoD) e Pronto para Iniciar (DoR)

### 4.1 Definition of Ready (DoR - Critério de Entrada)
Um item do backlog só pode ser movido para execução quando:
1. Possui escopo claramente delimitado e compreendido pelo desenvolvedor responsável.
2. Critérios de aceite estão expressos como itens verificáveis.
3. Não há dependências bloqueantes ativas sem plano de contingência ou mock.

### 4.2 Definition of Done (DoD - Critério de Conclusão)
Um card só é considerado concluído quando:
1. O código compila limpo e sem advertências críticas.
2. Testes unitários/de integração relevantes foram executados com sucesso.
3. Pull Request foi aprovado por pelo menos um revisor e integrado à branch principal.
4. A documentação correspondente (README, docstrings, arquivos `.md`) foi atualizada.
5. Comentário com evidência objetiva foi publicado na issue no GitHub.

---

## 5. Critérios de Avaliação e Obrigações Acadêmicas

Conforme diretriz do UniSENAI para a composição de notas do Projeto Integrador IV:
- **Avaliação Docente da Disciplina (55%):** Cumprimento rigoroso do conteúdo programático, qualidade técnica dos artefatos e rigor metodológico.
- **Avaliação do Projeto Integrador Integrado (35%):** Integração funcional ponta a ponta entre Backend, Frontend Web, Mobile e IoT, homologação e demonstração ao vivo.
- **Autoavaliação e Avaliação Interpares (10%):** Comprometimento com os acordos de equipe, assiduidade, qualidade das entregas atribuídas e proatividade na remoção de bloqueios mútuos.
