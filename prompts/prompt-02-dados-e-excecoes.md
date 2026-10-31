
# Prompt 02 – Geração de dados de teste e cenários de exceção

## Objetivo

Utilizar a GenAI para ampliar a cobertura dos testes de integração, explorando condições de contorno, dados inválidos e possíveis falhas na comunicação entre componentes.

## Prompt utilizado

Atue como um engenheiro de QA especializado em testes de integração.

Considere uma API REST de gerenciamento de tarefas integrada a um banco de dados PostgreSQL.

Gere dados de teste e cenários de falha para validar a integração entre os componentes.

Considere as seguintes situações:

1. Campos obrigatórios vazios ou nulos.
2. Tipos de dados incorretos.
3. Textos com caracteres especiais.
4. Identificadores inexistentes.
5. Requisições simultâneas para atualização do mesmo registro.
6. Indisponibilidade do banco de dados.
7. Falhas durante a persistência das informações.

Para cada cenário, informe:

- Identificador do caso de teste.
- Descrição do cenário.
- Dados utilizados.
- Requisição HTTP.
- Código HTTP esperado.
- Comportamento esperado no banco de dados.
- Critérios de validação.

Inclua cenários positivos e negativos quando aplicável.

Não invente comportamentos de negócio não especificados. Quando uma regra estiver ausente, sinalize a necessidade de validação humana.

## Resultado esperado

Uma coleção de casos de teste que explore situações menos comuns, condições de contorno e possíveis falhas de integração, contribuindo para uma suíte de testes mais robusta.
