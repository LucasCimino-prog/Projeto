# Sistema de Autenticação em PHP

Este projeto consiste em um sistema de autenticação de usuários simples, seguro e funcional, desenvolvido em PHP. Ele permite o controle de acesso a páginas restritas com base em login, senha e perfis de usuário (admin/user).

## Funcionalidades e Requisitos

### Requisitos Funcionais
- **RF1 (Login):** Formulário para autenticação com e-mail e senha.
- **RF2 (Autenticação):** Validação de credenciais contra o banco de dados, com criação de sessão para usuários válidos.
- **RF3 (Proteção de Páginas):** Um script "guard" (`verifica_sessao.php`) protege páginas restritas, verificando a sessão ativa e o perfil do usuário.
- **RF4 (Logout):** Funcionalidade para encerrar a sessão do usuário de forma segura.
- **RF5 (Usabilidade):** Exibição de mensagens de feedback claras para o usuário (sucesso, erro, acesso negado, etc.).

### Requisitos Técnicos
- **Banco de Dados:** MySQL.
- **Linguagem:** PHP com acesso ao banco de dados via PDO e uso de *prepared statements* para prevenir SQL Injection.
- **Segurança de Senhas:** As senhas são armazenadas no banco de dados utilizando hashing com as funções `password_hash()` e `password_verify()`.
- **Gerenciamento de Sessão:** O ID da sessão é regenerado após o login (`session_regenerate_id(true)`) para prevenir ataques de *session fixation*. As sessões são configuradas para serem mais seguras (HttpOnly, Secure, Strict Mode).

## Passos para Rodar o Projeto

### Pré-requisitos
- Servidor web local (Apache, Nginx, etc.).
- PHP (versão 7.4 ou superior recomendada).
- Servidor de banco de dados MySQL ou MariaDB.

### 1. Configuração do Banco de Dados
1.  Crie um banco de dados no seu servidor MySQL com o nome `sistema_auth`.
2.  Importe o arquivo `schema.sql` para criar a tabela `usuarios` e inserir um usuário de teste. Você pode usar um cliente de banco de dados como phpMyAdmin ou executar o seguinte comando no terminal:
    ```shell
    mysql -u seu_usuario -p sistema_auth < schema.sql
    ```

### 2. Configuração do Projeto
1.  Clone ou baixe os arquivos do projeto para o diretório raiz do seu servidor web (ex: `htdocs/` no XAMPP ou `www/` no WampServer).
2.  Abra o arquivo `config.php` e, se necessário, altere as credenciais de acesso ao banco de dados (DB_HOST, DB_USER, DB_PASS) para corresponderem à sua configuração local.

### 3. Acesso
- Abra seu navegador e acesse a URL correspondente ao projeto (ex: `http://localhost/nome_da_pasta_do_projeto/`). A página de login (`index.php`) será exibida.

## Credenciais de Teste

Para acessar o sistema, utilize o seguinte usuário de teste, que já está incluído no arquivo `.sql`:

-   **E-mail:** `admin@example.com`
-   **Senha:** `Senha123!`

## Fluxo da Aplicação

1.  O usuário acessa `index.php` e insere suas credenciais.
2.  Os dados são submetidos via POST para `autentica.php`.
3.  `autentica.php` valida as credenciais. Se forem válidas, uma sessão é criada, o ID da sessão é regenerado e o usuário é redirecionado para `dashboard.php`.
4.  `dashboard.php`, por sua vez, é uma página protegida que exige um perfil de 'admin'. Ela inclui `verifica_sessao.php` no topo para garantir que apenas usuários autenticados e autorizados possam acessá-la.
5.  Qualquer tentativa de acesso direto a uma página protegida sem uma sessão válida resultará em um redirecionamento para a página de login.
6.  O usuário pode clicar no link "Sair" para executar `logout.php`, que destrói a sessão e o redireciona de volta para a página de login.

## Observações
- Css será movido, e modificado, para se tornar externo com o andamento do projeto. 