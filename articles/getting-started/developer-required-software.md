<!-- Filename: J4.x:Developer:_Required_Software / Display title: Software Necessário -->

## Introdução

Este tutorial é destinado a iniciantes no desenvolvimento de código Joomla que desejam preparar extensões em um computador local. Não importa se você usa Windows, Mac ou Linux. Todo o software necessário está disponível para todas essas plataformas. Para começar em seu próprio laptop ou computador de mesa, que geralmente tem o nome de domínio *localhost*, você precisará instalar um conjunto padrão de itens de software separados.

- **Apache**, um servidor web. Outros servidores web estão disponíveis, mas os iniciantes devem ficar com o Apache.
- **MySQL** ou **MariaDB**, servidores de banco de dados. PostgreSQL também é suportado, mas não é para iniciantes.
- **PHP**, a versão mais recente recomendada pelo Joomla ou a versão mínima para sua plataforma.
- **phpMyAdmin**, uma ferramenta usada para gerenciar bancos de dados MySQL e MariaDB.
- **xDebug**, uma extensão do PHP usada para depuração.
- Um IDE como **VSCode**. Outros estão disponíveis e são abordados em um artigo separado.

## Pilhas de Software

Os primeiros quatro itens nesta lista são frequentemente chamados de stack e podem ser nomeados como LAMP, MAMP ou WAMP, onde as letras no acrônimo significam o seguinte:

- **Plataforma L, M ou W**. L para Linux, M para Mac e W para Windows.
- **A: Servidor web Apache**.
- **M: Banco de dados MySQL ou MariaDB**. Os dois são intercambiáveis.
- **P: Linguagem de script PHP**. Uma linguagem de script amplamente utilizada. Não há alternativa, pois o Joomla é codificado em PHP.

## Pilhas Empacotadas

Uma boa maneira de começar é usando um pacote que combina o software essencial:

- **WAMP** para Windows é gratuito no site do [Wampserver](https://www.wampserver.com/en/).
- **Bearsampp** para Windows é gratuito no site do [Bearsampp](https://bearsampp.com/). Ele possui mais ferramentas.
- **XAMPP** para Windows, Mac e Linux é gratuito no site do [Apache Friends](https://www.apachefriends.org/). Há um tutorial local para [XAMPP](jdocmanual?article=user/hosting/local-hosting-with-xampp).
- **MAMP** para Mac e Windows está disponível em versões gratuitas e comerciais no site do [MAMP](https://www.mamp.info/en/mac/).

## Sem Pilhas

Se você tiver um computador Linux ou Macintosh, verá que pode instalar cada um dos itens de software necessários independentemente dos repositórios remotos que suportam seu sistema operacional. É possível que já estejam instalados e prontos para usar. Para testar, abra o seu navegador web favorito e digite **localhost** na barra de URL. Você verá uma página de espera ou uma página de erro de conexão.

## Diretório Raiz do Documento do Servidor Web

Após a instalação, o seu servidor Apache terá definido um diretório raiz de documentos padrão. A localização varia de plataforma para plataforma e você precisará saber onde está ou criar um host virtual para colocá-lo onde desejar. Exemplos de locais padrão:

- Mac OS: "/Library/WebServer/Documents"
- Linux: /var/www/html
- Windows: ...

Para evitar problemas posteriores com permissões de arquivo, muitas vezes é conveniente criar um host virtual para apontar para o diretório public_html do seu próprio espaço de arquivos. Isso pode ser /home/username/public_html no Linux ou /Users/username/Sites no Mac.

Aqui está um exemplo de entrada de host virtual Mac no arquivo /etc/apache2/vhosts/localhost.conf:

```bash
<VirtualHost *:80>
        DocumentRoot "/Users/username/Sites"
        ServerName localhost
        ErrorLog "/private/var/log/apache2/localhost-error_log"
        CustomLog "/private/var/log/apache2/localhost-access_log" common
        <Directory "/Users/username/Sites">
            AllowOverride All
            Require all granted
        </Directory>
</VirtualHost>
```

Alternativamente, você pode criar um link simbólico do diretório raiz padrão do documento para a pasta public_html do seu espaço de arquivos pessoal.

*Traduzido por openai.com*

