<!-- Filename: Working_with_git_and_github / Display title: Trabalhando com git e github -->

## Introdução

Este documento fornecerá informações sobre como contribuir para o Joomla! CMS com a ajuda do Git e GitHub. Se você gostaria de fazer uma mudança simples (apenas um arquivo), é mais fácil usar esta documentação: [Using the Github UI to Make Pull Requests](https://docs.joomla.org/Using_the_Github_UI_to_Make_Pull_Requests). Se você deseja adicionar mudanças mais complexas ou está apenas interessado nisso, continue lendo!

## O que são Git e GitHub?

Git é um sistema de controle de versão distribuído. É um sistema que registra alterações em arquivos e mantém essas alterações em um arquivo de histórico. Você pode sempre voltar a uma versão anterior do seu código e restaurar as alterações, se desejar. Por causa do arquivo de histórico, o Git é muito útil quando você trabalha com muitas pessoas no mesmo projeto.

Aqui está como o GitHub pode ser usado. [GitHub](https://www.github.com) é um site que ajuda a gerenciar Projetos Git de maneira visual. Como proprietário de um projeto, você pode alterar o código e comparar diferentes versões. Como usuário do projeto, você pode contribuir fazendo Pull Requests. Um Pull Request é uma solicitação ao proprietário para puxar algum código para o projeto. Você está oferecendo um pedaço de código (talvez uma solução para um bug) e perguntando se o proprietário do projeto gostaria de usá-lo. Se o proprietário gostar, ele pode mesclá-lo (adicioná-lo) ao seu projeto.

Joomla! usa o GitHub e o Git para manter seu código. Qualquer pessoa pode contribuir para o software Joomla! através do seu [repositório no Github](https://github.com/joomla/joomla-cms).

## Inscreva-se no GitHub e instale o Git

Primeiro, você precisará [registrar-se no Github](http://www.github.com). É gratuito e fácil de fazer. Basta seguir os passos fornecidos.

Depois de se inscrever, você precisa instalar o Git no computador que utiliza para desenvolvimento (estação de trabalho ou laptop). Siga as instruções de instalação no site do [git](http://git-scm.com). O Git é um programa CLI (Interface de Linha de Comando). No início, isso pode ser confuso e um pouco assustador, mas este documento irá guiá-lo pelo processo.

Se você não é um usuário avançado, basta executar o instalador e pressionar os botões "próximo" até que o programa seja instalado. Git não danificará seu sistema. Mais tarde, você pode removê-lo como qualquer outro programa.

Com o Git instalado, abra um aplicativo Terminal. Comece configurando seu nome e endereço de e-mail no Git. O Git usará essas informações quando você contribuir para um projeto:

```sh
    git config --global user.name "Your name"
    git config --global user.email youremail@mail.com
```

Nos comandos acima, e em todos os outros comandos dados nesta documentação, cada linha é um novo comando. Então, você digita a primeira linha, pressiona enter e depois digita a segunda linha e pressiona enter.

Você agora está pronto para usar o Git e avançar com a configuração da sua instalação de teste.

## Configurando uma instalação de teste

Para sua instalação de teste, você precisa de um conjunto de softwares para que possa instalar e executar o Joomla! em seu computador. Conjuntos como MAMP, XAMP ou WAMP são abordados em outro local desta documentação.

Após a instalação da sua pilha de software, você precisa instalar a versão mais recente do Joomla!. Esta não é a última versão estável. A última versão do Joomla! é o branch de staging no GitHub.

## Fazer um Fork e Clonar o Joomla!

No GitHub, você pode encontrar projetos em chamados Repositórios. Dentro de um projeto, você pode encontrar várias versões. Tal versão é chamada de Branch. O Joomla! possui os seguintes branches:

- **4.2-dev** Arquivos para desenvolvimento da versão atual.
- **4.3-dev** Arquivos para desenvolvimento da próxima versão secundária.
- **4.4-dev** Arquivos para desenvolvimento da versão secundária subsequente.
- **5.0-dev** Arquivos para desenvolvimento da próxima versão principal.

No seu computador de teste, você vai usar o ramo **4.2-dev**. No entanto, você não pode modificar este ramo porque não é o proprietário dele. Você precisa fazer uma cópia dele. No GitHub, isso é chamado de Fork. Você é o proprietário dessa cópia, então pode modificá-la. Após modificar seu fork, você pode fazer um Pull Request para as alterações que fez. Mais sobre isso mais tarde. Você pode fazer um Fork de um ramo pressionando o botão Fork no [Joomla! CMS Github Repository](https://github.com/joomla/joomla-cms). Este botão está localizado no canto superior direito da página.

![Fork joomla in github](../../../en/images/getting-started/core-git-fork-joomla.png)

Após o fork, você precisa instalar o Joomla! no seu computador local. Vá para a pasta onde você pode colocar arquivos usados pelo seu servidor Web. Muitos programas usam uma pasta chamada `htdocs`. Alguns usam `www` e outros usam pastas completamente diferentes. Tudo depende se você está usando Windows, Mac ou Linux. Eventualmente, seu diretório raiz da web conterá diferentes pastas para diferentes sites. Uma vez que você está dentro da sua pasta raiz da web. Ou, em uma janela de Terminal aberta, use o comando cd para mudar o diretório atual para a raiz da web. Ou, no seu explorador de arquivos GUI, encontre a pasta raiz da web, pressione o botão direito do mouse e clique em: "Git Bash Here" ou "Open Terminal" ou algo semelhante.

No Terminal, com a pasta raiz do site definida como a pasta atual, digite o seguinte comando para baixar os arquivos do seu Fork do Joomla! CMS para o seu computador. Por favor, substitua *username* pelo nome de usuário que você está usando no GitHub.

```sh
    git clone https://github.com/username/joomla-cms.git
```

O processo de clonagem pode demorar bastante. Quando concluído, a raiz da sua web conterá uma pasta chamada joomla-cms. Você precisa tornar essa pasta a pasta atual para executar comandos git para essa pasta:

```sh
    cd joomla-cms
```

Por favor, lembre-se disso para outros comandos nesta documentação.

## Instalar o Joomla!

Seu clone baixado do seu repositório bifurcado precisa de mais ações antes de estar pronto para uso. Um dos arquivos baixados é chamado README.md. Abra-o com um editor de texto e siga as instruções em **Como obter uma instalação funcional a partir do código-fonte**.

Quando estiver pronto, abra seu navegador e acesse a instalação no seu localhost. Normalmente, a URL é algo como: `http://localhost/joomla-cms`. Você agora verá o processo padrão de instalação do Joomla!.

## Fazer Alterações no Código

Todas as alterações que você fizer no código Joomla em seu site local serão registradas e monitoradas pelo Git. A qualquer momento, você pode digitar o comando `git status` para ver quais arquivos foram modificados ou não rastreados. Não rastreados significa que o arquivo nesse local é novo para o Git.

Neste estágio, provavelmente é melhor usar um Ambiente de Desenvolvimento Integrado (IDE) para trabalhar no código do Joomla. O Visual Studio Code (VSCode) é altamente recomendado. É gratuito e funciona em todas as plataformas. Usando o VSCode, você pode fazer alterações, **commitá-las** no seu clone local do Git e **enviá-las** para o seu fork remoto no GitHub.

## Enviar Alterações para o Fork

Enviar mudanças é chamado de `push` em termos de Git. Antes de fazer isso, você precisa fazer algo muito importante. Você deve criar um novo branch para suas mudanças. (Um branch é uma versão do seu projeto, lembra?) Se você não fizer isso e fizer sua alteração diretamente no branch atual, na primeira vez não haverá problema. Mas se você fizer alterações uma segunda vez e as alterações que você fez na primeira vez ainda não foram mescladas, todas essas alterações também serão registradas como novas alterações.

Você pode configurar o VSCode para realizar todos os seguintes comandos com alguns cliques. Mas se você quiser usar os comandos do git a partir da linha de comando do terminal:

Então, o primeiro comando que você vai executar criará um novo branch. Substitua name-new-branch pelo nome do novo branch. Este nome deve ser curto e só pode conter letras minúsculas e números. **NÃO** use espaços. Em vez de espaços, use - (menos).

```sh
    git checkout -b name-new-branch
```

O próximo comando informa ao git que todas as alterações estão prontas para ser confirmadas.

```sh
    git add --all
```

O seguinte comando adiciona sua alteração ao branch. Por favor, substitua a mensagem por uma breve descrição de suas alterações. Esta descrição será o título da pull request que você vai fazer.

```sh
    git commit -m "description"
```

O comando final irá enviar (fazer upload) das alterações para seu fork. Por favor, substitua name-new-branch pelo nome do ramo que você criou alguns passos acima.

```sh
    git push origin name-new-branch
```

## Comparar Forks e Fazer um Pull Request

Após enviar sua alteração para o GitHub, vá para o seu fork do Joomla! CMS no site do GitHub. Selecione seu branch e faça um pull request.

Quando terminar, no seu clone local, mude de volta para o ramo original:

```sh
git checkout 4.2-dev
```

Agora, você pode fazer novas alterações sem afetar as alterações na sua ramificação anterior.

## Mantendo-se atualizado

Como a versão atual do Joomla! pode mudar todos os dias, é importante manter seu fork atualizado. Você pode fazer isso adicionando o repositório original do Joomla ao seu projeto fork:

```sh
    git remote add upstream https://github.com/joomla/joomla-cms.git
```

Em seguida, atualize seu clone local com o seguinte comando:

```sh
    git pull upstream 4.2-dev
```

E atualize seu fork remoto:

```sh
    git push
```

*Traduzido por openai.com*

