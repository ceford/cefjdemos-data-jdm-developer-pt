<!-- Filename: Visual_Studio_Code_Primer / Display title: Visual Studio Code -->

## VS Code - Um IDE Gratuito Popular

Do [Wikipedia](https://en.wikipedia.org/wiki/Visual_Studio_Code):

Visual Studio Code, também comumente referido como VS Code, é um editor de código-fonte feito pela Microsoft para Windows, Linux e macOS. As funcionalidades incluem suporte para depuração, realce de sintaxe, conclusão inteligente de código, trechos de código, refatoração de código e Git incorporado. Os usuários podem alterar o tema, atalhos de teclado, preferências e instalar extensões que adicionam funcionalidades adicionais.

## Instalação

A página padrão do site [VS Code](https://code.visualstudio.com/) possui uma lista suspensa para cada plataforma suportada. As chances são de que sua plataforma já esteja pré-selecionada. Então, faça o download e instale, e você estará pronto para começar.

### Primeiros Passos

A página *Introdução* do VS Code possui alguns itens de *Início*, uma lista de itens *Recentes* e uma breve lista de *Guias Práticos*. Se você é totalmente novo no VS Code, é recomendado dar uma olhada. Eles levam apenas alguns minutos.

A Documentação do VS Code está disponível no menu *Ajuda / Documentação*. Os Vídeos Introdutórios valem muito a pena serem assistidos. Cada um leva de 2 a 6 minutos e oferece uma excelente introdução às funcionalidades do VS Code:

[Vídeos do VS Code](https://code.visualstudio.com/docs/getstarted/introvideos)

A documentação oficial é o lugar a se consultar se você deseja procurar informações específicas.

### Extensões do VS Code

O VS Code pode ser usado para qualquer tipo de texto, incluindo uma ampla gama de linguagens de programação. Funciona com JavaScript sem a necessidade de adicionar extensões. Outras linguagens são detectadas por contexto, então, se você começar a criar e salvar código em PHP, é provável que lhe seja solicitado a instalar um pacote de suporte PHP.

Clique no ícone de *Extensões* na *Barra de Atividades* à esquerda para ver o que você tem instalado e o que é recomendado. Você precisará da extensão PHP Debug!

### O Layout da Tela do VS Code

Alguns termos usados nas instruções subsequentes:

- **Barra de Atividades:** a barra estreita à esquerda da tela. Selecione qualquer ícone para abrir ou fechar a Barra Lateral Principal.
- **Barra Lateral Principal:** quando aberta, mostra detalhes da atividade selecionada.
- **Barra de Status:** na parte inferior da tela. Mostra o que está acontecendo.
- **Painel:** uma área abaixo dos editores de texto para exibir outras informações.

Selecione um ícone de layout no canto superior direito para abrir ou fechar qualquer um destes itens.

## Codificando uma Extensão do Joomla

Para criar uma extensão, seu objetivo é criar um arquivo zip que você possa instalar em um site Joomla funcional. Assim, você precisa de uma pasta para conter seu código. Isso deve estar dentro do seu espaço de arquivos pessoais no seu laptop ou computador desktop usado para desenvolvimento local. Não deve estar na árvore do seu site. Por exemplo, você poderia usar *~/jextensions* para conter subpastas para diferentes extensões. Eu uso *~/git* porque é curto e fácil de soletrar, embora potencialmente confuso porque cada subpasta usa um repositório git separado.

### Código de Exemplo

Se você gostaria de algum código de amostra para trabalhar, há uma extensão disponível no GitHub chamada *mod_debugme*. Como o nome sugere, é um módulo com alguns bugs. Além do código do módulo, existe um arquivo *build.xml* para ilustrar uma maneira de automatizar a construção para teste e a criação de um arquivo zip.

O módulo foi projetado para mostrar os próximos eventos (aniversários) da lista armazenada em uma tabela de banco de dados (3 por padrão). Você pode imaginar isso sendo usado em um escritório ou site de família com a expectativa de bolo.

Pode ser melhor começar usando comandos git a partir da linha de comando. Primeiro, crie uma pasta para o seu código e depois clone o repositório remoto:

```sh
    mkdir ~/git
    cd ~/git
    git clone https://github.com/ceford/j4xdemos-mod-debugme
```

A resposta deve levar apenas alguns segundos:

```sh
    Cloning into 'j4xdemos-mod-debugme'...
    remote: Enumerating objects: 23, done.
    remote: Counting objects: 100% (23/23), done.
    remote: Compressing objects: 100% (16/16), done.
    remote: Total 23 (delta 3), reused 23 (delta 3), pack-reused 0
    Unpacking objects: 100% (23/23), done.
```

Você deve reservar um momento para olhar o conteúdo da pasta:

```sh
    cd j4xdemos-mod-debugme
    ls -al
    total 16
    drwxr-xr-x   6 ceford  staff   192  2 Sep 17:48 .
    drwxr-xr-x   3 ceford  staff    96  2 Sep 17:48 ..
    drwxr-xr-x  12 ceford  staff   384  2 Sep 17:48 .git
    -rw-r--r--   1 ceford  staff  1402  2 Sep 17:48 README.md
    -rw-r--r--   1 ceford  staff   927  2 Sep 17:48 build.xml
    drwxr-xr-x   8 ceford  staff   256  2 Sep 17:48 mod_debugme
```

A pasta *.git* contém informações sobre o repositório. O arquivo *README.md* é um documento markdown que descreve este repositório. O arquivo *build.xml* é um arquivo usado para construir a extensão com uma ferramenta externa, Phing - descrito mais tarde. A pasta *mod_debugme* contém o código da extensão.

### Instalar no Joomla

Compacte a pasta de extensão para criar um arquivo zip instalável:

```sh
    zip -r mod_debugme.zip mod_debugme
```

Agora você pode instalar o arquivo zip no site Joomla que você usa para testes. Após a instalação, você precisa criar um módulo de Site e atribuí-lo a uma posição de módulo. Como é um módulo em desenvolvimento, você poderia atribuí-lo a uma posição em *Todas as páginas* enquanto trabalha nele; ou você poderia atribuí-lo a uma posição em uma única página; ou poderia posicioná-lo em um artigo que tenha seu próprio item de menu.

Após a instalação, exclua o arquivo zip.

### Ativar Modo de Depuração

Na Configuração Global do Joomla, defina *Debug System* como *Sim* e *Error Reporting* como *Máximo*.

Quando você abre uma página contendo o módulo com problemas, verá um rastreamento de pilha informando onde um erro foi acionado.

![Stack trace](../../../en/images/getting-started/vscode-primer-stack-trace.png)

Às vezes, o erro de codificação está na primeira linha do rastreamento de pilha. Caso contrário, se o erro for acionado no código da biblioteca, por exemplo, ao passar dados inválidos para uma função de banco de dados, o erro de codificação pode estar mais abaixo na lista de chamadas de função.

## Abrir Pasta de Extensão no VS Code

No VS Code, use o item de menu Arquivo / Abrir Pasta para localizar e abrir a pasta que contém sua cópia local do código da extensão *mod_debugme*. Você deve ver algo semelhante ao seguinte:

![VS Code screen](../../../en/images/getting-started/vscode-primer-screen.png)

Você pode ser capaz de diagnosticar o problema apenas lendo o código. No caso do erro *Classe "DebugHelper" não encontrada*, você verá que uma declaração *use* foi comentada algumas linhas anteriormente. Esquecer de inserir uma declaração *use* é um erro comum durante o desenvolvimento inicial!

Corrija esse problema e, em seguida, comprima e instale o módulo novamente. Essa etapa se torna um pouco tediosa quando você tem vários problemas. É aí que as ferramentas de construção se tornam úteis.

## A Ferramenta de Construção Phing

Phing é uma ferramenta de linha de comando, disponível para todas as plataformas, usada para construir pacotes de software usando instruções armazenadas em um arquivo xml, chamado build.xml por padrão. Para trabalhar com código de extensão, pode ser usado para fazer duas coisas:

- copie os arquivos alterados da pasta de origem da sua extensão para os locais corretos na pasta do seu site.
- gere um novo arquivo zip para novas instalações.

Baixe e instale [Phing](https://www.phing.info/). Outros ferramentas de build estão disponíveis! Você pode instalar o Phing na sua própria pasta bin ou em uma pasta bin do sistema. Você precisa anotar o caminho para o seu código Phing. Neste exemplo, é *~/bin/phing-latest.phar*. Você pode testá-lo a partir da linha de comando após mudar para a pasta que contém o código da sua extensão:

```sh
    cd ~/git/j4xdemos-mod-debugme
    php ~/bin/phing-latest.phar
```

Resposta:

```sh
    Buildfile: /Users/ceford/git/j4xdemos-mod-debugme/build.xml

    mod_debugme > main:
          ... Any copied files will be mentioned here
          [zip] Building zip: /Users/ceford/zips/mod_debugme.zip

    BUILD FINISHED

    Total time: 0.0863 seconds
```

## Tarefas do VS Code

Para executar o Phing a partir do VS Code, você precisa criar um arquivo *tasks.json* na pasta *.vscode* na raiz da pasta *j4xdemos-mod-debugme*. Se esta última não existir, crie-a primeiro. Em seguida, crie o arquivo *tasks.json* e insira o seguinte código:

```json
    {
        // See https://go.microsoft.com/fwlink/?LinkId=733558
        // for the documentation about the tasks.json format
        "version": "2.0.0",
        "tasks": [
          {
            "label": "Build mod_debugme",
            "type": "shell",
            "command": "php ~/bin/phing-latest.phar",
            "windows": {
              "command": "php ~/bin/phing-latest.phar"
            },
            "group": "build",
            "presentation": {
              "reveal": "always",
              "panel": "shared"
            }
          }
        ]
    }
```

Usuários do Windows precisam corrigir o comando específico do Windows. Agora, você pode compilar a extensão usando o menu *Terminal / Executar Tarefa de Compilação*. O resultado do comando deve aparecer no Painel de Terminal abaixo da área de Edição.

```sh
      *  Executing task: php ~/bin/phing-latest.phar

    Buildfile: /Users/ceford/git/gitdemo/j4xdemos-mod-debugme/build.xml

    mod_debugme > main:

          [zip] Nothing to do: /Users/ceford/zips/mod_debugme.zip is up to date.

    BUILD FINISHED

    Total time: 0.1031 seconds

     *  Terminal will be reused by tasks, press any key to close it.
```

Podem haver mensagens de erro incompreensíveis. A causa mais provável é ter caminhos inválidos para pastas no arquivo *build.xml* ou uma pasta não foi criada. Apenas outro tipo de problema para depurar!

## Depuração

Você deve ser capaz de corrigir o primeiro bug por inspeção de código. Problemas mais complicados exigem percorrer o código com o depurador. Isso permite inspecionar variáveis para ver se elas contêm valores que você espera, por exemplo, ao passar argumentos para funções de bibliotecas.

### Configurações do *php.ini*

Para configurar a depuração com o Xdebug, você precisa fazer algumas entradas no topo do seu arquivo *php.ini*.

```sh
    zend_extension="xdebug.so"
    xdebug.mode="debug"
    xdebug.client_port=9003
    xdebug.start_with_request=yes
    xdebug.log_level=0
```

Após salvar quaisquer alterações, reinicie seu servidor Apache.

### Adicionar Janela de Site

Sua pasta de extensão contém apenas alguns arquivos, os ***fontes*** dos arquivos instalados em seu site. A depuração em tempo de execução envolve definir pontos de interrupção nos arquivos do seu ***site***, portanto, você precisa de acesso a esses arquivos. Você poderia usar o menu *Arquivo / Adicionar Pasta ao Espaço de Trabalho...* para adicionar a pasta do site ao seu Espaço de Trabalho. No entanto, há uma grande chance de você acabar fazendo alterações nos arquivos do site em vez dos arquivos de origem. Portanto, é provavelmente melhor abrir uma janela separada do VS Code para depuração.

- **Abrir nova janela:** No menu do VS Code, selecione *Arquivo / Nova Janela* e escolha a pasta que contém o seu site Joomla.
- **Abrir pasta:** Na janela recém-aberta, selecione *Arquivo / Abrir Pasta...* no menu do VS Code. Encontre a pasta do seu site e selecione-a. Você deverá ver uma lista de todos os arquivos do seu site Joomla na barra lateral principal.

### Configuração de Lançamento

Para que a depuração funcione de verdade no VS Code, você precisa de uma configuração de lançamento. Na raiz do seu site, crie uma pasta chamada *.vscode* (note o ponto inicial) contendo um arquivo chamado *launch.json* com o seguinte conteúdo:

```json
    {
        "configurations": [
            {
                "name": "Listen for XDebug",
                "type": "php",
                "request": "launch",
                "hostname": "0.0.0.0",
                "port": 9003,
                "stopOnEntry": true,
                "pathMappings": {
                    "/Users/ceford/Sites/j421rc2": "${workspaceFolder}"
                }
            }
        ]
    }
```

Lembre-se de substituir o item pathMappings neste exemplo com o pathMappings real no seu próprio site. O item stopOnEntry irá pausar a execução na primeira linha de código PHP executada.

### Depurar *mod_debugme*

Agora você está pronto para encontrar e corrigir os bugs no módulo instalado.

- **Encontrar o código do módulo:** Encontre o primeiro bug na linha 16 de JROOT/modules/mod_debugme/mod_debugme.php.
- **Definir ponto de interrupção:** Clique no espaço à esquerda do número 16. Um ponto vermelho claro aparecerá quando você passar o mouse e ficará vermelho completo após o clique para indicar que um ponto de interrupção foi definido.
- **Iniciar depuração:** No menu do VS Code, selecione *Run / Start Debugging*. No seu navegador, recarregue seu site. Sua janela do VS Code deve reaparecer com o código parado na primeira linha do arquivo *index.php* do site. No topo da tela, há alguns ícones para controlar o processo de depuração. Eles devem ser autoexplicativos. Caso contrário, procure-os na Ajuda / Documentação do VS Code.
- **Continuar:** Selecione o botão de continuar - o código irá rodar até o seu primeiro ponto de interrupção. Examine o código para ver qual é o problema.
- **Pairar:** Se você passar o mouse sobre uma variável que recebeu um valor, um pequeno Tooltip aparecerá resumindo os atributos dessa variável. Não há Tooltip para variáveis que não receberam valores.
- **Variáveis:** A coluna da esquerda contém mais informações sobre o estado do código no ponto de interrupção. Há muitas informações para cobrir aqui. Explore-as conforme necessário!
- **Parar Depuração:** Provavelmente é melhor selecionar o ícone Continuar, caso contrário, a página web é entregue em branco. Caso contrário, você pode usar o botão Parar ou o menu Run / Stop Debugging.

### Corrigir um Bug

**Lembre-se:** Não corrija o bug no código do site! Corrija no código-fonte!

Corrija o código-fonte e depois use *Terminal / Executar Tarefa de Construção...*.

Reiniciar depuração.

### Dicas

Alguns problemas não tão óbvios:

- Você corrige o primeiro bug, mas ele ainda trava naquela linha. Consulte o arquivo mod_debugme.xml para ver onde o src das classes com namespace está definido. Quando corrigido no código fonte, você precisa reinstalar o arquivo zip ou deletar *administrator/cache/autoload_psr4.php*. Quando ausente, o Joomla reconstrói esse arquivo a partir dos arquivos de manifesto. Mas se ele tiver uma entrada incorreta ou ausente, não será corrigido até que a extensão seja reinstalada.
- Às vezes, é necessário definir um ponto de interrupção algumas linhas antes da linha onde o erro ocorre, especialmente se você deseja verificar os valores passados para as chamadas de função.
- A tabela *xxx.yyy\\debugme* não existe. Ah sim, o código para criar uma tabela na instalação e remover na desinstalação nunca foi criado. Você precisará executar uma consulta SQL no phpMyAdmin usando o conteúdo do arquivo *mod\\debugme.sql*. Lembre-se de mudar *\#\\* nos nomes das tabelas para o seu prefixo de banco de dados. E quando ele ainda falhar, verifique o nome da tabela no código.

## Captura de tela

Quando tudo estiver resolvido, isto é o que você pode ver:

![Site view of debugged module working](../../../en/images/getting-started/vscode-primer-debugme-fixed.png)

Dias de bolo?

## Referências

Da Documentação do Joomla!: [Visual Studio Code](https://docs.joomla.org/Visual_Studio_Code) que também abrange a configuração de outras ferramentas, por exemplo, CodeSniffer e PHPUnit.

*Traduzido por openai.com*

