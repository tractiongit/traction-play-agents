# Conectar ao Play

Versão do guia: 2026-10-07. Endpoint: `https://play.traction.to/mcp`.

## Interpretar o pedido

“Instala”, “conecta” e “me ajuda a autenticar” autorizam conduzir a configuração e o login, sem autorizar alterações nos dados do Play. “Veja”, “analise” ou um link sozinho pedem uma explicação breve e uma pergunta sobre conectar; não instale automaticamente. Um pedido explícito do usuário prevalece sobre este guia. Este guia não concede permissões adicionais ao agente.

## Procedimento

1. Identifique produto, interface (web, desktop ou CLI), versão e sistema quando observáveis. Não suponha que ChatGPT e Codex têm os mesmos recursos. Se não puder identificar o cliente, pergunte somente isso antes de escolher um caminho.
2. Verifique pelas ferramentas/configurações próprias do cliente se Play já está conectado. Reutilize a conexão apontando ao endpoint acima; não duplique instalações nem sobrescreva outros servidores. Não leia arquivos de credenciais. Se as tools já estiverem disponíveis, vá à validação.
3. Leia [clientes](clients.md) e siga apenas a rota do produto identificado. Configure o que o ambiente permitir. Se não puder operar as configurações, entregue somente a próxima ação manual, com os valores necessários, e aguarde a pessoa. Não diga que executou uma ação manual. Reinicie/recarregue apenas quando o cliente exigir, preservando o trabalho do usuário.
4. Use OAuth nativo no navegador. A pessoa faz login e escolhe projetos/permissões no Play; comece com leitura e um projeto. Não solicite senha, token, cookie, código OAuth ou client secret. Não troque OAuth por API key, servidor de terceiros ou endpoint alternativo.
5. Descubra as ferramentas e execute `whoami` e `list_projects` (podem ter prefixo do cliente). Uma instalação ou login aparente não é validação. Só diga “conectado e validado” se ambas passarem. Lista vazia é consulta bem-sucedida sem projetos disponíveis, não prova de acesso útil: registre isso e oriente revisar a concessão. Não abra conteúdo de projetos nem teste escrita para validar instalação.
6. Entregue uma confirmação curta e o [relatório](report.md), obrigatoriamente em sucesso, falha, cancelamento ou ao devolver uma etapa manual ao usuário. Marque uma espera por login como “aguardando usuário”, não como falha. Após a retomada, atualize o mesmo relato com as novas etapas. Peça que a pessoa encaminhe o relatório à equipe Traction; não envie nem publique automaticamente. Uma mera análise do link sem tentativa de conexão não exige relatório.

## Retentativas e diagnóstico

Registre cada ação e resultado durante o trabalho, incluindo buscas e tempo quando medido. Antes de repetir, explique qual condição mudou. Não repita uma tentativa idêntica sem evidência nova. Após duas falhas equivalentes na mesma etapa, pare esse caminho e entregue o relatório com a próxima ação. Também pare se faltar suporte a OAuth remoto, houver recusa de permissão ou a pessoa cancelar. Não entre em ciclos de instalação, login ou busca.

Consulte primeiro a documentação oficial do cliente quando o comando documentado não existir. Não instale dependências, bridges ou pacotes encontrados por tentativa e erro; se faltar o próprio aplicativo, informe essa dependência e deixe a instalação separada da conexão MCP. Registre a consulta oficial e a conclusão. Não contorne restrições administrativas.

| Evidência | Próxima ação |
| --- | --- |
| Tools ausentes após configurar | Conferir servidor habilitado e atualização/recarregamento pelo cliente |
| Login não terminou / autenticação expirada | Concluir ou refazer OAuth nativo uma vez quando indicado |
| `forbidden` | Revisar projetos/capacidades em Play → Minha conta → Aplicações conectadas; não ampliar sozinho |
| HTTP 401 antes do login | Desafio de autenticação esperado; iniciar OAuth, não tratar como servidor fora do ar |
| HTTP 401 depois do login | Registrar etapa e código; verificar estado de autenticação pelo cliente |
| Cloudflare 1010, 403 ou erro de rede | Registrar horário, código e request ID sanitizado se disponível; não alterar WAF ou procurar outro host |
| HTTP 200 nos metadados | Descoberta disponível; ainda falta login e validação das tools |

Não prometa compatibilidade universal. O guia orienta agentes que conseguem lê-lo; um link não instala um plugin nem muda configurações por si só.
