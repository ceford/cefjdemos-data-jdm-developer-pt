<!-- Filename: Joomla_CodeSniffer / Display title: Padrões de Codificação -->

<div class="alert alert-warning">
A última parte deste artigo precisa ser atualizada!
</div>

## Uma Visão Geral da IA

Os padrões de codificação são importantes para o desenvolvimento de software porque eles:

- **Melhorar a qualidade do código**
  - Os padrões de codificação ajudam a garantir que o código seja confiável, seguro e protegido. Eles também podem ajudar a reduzir problemas de desempenho e preocupações de segurança que podem surgir de práticas de codificação inadequadas.
- **Tornar o código mais legível e fácil de manter**
  - Os padrões de codificação ajudam a tornar o código mais fácil de entender, ler e manter. Isso também pode facilitar o trabalho de novos desenvolvedores com o código.
- **Acelerar o desenvolvimento**
  - Os padrões de codificação podem ajudar os desenvolvedores a evitar erros comuns que podem atrasar os processos de codificação.
- **Melhorar a colaboração**
  - Os padrões de codificação podem ajudar a facilitar a colaboração entre desenvolvedores, mesmo em grandes equipes.
- **Garantir consistência**
  - Os padrões de codificação ajudam a garantir que o código seja consistente entre os projetos. Isso pode tornar mais fácil para os desenvolvedores trabalharem juntos nos mesmos projetos.
- **Melhorar a escalabilidade**
  - Os padrões de codificação podem ajudar a garantir que o código possa escalar sem se tornar incontrolável.
- **Fornecer critérios claros para revisões de código**
  - Os padrões de codificação podem ajudar a fornecer critérios claros para revisões de código, o que pode levar a um feedback mais eficaz.

Os padrões de codificação geralmente incluem regras para indentação, comprimento da linha, colocação de chaves e espaçamento.

Joomla usa o padrão de codificação [PSR-12](https://www.php-fig.org/psr/psr-12/). Você pode habilitar esse padrão de codificação em seu IDE e obter dicas se não estiver seguindo o padrão de codificação ou usar uma correção automática também. Recomendamos que você siga esse padrão ao desenvolver suas próprias extensões para manter a compatibilidade com o núcleo e garantir que seu código, com sorte, funcione com versões futuras.

## PHP Code Sniffer

Por favor, consulte o [PHP_CodeSniffer](https://github.com/PHPCSStandards/PHP_CodeSniffer/) atual para obter informações sobre esta utilidade e como instalá-la. Esteja ciente de que a fonte original está abandonada, mas pode ser listada pelos motores de busca. Existem dois scripts:

- **phpcs** detecta violações de um padrão de codificação e produz um relatório.
- **phpcbf** tenta corrigir violações de padrões de codificação e produz um relatório sobre o que foi feito.

Você pode instalar os scripts individuais ou usar o Composer para instalá-los. Você também pode encontrá-los em um clone do Joomla localizado em libraries/vendor/bin, junto com algumas outras utilidades úteis.

## Testando o PHP Code Sniffer

Se você colocar uma instalação global no seu `$PATH`, poderá executar o analisador de código a partir da linha de comando na raiz de um projeto. Tente isto para exibir uma lista de padrões de codificação:

```sh
phpcs -i
The installed coding standards are MySource, PEAR, PSR1, PSR2, PSR12, Squiz and Zend
```

Como exemplo, o seguinte comando foi usado em uma pasta de projeto mais antiga que utilizava o antigo padrão de codificação personalizado do Joomla. Entre outras coisas, ele usava tabulações em vez de espaços para layout. Muitas linhas semelhantes foram omitidas abaixo para brevidade.

```sh
phpcs --standard=PSR12 .

FILE: /Users/ceford/git/j4xdemos-plg-toc/j4xdemostoc/j4xdemostoc.php
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
FOUND 132 ERRORS AND 3 WARNINGS AFFECTING 116 LINES
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   1 | WARNING | [ ] A file should declare new symbols (classes, functions, constants, etc.) and cause no other side effects, or it should execute logic with side effects, but should not do both. The
     |         |     first symbol is defined on line 22 and the first side effect is on line 10.
   1 | ERROR   | [x] Header blocks must be separated by a single blank line
  22 | ERROR   | [ ] Each class must be in a namespace of at least one level (a top-level vendor name)
  24 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
  25 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
  26 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
  ...
  42 | ERROR   | [x] Expected 1 space after closing parenthesis; found newline
...
  48 | ERROR   | [x] No space found after comma in argument list
  48 | ERROR   | [x] Expected 1 space after closing parenthesis; found newline
...
  67 | ERROR   | [x] Expected 0 spaces before closing parenthesis; 1 found
...
  75 | ERROR   | [x] Space after opening parenthesis of function call prohibited
  75 | ERROR   | [x] Expected 0 spaces before closing parenthesis; 1 found
...
 138 | WARNING | [ ] Line exceeds 120 characters; contains 168 characters
 139 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
 139 | WARNING | [ ] Line exceeds 120 characters; contains 141 characters
...
 156 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
 157 | ERROR   | [x] Expected 1 newline at end of file; 0 found
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
PHPCBF CAN FIX THE 131 MARKED SNIFF VIOLATIONS AUTOMATICALLY
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Time: 123ms; Memory: 8MB
```

O exemplo de projeto anterior continha um único arquivo php e nenhum arquivo css ou js. O phpcs produz um relatório para cada arquivo php, css e js em um projeto. Aqui estão alguns exemplos para arquivos css e js:

```sh
FILE: /Users/ceford/git/j4x-demos-com-mediacat/com_mediacat/media/css/mediacat.css
----------------------------------------------------------------------------------
FOUND 33 ERRORS AFFECTING 32 LINES
----------------------------------------------------------------------------------
  3 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
...
 51 | ERROR | [x] Whitespace found at end of line
...
 79 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
----------------------------------------------------------------------------------
PHPCBF CAN FIX THE 33 MARKED SNIFF VIOLATIONS AUTOMATICALLY
----------------------------------------------------------------------------------

FILE: /Users/ceford/git/j4x-demos-com-mediacat/com_mediacat/media/css/file-icon-classic.min.css
-----------------------------------------------------------------------------------------------
FOUND 0 ERRORS AND 1 WARNING AFFECTING 1 LINE
-----------------------------------------------------------------------------------------------
 1 | WARNING | File appears to be minified and cannot be processed
-----------------------------------------------------------------------------------------------

FILE: /Users/ceford/git/j4x-demos-com-mediacat/com_mediacat/media/js/mediacat-site.js
-------------------------------------------------------------------------------------
FOUND 38 ERRORS AFFECTING 30 LINES
-------------------------------------------------------------------------------------
  3 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
  5 | ERROR | [x] Expected 1 space after FUNCTION keyword; 0 found
  6 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
...
 13 | ERROR | [x] Opening brace should be on a new line
...
 29 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
 29 | ERROR | [x] Expected at least 1 space before "+"; 0 found
 29 | ERROR | [x] Expected at least 1 space after "+"; 0 found
...
 36 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
-------------------------------------------------------------------------------------
PHPCBF CAN FIX THE 38 MARKED SNIFF VIOLATIONS AUTOMATICALLY
-------------------------------------------------------------------------------------
```

## Variações de Comando

Você pode obter ajuda com comandos phpcs:

```sh
phpcs --help
```

### Excluir um ou mais arquivos

Use uma lista de padrões de arquivos separados por vírgula para excluir arquivos da validação de estilo de código. Exemplo

```php
phpcs --standard=PSR12 --ignore='libraries/*' .
```

### Excluir uma ou mais regras

Joomla permite linhas mais longas do que o padrão PSR, 560 em vez de 120. O seguinte comando pode ser usado para omitir os avisos de linhas longas:

```sh
phpcs --standard=PSR12 --ignore='libraries/*' --exclude=Generic.Files.LineLength .
```

Você pode encontrar a regra que está sendo violada com este comando:

```sh
phpcs -s yourfile.php
```

### Exceções do Joomla

Para o desenvolvimento de uma extensão usando um IDE, você pode decidir usar o padrão PSR12 sem quaisquer exceções. O Joomla possui um [conjunto de regras personalizado](https://github.com/joomla/joomla-cms/blob/5.2-dev/ruleset.xml) que permite muitas exceções. Ele é usado para a validação de toda a instalação do Joomla durante os testes do sistema.

## Corrigindo Violações

O único arquivo php que `FOUND 132 ERRORS AND 3 WARNINGS AFFECTING 116 LINES` mostrado acima pode ser principalmente corrigido da seguinte forma:

```sh
phpcbf --standard=PSR12 .

PHPCBF RESULT SUMMARY
-----------------------------------------------------------------------------------
FILE                                                               FIXED  REMAINING
-----------------------------------------------------------------------------------
/Users/ceford/git/j4xdemos-plg-toc/j4xdemostoc/j4xdemostoc.php     131    4
-----------------------------------------------------------------------------------
A TOTAL OF 131 ERRORS WERE FIXED IN 1 FILE
-----------------------------------------------------------------------------------

Time: 232ms; Memory: 8MB
```

Executar novamente a ferramenta phpcs mostra quais problemas permanecem:

```sh
phpcs --standard=PSR12 .

FILE: /Users/ceford/git/j4xdemos-plg-toc/j4xdemostoc/j4xdemostoc.php
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
FOUND 1 ERROR AND 3 WARNINGS AFFECTING 4 LINES
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   1 | WARNING | A file should declare new symbols (classes, functions, constants, etc.) and cause no other side effects, or it should execute logic with side effects, but should not do both. The first
     |         | symbol is defined on line 23 and the first side effect is on line 11.
  23 | ERROR   | Each class must be in a namespace of at least one level (a top-level vendor name)
 132 | WARNING | Line exceeds 120 characters; contains 168 characters
 133 | WARNING | Line exceeds 120 characters; contains 141 characters
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Time: 127ms; Memory: 8MB
```

Conclusão: uma extensão codificada para uma versão anterior do Joomla e usando um padrão de codificação diferente agora precisa de algum trabalho!

## Instalação em IDEs

A maioria dos Ambientes de Desenvolvimento Integrado pode usar o verificador de código enquanto você trabalha ou quando salva um arquivo.

### Instalação no VSCode

No VSCode (e/ou VScodium), selecione o ícone Extensões, procure por PHP_CodeSniffer e instale-o. Ele precisa de configuração:

1. Em **Configurações**, encontre PHP_CodeSniffer
2. Defina o campo **PHP Code Sniffer → Exec:** para corresponder à localização do seu binário phpcs.
3. Na lista **PHP Code Sniffer: Standard**, selecione **PSR12**.

Feche e você está pronto para a ação.

Alguns dos problemas mostrados acima podem ser corrigidos com diretrizes PSR1.

```php
<?php

/**
 * @package     Whatever
 *
 * @phpcs:disable PSR1.Classes.ClassDeclaration.MissingNamespace
 */

use joomla\CMS\...

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects
```

Outros precisam de alguma reflexão!

Após a instalação no VSCode, violações de estilo de código serão detectadas e marcadas com um sublinhado ondulado vermelho. Passe o cursor sobre o problema para ver uma mensagem e uma solução potencial, como neste exemplo:

```txt
Header blocks must be separated by a single blank line
PHP_CodeSniffer(PSR12.Files.FileHeader.SpacingAfterBlock)
```

<div class="alert alert-warning">
As seguintes seções precisam ser atualizadas!
</div>

### Instalação no PhpStorm

O Code Sniffer é suportado nativamente no PhpStorm. Vá para Configurações e, em **Editor → Inspeções**, você verá a lista de sniffers que você instalou.

#### Definir Caminho para o Code Sniffer

1. Abra Configurações (CTRL-ALT-S / CMD-,)
2. Vá para Idiomas & Frameworks
3. Clique em PHP
4. Clique em Ferramentas de Qualidade
5. Clique na seta suspensa do PHP cs fixer
6. A configuração está definida como Local por padrão
7. Clique nos 3 pontos atrás para abrir a tela de configuração
8. A primeira opção é o caminho do PHP Code Sniffer (phpcs)
9. Clique nos 3 pontos atrás do caminho para selecionar o local do arquivo phpcs. Veja acima onde o phpcs pode estar instalado no seu site
10. Clique em Validar para garantir que o caminho está correto e que o phpcs está funcionando
11. Clique em OK

#### Ativando o Estilo de Código

1. Abrir Configurações (CTRL-ALT-S / CMD-,)
2. Ir para Editor
3. Clicar em Inspeções
4. Na lista, ir para PHP
5. Clicar em Validação do PHP Code Sniffer
6. Clicar na caixa de seleção atrás dela para ativá-la
7. Clicar no botão Recarregar (2 setas) para forçar o recarregamento das regras do disco
8. Joomla deve agora estar disponível na lista. Veja a imagem a seguir.
9. Clicar em OK

![CodeSniffer in PHPStorm](../../../en/images/getting-started/core-phpstorm-code-sniffer.png)

### Instalação no Netbeans

O Netbeans tem a funcionalidade de sniffer integrada no sistema central.

1. Inicie seu IDE Netbeans
2. Abra **Ferramentas → Opções → PHP → Análise de Código → Code Sniffer**
3. Você deve definir o caminho para *phpcs.bat* do pacote PEAR PHP_CodeSniffer instalado
   - Para sistemas baseados em Unix, o caminho é algo como /usr/bin/phpcs
   - No XAMPP (Windows) você pode encontrar o arquivo na pasta raiz do PHP (por exemplo, C:\xampp\php\phpcs.bat)
4. Como "Padrão Padrão", escolha "Joomla" para usar o padrão Joomla!
5. Agora você pode clicar em *OK* para começar a analisar
6. Abra no menu superior **Fonte → Inspecionar...**
7. Aproveite

### Instalação no Eclipse

1. **Ajuda → Instalar Novo Software...**
2. **Trabalhar com** Preencha um dos URLs do site de atualização.
3. Selecione as ferramentas desejadas.
4. Reinicie o Eclipse.
5. **Janela → Preferências**
6. **Ferramentas PHP → PHP CodeSniffer**

![Eclipse PTI settings](../../../en/images/getting-started/core-eclipse-pti-settings.png)

Agora você pode verificar violações de código contra padrões comuns.

![Codesniffer in Eclipse](../../../en/images/getting-started/core-eclipse-pti.png)

### Instalação no Geany

- Abra um arquivo PHP. (Caso contrário, o menu de construção não ficará acessível.)
- No menu superior, selecione **Construir → Definir Comandos de Construção**.
- Selecione o segundo campo e nomeie como desejar. Insira este código no Comando:<br>
  `phpcs --standard=Joomla "%f" | sed -e 's/^/%f |/' | egrep 'WARNING|ERROR'`
- Insira este código no campo Expressão Regular de Erro: `(.+) [|]\s+([0-9]+)`
- Selecione OK.
- Se a Janela de Mensagens não estiver aberta, exiba-a selecionando no menu superior Visualizar.
- Ao visualizar qualquer arquivo PHP, pressione F9 para ver os erros encontrados.

### Instalação no Atom

- Instale o phpcs e os padrões do Joomla conforme descrito acima.
- Em **Atom → Preferences → Install** instale **linter-phpcs** e todos os seus requisitos.
- Em **Atom → Preferences → Packages → linter-phpcs → Settings** ajuste
  - **Executable Path** para o caminho do seu phpcs
  - **Code Standard Or Config File**: PSR12
  - **Tab Width**: 4

*Traduzido por openai.com*
