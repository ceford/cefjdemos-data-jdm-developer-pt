<!-- Filename: J4.x:Developer:_Eclipse_PDT / Display title: Eclipse PDT -->

## Introdução

Como um desenvolvedor PHP, você precisará de algumas ferramentas para ajudá-lo em seu trabalho. O Eclipse é um IDE (Ambiente de Desenvolvimento Integrado) que pode ser usado para todos os tipos de projetos em todos os tipos de linguagens de programação. O Eclipse PDT (Ferramentas do Desenvolvedor PHP) inclui as extensões necessárias para o desenvolvimento em PHP. Algumas das características mencionadas em sua página inicial incluem:

- Realce de Sintaxe
- Validação de Sintaxe
- Assistência de Conteúdo
- Navegação de Código
- Depuração PHP (Zend Debugger / Xdebug)
- Perfilamento PHP (Zend Debugger / Xdebug)

Adicione a isso a capacidade de copiar arquivos para onde eles precisam estar em seu site de teste local e criar um arquivo zip, há material suficiente para trabalhar por anos. Aprender a usar o Eclipse PDT leva tempo, um dia ou mais, mas vale a pena. Existem outras IDEs e editores de código disponíveis!

### Alternativas

**IDEs** têm todos os recursos necessários para construir projetos PHP. Exemplos multi-plataforma conhecidos por serem usados por alguns desenvolvedores do Joomla incluem:

- **JetBrains PhpStorm** Comercial, Multiplataforma.
- **Apache NetBeans** Gratuito, Código Aberto, Multiplataforma.
- **Visual Studio Code** Gratuito, Multiplataforma.

**Editores PHP** são bons para editar código mas carecem de alguns recursos necessários para grandes projetos. Exemplos incluem:

- **Notepad++** Gratuito, apenas para Windows.

## Instalar o Eclipse PDT

Vá para o site [Eclipse PDT](https://www.eclipse.org/pdt/) e faça o download da versão disponível para sua plataforma (Linux, Mac ou Windows).

Siga as instruções de instalação para a sua plataforma.

## O Espaço de Trabalho do Eclipse

Existem pelo menos três lugares diferentes onde o código do seu projeto estará localizado:

- Arquivos de **origem do projeto** são aqueles que você cria e edita. Eles não devem estar na sua árvore web. Eles devem estar no seu espaço de arquivos pessoal. Exemplos, onde cada projeto estará em uma subpasta separada:
  - /Users/username/git (Mac)
  - /home/username/git (Linux)
  - ... (Windows)
- A localização da **árvore web** depende da instalação do seu stack de software. Você pode usar seu próprio espaço de arquivos. Exemplos:
  - /Users/username/Sites/j4test (Mac)
  - /home/username/public_html/j4test (Linux)
  - ... (Windows).
- **Workspace Eclipse** é onde o Eclipse armazena informações sobre projetos individuais. A localização padrão é a raiz do seu próprio espaço de arquivos. Exemplos:
  - /Users/username/eclipse-workspace (Mac)
  - /home/username/eclipse-workspace (Linux)
  - ... (Windows).

Pronto para iniciar o Eclipse?

## Iniciar o Eclipse

Após a inicialização, você será solicitado a confirmar várias configurações. Em algum momento, será solicitado que você escolha um espaço de trabalho. O padrão é /home/username/eclipse-workspace, mas você desejará criar uma subpasta para cada projeto, então selecione o botão Browse e, em seguida, o botão Nova pasta. No exemplo abaixo, eu criei uma pasta chamada j4tutorials.

![Choose eclipse workspace location](../../../en/images/getting-started/eclipse-pdt-choose-workspace.png)

Selecione o botão **Lançar**. Se algo estiver errado, você pode selecionar Arquivo / Trocar Espaço de Trabalho em outro momento e tentar novamente. Você também pode excluir os espaços de trabalho não utilizados mais tarde.

Ao iniciar pela primeira vez, é apresentada uma tela de boas-vindas. Você também pode acessar esta tela a partir dos itens de menu **Ajuda / Boas-vindas**.

![Eclipse welcome screen](../../../en/images/getting-started/eclipse-pdt-welcome.png)

Comece com Revisar Configurações de Configuração do IDE. Você pode Marcar ou Cruzar qualquer uma que pareça apropriada, ou Desmarcar ou Descrossar ou seguir em frente se estiver em dúvida. Você também pode alterar as configurações novamente mais tarde.

## Criar um novo projeto PHP

O primeiro projeto a adicionar é o código do site de teste. Você precisará disso para verificar se seus próprios arquivos estão sendo copiados para os lugares corretos e para depuração mais tarde. Selecione o item na tela de boas-vindas. Se você já estiver no ambiente de trabalho do Eclipse, selecione Criar um Projeto PHP no Explorer de Projetos. No formulário Novo Projeto PHP:

- Insira um Nome de Projeto adequado. Deve ser uma palavra curta que aparecerá no Explorador de Projetos.
- Selecione o botão de rádio **Criar projeto em localização existente (de fonte existente)**.
- **Navegue** até a localização do seu site de teste Joomla e selecione-o.
- Selecione **Concluir**.

![Eclipse new php project](../../../en/images/getting-started/eclipse-pdt-new-project.png)

Seus arquivos do site serão adicionados ao Explorador de Projetos. Pode levar um ou dois minutos para que o Eclipse conclua esse processo, pois ele faz algumas preparações nos bastidores. Você pode selecionar o Projeto para expandir o primeiro nível da pasta.

Dois arquivos serão adicionados à sua pasta do site: .buildpath e .project. Como eles começam com um ponto (.), você pode não vê-los e não precisa se preocupar com eles. Eles são arquivos XML contendo informações usadas pelo Eclipse.

## A Perspectiva do PHP

A coleção de painéis na tela do Eclipse é conhecida como uma perspectiva. As duas mais comumente usadas são a Perspectiva PHP e a Perspectiva de Depuração. Você pode alternar entre elas usando os ícones no canto superior direito da Barra de Ferramentas. Você também pode usar o menu: Janela / Perspectiva / Abrir Perspectiva / PHP ou Depuração.

As ilustrações a seguir mostram a Perspectiva PHP com alguns formulários de edição abertos

![Eclipse php perspective](../../../en/images/getting-started/eclipse-pdt-php-perspective.png)

Os painéis do Eclipse:

- O painel esquerdo é o Explorador de Projetos, onde você pode navegar pela estrutura dos seus arquivos.
- O painel no centro superior é onde os editores de texto abertos aparecem.
- O painel superior direito normalmente mostra um esboço do painel de edição selecionado. Pode exibir outras informações.
- O painel inferior direito mostra uma de várias Visualizações, selecionável a partir do menu Janela / Mostrar Visualização.

A visão de Problemas diz Erros (100 de 791 itens) e Avisos (100 de 11629). Isso parece muito, mas não é motivo de preocupação.

## Um novo projeto PHP Hello Universe

Você está agora pronto para criar um novo Projeto PHP para a extensão que deseja desenvolver. Para ilustração, você pode começar com um componente simples chamado com_hellouniverse. Para mim, o código do Hello Universe estará localizado em /Users/username/git/j4xtutorials-com-hellouniverse e vou usar j4xtutorials como minha afiliação de namespace (a primeira palavra no espaço de nome do componente).

No menu do Eclipse, selecione Arquivo / Novo / Projeto PHP. O formulário é o ilustrado acima. Meus dados:

- Nome do projeto: HelloUniverse
- Conteúdo: selecione Criar projeto em localização existente (a partir de fonte existente).
- Navegar: Vá até /Home/username/git e selecione o botão Nova Pasta.
- Na caixa de diálogo Nova Pasta, insira j4xtutorials-com-hellouniverse e pressione Criar.
- Com essa pasta vazia aberta, selecione Abrir.
- O diretório selecionado deve dizer: /Users/username/git/j4xtutorials-com-hellouniverse
- Selecione Concluir.

Agora você verá o novo projeto no Explorador de Projetos junto com o projeto do seu site. O novo projeto contém dois itens, ambos relacionados ao suporte PHP. Existem alguns itens ocultos usados pelo Eclipse: .settings(pasta), .buildpath e .project.

## Adicionar pasta com_hellouniverse

Com o projeto HelloUniverse selecionado:

- Selecione o item de menu Arquivo ou clique com o botão direito no nome do projeto.
- Selecione os itens de menu Novo / Pasta.
- No formulário Nova Pasta, insira com_hellouniverse no campo Nome da pasta:.
- Selecione Concluir.

A pasta com_hellouniverse é onde o código da sua extensão será colocado. Qualquer coisa dentro dessa pasta acabará em um arquivo zip que você pode usar para instalar no Joomla. Qualquer coisa fora dessa pasta é usada para outros propósitos. Dois arquivos comuns neste nível:

- README.md é um arquivo de texto formatado em Markdown que descreve o componente. Esses arquivos são comumente usados em conjunto com armazenamento de código remoto, como no Github (mais sobre isso em outro lugar).
- build.xml é um arquivo que contém instruções sobre o que fazer após você ter feito alterações no código. Mais comumente, você desejará copiar os arquivos alterados para os lugares corretos em sua árvore de site e regenerar o arquivo zip. Então, para a maioria das mudanças, você pode simplesmente recarregar a página da web em que está trabalhando. Você não precisa reinstalar o componente. Isso é um economizador de tempo enorme!

## Adicionar pastas admin, site e mídia

- Selecione a pasta com_hellouniverse e use os itens de menu Arquivo / Novo / Pasta para criar uma nova pasta chamada admin.
- Novamente, desta vez crie uma nova pasta chamada media. ATENÇÃO: certifique-se de que o pai é com_hellouniverse e não HelloUniverse.
- Novamente, desta vez crie uma nova pasta chamada site. Se criada no lugar errado, ela pode ser arrastada para o lugar correto.

## build.xml

O seguinte código contém um exemplo de arquivo build.xml para colocar na raiz do seu projeto HelloUniverse.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="hellouniverse" basedir="." default="main">
    <property file=".project" />

    <!-- Source and Destinations -->

    <property name="package"  value="${phing.project.name}" override="true" />
    <property name="srcdir" value="${project.basedir}/com_hellouniverse" override="true" />
    <property name="sitedir" value="/Users/username/Sites/j4tutorials"  override="true" />
    <property name="zipsdir" value="/Users/username/zips"  override="true" />

    <!-- Filesets -->

    <fileset dir="${srcdir}/admin" id="adminfiles">
        <include name="**" />
    </fileset>
    <fileset dir="${srcdir}/media" id="mediafiles">
        <include name="**" />
    </fileset>
    <fileset dir="${srcdir}/site" id="sitefiles">
        <include name="**" />
    </fileset>
    <fileset dir="${srcdir}" id="allfiles">
        <include name="**" />
    </fileset>

    <!-- Targets -->

    <target name="main" description="main target">
        <copy todir="${sitedir}/administrator/components/com_hellouniverse">
            <fileset refid="adminfiles" />
        </copy>
        <copy todir="${sitedir}/media/com_hellouniverse">
            <fileset refid="mediafiles" />
        </copy>
        <copy todir="${sitedir}/components/com_hellouniverse">
            <fileset refid="sitefiles" />
        </copy>
        <zip destfile="${zipsdir}/com_hellouniverse.zip">
            <fileset refid="allfiles" />
        </zip>
    </target>
</project>
```

Algumas explicações:

- **srcdir** é a localização no sistema de arquivos do seu código-fonte, de onde os arquivos são copiados.
- **sitedir** é a localização no sistema de arquivos do seu site de teste, para onde os arquivos são copiados.
- **zipsdir** é um local para o arquivo zip - acho conveniente manter arquivos zip de projetos diferentes juntos em uma pasta de zips.
- **Conjuntos de arquivos** são grupos de origem a serem copiados para diferentes destinos. significa todas as pastas e arquivos.
- **Destinos** são os locais e o que precisa ser copiado para lá.

Crie um arquivo build.xml contendo o código acima:

- Selecione Arquivo / Novo / Arquivo XML no menu do Eclipse.
- Certifique-se de que HelloUniverse esteja selecionado como o pai e insira o nome build.xml (exatamente assim).
- Selecione Concluir
- Na Visualização do Código-fonte (escolha no canto inferior esquerdo) copie e cole o código acima no lugar da única linha já existente.
- Salvar.

Para que isso funcione, você precisa de uma ferramenta de build: Phing.

## A Ferramenta de Build Phing¶

Vá para o site do [Phing](https://www.phing.info/) e baixe o arquivo Phar. Você pode usar este [link direto](https://www.phing.info/get/phing-latest.phar). Salve o arquivo em uma pasta phing na sua pasta pessoal bin /Users/username/bin/phing. Altere as permissões do arquivo para 755 para que ele possa ser executado a partir da linha de comando. Para testar, abra um terminal, mude para sua pasta bin/phing e insira ./phing-latest.phar -v para ver o número da versão. Lembre-se do caminho completo para o arquivo:

- /Usuarios/nomedeusuario/bin/phing/phing-maisrecente.phar

Você vai precisar disso mais tarde.

## Preferências do Eclipse - Construtores

É aqui que você configura o Phing para construir seu projeto sempre que fizer alterações no código.

- No Project Explorer, selecione o projeto HelloUniverse.
- Selecione os itens de menu Arquivo / Propriedades.
- Na caixa de diálogo Propriedades, selecione Construtores e, em seguida, o botão Novo.
- Na caixa de diálogo Tipo de Configuração, selecione Programa e depois OK.
- na caixa de diálogo de propriedades de configuração de lançamento, insira um título adequado: Build HelloUniverse.
- no campo Localização, insira o caminho para o programa phing ou use o botão Procurar Sistema de Arquivos para buscá-lo: /Users/ceford/bin/phing/phing-latest.phar
- Para o campo Diretório de trabalho, selecione o botão Procurar espaço de trabalho e depois selecione HelloUniverse.
- Clique em OK, depois Aplicar e Fechar.

Para testar: selecione os itens de menu Projeto / Construir Projeto. A visualização do Console na parte inferior da tela mostrará o progresso da construção. Nesta fase, provavelmente mostrará CONSTRUÇÃO FALHOU em vermelho. Isso é esperado - as pastas dos componentes serão criadas na instalação do arquivo zip. Ainda não existe porque não há código. Mas isso mostra que a ferramenta de construção Phing está funcionando.

## Como Depurar

Quando algo dá errado, você pode querer passar pelo código linha por linha para ver o que realmente está acontecendo. Se você configurou o Sistema de Depuração para Sim e a Exibição de Erros para Máximo na Configuração Global do Joomla, você pode ter um rastreamento de pilha que mostra onde um erro está ocorrendo no código. Ou você pode estar vendo algo incomum na saída e ter uma boa ideia de onde a falha pode estar. Em ambos os casos, você precisa definir pontos de interrupção onde a execução será pausada para permitir que você veja os valores das variáveis e prossiga pelo código linha por linha.

### Definir um Ponto de Interrupção

Os pontos de interrupção precisam ser definidos no projeto do site, J4Tutorials. Como exemplo, no painel Project Explorer, expanda o projeto J4Tutorials e encontre administrator / components / com_users / src / Model e dê um duplo clique em UsersModel.php para abri-lo em uma janela de edição. Vá para a linha 87 e dê um duplo clique no número 87. Um pequeno marcador azul aparece para indicar que um ponto de interrupção foi definido. A execução do código deve parar aqui quando você visualizar a lista de Usuários através dos itens de menu Administrator / Users / Manage.

### Criar uma Configuração de Depuração

No menu superior, selecione Executar / Configurações de Depuração. No formulário, insira um título reconhecível, por exemplo Debug Admin, para selecionar mais tarde de uma lista suspensa. Certifique-se de que o arquivo selecionado seja /J4Tutorials/administrator/index.php. No formulário do painel Comum, selecione Depurar na lista de exibição em favoritos. Verifique se o Depurador está configurado para Xdebug. Selecione Aplicar e Fechar.

Agora você pode selecionar Debug Admin na lista suspensa de depuração da barra de ferramentas, o ícone de símbolo de bug.

![Eclipse debug tools](../../../en/images/getting-started/eclipse-pdt-debug-tools.png)

Ícones de depuração, passe o cursor para ver os rótulos:

- **Pular Todos os Pontos de Interrupção** Um botão para pular pontos de interrupção, exceto a primeira linha do index.php.
- **Retomar** Continuar a execução normal até o próximo ponto de interrupção.
- **Terminar** Parar a depuração (mas você também precisa remover o cookie do Xdebug).
- **Entrar** Em uma linha contendo uma chamada de função, entre nessa função.
- **Passar por Cima** Em uma linha contendo uma chamada de função, não entre nessa função.
- **Sair de** Em uma função, pule as paradas em cada linha e retorne ao chamador.

### Procedimento de Depuração

Ao iniciar uma sessão de depuração, a execução pausa na primeira linha de administrator/index.php. Essa é a página do Painel Inicial. Você precisa selecionar o símbolo de Retomar (barra amarela e triângulo verde à direita). Após um atraso de um segundo ou mais, há mais atividade e mais lançamentos Remotos pausados no painel esquerdo de Depuração do Administrador. Esta é a página Inicial usando ajax para buscar informações de atualização. Continue clicando em Retomar até que a atividade pare. Então, no seu navegador, selecione o item Usuários do Painel Inicial. O Eclipse ganha vida e para a execução no ponto de interrupção que você configurou.

![Eclipse PHP debug perspective](../../../en/images/getting-started/eclipse-pdt-debug-perspective.png)

Recursos a observar:

- A linha de código atual está marcada com um fundo verde claro.
- O painel esquerdo mostra um rastreamento de pilha - as chamadas de função anteriores que levaram à função atual. Selecione qualquer item para ver o código pai.
- O painel direito pode mostrar variáveis ativas ou pontos de interrupção. Expanda objetos conforme necessário para ver detalhes.

### Alguns problemas

- Falha ao parar em pontos de interrupção: Isso acontece se você abrir outro programa PHP, como o phpMyAdmin. Para corrigir:
  - Vá para Executar / Configurações de Depuração e selecione seu item de Administração de Depuração.
  - Na guia Depurador, selecione Configurar...
  - Em Mapeamento de Caminho, selecione e Remova qualquer caminho não relacionado ao seu site de teste.
  - Selecione Concluir - você pode precisar Terminar e recarregar a sessão de depuração.
- A depuração é retomada após selecionar o botão Terminar. Para corrigir:
  - Use as Ferramentas do Desenvolvedor do seu navegador para abrir uma janela de inspeção.
  - Encontre os cookies que seu navegador está usando (Armazenamento no Firefox)
  - Selecione e exclua o cookie XDebug.

## Usando o Git

O Git é um sistema de controle de versão amplamente utilizado para gerenciar qualquer tipo de texto, principalmente código, mas pode ser qualquer coisa. Ele funciona a partir de uma linha de comando, mas geralmente é acionado por ferramentas gráficas como o Eclipse. Se você quiser ler sobre o git, veja o [site do git](https://git-scm.com/).

Se você quiser usar o git, você precisa instalá-lo para sua plataforma. Em seguida, no Eclipse, selecione seu projeto HelloUniverse, clique com o botão direito e selecione Equipe / Compartilhar Projeto. No diálogo Compartilhar Projeto, selecione **Usar ou criar repositório na pasta pai do projeto** e selecione o projeto HelloUniverse da lista. Há um campo para indicar onde o repositório será criado (/Users/ceford/git/j4xtutorials-com-hellouniverse) - selecione o botão Criar Repositório adjacente. Finalmente, selecione o botão Concluir.

![Configure Git Repository](../../../en/images/getting-started/eclipse-pdt-configure-git.png)

Você notará que algumas novas decorações apareceram ao lado dos itens na visualização do Project Explorer:

- O marcador \> indica que há conteúdo que foi alterado mas não foi enviado para o repositório.
- O marcador ? indica que este item não foi adicionado à lista de itens a serem rastreados.

![Git Markers](../../../en/images/getting-started/eclipse-pdt-git-markers.png)

Você agora está configurado para controle de versão. Clique com o botão direito no projeto e veja como é o menu Equipe. Muito para cobrir aqui!

## Finalmente

Pronto para começar a trabalhar no seu próprio código?

*Traduzido por openai.com*

