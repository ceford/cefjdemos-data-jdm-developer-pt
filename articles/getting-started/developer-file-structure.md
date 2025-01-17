<!-- Filename: J4.x:Developer:_File_Structure / Display title: Estrutura de Arquivo de Exemplo -->

## Introdução

Como um indivíduo começando a desenvolver algumas extensões do Joomla em um computador pessoal, laptop ou desktop, você precisa configurar uma estrutura de arquivos adequada para o código da sua extensão. A localização do seu site Joomla é predefinida pelo seu sistema operacional e instalação do Apache. A localização do código que você cria é de sua escolha.

## Localização do Site de Teste

Neste exemplo, os sites de teste do Joomla estão localizados em subpastas da raiz do documento. Isso permite a criação de muitos sites para todos os tipos de projetos diferentes sem a necessidade de criar hosts virtuais. Alguns sites de teste podem não estar relacionados ao Joomla de forma alguma. A raiz do site para diferentes plataformas:

- Mac: /Users/nome_de_usuário/Sites
- Linux: /home/nome_de_usuário/public_html
- Windows: ...

Este é um screenshot de parte de uma lista de pasta de Sites mostrando uma seleção de muitos sites de teste:

![multiple sites on mac](../../../en/images/getting-started/developer-file-structure-mac-sites.png)

Cada um é acessado pelo nome da sua subpasta. Exemplos:

- `http://localhost/j4teste`
- `http://localhost/j520`

Existem circunstâncias em que você pode preferir criar sites virtuais separados. Isso não está coberto aqui.

## Estrutura de Arquivos do Site de Teste

Se ainda não o fez, será necessário familiarizar-se com a estrutura de um site Joomla. A ilustração a seguir mostra uma árvore de arquivos e pastas típica do Joomla, com a pasta do Administrador expandida para mostrar seu conteúdo.

![joomla file structure with administrator expanded](../../../en/images/getting-started/developer-file-structure-mac-joomla.png)

Este é o local onde o código funcional será instalado. O código-fonte está em outro lugar.

## Localização do Código da Extensão do Desenvolvedor

A localização do seu código de extensão é uma escolha pessoal. Eu gosto de manter meu código de extensão em uma estrutura de arquivos adequada para a criação de um arquivo zip instalável. A base da minha árvore é /Users/username/git porque eu sei soletrar git e uso git para controle de versão. Você não precisa fazer isso - git será abordado em um tutorial separado. Minha pasta pai do git contém muitas subpastas que podem usar pastas git separadas para controle de versão. Esta é uma captura de tela mostrando uma lista parcial de projetos:

![joomla file structure project folders](../../../en/images/getting-started/developer-file-structure-mac-project-folders.png)

Observe que alguns dos nomes das pastas começam com `j4xdemos`, que adotei para usar como a primeira parte do namespace utilizado para meus projetos criados com fins de tutoriais do Joomla 4. Não é necessário como parte do nome da pasta, mas é algo a se considerar: a primeira parte do seu namespace precisa ser algo único para você ou sua organização. Desde então, adotei `cefjdemos` como meu prefixo de namespace, pois é mais pessoal e não específico de uma versão do Joomla.

### Estrutura de Pastas do Projeto

Tomando o j4xdemos-com-mywalks como exemplo, todo o código que entrará na extensão está dentro da pasta com_mywalks. Quando esta é compactada, o arquivo com_mywalks.zip criado é usado para instalação no Joomla. Nenhum dos outros arquivos na raiz é incluído no arquivo zip, mas pode ser incluído no Repositório do GitHub. Por exemplo, README.md é um arquivo de texto em formato Markdown que contém uma breve descrição da extensão. O nome da pasta j4xdemos-com-mywalks não é significativo. Ele não é usado em nenhum outro lugar além de ordenar as pastas em ordem alfabética.

Na ilustração a seguir, a pasta j4xdemos-com-mywalks foi aberta no VSCodium para mostrar a estrutura do código do projeto. O arquivo mywalks.xml é um arquivo de manifesto que informa ao Joomla o que instalar e onde. As pastas admin e site contêm código que será colocado em administrator/components/com_mywalks e components/com_mywalks.

![Project folder open in vscodium](../../../en/images/getting-started/developer-file-structure-mac-vscodium.png)

Deveria ser óbvio que mesmo um componente pequeno precisa de uma quantidade considerável de pastas e arquivos. Existem ferramentas de modelo para criar rapidamente um componente básico. Elas são abordadas em outro lugar. A Fazer

Pronto para criar algum código?

*Traduzido por openai.com*

