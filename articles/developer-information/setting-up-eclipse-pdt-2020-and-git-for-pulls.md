<!-- Filename: Setting_up_Eclipse_PDT_2020_and_Git_for_Pulls / Display title: Configurando Eclipse PDT 2020 e Git para Pulls -->

## Introdução

Comecei a usar o Eclipse há muitos anos para um projeto privado de Joomla e um repositório git remoto privado que não estava no Github. Li os tutoriais disponíveis e consegui me virar feliz até este ano, quando decidi ajudar nos testes principais e correção de bugs do Joomla! 4. E então alguns pull requests. Foi quando percebi que não tinha entendido exatamente o que estava fazendo. Finalmente, decidi começar de novo e documentar o processo para outros desenvolvedores semi-experientes que são novos no Joomla, especialmente as partes que não compreendi completamente na primeira vez. Primeiro na lista:

## Estrutura de Arquivos

Não é óbvio antes de você baixar e instalar o Eclipse que há pelo menos dois locais onde os dados são armazenados, além de onde o código do Eclipse está localizado.

### O Espaço de Trabalho

Este é o local onde o Eclipse armazena seus próprios dados para cada projeto. Não deve estar na árvore da web! Como eu trabalho principalmente em um laptop Mac, o local padrão para mim é **/Users/username/eclipse-workspace**. Há uma subpasta para cada projeto. Assim, uma delas poderia ser **/Users/username/eclipse-workspace/joomla-cms**. Ela contém uma pasta: .metadata. Usuários de Linux provavelmente saberão substituir Users por home.

### O repositório local do git e site de teste

Aqui é onde o código do projeto é armazenado. Pode estar na árvore web local se você quiser usá-lo para testes. Para mim, é **/Users/username/Sites/joomla-cms-4**. Usuários de Linux provavelmente saberão substituir Sites por public_html. Fique atento aos passos extras necessários para fazer o repositório local funcionar como um site Joomla.

### Um site de teste separado

Isso é opcional, mas requer que o repositório git tenha um arquivo build.xml personalizado, digamos build-local.xml, abordado no Apêndice.

## Software Necessário

Para configurar um site de desenvolvimento e teste funcional, você precisará primeiro instalar o seguinte software:

- Apache
- MySQL ou Maridb
- PHP
- phpMyAdmin - [Página inicial do PhpMyAdmin](https://www.phpmyadmin.net/)
- Composer - [Página inicial do Composer](https://getcomposer.org/)
- Node.js - [Página inicial do Node.js](https://nodejs.org/en/)
- Eclipse PDT - [Ferramentas de Desenvolvimento PHP do Eclipse](https://www.eclipse.org/pdt/)
- git (opcional para usuários de git na linha de comando) - [Página inicial do git](https://git-scm.com/)
- phing (opcional para builds personalizados) - [Página inicial do phing](https://www.phing.info/)

Os primeiros três ou quatro geralmente vêm como um pacote para sua plataforma, conhecido como stack LAMP, WAMP ou XAMP. Basta usar o que sua plataforma oferece ou consultar o Apache Friends [XAMPP](https://www.apachefriends.org/)

Vamos supor que você tenha instalado tudo, exceto o Eclipse.

## Fazer um fork de joomla-cms no Github

Há um fluxo de trabalho descrito em [My first pull request to Joomla! on Github](https://docs.joomla.org/My_first_pull_request_to_Joomla!_on_Github) que eu não posso elogiar demais. Ele mostra exatamente o que você precisa fazer:

![Github work flow](../../../en/images/getting-started/core-work-flow-joomla.png)

Passos

- Vá para o [Github](https://github.com/) e obtenha uma conta, gratuita e rápida.
- Na sua conta do github, vá para o repositório joomla/joomla-cms: digite joomla/joo... na caixa de pesquisa no canto superior esquerdo e selecione quando aparecerem as opções.
- No repositório joomla/joomla-cms, clique no botão de fork no canto superior direito. Isso lhe dará uma cópia bifurcada de todo o código para Joomla 4, Joomla 5, ..., tudo, na sua própria conta do Github.

De volta à sua estação de trabalho.

## Instalar Eclipse

Já tenho duas versões do Eclipse instaladas, Oxygen de alguns anos atrás e Cocoa de 2020. A partir daqui, estou instalando uma segunda instância do Cocoa. Vamos ver o que acontece:

- Vá para o [site do Eclipse](https://www.eclipse.org/pdt/) e faça o download da versão para sua plataforma.
- Siga o procedimento de instalação e, eventualmente, inicie o aplicativo Eclipse, para mim **Eclipse 2.app**.
- Aviso: *Eclipse 2.app* é um aplicativo baixado da internet. Tem certeza de que deseja abri-lo? **Abrir**
- Selecione um diretório como espaço de trabalho - O padrão é /Users/username/eclipse-workspace. **Navegar** e crie uma subpasta joomla-cms-4.
- Lançamento: o Eclipse está instalado e exibe a página de Boas-vindas.
- Revise as configurações de configuração do IDE. Configure os itens 1, 2, 5 e 6.
- Selecione o ícone do Workbench no canto superior direito.

Em vez de instalar outra versão do Eclipse, eu poderia ter aberto um novo espaço de trabalho vazio.

Até agora, tudo bem!

## Importar fork para o Eclipse

Na sua nova instalação local do Eclipse:

- Abra Preferências e defina Equipe / Git / Pasta padrão do repositório para /Users/username/git (você pode ou não usar essa localização)
- Abra Arquivo / Importar / Git / Projetos do Git (com importação inteligente). Próximo ...
- Clonar URI. Próximo ...
- Copie a barra de URL do **seu fork do Github** e cole no campo URL. Você não precisa adicionar credenciais de autenticação. Próximo ...
- Ramificações para importar ... er ... Provavelmente é melhor importar tudo. Próximo ...
- Diretório. Aqui você pode escolher um local diferente para manter o código. Eu naveguei até /Users/username/public_html/joomla-cms-4, criando-o se necessário.
- Ramificação inicial - se você importou todas as ramificações. Estou trabalhando no Joomla 4, então selecionei 4.0-dev. E notei que meu clone será **origin**. Próximo ...
- Tomar um café. A clonagem levará alguns minutos.
- Importar origem. A origem deve ser o local do código. Concluir.
- O Eclipse agora mostra a raiz da árvore de código no painel Explorador de Projetos. Clique para ver mais da árvore. Observe que este código ainda não funcionará como um site Joomla. Entre outras coisas, não há pasta de mídia.

## Adicionar repositório joomla-cms original ao Eclipse

- Mostre a janela dos Repositórios Git: selecione Janela / Mostrar Visualização / Outro
- Selecione Git / Repositórios Git - a janela aparece na parte inferior da tela.
- Expanda joomla-cms / remotes / origin - se você fizer alterações no seu código e enviar para origin, é para onde ele vai.
- Clique com o botão direito em Remotos e selecione Criar Remoto...
- Defina o nome do Remoto para **joomla-origin** e selecione **Configurar busca**.
- Em Configurar Busca, selecione **Alterar**.
- Em Selecionar um URI, cole a url do repositório original joomla-cms: `https://github.com/joomla/`
- Deixe Credenciais em branco. Finalizar.
- em Configurar Busca: **Salvar e Buscar**.

## Criar um site funcional

Sua cópia do código joomla-cms precisa de mais etapas para torná-lo utilizável como um site.

- Abra um terminal e mude para a pasta contendo seu código clonado.
- Execute o composer install:
  - Usuários de Linux e OSX podem configurar o seguinte alias bash colocando o seguinte dentro do arquivo `~/.bash_profile` ou `~/.zsh` (`\$ source ~/.bash_profile` para efeito imediato):
```sh
    alias jclean="rm -rf administrator/templates/atum/css; \
    rm -rf templates/cassiopeia/css; \
    rm -rf administrator/templates/system/css; \
    rm -rf templates/system/css; \
    rm -rf media/; \
    rm -rf node_modules/; \
    rm -rf libraries/vendor/; \
    rm -f administrator/cache/autoload_psr4.php; \
    rm -rf installation/template/css"
    alias jinstall="jclean; composer install --ignore-platform-reqs; npm ci"
```

- composer não está no meu caminho, então substituí por php ~/composer/composer.phar
- jinstall
- que busca todas as dependências PHP do Joomla, dependências de Javascript, compila todo o Javascript ES6 e coloca os arquivos em seus locais apropriados.
- gole de café enquanto as dependências são baixadas e os arquivos de mídia são criados.
- No Eclipse, clique com o botão direito no projeto raiz e selecione Atualizar. Você verá que seu código agora tem uma pasta de mídia.
- Se você estiver interessado, use um gerenciador de arquivos para ver que a raiz também contém um arquivo chamado .gitignore e a pasta de mídia é mencionada nele. Isso significa que não será comprometida com seus repositórios git locais ou remotos clonados.

Agora você está pronto para uma instalação do Joomla:

- Crie um banco de dados usando o phpMyAdmin (ou a linha de comando mysql, se preferir).
- Criei um banco de dados chamado joomla-cms-4 com collation utf8mb4-unicode-ci.
- Crie um novo usuário: o meu é jcms4 com uma senha aleatória gerada (GAOC26r77bBLkkdA). Você precisa anotar a senha para usar durante a instalação. Ela será armazenada em texto simples no arquivo de configuração.
- Conceda Todos os Privilégios no banco de dados para este usuário - o padrão.
- No seu navegador favorito, vá para a raiz do novo site: localhost/joomla-cms-4/

### No meu Mac executando o macOS Catalina

- Configuração do Ambiente Incompleta: Mais detalhes. Bah - apenas conserte e verifique se a barra de URL contém a URL que você digitou - a minha de alguma forma adicionou alguns caracteres extras.
- Caso contrário, ele acessa um site em funcionamento - não exclua a pasta de instalação.

### No meu workstation Linux rodando o Linux Mint 20

Ops! Algo deu errado!

O problema é que eu tenho meu código Joomla no meu espaço de arquivos pessoal para acesso de leitura/escrita pelo Eclipse. O servidor web também precisa de acesso de escrita para gravar arquivos de configuração, cache e log, mas está sendo executado como um usuário e grupo com poucos privilégios. Como estou em uma rede doméstica privada, editei o arquivo /etc/apache2/apache2.conf para comentar User \${APACHE_RUN_USER} e Group \${APACHE_RUN_GROUP} e adicionar User meuusuário e Group meugrupo. Reinicie o apache e, em seguida...

- Ele vai para um site em funcionamento - não apague a pasta de instalação.

## Revisão de Código

Em resumo:

- Buscar do joomla-origin para garantir que meu clone local está atualizado.
- Equipe / Mesclar / Selecionar ramificação para mesclar - cuidado - eu selecionei joomla-origin/4.0-dev
- Enviar para a origem para garantir que meu fork remoto está atualizado.
- Criar uma ramificação para algumas alterações de código que quero fazer.
- Fazer as alterações de código
- Se as alterações forem em arquivos fonte css ou js (aqueles em sass ou es6) vá para uma janela de terminal e execute o jinstall novamente.
- TESTE sua instalação local para ver se há algum problema.
- Confirmar as alterações de código
- Enviar para a origem para atualizar meu fork remoto com minhas alterações.
- Vá para sua própria conta no Github e selecione a ramificação que você criou com o código atualizado. Algo assustador: diz **Este ramo está 11084 commits à frente, 134 commits atrás de joomla:staging.** Fiz algo errado? Aparentemente não!
- Selecione o botão Pull Request. Certifique-se de que você selecionou o ramo correto do joomla para mesclar. Para mim, é 4.0-dev. E certifique-se de que você selecionou sua ramificação com o código alterado. Vá em frente!
- O pull request deve ser testado e aprovado e pode levar dias, semanas ou meses. E a mudança pode ser rejeitada!

## Enquanto isso

De volta à sua estação de trabalho:

- Volte para o seu branch original, para mim: Equipe / Mudar Para / 4.0-dev
- Reconstruir: para mim Projeto / Construir Projeto
- Veja os arquivos anteriormente alterados sendo copiados para o seu site de trabalho novamente.
- TESTE: seu site de trabalho está de volta ao estado em que estava antes das suas alterações de código.

Você está agora pronto para criar outro branch para outro conjunto de alterações de código.

## Se Ocorrer um Desastre

Em um determinado momento, meu clone local de alguma forma ficou corrompido e eu não sabia como consertá-lo. Então apaguei meu clone local e todos os arquivos associados, esvaziei o banco de dados e voltei para a etapa **Importar fork no Eclipse** mencionada acima. Isso colocou meu clone local em sincronia com meu fork remoto, incluindo quaisquer ramificações que criei para solicitações pull. A nova instalação funcionou sem problemas e eu fiquei feliz!

## Outros Recursos

- [Configurando Eclipse para desenvolvimento Joomla](https://docs.joomla.org/Configuring_Eclipse_for_joomla_development) (2012-2013) Mas obtenha a versão mais recente do Eclipse PDT!
- [Meu primeiro pull request para o Joomla! no Github](https://docs.joomla.org/My_first_pull_request_to_Joomla!_on_Github) (2011-2014) Bom panorama, embora um pouco desatualizado.
- [Trabalhando com git e github](https://docs.joomla.org/Working_with_git_and_github) (2011-2015)
- [Configurando seu ambiente local](https://docs.joomla.org/J4.x:Setting_Up_Your_Local_Environment) (2018-2020)
- [Configurando Eclipse e Xdebug](https://docs.joomla.org/Configuring_Eclipse_and_Xdebug) (2013) Tudo sobre depuração.
- [Trabalhando com Git e Eclipse](https://docs.joomla.org/Working_with_Git_and_Eclipse) (2014) Método para edições antigas do Eclipse.
- [Executando Testes Automatizados no Eclipse](https://docs.joomla.org/Running_Automated_Tests_from_Eclipse) (2020) Para usuários avançados?
- [Configurando o Xdebug para desenvolvimento PHP/Linux](https://docs.joomla.org/Configuring_Xdebug_for_PHP_development/Linux) (2016) Instalar e configurar.
- [Configurando o Eclipse IDE para desenvolvimento PHP/Linux](https://docs.joomla.org/Configuring_Eclipse_IDE_for_PHP_development/Linux) (2019) Instalar e configurar para Linux.
- [Configurando o Xdebug para desenvolvimento PHP](https://docs.joomla.org/Configuring_Xdebug_for_PHP_development) (2014) Passos para Linux, Windows e Mac OS X.
- [Webinar: Usando Eclipse para Desenvolvimento Joomla!](https://docs.joomla.org/Webinar:_Using_Eclipse_for_Joomla!_Development) (2014) Este webinar em vídeo de 45 minutos, gravado em 30 de abril de 2009, fornece uma visão geral dos recursos do Eclipse para desenvolvimento Joomla!.
- [Configurando sua workstation para desenvolvimento Joomla](https://docs.joomla.org/Setting_up_your_workstation_for_Joomla_development) (2020) Breve visão geral do software necessário e IDEs alternativos.

## Apêndice

Em um determinado momento, tive meu repositório git local fora da raiz do meu site e precisei copiar quaisquer alterações feitas para um site local instalado separadamente. Isso exigia um arquivo de compilação personalizado, mostrado aqui para referência:

### Criar um arquivo build-local.xml

O clone do Eclipse contém um arquivo build.xml, mas ele é usado para testar e construir um arquivo zip para download para uma nova instalação. O que eu quero fazer é copiar quaisquer alterações que eu faça no meu código clonado para o meu site de teste no meu laptop. Observe que eu só quero fazer alterações no código PHP e não em Javascript ou CSS. Para isso, criei um arquivo separado chamado build-local.xml na raiz do projeto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="joomla-cms" basedir="." default="main">
    <property file=".project" />

    <property name="joomladir" value="/Users/username/public_html/joomla-cms"  override="true" />

    <property name="srcdir" value="${project.basedir}" override="true" />

    <!-- Fileset for all files -->
    <fileset dir="${srcdir}" id="allfiles">
        <include name="administrator/**" />
        <include name="api/**" />
        <include name="cli/**" />
        <include name="components/**" />
        <include name="images/**" />
        <include name="includes/**" />
        <include name="language/**" />
        <include name="layouts/**" />
        <include name="libraries/**" />
        <include name="modules/**" />
        <include name="plugins/**" />
        <include name="templates/**" />
        <include name="index.php" />

        <exclude name="**/.*" />
    </fileset>

    <!-- ============================================  -->
    <!-- (DEFAULT) Target: main                        -->
    <!-- ============================================  -->
    <target name="main" description="main target">
        <copy todir="${joomladir}">
            <fileset refid="allfiles" />
        </copy>
    </target>
</project>
```

### Adicionar uma ferramenta de build

- Clique com o botão direito no raiz do projeto e selecione Propriedades.
- Selecione Constructors / Novo / Programa / OK.
- Nome: Compilação local com phing
- Localização: onde quer que o phing esteja instalado. Para mim é /usr/local/php5/bin/phing, mesmo eu estando usando o PHP 7.4.
- Diretório de Trabalho: Navegue pelo Espaço de Trabalho e selecione joomla-cms - aparece como \${workspace_loc:/joomla-cms}
- Argumentos: -f build-local.xml
- Aplicar / OK
- Em Constructors: Aplicar e Fechar
- Projeto / Construir Projeto
- Veja o que acontece:

```sh
    Buildfile: /Users/username/git/joomla-cms/build-local.xml
     [property] Loading /Users/username/git/joomla-cms/.project

    joomla-cms > main:

    BUILD FINISHED

    Total time: 0.2121 seconds
```

*Traduzido por openai.com*

