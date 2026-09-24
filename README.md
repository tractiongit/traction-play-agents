# Traction Play para agentes

Pacote público de instruções e configuração para conectar agentes ao Traction Play pelo MCP remoto. Não contém uma cópia do Play, não executa servidor local e não guarda credenciais.

> **Beta:** o endpoint MCP e o OAuth do Play estão publicados. O Codex já confirmou login, identidade e listagem de projetos em modo somente leitura. O plugin e seus manifests foram validados, mas o OAuth ainda não foi homologado ponta a ponta dentro do Claude Code; as demais tools e o ciclo de renovação/revogação também estão em validação. Comece somente com leitura e um projeto. Nunca cole tokens neste repositório, no chat ou no terminal.

O pacote é público porque contém apenas instruções e configuração; ele não dá acesso aos projetos. O Play autentica cada pessoa e aplica os projetos e as permissões escolhidos no consentimento.

## Claude Code

No Claude Code, peça ao agente:

> Instale o conector Traction Play do marketplace `tractiongit/traction-play-agents`. Leia o estado atual no README, não me peça tokens e pare para eu concluir a autorização OAuth no navegador. Depois valide a conexão com `whoami` e `list_projects`, sem alterar dados. Se a autorização ou uma dessas consultas falhar, informe o bloqueio sem tentar contornar o fluxo.

Registre e instale o marketplace pelos comandos oficiais no Claude Code:

```text
/plugin marketplace add tractiongit/traction-play-agents
/plugin install traction-play@traction-play-agents
/mcp
```

Abra `/mcp`, escolha Play e conclua o login/consentimento no navegador. Autorize apenas os projetos e capacidades necessários. Depois peça ao agente para executar `whoami` e `list_projects` sem alterar dados. Se essas ferramentas não aparecerem ou retornarem erro, pare e reporte o erro; não cole tokens nem tente contornar o OAuth. Mesmo que a leitura funcione, considere escritas em beta até a equipe concluir a homologação completa do Claude Code.

Para remover o plugin, use `/plugin` e desinstale **traction-play**. Para desconectar a autorização, use a opção de desconexão/limpeza de autenticação em `/mcp` e, se necessário, revogue também a conexão em **Play → Minha conta → Aplicações conectadas**.

## Outros agentes

A skill em `plugins/traction-play/skills/play/SKILL.md` usa o formato aberto Agent Skills e pode ser reutilizada por clientes que o implementem. O endpoint é MCP remoto por Streamable HTTP com OAuth; cada cliente precisa oferecer esse transporte e um fluxo OAuth compatível. Os passos de instalação e a configuração variam por produto. Este repositório empacota atualmente o plugin do Claude Code; os demais adaptadores ainda não estão homologados.

## O que o conector orienta o agente a fazer

- Conferir a identidade autenticada e os projetos acessíveis antes de consultar dados.
- Consultar e, quando autorizado, criar/editar tarefas, pulsos semanais e informações de marca usando as ferramentas MCP disponíveis.
- Respeitar permissões do usuário, capacidades concedidas, conflitos e respostas do servidor.
- Não inventar ferramentas: extração de reunião para o Pulso, sugestões de tarefas e anotações rápidas só podem ser usadas se aparecerem como ferramentas disponíveis no MCP.

## Segurança

- Este repositório contém somente instruções e manifests públicos; não coloque tokens, client secrets ou dados de clientes aqui.
- Instalar o plugin não concede acesso aos projetos. A autenticação OAuth e as permissões aplicadas pelo Play controlam o acesso.
- A URL do MCP não é uma credencial. Não substitua OAuth por token pessoal de API ou por uma variável de ambiente compartilhada.
- Revise as alterações do marketplace antes de atualizar uma instalação sensível.

## Desenvolvimento

Não há stack de execução: Markdown, JSON e Git. O Play hospeda o servidor e seus dados. Valide os manifests e a skill com Claude Code:

```bash
claude plugin validate .
claude plugin validate ./plugins/traction-play
```

O pacote não solicita instalação de dependências, scripts de shell ou alterações automáticas em outras configurações do usuário.
