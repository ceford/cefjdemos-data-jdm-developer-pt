<!-- Filename: https://docs.joomla.org/Package / Display title: Pacotes -->

## Introdução aos Pacotes

Às vezes, um módulo (ou plugin ou outra extensão) utiliza os modelos ou auxiliares de um componente. Nessas ocasiões, é melhor poder instalar ou desinstalar um módulo dependente quando o próprio componente é instalado ou desinstalado. No Joomla, essa funcionalidade é alcançada com um pacote, embora o uso de pacotes não seja infalível.

Um pacote é uma extensão que é usada para instalar várias extensões de uma só vez. Combiná-las em um pacote permite que o usuário instale e desinstale duas ou mais extensões em uma única operação.

## Criação de Pacote

Um pacote é criado ao compactar todos os arquivos `.zip` individuais da extensão juntamente com um arquivo de manifesto `.xml`. Por exemplo, para um pacote composto de:

* **componente** helloworld
* **módulo** helloworld
* **biblioteca** helloworld
* **plugin de sistema** helloworld
* **modelo** helloworld

O pacote teria a seguinte árvore no arquivo zip:

```sh
  -- pkg_helloworld.xml
  -- packages <dir>
      |-- com_helloworld.zip
      |-- mod_helloworld.zip
      |-- lib_helloworld.zip
      |-- plg_sys_helloworld.zip
      |-- tpl_helloworld.zip
  -- pkg_script.php
```

O `pkg_helloworld.xml` poderia ter o seguinte conteúdo:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<extension type="package" method="upgrade">
<name>Hello World Package</name>
<author>Hello World Package Team</author>
<creationDate>May 2022</creationDate>
<packagename>helloworld</packagename>
<version>1.0.0</version>
<url>http://www.yoururl.com/</url>
<packager>Hello World Package Team</packager>
<packagerurl>http://www.yoururl.com/</packagerurl>
<description>Example package to combine multiple extensions</description>
<update>http://www.updateurl.com/update</update>
<scriptfile>pkg_script.php</scriptfile>
<blockChildUninstall>true</blockChildUninstall>
<files folder="packages">
    <file type="component" id="com_helloworld">com_helloworld.zip</file>
    <file type="module" id="helloworld" client="site">mod_helloworld.zip</file>
    <file type="library" id="helloworld">lib_helloworld.zip</file>
    <file type="plugin" id="helloworld" group="system">plg_sys_helloworld.zip</file>
    <file type="template" id="helloworld" client="site">tpl_helloworld.zip</file>
</files>
</extension>
```

Quando compactado e instalado, o pacote será visível na lista de extensões, permitindo que um usuário desinstale todas as extensões contidas no pacote.

Lembre-se de usar o desinstalador de pacotes em vez dos desinstaladores de subpacotes individuais para evitar entradas órfãs de extensões no gerenciador de extensões. Esta é a parte que não é totalmente segura!

### ID do arquivo

O elemento id na tag `<file ..>` **não** é arbitrário! O `id=` deve ser configurado para o valor da coluna `element` na tabela `#__extensions`. Se não estiverem configurados corretamente, ao desinstalar o pacote, o arquivo filho **não** será encontrado e desinstalado.

### Nome do Arquivo de Manifesto e Nome do Pacote

O nome do arquivo de manifesto e a capacidade de desinstalar o próprio arquivo do pacote estão intimamente relacionados. O arquivo de manifesto deve ter um prefixo **pkg_**. O restante do nome do manifesto (sem a extensão **.xml**) deve ser usado como `<packagename>`. Ou, de outra forma, um pacote que você deseja identificar como **blurpblurp_J3** recebe isso como seu `<packagename>` e deve estar em um arquivo de manifesto nomeado **pkg_blurpblurp_J3.xml**. Caso contrário, será impossível desinstalar o próprio pacote.

Um opcional `<pkg_script.php>` que contém uma classe `pkg_<packagename>InstallerScript` com a função pública **postflight** pode ser usado.

### Tag de Extensão

A tag `<extension>` deve incluir `method="upgrade"` para que uma atualização de pacote seja bem-sucedida em instalações subsequentes.

### Desinstalação de Dependência de Extensão

Uma extensão de pacote pode declarar que seus elementos filhos não podem ser desinstalados de forma independente com um elemento `<blockChildUninstall>true</blockChildUninstall>` no manifesto do pacote. Se o seu pacote precisar de todas as suas extensões para operar de forma eficaz, defina isso como true ou 1.

*Traduzido por openai.com*

