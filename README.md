# QA Automation Cypress

Projeto de **Quality Assurance e Automação de Testes E2E** utilizando Cypress, desenvolvido com foco na demonstração prática de experiência em processos, estratégias e técnicas de QA aplicadas a uma aplicação web.

> **Importante:** este repositório não foi criado como um curso, tutorial ou conjunto de exercícios para aprendizado de Cypress.
>
> O objetivo é apresentar uma **demonstração prática de experiência em QA**, utilizando uma aplicação pública como *System Under Test (SUT)* e aplicando uma abordagem estruturada de análise, planejamento, execução, automação e documentação de testes.

---

## Objetivo

Demonstrar, por meio de um projeto prático, como uma atividade de QA pode ser estruturada desde a análise inicial do sistema até a implementação e execução dos testes automatizados.

O projeto busca evidenciar não apenas o conhecimento da ferramenta Cypress, mas principalmente a capacidade de:

* analisar funcionalidades e comportamentos;
* interpretar requisitos e regras de negócio;
* identificar riscos;
* definir escopo e estratégia de testes;
* elaborar cenários de teste;
* priorizar cenários;
* transformar cenários em testes automatizados;
* validar resultados;
* registrar evidências;
* analisar falhas;
* manter rastreabilidade entre documentação e automação.

---

# System Under Test

A aplicação utilizada como **System Under Test (SUT)** é uma aplicação web pública de demonstração voltada ao cenário de **e-commerce**.

A escolha de uma aplicação pública permite desenvolver e disponibilizar o projeto sem utilizar sistemas, dados, informações ou artefatos pertencentes a ambientes corporativos.

A aplicação utilizada no projeto é o **SauceDemo**.

---

# Abordagem de QA

A automação não será tratada como uma atividade isolada.

O projeto seguirá uma abordagem baseada no fluxo:

```text
Requisitos / Contexto
        ↓
Análise da funcionalidade
        ↓
Regras de negócio
        ↓
Identificação de riscos
        ↓
Estratégia de testes
        ↓
Mapa de testes
        ↓
Cenários de teste
        ↓
Casos de teste
        ↓
Automação
        ↓
Execução
        ↓
Evidências
        ↓
Análise dos resultados
```

A intenção é demonstrar que **a automação é consequência de uma estratégia de testes**, e não o ponto de partida do processo.

---

# Escopo inicial

O projeto será desenvolvido inicialmente considerando os principais fluxos de um e-commerce:

### Autenticação

* Login com credenciais válidas;
* Login com credenciais inválidas;
* validações de autenticação;
* comportamento de usuário bloqueado.

### Produtos

* listagem de produtos;
* ordenação;
* acesso aos detalhes;
* inclusão de produtos no carrinho.

### Carrinho

* inclusão de produtos;
* visualização dos itens;
* remoção de produtos;
* comportamento do carrinho vazio.

### Checkout

* preenchimento dos dados;
* validação dos campos;
* resumo da compra;
* finalização do pedido.

### Smoke Test

Validação do fluxo crítico:

```text
Login
  ↓
Produtos
  ↓
Carrinho
  ↓
Checkout
  ↓
Finalização
```

O escopo poderá ser ampliado conforme a evolução do projeto.

---

# Estratégia de testes

A estratégia será definida considerando **risco, criticidade e impacto funcional**, e não apenas a facilidade de automação.

Os principais tipos de teste considerados são:

| Tipo         | Objetivo                                                                     |
| ------------ | ---------------------------------------------------------------------------- |
| Smoke        | Validar rapidamente os fluxos críticos da aplicação                          |
| Funcional    | Validar o comportamento esperado das funcionalidades                         |
| Regressão    | Verificar se alterações impactaram funcionalidades existentes                |
| Negativo     | Validar comportamentos diante de entradas ou condições inválidas             |
| Exploratório | Identificar comportamentos não previstos nos cenários inicialmente definidos |
| E2E          | Validar fluxos completos sob a perspectiva do usuário                        |

---

# Documentação

A documentação será mantida separada da implementação da automação.

Os cenários serão definidos e documentados antes de sua implementação no Cypress, permitindo rastrear a relação entre:

```text
Cenário de QA
      ↓
Caso de teste
      ↓
Teste automatizado
      ↓
Execução
      ↓
Resultado
      ↓
Evidência
```

---

# Arquitetura do projeto

A estrutura do repositório será organizada de forma a separar documentação, especificações, automação, dados e evidências.

```text
qa-automation-cypress/
│
├── README.md
│
├── docs/
│   │
│   ├── estrategia/
│   │   └── estrategia-de-testes.md
│   │
│   ├── requisitos/
│   │   └── requisitos.md
│   │
│   ├── cenarios/
│   │   ├── login.md
│   │   ├── produtos.md
│   │   ├── carrinho.md
│   │   └── checkout.md
│   │
│   ├── mapa-de-testes/
│   │   └── mapa-de-testes.md
│   │
│   └── resultados/
│       └── README.md
│
├── cypress/
│   │
│   ├── e2e/
│   │
│   ├── fixtures/
│   │
│   └── support/
│
├── evidencias/
│   └── README.md
│
├── .gitignore
├── cypress.config.js
└── package.json
```

A estrutura será evoluída conforme novas necessidades surgirem. Pastas e recursos não serão adicionados apenas por convenção, mas quando houver uma finalidade dentro do projeto.

---

# Automação

A automação será implementada utilizando:

* **Cypress**
* **JavaScript**
* **Node.js**

A implementação buscará seguir princípios de:

* legibilidade;
* reutilização;
* manutenção;
* estabilidade;
* independência entre testes;
* assertions claras;
* organização por funcionalidade;
* redução de duplicidade;
* boas práticas de automação E2E.

---

# Dados de teste

Os dados utilizados durante os testes serão organizados de forma independente da implementação sempre que aplicável.

Serão considerados recursos como:

* fixtures;
* massa de dados;
* variáveis de ambiente;
* dados específicos por cenário.

Informações sensíveis, credenciais pessoais ou dados pertencentes a ambientes corporativos não serão armazenados no repositório.

---

# Evidências e resultados

A execução dos testes poderá gerar artefatos destinados à análise dos resultados, incluindo:

* screenshots;
* vídeos;
* logs;
* relatórios;
* resultados de execução.

As evidências serão utilizadas para facilitar a investigação de falhas e demonstrar a rastreabilidade dos testes.

---

# Critérios de qualidade

O resultado do projeto não será avaliado apenas pela quantidade de testes automatizados.

Também serão considerados:

* cobertura dos cenários relevantes;
* priorização baseada em risco;
* clareza da documentação;
* qualidade dos cenários;
* estabilidade da automação;
* facilidade de manutenção;
* qualidade das assertions;
* rastreabilidade;
* qualidade das evidências;
* capacidade de análise dos resultados.

---

# Evolução do projeto

O projeto será desenvolvido de forma incremental.

## Planejamento e análise

* [x] Definir objetivo do projeto
* [x] Definir aplicação sob teste
* [x] Definir abordagem de QA
* [x] Definir arquitetura inicial
* [ ] Levantar funcionalidades
* [ ] Identificar requisitos e regras
* [ ] Identificar riscos
* [ ] Definir estratégia de testes
* [ ] Criar mapa de testes

## Cenários

* [ ] Criar cenários de autenticação
* [ ] Criar cenários de produtos
* [ ] Criar cenários de carrinho
* [ ] Criar cenários de checkout
* [ ] Definir cenários de smoke
* [ ] Definir cenários de regressão

## Automação

* [ ] Configurar Cypress
* [ ] Implementar primeiros testes E2E
* [ ] Implementar assertions
* [ ] Estruturar dados de teste
* [ ] Criar comandos reutilizáveis
* [ ] Organizar testes por funcionalidade
* [ ] Implementar smoke test

## Execução e evidências

* [ ] Executar testes
* [ ] Registrar resultados
* [ ] Gerar evidências
* [ ] Analisar falhas
* [ ] Documentar resultados

## Evolução

* [ ] Interceptação de APIs
* [ ] Testes de API quando aplicável
* [ ] Execução headless
* [ ] Relatórios
* [ ] Integração com CI/CD

---

# Tecnologias

| Tecnologia | Utilização                   |
| ---------- | ---------------------------- |
| Cypress    | Automação de testes E2E      |
| JavaScript | Desenvolvimento dos testes   |
| Node.js    | Ambiente de execução         |
| Git        | Controle de versão           |
| GitHub     | Versionamento e documentação |

---

# Status

**Em desenvolvimento**

O projeto será evoluído progressivamente, mantendo a documentação alinhada às funcionalidades analisadas, aos cenários definidos e à implementação automatizada.

---

## Considerações

Este repositório representa uma **demonstração prática de conhecimentos e experiência em Quality Assurance e automação de testes**.

A aplicação utilizada é pública e serve exclusivamente como *System Under Test* para a construção deste projeto.

Nenhum sistema, dado, requisito confidencial, documentação interna ou informação pertencente a projetos corporativos é utilizado neste repositório.
