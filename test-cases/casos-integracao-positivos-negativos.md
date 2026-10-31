
# Casos de Teste – Integração API REST e PostgreSQL

## 1. Objetivo

Validar a comunicação entre a API REST de gerenciamento de tarefas e o banco de dados PostgreSQL, verificando o processamento das requisições e a consistência das informações armazenadas.

## 2. Casos de teste

### CT01 – Cadastro de tarefa com dados válidos

- **Prioridade:** Alta
- **Tipo:** Positivo
- **Endpoint:** POST /tasks

**Pré-condições:**
- API disponível.
- Banco de dados conectado.

**Dados de entrada:**
```json
{
  "title": "Estudar testes de integração",
  "description": "Praticar testes de API",
  "status": "pending"
}
```

**Passos:**
1. Enviar uma requisição POST para /tasks.
2. Informar os dados válidos.
3. Verificar a resposta da API.
4. Consultar o banco de dados para confirmar a gravação.

**Resultado esperado:**
- Retorno HTTP 201.
- Tarefa cadastrada com sucesso.
- Registro persistido corretamente no PostgreSQL.

---

### CT02 – Listagem de tarefas cadastradas

- **Prioridade:** Alta
- **Tipo:** Positivo
- **Endpoint:** GET /tasks

**Pré-condições:**
- Existência de tarefas cadastradas.

**Passos:**
1. Enviar uma requisição GET para /tasks.
2. Verificar os dados retornados.
3. Comparar os registros retornados com os dados armazenados no banco.

**Resultado esperado:**
- Retorno HTTP 200.
- Lista de tarefas apresentada corretamente.
- Dados consistentes com os registros do banco.

---

### CT03 – Consulta de tarefa existente

- **Prioridade:** Alta
- **Tipo:** Positivo
- **Endpoint:** GET /tasks/{id}

**Pré-condições:**
- Existência de uma tarefa cadastrada.

**Dados de entrada:**
- ID de uma tarefa existente.

**Passos:**
1. Enviar uma requisição GET utilizando um ID válido.
2. Verificar os dados retornados.
3. Comparar as informações com o registro no banco.

**Resultado esperado:**
- Retorno HTTP 200.
- Dados da tarefa apresentados corretamente.
- Informações consistentes com o banco de dados.

---

### CT04 – Atualização de tarefa existente

- **Prioridade:** Alta
- **Tipo:** Positivo
- **Endpoint:** PUT /tasks/{id}

**Pré-condições:**
- Existência de uma tarefa cadastrada.

**Dados de entrada:**
```json
{
  "title": "Estudar automação de testes",
  "description": "Atualização da tarefa",
  "status": "completed"
}
```

**Passos:**
1. Enviar uma requisição PUT com o ID existente.
2. Informar os novos dados.
3. Verificar a resposta da API.
4. Consultar o registro no banco.

**Resultado esperado:**
- Retorno HTTP 200.
- Dados atualizados corretamente.
- Alterações persistidas no PostgreSQL.

---

### CT05 – Exclusão de tarefa existente

- **Prioridade:** Alta
- **Tipo:** Positivo
- **Endpoint:** DELETE /tasks/{id}

**Pré-condições:**
- Existência de uma tarefa cadastrada.

**Passos:**
1. Enviar uma requisição DELETE com um ID válido.
2. Verificar a resposta da API.
3. Consultar o banco de dados para verificar a exclusão.

**Resultado esperado:**
- Retorno HTTP 204, caso esse seja o contrato definido.
- Registro excluído ou marcado como excluído, conforme a regra implementada.
- A tarefa não deve ser retornada em consultas que desconsiderem registros excluídos.

---

### CT06 – Cadastro de tarefa sem título

- **Prioridade:** Alta
- **Tipo:** Negativo
- **Endpoint:** POST /tasks

**Dados de entrada:**
```json
{
  "description": "Tarefa sem título",
  "status": "pending"
}
```

**Passos:**
1. Enviar uma requisição POST sem o campo title.
2. Verificar a resposta da API.
3. Consultar o banco para confirmar que não houve gravação indevida.

**Resultado esperado:**
- Retorno HTTP 400, conforme contrato esperado.
- Mensagem informando a ausência de campo obrigatório.
- Nenhum registro inválido persistido.

---

### CT07 – Consulta de identificador inexistente

- **Prioridade:** Média
- **Tipo:** Negativo
- **Endpoint:** GET /tasks/{id}

**Dados de entrada:**
- ID inexistente: 999999.

**Passos:**
1. Enviar uma requisição GET com o ID inexistente.
2. Verificar a resposta da API.

**Resultado esperado:**
- Retorno HTTP 404.
- Mensagem informando que a tarefa não foi encontrada.
- Nenhuma alteração no banco de dados.

---

## 3. Observações

Os códigos HTTP e as regras de persistência apresentados representam o comportamento esperado para este cenário didático.

Antes da execução em uma aplicação real, é necessário validar os resultados com o contrato da API e as regras de negócio.

## 4. Critérios gerais de aprovação

- A API deve processar corretamente as requisições.
- Os códigos HTTP devem estar de acordo com o contrato.
- Os dados devem ser persistidos e recuperados corretamente.
- Não devem ocorrer inconsistências entre a resposta da API e o banco de dados.
- As operações inválidas devem ser tratadas adequadamente.
