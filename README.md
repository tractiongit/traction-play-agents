# Traction Play para agentes

Pacote público de instruções e configuração para conectar agentes ao Traction Play pelo MCP remoto. Não contém uma cópia do Play, não executa servidor local e não guarda credenciais.

> **Beta:** o endpoint MCP e o OAuth do Play estão publicados. O Codex já confirmou login, identidade e listagem de projetos em modo somente leitura. O plugin e seus manifests foram validados, mas o OAuth ainda não foi homologado ponta a ponta dentro do Claude Code; as demais tools e o ciclo de renovação/revogação também estão em validação. Comece somente com leitura e um projeto. Nunca cole tokens neste repositório, no chat ou no terminal.

O pacote é público porque contém apenas instruções e configuração; ele não dá acesso aos projetos. O Play autentica cada pessoa e aplica os projetos e as permissões escolhidos no consentimento.

## Começar em uma linha (qualquer agente)

Copie e cole esta instrução no chat do agente:

> Conecte minha conta do Traction Play a este agente seguindo https://github.com/tractiongit/traction-play-agents. Configure o que este ambiente permitir, conduza o login pelo navegador e valide minha identidade e meus projetos. Se alguma etapa precisar ser feita por mim, explique apenas o próximo passo. Não altere dados do Play durante a configuração. Ao concluir ou encontrar um bloqueio, gere o relatório de conexão descrito no repositório.

Essa é uma instrução para o agente, não um instalador universal: cada produto guarda a configuração MCP em um lugar diferente. Ela funciona quando o agente consegue ler o guia e configurar o próprio cliente; se não, use um exemplo abaixo ou a tela de configurações MCP do produto. Não clone este repositório para executar um servidor local.

## Para o agente que recebeu este link

Leia o [guia de conexão](plugins/traction-play/skills/play/references/connection.md), escolha o [caminho do cliente](plugins/traction-play/skills/play/references/clients.md) e entregue o [relatório de conexão](plugins/traction-play/skills/play/references/report.md) tanto em sucesso quanto em bloqueio. Reutilize conexões existentes, conduza apenas a próxima etapa manual e valide `whoami` e `list_projects` antes de dizer que está conectado.

Pedidos como “instala”, “conecta” e “me ajuda a autenticar” seguem esse fluxo. Se a pessoa pedir apenas “veja” ou colar o link sem explicar o que quer, apresente o conector e pergunte se deseja conectar; não inicie instalação automaticamente. O repositório não pode conceder acesso às configurações do cliente nem substituir a autorização do usuário.

## ChatGPT, Codex e Freebuff

- **ChatGPT:** crie uma conexão MCP personalizada com URL `https://play.traction.to/mcp` e OAuth na interface disponível. O link do GitHub é o guia, não o endereço do servidor. [Passos e limitações](plugins/traction-play/skills/play/references/clients.md#chatgpt).
- **Codex:** reutilize a conexão existente ou configure pelo MCP nativo; [CLI e desktop](plugins/traction-play/skills/play/references/clients.md#codex-cli-ou-desktop).
- **Freebuff:** confirme interface, versão e suporte a OAuth remoto antes de configurar. Ainda não homologado; [procedimento sem bridges](plugins/traction-play/skills/play/references/clients.md#freebuff).
- **Gemini CLI:** [configuração candidata](plugins/traction-play/skills/play/references/clients.md#gemini-cli), ainda não homologada no Play.

## Relato para melhorar a conexão

Ao terminar, o agente entrega um relatório copiável com tentativas, retentativas, instalações, buscas adicionais, tempo quando medido, validações e próxima ação. Também entrega um relatório parcial ao aguardar uma ação manual, atualizando-o na retomada. Encaminhe esse relatório à equipe Traction. Não inclua tokens, códigos OAuth, e-mails ou dados dos projetos. Nenhum envio é automático.

## Claude Code

No Claude Code, peça ao agente:

> Instale o conector Traction Play do marketplace `tractiongit/traction-play-agents`. Leia o estado atual no README, não me peça tokens e pare para eu concluir a autorização OAuth no navegador. Depois valide a conexão com `whoami` e `list_projects`, sem alterar dados. Siga o guia de conexão deste repositório e entregue o relatório de conexão tanto em sucesso quanto em bloqueio, sem tentar contornar o fluxo.

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

Configurações candidatas para clientes que não usam o plugin Claude:

**Codex CLI** — testado no Play para OAuth, identidade e projetos ([documentação](https://developers.openai.com/codex/mcp)):

```bash
codex mcp add play --url https://play.traction.to/mcp
codex mcp login play
```

**Cursor** — adicione a `.cursor/mcp.json` do projeto ([MCP](https://docs.cursor.com/context/model-context-protocol), [CLI](https://docs.cursor.com/en/cli/reference/parameters)):

```json
{
  "mcpServers": {
    "play": { "url": "https://play.traction.to/mcp" }
  }
}
```

**VS Code com Copilot em Agent mode** — adicione a `.vscode/mcp.json` ([configuração](https://code.visualstudio.com/docs/agents/reference/mcp-configuration)):

```json
{
  "servers": {
    "play": { "type": "http", "url": "https://play.traction.to/mcp" }
  }
}
```

**Hermes Agent** — configure no `config.yaml` e inicie o OAuth ([documentação MCP](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp)):

```yaml
mcp_servers:
  play:
    url: "https://play.traction.to/mcp"
    auth: oauth
```

```bash
hermes mcp login play
```

Esses três exemplos são configurações do protocolo, **não homologação do Play nesses clientes**. Em todos, comece com `whoami` e `list_projects`, somente leitura e um projeto. Se OAuth não abrir ou as ferramentas falharem, reporte o erro sem compartilhar tokens nem tentar autenticação alternativa.

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
