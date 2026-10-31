
# Casos de Teste – Exceções e Condições de Contorno

## 1. Objetivo

Avaliar o comportamento da integração entre a API REST e o PostgreSQL em situações de erro, dados inválidos e condições que possam comprometer a consistência das informações.

## 2. Casos de teste

### CT08 – Cadastro com campo nulo

- **Prioridade:** Alta
- **Tipo:** Negativo
- **Endpoint:** POST /tasks

**Dados de entrada:**
```json
{
  "title": null,
  "description": "Teste de campo nulo",
  "status": "pending"
}
```

**Passos:**
1. Enviar a requisição POST com title nulo.
2. Verificar a resposta da API.
3. Consultar o banco de dados.

**Resultado esperado:**
- Requisição rejeitada conforme validação do contrato.
- Retorno HTTP 400.
- Nenhum registro inválido persistido.

---

### CT09 – Envio de tipo de dado incorreto

- **Prioridade:** Média
- **Tipo:** Negativo
- **Endpoint:** POST /tasks

**Dados de entrada:**
```json
{
  "title": 12345,
  "description": "Teste de tipo incorreto",
  "status": "pending"
}
```

**Passos:**
1. Enviar a requisição com tipo incorreto no campo title.
2. Verificar o processamento da API.
3. Consultar o banco para verificar a persistência.

**Resultado esperado:**
- Requisição rejeitada pela validação da API.
- Retorno HTTP 400 ou 422, conforme contrato.
- Nenhum registro inválido persistido.

---

### CT10 – Cadastro com caracteres especiais

- **Prioridade:** Média
- **Tipo:** Positivo
- **Endpoint:** POST /tasks

**Dados de entrada:**
```json
{
  "title": "Teste de integração: ação, revisão e automação!",
  "description": "Validação de caracteres especiais: @#$%&*",
  "status": "pending"
}
```

**Passos:**
1. Enviar a requisição POST.
2. Verificar o retorno da API.
3. Consultar o banco de dados.
4. Recuperar a tarefa cadastrada.

**Resultado esperado:**
- Cadastro realizado com sucesso, caso os caracteres sejam permitidos.
- Dados armazenados sem corrupção.
- Informações recuperadas corretamente.

---

### CT11 – Atualizações simultâneas no mesmo registro

- **Prioridade:** Alta
- **Tipo:** Concorrência
- **Endpoint:** PUT /tasks/{id}

**Pré-condições:**
- Existência de uma tarefa cadastrada.
- Possibilidade de enviar requisições simultâneas.

**Dados de entrada:**

Requisição A:
```json
{
  "title": "Atualização A",
  "description": "Alteração realizada pelo usuário A",
  "status": "pending"
}
```

Requisição B:
```json
{
  "title": "Atualização B",
  "description": "Alteração realizada pelo usuário B",
  "status": "completed"
}
```

**Passos:**
1. Enviar duas requisições PUT simultaneamente para o mesmo ID.
2. Verificar as respostas recebidas.
3. Consultar o registro no banco.
4. Avaliar a consistência dos dados.

**Resultado esperado:**
- As requisições devem ser processadas conforme a estratégia de concorrência definida.
- O registro deve permanecer consistente.
- Caso exista controle de versão, conflitos devem ser tratados adequadamente.

**Ponto de atenção:** validar se a aplicação utiliza controle de concorrência otimista ou pessimista.

---

### CT12 – Indisponibilidade do banco de dados

- **Prioridade:** Alta
- **Tipo:** Exceção
- **Endpoint:** POST /tasks

**Pré-condições:**
- API em execução.
- Banco de dados temporariamente indisponível.

**Dados de entrada:**
```json
{
  "title": "Teste de indisponibilidade",
  "description": "Validar falha de conexão",
  "status": "pending"
}
```

**Passos:**
1. Simular a indisponibilidade do PostgreSQL em ambiente controlado.
2. Enviar uma requisição POST.
3. Verificar a resposta da API.
4. Consultar os logs da aplicação.

**Resultado esperado:**
- A aplicação deve tratar a falha de conexão.
- Retorno HTTP 503 ou outro código definido pelo contrato.
- Mensagem de erro controlada, sem exposição de informações internas.
- Nenhum registro parcialmente persistido.

---

### CT13 – Falha durante a persistência dos dados

- **Prioridade:** Alta
- **Tipo:** Exceção
- **Endpoint:** POST /tasks

**Pré-condições:**
- API disponível.
- Banco de dados conectado.
- Possibilidade de simular falha durante uma transação em ambiente de testes.

**Passos:**
1. Iniciar uma operação de cadastro.
2. Simular uma falha durante a gravação.
3. Verificar a resposta da API.
4. Consultar o banco de dados.
5. Verificar se houve gravação parcial.

**Resultado esperado:**
- Falha tratada adequadamente.
- Operação revertida quando houver transação com rollback.
- Ausência de registros inconsistentes.
- Registro do erro nos logs da aplicação.

---

## 3. Critérios gerais de aprovação

- A aplicação deve tratar entradas inválidas sem comprometer a integridade dos dados.
- Falhas de conexão devem gerar respostas controladas.
- Operações com falha devem respeitar as garantias transacionais implementadas.
- Atualizações simultâneas não devem gerar inconsistências.
- Os dados devem permanecer íntegros após as operações.

## 4. Pontos que precisam de validação humana

Alguns comportamentos dependem de regras que não foram especificadas no cenário:

- Código HTTP para indisponibilidade do banco.
- Política de concorrência entre atualizações.
- Política de exclusão física ou lógica.
- Limites de caracteres dos campos.
- Estratégia de rollback e tratamento de transações.
- Possibilidade de repetição automática de requisições após falhas.

Esses pontos devem ser confirmados antes da execução dos testes em um sistema real.
