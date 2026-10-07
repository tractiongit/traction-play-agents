# Relatório de conexão

Formato v1; guia 2026-10-07. Entregue em bloco copiável; arquivo `.txt` é opcional se o ambiente permitir. Preencha todos os campos com fatos observados ou “não disponível”/“não executado”. Não invente duração ou causa. Diferencie hipótese de diagnóstico confirmado.

Antes de entregar, remova tokens, cookies, senhas, client secrets, códigos OAuth, cabeçalhos de autenticação, URLs de autorização/callback, query strings e fragmentos. Resuma o pedido inicial sem informações privadas. Substitua e-mails, nomes/IDs de pessoas e projetos, caminhos pessoais e conteúdo de clientes por `[removido]`. Não cole saídas integrais de ferramentas, configuração ou logs. Erros também precisam ser sanitizados. Preserve apenas mensagens úteis sanitizadas, códigos HTTP, horários e request IDs de diagnóstico não secretos. Nunca salve o relatório neste repositório público ou abra uma issue automaticamente.

```text
RELATÓRIO DE CONEXÃO — TRACTION PLAY
Formato: v1
Guia: 2026-10-07
Revisão do pacote/commit: [quando observável]
Resultado: [validado / parcial / bloqueado / aguardando usuário / cancelado]
Agente e versão:
Interface: [web / desktop / CLI]
Sistema operacional:
Data/hora e fuso:
Tempo total: [medido / estimado explicitamente / não medido]
Tempo de espera pelo usuário: [quando medido]
Pedido inicial: [resumo sanitizado]
Conexão anterior: [existia / não existia / não verificado]

Etapas e tentativas, em ordem:
1. [ação ou busca, resultado observado, duração se medida]
2. [ação, resultado]
Retentativas: [quantidade, motivo, condição que mudou e resultado; ou nenhuma]

Instalações/configurações: [o que mudou ou nenhuma]
Intervenções do usuário: [ações necessárias; sem dados de login]
OAuth: [não iniciado / aguardando / concluído / falhou / não suportado]
Tools descobertas: [sim / não / não verificado]
whoami: [passou / falhou / não executado; sem identidade pessoal]
list_projects: [passou / falhou / não executado; quantidade, sem nomes/IDs]
Erros: [etapa, mensagem sanitizada, HTTP, request ID e horário quando disponíveis]
Dificuldades/buscas adicionais:
Diagnóstico: [confirmado ou hipótese; não disponível se desconhecido]
Situação final e próxima ação:
```

Finalize: “Encaminhe este relatório à equipe Traction para ajudar a melhorar a conexão.” Isso não autoriza envio pelo agente. Relatórios de conexão rápida também são úteis; não omita o relatório só porque deu certo.
