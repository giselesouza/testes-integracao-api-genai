
# Evidências – Experimentação de Prompts com GenAI

## 1. Identificação da experimentação

| Informação | Descrição |
|---|---|
| Ferramenta utilizada | ChatGPT |
| Tecnologia | Inteligência Artificial Generativa |
| Modelo | LLM |
| Tema | Testes de integração |
| Cenário | API REST integrada ao PostgreSQL |
| Quantidade de prompts | 2 |

## 2. Experimentação do Prompt 01

**Objetivo:** gerar cenários de integração entre a API REST e o banco de dados.

**Prompt utilizado:**

Consultar o arquivo:
`prompts/prompt-01-cenarios-integracao.md`

**Resultado esperado da experimentação:**

A LLM deve produzir casos de teste relacionados às operações de cadastro, consulta, atualização e exclusão de tarefas.

Entre os cenários identificados estão:

- Cadastro de tarefa com dados válidos.
- Consulta de tarefas cadastradas.
- Atualização de registros existentes.
- Exclusão de tarefas.
- Consulta de identificadores inexistentes.
- Envio de informações inválidas.
- Verificação da persistência dos dados.

**Avaliação da qualidade:**

O prompt direcionado à geração de cenários contribui para organizar os fluxos principais da aplicação e identificar diferentes possibilidades de validação.

A definição dos endpoints e dos campos esperados permite obter resultados mais estruturados e relacionados ao contexto apresentado.

## 3. Experimentação do Prompt 02

**Objetivo:** gerar dados de teste, condições de contorno e cenários de exceção.

**Prompt utilizado:**

Consultar o arquivo:
`prompts/prompt-02-dados-e-excecoes.md`

**Resultado esperado da experimentação:**

A LLM deve explorar situações menos comuns, como:

- Campos obrigatórios nulos.
- Tipos de dados incorretos.
- Caracteres especiais.
- Identificadores inexistentes.
- Atualizações simultâneas.
- Indisponibilidade do banco de dados.
- Falhas durante a persistência.

**Avaliação da qualidade:**

O segundo prompt amplia a diversidade dos cenários, direcionando a análise para condições de erro e situações que podem comprometer a integridade das informações.

A solicitação de critérios de validação no banco de dados contribui para que os testes não fiquem restritos apenas à verificação do código HTTP.

## 4. Ajustes realizados nos prompts

Durante o refinamento dos prompts, foram considerados os seguintes ajustes:

| Ajuste | Benefício esperado |
|---|---|
| Informar os endpoints da API | Reduzir respostas genéricas |
| Descrever os componentes envolvidos | Contextualizar a integração |
| Separar cenários positivos e negativos | Melhorar a organização |
| Solicitar dados de entrada | Facilitar a execução dos testes |
| Definir os campos da tabela de saída | Padronizar os casos |
| Solicitar validação no banco | Ampliar a cobertura da integração |
| Orientar a não inventar regras | Reduzir suposições indevidas |

## 5. Comparação entre os prompts

| Critério | Prompt 01 | Prompt 02 |
|---|---|---|
| Foco principal | Fluxos de integração | Falhas e exceções |
| Cenários positivos | Sim | Quando aplicável |
| Cenários negativos | Sim | Sim |
| Dados de teste | Básicos | Diversificados e de contorno |
| Validação de persistência | Sim | Sim |
| Concorrência | Não é o foco | Sim |
| Indisponibilidade do banco | Sim | Sim |

## 6. Análise crítica

A utilização dos dois prompts demonstrou que a forma de estruturar uma solicitação influencia diretamente a qualidade dos resultados produzidos pela LLM.

O primeiro prompt direciona a geração de cenários relacionados ao funcionamento esperado da aplicação, enquanto o segundo explora situações de falha, entradas inválidas e condições de contorno.

A combinação das duas abordagens permite construir uma suíte de testes mais diversificada.

Entretanto, a LLM pode sugerir códigos HTTP, regras de validação e comportamentos que não correspondem necessariamente à implementação real. Por isso, a revisão humana é indispensável.

## 7. Evidências reais da execução

**Inserir nesta seção as capturas de tela das interações realizadas com o ChatGPT.**

### Evidência 01 – Execução do Prompt 01

- Captura de tela do prompt enviado.
- Captura de tela dos casos de teste retornados pela LLM.

Arquivo sugerido:
`evidencia-prompt-01.png`

### Evidência 02 – Execução do Prompt 02

- Captura de tela do prompt enviado.
- Captura de tela dos cenários de exceção retornados pela LLM.

Arquivo sugerido:
`evidencia-prompt-02.png`

### Evidência 03 – Refinamento dos resultados

- Captura de tela de uma interação solicitando melhorias ou ajustes nos casos gerados.
- Exemplo: solicitar critérios de validação no banco de dados e separação dos cenários por prioridade.

Arquivo sugerido:
`evidencia-refinamento.png`

## 8. Conclusão

A experimentação com GenAI evidencia seu potencial como ferramenta de apoio ao trabalho de QA, especialmente na identificação de cenários de integração, geração de dados de teste e exploração de situações de exceção.

Os prompts mais específicos permitem resultados mais organizados e contextualizados.

Conclui-se que a GenAI pode atuar como copiloto na construção de suítes de testes mais robustas, desde que os resultados sejam revisados e validados por um profissional.

A responsabilidade pela qualidade final dos casos de teste continua sendo humana.
