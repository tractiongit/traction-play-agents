---
name: play
description: Conecte ou autentique agentes no Traction Play, diagnostique a conexão e gere o relatório de instalação. Use o MCP autenticado do Traction Play quando a pessoa pedir para consultar ou atualizar projetos, tarefas, pulsos semanais ou informações de marca no Play. Não use para desenvolvimento genérico do repositório nem para capacidades que não apareçam nas ferramentas MCP disponíveis.
---

# Traction Play

Use as ferramentas MCP `play` para trabalhar com os dados do Traction Play. A skill ensina o fluxo; o servidor MCP e as permissões do Play determinam o que está realmente disponível.

## Conexão, autenticação e diagnóstico

Quando a pessoa pedir para instalar, conectar, autenticar ou corrigir a conexão, leia [o guia de conexão](references/connection.md) e o caminho do cliente indicado nele. Entregue obrigatoriamente o [relatório sanitizado](references/report.md) em sucesso, falha, cancelamento ou espera por ação manual; atualize na retomada. Isso se aplica à configuração/autenticação, não a cada consulta normal de dados. Um pedido de “veja” ou análise do link não autoriza instalar.

## Estado beta e primeiro uso

O servidor está publicado; login, identidade e listagem de projetos foram confirmados no Codex. Este plugin ainda não completou o teste OAuth ponta a ponta no Claude Code. Após autenticar, valide somente `whoami` e `list_projects` primeiro. Se qualquer uma falhar, reporte a mensagem sanitizada no relatório de conexão e pare; não tente endpoints alternativos nem credenciais pessoais. Até a homologação do cliente e das operações ser concluída, não presuma que uma tool publicada está validada em produção.

## Antes de consultar

1. Confirme a conexão. Se necessário, use `whoami` para verificar a conta autenticada.
2. Use `list_projects` para identificar os projetos que essa conta pode acessar. Se a pessoa nomear um projeto, confira o nome na lista e não escolha um projeto parecido por conta própria.
3. Se o MCP estiver desconectado, peça à pessoa para concluir a autorização no fluxo OAuth do próprio cliente. Nunca solicite, aceite ou imprima tokens, cookies ou credenciais.
4. Respeite as capacidades efetivamente concedidas. Uma conexão somente de leitura não autoriza escrita; uma falha `forbidden` significa parar, não procurar uma rota alternativa.

## Consultas e alterações

- Use `get_brand` para consultar informações de marca e `get_project`, `list_tasks`, `get_task`, `list_pulses`, `get_pulse` e ferramentas relacionadas para consultar os dados correspondentes. Use paginação quando oferecida; não conclua que um resultado parcial é a lista completa.
- Para uma solicitação de leitura, consulte apenas o projeto e o escopo pedidos. Não exponha dados pessoais de membros se não forem necessários à solicitação.
- Faça uma alteração quando a pessoa a tiver pedido claramente e a ferramenta/capacidade necessária estiver disponível. Se projeto, registro, conteúdo ou resultado pretendido estiver ambíguo, pergunte antes de gravar.
- Prefira alterações pontuais. Para marca, não substitua um módulo inteiro quando a solicitação for mudar um campo ou item. Para tarefas e pulsos, preserve campos não mencionados.
- Antes de concluir uma tarefa, verifique que a pessoa pediu a conclusão. Não interprete “revisar” ou “atualizar” como autorização para concluir ou apagar dados.
- Em conflito de versão, leia a versão atual e reavalie a alteração; não sobrescreva silenciosamente. Em falha após uma criação, confira se o registro já foi criado antes de tentar de novo.
- Depois de gravar, verifique a resposta da ferramenta e resuma o que mudou, em qual projeto e o que não foi concluído. Não diga que uma alteração foi salva se a ferramenta não confirmou.

## Limites

- Use somente as ferramentas que o servidor realmente anuncia. Os nomes e capacidades podem mudar; não invente endpoints, ferramentas nem resultados.
- O MCP atual cobre identidade, projetos, tarefas, pulsos semanais e informações de marca. Não presuma acesso a relatórios mensais, anotações rápidas da Central do Consultor, sugestões de tarefas ou processamento/extrator de reuniões. Se essas funções não aparecerem como ferramentas, explique a limitação e não simule o resultado.
- Um pulso ou item que o servidor recuse por estar fechado ou fora do escopo não deve ser alterado por API alternativa.
- Se não houver acesso a um projeto, se a conexão não autenticar ou se uma resposta vier vazia/incompleta de forma inesperada, reporte exatamente isso e pare. Não deduza que a pessoa não tem dados nem tente usar token pessoal como fallback.

## Ao terminar

Responda em português, de forma direta. Diferencie dados lidos, alterações confirmadas e ações bloqueadas. Para consultas, cite o projeto e os itens usados como base; para alterações, informe o resultado confirmado pela ferramenta.
