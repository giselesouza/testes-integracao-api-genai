
# Testes de Integração de API com GenAI

## 1. Objetivo

Este projeto tem como objetivo demonstrar como a Inteligência Artificial Generativa (GenAI) pode apoiar a criação de casos de teste de integração, contribuindo para ampliar a cobertura dos testes e identificar possíveis falhas na comunicação entre componentes de software.

A atividade utiliza dois tipos de prompts para gerar cenários de integração, dados de teste e situações de exceção.

## 2. Cenário escolhido

Foi utilizado como exemplo um sistema de gerenciamento de tarefas, composto por:

- API REST responsável pelo recebimento e processamento das requisições.
- Banco de dados PostgreSQL responsável pelo armazenamento das informações.
- Comunicação entre API e banco de dados para cadastro, consulta, atualização e exclusão de tarefas.

### Endpoints considerados

| Método | Endpoint | Descrição |
|---|---|---|
| POST | /tasks | Cadastrar tarefa |
| GET | /tasks | Listar tarefas |
| GET | /tasks/{id} | Consultar tarefa |
| PUT | /tasks/{id} | Atualizar tarefa |
| DELETE | /tasks/{id} | Excluir tarefa |

## 3. Ferramenta de GenAI utilizada

- Ferramenta: ChatGPT
- Tipo de modelo: Large Language Model (LLM)
- Aplicação: geração e refinamento de cenários de testes de integração.

## 4. Prompts utilizados

Foram definidos dois tipos de prompts:

### Prompt 01 – Geração de cenários de integração

Objetivo: gerar cenários positivos e negativos para validar a comunicação entre a API REST e o banco de dados.

O prompt solicita casos de teste para operações de cadastro, consulta, atualização e exclusão, considerando a persistência e recuperação das informações.

### Prompt 02 – Geração de dados de teste e cenários de exceção

Objetivo: explorar situações de erro e condições de contorno que possam comprometer a integração.

Foram considerados campos obrigatórios vazios, tipos de dados incorretos, caracteres especiais, identificadores inexistentes, requisições simultâneas e indisponibilidade do banco de dados.

Os prompts completos estão disponíveis na pasta `prompts`.

## 5. Casos de teste gerados

Os casos de teste foram organizados em duas categorias:

- `casos-integracao-positivos-negativos.md`: operações principais e validações de integração.
- `casos-integracao-excecoes.md`: condições de contorno, falhas e tratamento de exceções.

Cada caso apresenta identificador, cenário, pré-condições, dados de entrada, passos e resultado esperado.

## 6. Estratégia de validação

A validação dos cenários considera:

- Recebimento correto das requisições pela API.
- Retorno dos códigos HTTP esperados.
- Persistência correta das informações no PostgreSQL.
- Consistência dos dados após operações de atualização e exclusão.
- Tratamento adequado de entradas inválidas.
- Ausência de registros inconsistentes em situações de falha.

Os comportamentos esperados devem ser confrontados com o contrato da API e as regras de negócio efetivamente definidas.

## 7. Análise dos resultados

O primeiro prompt contribuiu para organizar os cenários relacionados ao fluxo principal da aplicação, permitindo identificar situações positivas e negativas nas operações disponibilizadas pela API.

O segundo prompt ampliou a diversidade dos testes ao explorar dados inválidos, condições de contorno e falhas na comunicação entre os componentes.

Durante o refinamento, foi necessário fornecer informações mais específicas sobre os endpoints, os componentes envolvidos e o formato esperado para os casos de teste.

Também foi importante orientar a LLM a não presumir regras de negócio não especificadas, indicando quando uma validação humana seria necessária.

## 8. Considerações finais

A utilização da GenAI como copiloto na elaboração de testes de integração pode contribuir para aumentar a produtividade do QA, ampliar a cobertura dos cenários e identificar situações que poderiam passar despercebidas durante a elaboração manual dos testes.

Entretanto, os resultados gerados precisam ser revisados por um profissional de QA, principalmente para validar regras de negócio, critérios de aceitação e comportamentos esperados.

A GenAI auxilia na construção da suíte de testes, mas não substitui o conhecimento técnico e o julgamento humano.

## 9. Evidências

Os prompts utilizados, exemplos de resultados e análise crítica estão documentados na pasta `evidencias`.

As evidências de execução devem ser complementadas com os registros reais das interações com a LLM.

---

**Projeto acadêmico – Unidade III**  
**Tema:** Testes de integração apoiados por Inteligência Artificial Generativa.
