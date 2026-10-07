# Caminhos por cliente

Guia 2026-10-07. Use junto com [procedimento](connection.md) e [relatório](report.md). Não interprete suporte documentado pelo fabricante como homologação do Play.

## ChatGPT

Na interface que oferecer criação de MCP personalizado, abra as configurações de apps/plugins/conectores e a opção de criar conexão personalizada. Os nomes, disponibilidade e acesso administrativo variam por conta/interface; se a opção não aparecer, consulte a documentação oficial e registre a limitação, sem inventar menus.

Preencha nome `Traction Play`, URL `https://play.traction.to/mcp` e autenticação OAuth. Conclua o login/consentimento no navegador e habilite a conexão na conversa quando necessário. Não use a URL do GitHub como URL do servidor. Se o agente não puder operar essa interface, conduza a pessoa uma etapa por vez. Valide as duas tools quando disponíveis na conversa.

Referência: https://developers.openai.com/api/docs/guides/custom-mcp-server

## Codex (CLI ou desktop)

No CLI disponível, confira a conexão existente com `codex mcp list`, sem compartilhar saídas privadas. Só se Play ainda não estiver cadastrado:

```bash
codex mcp add play --url https://play.traction.to/mcp
```

Se precisar autenticar:

```bash
codex mcp login play
```

No desktop, use as configurações MCP oferecidas pelo aplicativo ou o CLI disponível nesse mesmo ambiente. Não suponha que outra máquina/host compartilhe a configuração. Se as tools não aparecerem na conversa, use o mecanismo de atualização do cliente; pode ser necessário reabrir a sessão. Não instale o CLI só para contornar uma limitação do desktop.

Referência: https://developers.openai.com/codex/mcp
Estado Play: OAuth, identidade e projetos confirmados no Codex; ciclo completo de operações, renovação e revogação ainda em validação.

## Claude Code

Escolha uma rota e não instale as duas. Para instalar o plugin com as orientações de uso:

```text
/plugin marketplace add tractiongit/traction-play-agents
/plugin install traction-play@traction-play-agents
/mcp
```

Para quem deseja somente o servidor MCP, no terminal:

```bash
claude mcp add --transport http play https://play.traction.to/mcp
```

Depois abra `/mcp` dentro do Claude Code e conclua OAuth. Reutilize instalação existente. Referência: https://code.claude.com/docs/en/mcp
Estado Play: manifests validados; OAuth completo no Claude e ciclo completo ainda não homologados.

## Freebuff

Identifique primeiro a interface e a versão usada pela pessoa. O projeto oficial tem configuração MCP, mas este pacote ainda não tem uma receita OAuth do Play homologada no Freebuff. Confira no cliente/documentação oficial se essa versão oferece servidor remoto Streamable HTTP e OAuth pelo navegador. Se oferecer, cadastre `https://play.traction.to/mcp` pelo mecanismo nativo e siga o procedimento; registre os passos exatos sanitizados para permitir reproduzir.

Se o suporte ou a configuração não puderem ser confirmados, pare com resultado parcial/bloqueado e relatório. Não invente comando, arquivo de configuração ou suporte ao marketplace do Claude. Não confunda servidores de terceiros que permitem controlar Freebuff a partir de outro agente com conectar Freebuff ao Play. Não instale essas bridges.

Referência oficial: https://github.com/CodebuffAI/freebuff
Estado Play: conexão não homologada neste cliente.

## Gemini CLI

Se o CLI já estiver disponível e não existir conexão:

```bash
gemini mcp add play https://play.traction.to/mcp --transport http
```

Na sessão Gemini, use `/mcp auth play` e conclua o navegador. Referência: https://geminicli.com/docs/tools/mcp-server/
Estado Play: configuração candidata, sem homologação específica neste cliente.

## Outros clientes

Use os exemplos no README e documentação oficial do produto para HTTP remoto e OAuth. Se não houver suporte, entregue a limitação e o relatório. Não substitua o cliente escolhido pela pessoa sem ela pedir.
