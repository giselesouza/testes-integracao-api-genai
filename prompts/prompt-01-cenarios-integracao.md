
# Prompt 01 – Geração de cenários de integração

## Objetivo

Utilizar a GenAI para gerar casos de teste de integração entre uma API REST e um banco de dados PostgreSQL.

## Prompt utilizado

Atue como um analista de QA especializado em testes de integração de APIs REST.

Considere uma API de gerenciamento de tarefas integrada a um banco de dados PostgreSQL.

A API possui os seguintes endpoints:

- POST /tasks: cadastrar tarefa.
- GET /tasks: listar tarefas.
- GET /tasks/{id}: consultar tarefa.
- PUT /tasks/{id}: atualizar tarefa.
- DELETE /tasks/{id}: excluir tarefa.

Gere casos de teste de integração considerando:

1. Comunicação entre API e banco de dados.
2. Persistência e recuperação das informações.
3. Atualização e exclusão de registros.
4. Dados inválidos ou inexistentes.
5. Falhas na comunicação com o banco.

Apresente os resultados em uma tabela contendo:

- ID do caso de teste.
- Cenário.
- Pré-condições.
- Dados de entrada.
- Passos para execução.
- Resultado esperado.
- Prioridade.

Inclua cenários positivos, negativos e situações de exceção.

Não presuma regras de negócio que não foram informadas. Quando necessário, sinalize os pontos que precisam de validação humana.

## Resultado esperado

Uma lista estruturada de casos de teste que contemple os principais fluxos de integração entre a API REST e o PostgreSQL.
