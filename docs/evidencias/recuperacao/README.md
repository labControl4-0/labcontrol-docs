# Evidências de Recuperação (GOV-07)

Esta pasta guarda os **registros dos testes de backup, restauração e rollback** descritos em [`../../rollback.md`](../../rollback.md).

**Status:** nenhum teste executado até o momento — por isso não há registros aqui. Não crie registros de teste que não ocorreram.

## O que guardar

Um arquivo por teste, `AAAA-MM-DD-REC-NN.md`, com:

| Campo | Conteúdo |
| :--- | :--- |
| Teste | ID (REC-01…), cenário e objetivo |
| Versão | SHA/tag do código e imagens usadas |
| Executor e data/hora | Quem executou, início (T0) e fim (T1) |
| Backup | Nome do arquivo e **hash SHA-256** (não o arquivo) |
| Resultados medidos | RTO (T1 − T0) e RPO |
| Integridade | Contagens por tabela (origem × restaurado) e resultado das consultas de órfãos |
| Verificação funcional | Login e listagem de plantas/máquinas na API apontando para o banco restaurado |
| Falhas e ações corretivas | O que deu errado, impacto e correção |
| Capturas/logs | Sanitizados (sem tokens, senhas, IPs reais ou dados de usuários) |

## O que NÃO guardar

- Arquivos de backup (`.dump`, `.sql`) e qualquer dado de banco.
- Credenciais, tokens ou conteúdo de `.env`.

## Modelo

```markdown
# REC-NN — <cenário>
- Data / executor:
- Versão (SHA/tag):
- Backup: <nome> — SHA-256 <hash>
- T0 / T1 / RTO medido:
- RPO medido:
- Contagens origem × restaurado: (tabela)
- Órfãos (esperado 0): Machines / MachineMetrics / MachineEvents
- Verificação funcional (login + listagem): ok / falhou
- Falhas e ações corretivas:
```
