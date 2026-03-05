# Teste Técnico - QA Tester (4blue) 🐛

[cite_start]Este repositório contém a documentação e a análise de testes manuais exploratórios realizados no microssistema disponibilizado para o processo seletivo da **4blue**[cite: 2, 3].

## 💻 Sistema Testado
[cite_start]**Acesso:** [https://qa-play-sim.lovable.app/](https://qa-play-sim.lovable.app/) [cite: 12]

## 🎯 Objetivo da Avaliação
Explorar o sistema livremente para identificar, relatar e priorizar:
- [cite_start]Bugs funcionais [cite: 8]
- [cite_start]Inconsistências de experiência do usuário (UX/UI) [cite: 9]
- [cite_start]Problemas básicos de segurança [cite: 10]

---

## 📋 Relatório de Bugs Encontrados

Abaixo estão descritos os 13 bugs identificados durante a execução dos testes, agrupados por contexto de tela e categoria.

### 📱 Tela Inicial (Login)

**Bug 1: Regra de criação de senha exibida na tela de login**
- **Descrição:** A tela de login apresenta um texto informando: *"A senha precisa ter no mínimo 8 caracteres e 1 caractere especial"*. Esta regra pertence ao processo de criação de conta. A tela de login deve apenas receber a credencial, não informar regras de criação, o que gera inconsistência na experiência (UX).
- **Passos para reproduzir:** 1. Acessar a tela inicial de login. 2. Observar o texto de apoio abaixo do campo "Senha".
- **Resultado atual:** O texto de regra de senha está visível.
- **Resultado esperado:** O texto explicativo não deve ser exibido na tela de login.
- **Severidade:** Baixo
- **Prioridade:** Baixa

**Bug 2: Mensagem incorreta e falta de validação no login com campos vazios**
- **Descrição:** Ao tentar realizar o login sem preencher os campos, o sistema não bloqueia a ação no *front-end*. Ele processa a requisição e retorna um erro inadequado, tratando campos vazios como se fosse uma busca no banco de dados.
- **Passos para reproduzir:** 1. Acessar a tela de login. 2. Deixar Email e Senha em branco. 3. Clicar em "Entrar".
- **Resultado atual:** Popup exibe a mensagem "Usuário não encontrado".
- **Resultado esperado:** O sistema deve validar os campos antes do envio e exibir alertas de preenchimento obrigatório.
- **Severidade:** Médio
- **Prioridade:** Média

**Bug 3: Falha de autenticação permitindo acesso nulo (Segurança)**
- **Descrição:** Após falhas na criação de conta, o sistema passa a permitir que o login seja realizado com sucesso mesmo quando os campos de E-mail e Senha são enviados totalmente em branco.
- **Passos para reproduzir:** 1. Acessar a tela de login. 2. Deixar campos de credenciais vazios. 3. Clicar em "Entrar".
- **Resultado atual:** O usuário é autenticado e redirecionado para a tela de sucesso.
- **Resultado esperado:** O acesso deve ser bloqueado, exigindo credenciais válidas.
- **Severidade:** Crítico
- **Prioridade:** Alta

**Bug 4: Popup de erro inesperado ao realizar login**
- **Descrição:** Durante as tentativas de login, o sistema dispara ocasionalmente um popup informando um erro inesperado no processamento do sistema.
- **Passos para reproduzir:** 1. Inserir credenciais na tela de login. 2. Clicar em "Entrar".
- **Resultado atual:** Exibição de popup de erro inesperado.
- **Resultado esperado:** O login deve ocorrer sem mensagens de erro de sistema genéricas.
- **Severidade:** Alto
- **Prioridade:** Alta

---

### 📝 Tela de Criação de Conta

**Bug 5: Sistema permite criação de conta com campos obrigatórios vazios**
- **Descrição:** O formulário de cadastro não exige o preenchimento obrigatório dos dados. É possível criar um usuário enviando o formulário totalmente em branco ou preenchendo apenas campos isolados.
- **Passos para reproduzir:** 1. Acessar a tela "Criar conta". 2. Deixar todos os campos em branco. 3. Clicar em "Criar conta".
- **Resultado atual:** A conta é criada com sucesso sem os dados necessários.
- **Resultado esperado:** O botão "Criar conta" deve ser bloqueado ou retornar erro nos campos vazios.
- **Severidade:** Crítico
- **Prioridade:** Alta

**Bug 6: Ausência de validação de formatos e regras de negócio**
- **Descrição:** O formulário não valida os dados inseridos. Falhas mapeadas: 1) E-mails aceitos sem "@". 2) Telefone aceita letras. 3) Campos sem limite de caracteres. 4) O sistema aceita senhas divergentes na confirmação. 5) Permite senhas sem caractere especial e com menos de 8 dígitos (ignorando a própria regra da tela).
- **Passos para reproduzir:** 1. Acessar "Criar conta". 2. Preencher dados fora do padrão e clicar em "Criar conta".
- **Resultado atual:** O sistema cria o cadastro com dados inválidos e inconsistentes.
- **Resultado esperado:** O sistema deve aplicar máscaras, validar formato de e-mail, checar limite de caracteres, e forçar a complexidade de senha.
- **Severidade:** Alto
- **Prioridade:** Alta

**Bug 7: Sistema permite múltiplos cadastros com os mesmos dados**
- **Descrição:** O banco de dados/sistema não verifica se as chaves únicas (e-mail e celular) já existem, permitindo duplicidade.
- **Passos para reproduzir:** 1. Criar uma conta. 2. Voltar à tela de cadastro e criar uma nova conta utilizando exatamente os mesmos dados.
- **Resultado atual:** A segunda conta é criada com sucesso.
- **Resultado esperado:** Exibir a mensagem "E-mail/Celular já cadastrado".
- **Severidade:** Alto
- **Prioridade:** Alta

**Bug 8: Quebra de Interface (UI) nos campos do formulário**
- **Descrição:** Os componentes visuais dos inputs de "Telefone" e "Confirmar Senha" na tela de cadastro estão fora do esquadro, ultrapassando os limites do container principal.
- **Passos para reproduzir:** 1. Acessar a tela de Criação de conta. 2. Observar o alinhamento dos campos à direita.
- **Resultado atual:** Inputs quebram o limite do container branco.
- **Resultado esperado:** Os campos devem ser responsivos e respeitar as margens do container.
- **Severidade:** Baixo
- **Prioridade:** Média

---

### ✅ Tela de Sucesso

**Bug 9: Texto do botão inconsistente após cadastro (Erro de UX)**
- **Descrição:** Após criar a conta, a tela informa: *"Você já pode acessar a plataforma"*. Contudo, o botão de ação principal exibe *"Sair da conta"*, gerando confusão.
- **Passos para reproduzir:** 1. Concluir a criação de uma conta. 2. Observar o botão na tela de Sucesso.
- **Resultado atual:** O botão diz "Sair da conta".
- **Resultado esperado:** O botão deveria exibir "Ir para a tela inicial" ou "Fazer Login".
- **Severidade:** Baixo
- **Prioridade:** Média

---

### 🛡️ Segurança e Inspeção Técnica

**Bug 10: Vazamento de credenciais em texto plano no Console**
- **Descrição:** Ao realizar login ou cadastro, o sistema realiza um `console.log` dos dados informados, expondo o e-mail e a senha do usuário nas ferramentas de desenvolvedor.
- **Passos para reproduzir:** 1. Abrir o DevTools (F12) na aba Console. 2. Preencher dados e enviar o formulário.
- **Resultado atual:** E-mail e senha são impressos em texto plano.
- **Resultado esperado:** Nenhum dado sensível deve ser registrado via log no front-end.
- **Severidade:** Crítico
- **Prioridade:** Alta

**Bug 11: Navegação Forçada / IDOR (Bypass de Autenticação)**
- **Descrição:** A página protegida de sucesso não valida a sessão do usuário. É possível acessá-la colando a URL diretamente em uma guia anônima sem autenticação.
- **Passos para reproduzir:** 1. Abrir uma guia anônima. 2. Acessar `https://qa-play-sim.lovable.app/sucesso?op=login`.
- **Resultado atual:** A página logada é renderizada normalmente.
- **Resultado esperado:** A rota deve validar o token de sessão e redirecionar para o login se for inválido.
- **Severidade:** Crítico
- **Prioridade:** Alta

**Bug 13: Ausência de sanitização de inputs (Vulnerabilidade a XSS e SQLi)**
- **Descrição:** Os campos de input não realizam a higienização dos dados inseridos. É possível inserir scripts maliciosos (como `<script>alert(1)</script>`) ou *payloads* de injeção SQL (como `' OR 1=1 --`), caracterizando um risco grave de *Cross-Site Scripting* (XSS) e *SQL Injection*.
- **Passos para reproduzir:** 1. Acessar a tela de login ou cadastro. 2. Inserir *payloads* de XSS ou SQLi nos campos de texto. 3. Enviar o formulário.
- **Resultado atual:** O sistema aceita a entrada sem filtrar os caracteres especiais.
- **Resultado esperado:** O sistema deve aplicar filtros de sanitização (ex: *escape* de HTML) para neutralizar caracteres especiais e evitar a execução de código arbitrário.
- **Severidade:** Crítico
- **Prioridade:** Alta

---

### 📱 Responsividade (Mobile)

**Bug 12: Falta de responsividade do layout em dispositivos móveis**
- **Descrição:** A interface não é responsiva. Ao acessar via smartphone, o layout quebra e parte dos campos fica oculta.
- **Passos para reproduzir:** 1. Acessar o sistema via mobile. 2. Observar a tela de cadastro.
- **Resultado atual:** Elementos visuais são cortados.
- **Resultado esperado:** O layout deve empilhar os campos em telas menores, garantindo 100% de visibilidade.
- **Severidade:** Alto
- **Prioridade:** Alta

---

## 📌 Conclusão e Priorização

### [cite_start]Quais 2 bugs você corrigiria primeiro e por quê? [cite: 34]

Com base na análise de impacto ao negócio e à segurança, a correção prioritária seria:

1. **Bug 10 (Vazamento de credenciais no Console):** Esta é a falha mais crítica sob a ótica de segurança da informação. Expor senhas em texto plano no ambiente do cliente (front-end) é uma violação gravíssima de privacidade. A prioridade é "Alta" porque é um *Quick Win*: a correção é rápida e elimina um risco altíssimo de roubo de credenciais.
2. **Bug 5 (Criação de conta com campos vazios):** Este erro destrói o propósito principal ("Core") da aplicação. Permitir o envio de formulários em branco corrompe a integridade do banco de dados e gera o efeito cascata que possibilita o acesso não autorizado posterior (Bug 3). Bloquear formulários inválidos é o pilar de uma aplicação funcional.

---

## [cite_start]💡 Sugestões de Melhorias [cite: 35]

Durante os testes, identifiquei oportunidades para tornar a aplicação mais robusta, amigável e segura:

**1. Melhorias de Experiência do Usuário (UX/UI)**
- **Ícone de "Ver/Ocultar Senha" (Olhinho):** Incluir um botão de *toggle* nos campos de senha. Isso reduz drasticamente a taxa de erro de digitação e frustração.
- **Validação em Tempo Real (*Inline Validation*):** O sistema poderia validar os campos assim que o usuário tira o cursor deles (*onBlur*), contornando de verde (correto) ou vermelho (erro) imediatamente.
- **Medidor de Força de Senha:** Adicionar uma barra visual que indique se a senha digitada é "Fraca", "Média" ou "Forte", incentivando senhas seguras.
- **Máscaras Dinâmicas:** Aplicar formatação automática no campo de telefone enquanto o usuário digita (Ex: (11) 99999-9999).

**2. Melhorias Funcionais (Novas Features)**
- **Fluxo de "Esqueci minha senha":** A tela de login carece de um botão para recuperação de credenciais, padrão de mercado essencial para retenção de acessos.
- **Redirecionamento Automático:** Na tela de Sucesso, o sistema poderia ter um redirecionamento automático (ex: *"Você será redirecionado em 5 segundos..."*) para um fluxo mais fluido.
- **Login Social (SSO):** Adicionar botões "Entrar com Google/Apple" para diminuir a fricção do cadastro.

**3. Melhorias de Segurança**
- **Proteção contra Força Bruta (*Rate Limiting*):** Implementar bloqueio temporário ou exigir CAPTCHA após um número elevado de tentativas falhas de login (ex: 5 tentativas), mitigando ataques de robôs.

---

**Autor:** Ykaro Andrade  
[cite_start]*Análise realizada para a vaga de QA Tester da 4blue.* [cite: 2]