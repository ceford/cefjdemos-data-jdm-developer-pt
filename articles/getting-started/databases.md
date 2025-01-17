<!-- Filename: J4.x:Developer:_Required_Software / Display title: Configuração do Banco de Dados -->

## Sobre MySQL e MariaDB

Os recém-chegados podem ter a impressão de que MySQL e MariaDB são bancos de dados e podem ficar confusos quando as instruções dizem *criar um novo banco de dados*. Na verdade, ambos são Sistemas de Gerenciamento de Banco de Dados Relacional (RDBMS) que podem gerenciar muitos bancos de dados individuais. Seu site de teste local pode ter muitas instalações individuais do Joomla, cada uma com seu próprio banco de dados. Por exemplo, você pode querer testar sua extensão na versão atual do Joomla e separadamente em uma versão candidata próxima.

A captura de tela a seguir mostra parte de uma lista com mais de 30 bancos de dados criados para testar várias instalações e projetos de extensões do Joomla.

![Phypadmin screenshot of list of databases](../../../en/images/getting-started/phpmyadmin-databases.png)

Uma observação lateral: as colações são principalmente utf8mb4_0900_ai_ci:

- utf8mb4 significa que cada caractere é armazenado com um máximo de 4 bytes no esquema de codificação UTF-8.
- 0900 refere-se à versão do Algoritmo de Colação Unicode.
- ai refere-se à insensibilidade a acentos, não há diferença entre e, è, é, ê e ë ao ordenar.
- ci refere-se à insensibilidade a maiúsculas e minúsculas, não há diferença entre p e P ao ordenar.

Tabelas e colunas individuais podem ter uma colação diferente. As tabelas do Joomla geralmente têm a colação utf8mb4_unicode_ci.

## Configuração de Banco de Dados com phpMyAdmin

Antes de instalar o Joomla, você precisa de um banco de dados vazio pronto para ser preenchido. Você também precisa de um usuário de banco de dados.

### Criar um Banco de Dados

- **Iniciar phpMyAdmin** Insira localhost/phpmyadmin na barra de URL do seu navegador.
- **Entrar** Dependendo de como foi instalado, o nome de usuário será root ou admin e pode ou não haver uma senha.
- Selecione **Bancos de Dados** no menu superior da página inicial do phpMyAdmin.
- Em **Criar Banco de Dados**, insira um nome curto no lugar da dica **Nome do banco de dados**, por exemplo, jtest.
- Selecione **utf8mb4_0900_ai_ci** na lista suspensa de Conjunto de Comparação.
- Selecione **Criar** para criar o banco de dados.

Isso o levará a um banco de dados vazio. No topo, há uma mensagem: *Nenhuma tabela encontrada no banco de dados.*

### Criar um Usuário

- Selecione o ícone **Início** no canto superior esquerdo do phpMyAdmin para ir para a página inicial.
- Selecione **Contas de Usuário** no menu superior da página inicial.
- Selecione **Adicionar Conta de Usuário** no painel Novo abaixo da lista de usuários atuais (se houver).
- Insira um **Nome de Usuário**, que pode ser um nome curto que você precisará mais tarde durante a instalação do Joomla. Exemplo: jtest. Você pode usar este mesmo usuário para outros bancos de dados criados posteriormente!
- Selecione **Local** na lista do campo Nome do Host. Isso definirá localhost no campo de valor adjacente.
- Use o botão **Gerar** para gerar uma senha. Você precisa copiar o valor gerado e colá-lo em um editor de texto para uso posterior. Você não precisa memorizá-la a longo prazo, pois ela será armazenada como texto simples no arquivo configuration.php do Joomla. Exemplo: 8t8mGQq.gw\[\]8lp(
- **Salvar** pulando as seções de Banco de Dados para o usuário e Privilégios Globais do formulário. O botão **Ir** (Salvar) está na parte inferior.

### Atribuir Permissões de Banco de Dados ao Usuário

- Na página de **Contas de Usuário**, selecione o usuário (jtest), se necessário, através de Início / Contas de Usuário / Nome do Usuário.
- Selecione **Banco de Dados** na parte superior da página. Isso mostrará uma lista de bancos de dados aos quais este usuário recebeu permissões de acesso e, na parte inferior, uma lista de bancos de dados aos quais o usuário não recebeu acesso.
- **Selecione** o banco de dados ao qual o acesso deve ser concedido e selecione o botão **Go**.
- **Privilégios específicos do banco de dados** Selecione **Marcar todos** e depois **Go** para salvar.

Isso é tudo! Agora você pode sair do phpMyAdmin. Esqueceu de anotar a senha do usuário do banco de dados? Volte e edite a conta do usuário que você criou para alterá-la. Se você usar o mesmo usuário de banco de dados para múltiplos bancos de dados do Joomla, encontrará a senha no arquivo configuration.php do Joomla.

*Traduzido por openai.com*
