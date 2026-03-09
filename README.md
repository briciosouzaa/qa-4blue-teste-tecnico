# Teste Técnico – QA Tester – 4blue

Este repositório contém a análise de testes realizada no microssistema disponibilizado no processo seletivo para a vaga de QA Tester da 4blue.

## Índice
- [1. Objetivo](#1-objetivo)
- [2. Sistema analisado](#2-sistema-analisado)
- [3. Estratégia de teste utilizada](#3-estratégia-de-teste-utilizada)
- [4. Bugs encontrados](#4-bugs-encontrados)
- [5. Quais 2 bugs corrigiria primeiro e por quê](#5-quais-2-bugs-corrigiria-primeiro-e-por-quê)
- [6. Sugestões de melhoria](#6-sugestões-de-melhoria)
- [7. Resumo da análise](#7-resumo-da-análise)

## 1. Objetivo

Realizar a análise funcional, de experiência do usuário e de segurança do microssistema disponibilizado no teste técnico da 4blue.

## 2. Sistema analisado

Sistema analisado:
- Tela de Login
- Tela de Criação de Conta
- Tela de Sucesso

URL:
- https://qa-play-sim.lovable.app/

## 3. Estratégia de teste utilizada

A análise foi realizada por meio de testes exploratórios, com foco em:

- validação funcional dos fluxos principais
- validação de campos e regras de negócio
- identificação de inconsistências de experiência do usuário
- verificação de problemas básicos de segurança
- priorização de defeitos por impacto

## 4. Bugs encontrados

### Bug 1 — Formulário de criação de conta permite envio com campos obrigatórios vazios

**Descrição:** O formulário permite a criação de conta mesmo quando nenhum campo é preenchido.

**Passos para reproduzir**
1. Na tela de Login, clicar em "Criar Conta".
2. Ao acessar a tela de criação de conta, não preeencher nenhum campo.
3. Clicar em **Criar conta**.

**Resultado atual:**
A conta é criada com sucesso.

**Resultado esperado:**
O sistema deve impedir o envio do formulário e exibir mensagens indicando os campos obrigatórios.

**Severidade:**
Alto

**Prioridade:**
Alta

### Bug 2 — Sistema aceita senha fora da política definida

**Descrição:**
A interface informa que a senha deve ter mínimo de 8 caracteres e 1 caractere especial, porém o sistema aceita senhas simples como 123.

**Passos para reproduzir**
1. Na tela de Login, clicar em "Criar Conta".
2. Ao acessar a tela de criação de conta, preencher os campos obrigatórios.
3. No campo "Senha", inserir a senha 123.
4. No campo "Confirmar Senha", confirmar a senha 123.
5. Clicar em Criar conta.

**Resultado atual:**
Conta criada com sucesso.

**Resultado esperado:**
O sistema deve impedir o cadastro e informar que a senha não atende à política de segurança.

**Severidade:**
Alto

**Prioridade:**
Alta

### Bug 3 — Senha exposta no DOM ao inspecionar o campo

**Descrição:** Ao inspecionar o campo de senha no navegador, o valor da senha digitada aparece no atributo value do input.

**Passos para reproduzir**
1. Acessar a tela de Login.
2. Digitar uma senha (123).
3. Abrir o DevTools (F12).
4. Inspecionar o campo de senha.

**Resultado atual:** A senha digitada aparece no atributo value.

**Resultado esperado:** A senha não deve ficar exposta no DOM.

**Severidade:** Alto

**Prioridade:** Alta

### Bug 4 — Login é permitido sem validação correta de credenciais

**Descrição:** O sistema permite acesso mesmo quando as credenciais informadas são inválidas ou inexistentes.

**Passos para reproduzir**
1. Acessar a tela de login.
2. Informar credenciais inválidas ou deixar campos vazios.
3. Clicar em Entrar.

**Resultado atual:** O acesso ao sistema é permitido.

**Resultado esperado:** O sistema deve validar credenciais antes de permitir acesso.

**Severidade:** Crítico

**Prioridade:** Alta

### Bug 5 — Acesso ao sistema possível apenas manipulando a URL

**Descrição:** É possível acessar a área interna do sistema diretamente através da URL, sem autenticação.

**Passos para reproduzir**
1. Copiar a URL da tela de sucesso.
2. Abrir nova aba do navegador.
3. Colar a URL diretamente.

**Resultado atual:** A página é carregada mesmo sem login.

**Resultado esperado:** O sistema deve redirecionar o usuário para a tela de login caso não esteja autenticado.

**Severidade:** Crítico

**Prioridade:** Alta

### Bug 6 — Campo “Nome completo” aceita apenas um nome

**Descrição:** O campo “Nome completo” permite cadastro utilizando apenas um nome.

**Passos para reproduzir**
1. Na tela de Login, clicar em "Criar Conta".
2. Ao acessar a tela de criação de conta, inserir apenas um nome no campo.
3. Completar cadastro.
4. Clicar em Criar Conta.

**Resultado atual:** Conta criada normalmente.

**Resultado esperado:** O sistema deve exigir nome e sobrenome ou alterar o label para apenas "Nome".

**Severidade:** Médio

**Prioridade:** Média

### Bug 7 — Campo telefone não aplica máscara de formatação

**Descrição:** O campo telefone sugere um formato específico, mas não aplica máscara automática.

**Passos para reproduzir**
1. Na tela de Login, clicar em "Criar Conta".
2. Ao acessar a tela de criação de conta, inserir caracteres e numeros no campo Telefone.
3. Completar cadastro.
4. Clicar em Criar Conta.

**Resultado atual:** Aceita números sem formatação e caracteres.

**Resultado esperado:** Aplicar máscara automaticamente ou validar formato não permitindo caracteres, somente números.

**Severidade:** Baixo

**Prioridade:** Baixa

### Bug 8 — Ausência de mensagens de validação no formulário

**Descrição:** O sistema não apresenta feedback de erro ao usuário quando dados inválidos são inseridos.

**Passos para reproduzir**
1. Na tela de Login, clicar em "Criar Conta".
2. Ao acessar a tela de criação de conta, deixar algum campo vazio ou preencher o campo de e-mail com e-mail inválido.
3. Completar cadastro.
4. Clicar em Criar Conta.

**Resultado atual:** Nenhuma mensagem ou indicação visual aparece.

**Resultado esperado:** O sistema deve apresentar mensagens claras de validação.

**Severidade:** Médio

**Prioridade:** Média

### Bug 9 — Sistema exibe mensagem “Erro inesperado” após login

**Descrição:** Após realizar login, o sistema apresenta mensagem de erro mesmo quando o acesso ocorre.

**Passos para reproduzir**
1. Na tela de Login, efetuar o login com as credênciais válidas.
2. Ao acessar a tela de criação de conta, inserir apenas um nome no campo..
3. Clicar em Entrar.

**Resultado atual:** Mensagem “Erro inesperado” aparece após login.

**Resultado esperado:** Caso o login seja bem sucedido, nenhuma mensagem de erro deve ser exibida.

**Severidade:** Médio

**Prioridade:** Média

## 5. Quais 2 bugs corrigiria primeiro e por quê

### 1. Login permitido sem validação de credenciais
Esse bug possui severidade crítica, pois compromete diretamente o mecanismo de autenticação do sistema e permite acesso indevido.

### 2. Acesso ao sistema possível apenas manipulando a URL
Esse bug também possui severidade crítica, pois caracteriza bypass de autenticação e permite acesso a páginas internas sem sessão válida.

## 6. Sugestões de melhoria

### Validação
- Implementar validação de formulário antes do envio
- Bloquear submissão com campos obrigatórios vazios
- Validar corretamente a política de senha

### UX
- Exibir mensagens de erro claras abaixo dos campos
- Aplicar máscara automática no campo telefone
- Destacar visualmente campos inválidos

### Segurança
- Impedir acesso a páginas internas sem autenticação
- Validar credenciais corretamente no login
- Evitar exposição de dados sensíveis no DOM

## 7. Resumo da análise

| Severidade | Quantidade |
|------------|------------|
Crítico | 2 |
Alto | 3 |
Médio | 3 |
Baixo | 1 |

Total de bugs encontrados: **9**
