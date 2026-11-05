# LabControl 4.0 - Política de Gestão de Mudanças e Integração Contínua (CI)

**Identificador da Entrega:** `[S4][GOV-04]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/governanca/mudancas-ci.md`  
**Disciplina / Área:** Governança de TI  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#12](https://github.com/labControl4-0/labcontrol-docs/issues/12)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Política de Gestão de Mudanças (Change Enablement)

Alinhada às boas práticas de governança de TI (COBIT e ITIL 4 - Prática de Habilitação de Mudanças), toda alteração em código-fonte, arquitetura, infraestrutura ou documentação regulatória do LabControl 4.0 segue um ciclo controlado, rastreável e auditável.

### 1.1 Classificação das Mudanças

```
+------------------+-------------------------------------------------------+-----------------------------+
| Categoria        | Descrição                                             | Fluxo de Aprovação          |
+------------------+-------------------------------------------------------+-----------------------------+
| 1. Mudança       | Alterações rotineiras de baixo risco com testes       | PR + 1 aprovação de par     |
|    Padrão        | automatizados validados (novas telas, DTOs, docs).    | no GitHub (CI obrigatório). |
+------------------+-------------------------------------------------------+-----------------------------+
| 2. Mudança       | Alterações em contratos de API, quebra de schema      | Discussão documentada na    |
|    Normal        | de banco de dados, migração de broker ou protocolos.  | Issue + 2 aprovações de PR. |
+------------------+-------------------------------------------------------+-----------------------------+
| 3. Mudança       | Correção crítica de segurança (vulnerabilidade ativa) | Hotfix em branch dedicada,  |
|    Emergencial   | ou indisponibilidade total do pipeline de integração. | merge com revisão imediata. |
+------------------+-------------------------------------------------------+-----------------------------+
```

---

## 2. Regras de Branch Protection e Pull Request

Para mitigar o risco de regressão e garantir integridade nos repositórios da organização `labControl4-0`:
1. **Branch `main` Protegida:** Commits diretos e operações com `git push --force` são desabilitados.
2. **Revisão Obrigatória de Código:** Todo Pull Request deve receber aprovação (`Approved`) de pelo menos um desenvolvedor antes do merge. O autor do PR não pode aprovar seu próprio código.
3. **Status Checks Obrigatórios:** O pipeline de CI deve concluir com status verde (sucesso) em todos os passos (build, lint e suíte de testes automatizados).
4. **Resolução de Comentários:** Conversas e apontamentos abertos durante o code review devem ser expressamente resolvidos antes do fechamento.

### 2.1 Checklist Padrão de Pull Request (PR Template)
Cada PR deve conter no seu corpo de abertura:
```markdown
### Descrição da Mudança
- Resumo claro do que foi implementado ou corrigido.

### Issue Relacionada
- Closes #XYZ ou Resolves #XYZ

### Tipo de Mudança
- [ ] Nova funcionalidade (feat)
- [ ] Correção de erro (fix)
- [ ] Documentação ou Governança (docs)
- [ ] Refatoração ou Performance (refactor)

### Verificações do Desenvolvedor
- [ ] Build local executou com sucesso
- [ ] Testes automatizados executados e passando
- [ ] Nenhum segredo, token, senha ou dado sensível exposto
- [ ] Documentação associada atualizada
```

---

## 3. Arquitetura das Pipelines de CI (GitHub Actions)

A integração contínua é padronizada via workflows nativos do GitHub Actions em cada repositório da organização:

### 3.1 Pipeline de Documentação (`labcontrol-docs`)
- **Gatilho:** `push` em `main` e `pull_request` apontando para `main`.
- **Validações:**
  1. Verificação sintática e de links quebrados em arquivos Markdown.
  2. Auditoria estática de segredos versionados (prevenção de credenciais).
  3. Verificação de integridade da estrutura de pastas (`docs/gestao`, `docs/governanca`, `docs/seguranca`, etc.).

### 3.2 Pipeline Frontend Web (`labcontrol-web`)
- **Gatilho:** `pull_request` e `push` em `main` / `develop`.
- **Passos:** Setup Node.js -> `npm ci` -> `npm run lint` -> `npm run test` (Vitest) -> `npm run build` (Vite).

### 3.3 Pipeline Mobile (`labcontrol-mobile`)
- **Passos:** Setup Node.js -> `npm ci` -> Checagem de tipagem TypeScript (`npx tsc --noEmit`) -> Linter Expo.

### 3.4 Pipeline Backend (`labcontrol-api`)
- **Passos:** Validação de compilação da aplicação, execução de testes unitários e empacotamento em container Docker.
