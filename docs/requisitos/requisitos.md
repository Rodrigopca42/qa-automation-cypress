# Requisitos

## 1. Objetivo

Documentar os requisitos funcionais, comportamentos observados e características identificadas durante a análise inicial do **SauceDemo**, utilizado neste projeto como *System Under Test (SUT)*.

Este documento servirá como base para a definição da estratégia de testes, identificação de riscos, elaboração dos cenários e posterior implementação da automação com Cypress.

---

# 2. Sistema sob teste

**Aplicação:** SauceDemo
**Domínio:** E-commerce
**Tipo:** Aplicação Web
**Modelo de produto:** Produtos físicos

A aplicação apresenta um fluxo de compra composto, principalmente, por:

```text
Autenticação
    ↓
Catálogo
    ↓
Produto
    ↓
Carrinho
    ↓
Checkout
    ↓
Finalização
```

---

# 3. Acesso e autenticação

## 3.1 Acesso ao sistema

### Requisitos / comportamentos identificados

* O usuário não consegue acessar a área principal da aplicação sem realizar autenticação.
* A aplicação não apresenta uma página inicial de apresentação antes do login.
* O acesso depende de um usuário e senha previamente cadastrados.
* Não foi identificada funcionalidade de criação de novos usuários.

### Validações observadas

| Cenário                                              | Comportamento observado              |
| ---------------------------------------------------- | ------------------------------------ |
| Usuário válido + senha válida                        | Permite acesso ao sistema            |
| Usuário inválido + senha válida                      | Apresenta mensagem de erro           |
| Usuário válido + senha inválida                      | Apresenta mensagem de erro           |
| Usuário não autenticado tentando acessar a aplicação | Permanece dependente da autenticação |

---

# 4. Catálogo de produtos

Após a autenticação, o usuário tem acesso ao catálogo de produtos.

Os produtos apresentados são produtos físicos.

## 4.1 All Items

A página **All Items** apresenta os produtos disponíveis para seleção e inclusão no carrinho.

Cada card de produto apresenta:

* título;
* descrição;
* preço;
* imagem;
* botão para adicionar o produto ao carrinho.

A área de interação do produto inclui:

* título do produto;
* botão de ação.

O título direciona o usuário para a página de detalhes do produto (PDP).

---

# 5. Dynamic Catalog

O menu apresenta uma opção denominada **Dynamic Catalog**.

Essa área disponibiliza as seguintes opções:

* Lazy Load;
* Spinner;
* Slider.

Os produtos apresentados nessas páginas não disponibilizam a opção observada de inclusão no carrinho.

Essas páginas serão consideradas no escopo de análise, porém seu comportamento será tratado separadamente do catálogo utilizado para o fluxo principal de compra.

---

# 6. Página de detalhes do produto — PDP

A PDP apresenta:

* título;
* descrição;
* preço;
* botão de ação.

O título do produto na PDP não é clicável.

## 6.1 Estado do produto

Quando o produto não está no carrinho:

```text
Add to cart
```

Quando o produto está no carrinho:

```text
Remove
```

Ao adicionar um produto:

* o texto do botão é alterado de `Add to cart` para `Remove`;
* o botão altera sua apresentação visual;
* o indicador do minicart passa a apresentar a quantidade de produtos adicionados.

---

# 7. Navegação entre catálogo e produto

Foi observado que o acesso aos detalhes do produto ocorre por meio do título do produto.

Esse comportamento é aplicável às áreas observadas de:

* PLP / catálogo;
* carrinho;
* checkout.

O acesso direciona o usuário para a página correspondente ao produto.

---

# 8. Menu de navegação

O sistema possui um menu acessível por meio do botão *hamburger*.

Ao acioná-lo, uma lista de opções é apresentada.

As opções observadas são:

* All Items;
* Dynamic Catalog;
* About;
* Logout;
* Reset App State.

## 8.1 Logout

A opção **Logout** encerra a sessão do usuário.

## 8.2 About

A opção **About** direciona o usuário para outro site.

Durante a análise foi observado que a página de destino não apresenta uma opção aparente para retornar diretamente à aplicação SauceDemo.

## 8.3 Reset App State

A opção **Reset App State** está disponível no menu.

Durante a análise inicial, não foi observado comportamento aparente após sua utilização.

> Esse comportamento será tratado como **ponto de investigação**, não como defeito confirmado.

---

# 9. Minicart

O minicart pode ser acessado mesmo quando nenhum produto foi selecionado.

Quando existem produtos adicionados ao carrinho, o minicart apresenta um indicador visual com a quantidade de produtos.

Também foi observado que:

* o usuário consegue acessar o carrinho vazio;
* o usuário consegue prosseguir para o checkout mesmo sem produtos no carrinho;
* foi observado um fluxo de finalização de compra sem produtos.

Esses comportamentos serão analisados posteriormente sob a perspectiva de regra de negócio e risco.

---

# 10. Carrinho

Os produtos adicionados ao carrinho apresentam:

* quantidade;
* título;
* descrição;
* preço;
* opção para remoção do produto.

## 10.1 Elementos não observados

Na análise inicial não foram identificados:

* controles `+` e `-` para alteração da quantidade;
* soma individual dos produtos apresentada como subtotal;
* informação de frete;
* resumo detalhado do pedido.

Essas características serão consideradas na análise funcional e de escopo.

---

# 11. Sessão

Durante a análise foi observado que, após determinado período de inatividade, o usuário pode ser deslogado automaticamente.

Esse comportamento será posteriormente investigado para determinar:

* condição necessária para expiração;
* tempo aproximado;
* comportamento esperado após a expiração;
* impacto sobre dados eventualmente inseridos pelo usuário.

---

# 12. Checkout

O checkout exige o preenchimento de informações de identificação do comprador.

Os campos observados são:

* First Name;
* Last Name;
* Zip/Postal Code.

## 12.1 Validação dos dados

Foi observado que o avanço no checkout depende do preenchimento dessas informações.

Caso qualquer um dos campos obrigatórios não seja informado, o usuário não consegue prosseguir.

---

# 13. Segunda etapa do checkout

Após o preenchimento dos dados obrigatórios, o usuário é direcionado para uma segunda etapa do checkout.

Essa etapa apresenta:

* quantidade do produto;
* título do produto;
* descrição;
* preço;
* preço total;
* opção para finalizar a compra;
* opção para cancelar a compra.

O preço total apresentado considera a soma dos produtos presentes no pedido.

---

# 14. Pontos de investigação

Durante a análise inicial foram identificados comportamentos que deverão ser investigados antes de serem classificados como defeitos:

### 14.1 Checkout sem produtos

Foi observado que é possível acessar o checkout com o carrinho vazio e prosseguir pelo fluxo até a etapa de finalização.

**Questão de QA:** o sistema deveria impedir a continuidade quando não existem produtos no pedido?

---

### 14.2 Identificação no checkout

Mesmo após a autenticação, o checkout solicita novamente:

* nome;
* sobrenome;
* CEP.

**Questão de QA:** essa identificação representa uma etapa necessária para a conclusão da compra ou deveria utilizar informações previamente associadas ao usuário autenticado?

---

### 14.3 Reset App State

A opção está disponível no menu, porém não foi observado comportamento aparente durante a análise inicial.

**Questão de QA:** quais estados da aplicação deveriam ser restaurados por essa funcionalidade?

---

### 14.4 Expiração da sessão

Foi observado logout após período de inatividade.

**Questão de QA:** qual é o tempo definido para expiração e quais dados devem ser preservados ou descartados após o logout?

---

# 15. Premissas e limitações

* A aplicação utilizada é pública e foi escolhida exclusivamente como SUT para este projeto.
* O comportamento documentado neste arquivo representa o resultado da análise realizada durante a construção do projeto.
* Um comportamento observado não será automaticamente classificado como defeito.
* A classificação de defeitos dependerá da definição do comportamento esperado ou da regra de negócio correspondente.
* Não serão utilizados dados ou informações provenientes de sistemas corporativos.
* Requisitos que não possam ser determinados diretamente pela aplicação serão tratados como premissas ou pontos de investigação.

---

# 16. Próximas etapas

A partir deste levantamento serão desenvolvidos:

1. **Regras de negócio**
2. **Análise de riscos**
3. **Estratégia de testes**
4. **Mapa de testes**
5. **Cenários de teste**
6. **Casos de teste**
7. **Automação com Cypress**
