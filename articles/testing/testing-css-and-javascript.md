<!-- Filename: J4.x:SCSS_and_Sass / Display title: Testando CSS e JavaScript -->

## Introdução

Em um site Joomla de produção, o Joomla entrega arquivos CSS e Javascript comprimidos (aqueles com `.min` no nome do arquivo). Os servidores enviarão as versões em gzip se elas estiverem disponíveis (aquelas que terminam com o sufixo `.gz`). Esses arquivos são criados a partir de fontes não comprimidas. No caso dos arquivos CSS, eles são frequentemente criados ao processar precursores SCSS. Para testar código que inclui CSS ou JavaScript novos ou atualizados, é necessário reconstruir os arquivos CSS e as versões comprimidas e minificadas a partir das fontes alteradas.

## Teste de Instalação

Para fins de teste, você precisa de um servidor de teste que tenha Git, Node.js e Composer instalados. Vá para o repositório [Joomla CMS](https://github.com/joomla/joomla-cms) no GitHub e siga as instruções em *Como obter uma instalação funcional a partir do código fonte* perto do final do texto README.

Após a conclusão da instalação do Joomla, não exclua o Diretório de Instalação! Isso também excluirá o diretório `build` que é necessário para reconstruir os arquivos CSS e JavaScript.

Os arquivos principais `.scss` estão nos seguintes diretórios:

- mídia/modelos/site/cassiopeia/scss
- mídia/modelos/administrador/atum/scss

O script de geração CSS, o compilador SCSS e outras ferramentas de build similares estão localizados no diretório `build/`. O diretório de build está disponível apenas a partir da fonte do Joomlaǃ, não está incluído em uma versão oficial do Joomlaǃ.

As instruções de instalação incluem o seguinte:

```sh
git checkout 5.2-dev (or whatever branch you wish to work with)
composer install
npm ci
```

O comando `npm ci` é um sinônimo para `npm clean-install` usado em qualquer situação em que você queira garantir que está realizando uma instalação limpa de suas dependências.

## Uso diário

Existem comandos alternativos para uso em situações em que apenas os arquivos SCSS ou JavaScript foram alterados:

```sh
npm run build:css¶
    This command compiles SCSS files to CSS and also creates the minified files.

npm run build:js¶
    This command compiles and transpiles the JavaScript files to the correct format and creates minified files.
```

Os comandos vasculham os diretórios de mídia e modelos e constroem as versões finais dos arquivos necessárias para uma instalação do Joomla.

## Sass, SCSS e CSS

> Sass é uma linguagem de folhas de estilo que é compilada para CSS. Ela permite que você use variáveis, regras aninhadas, mixins, funções e mais, tudo com uma sintaxe totalmente compatível com CSS. Sass ajuda a manter grandes folhas de estilo bem organizadas e facilita o compartilhamento de design dentro e entre projetos. Os arquivos Sass têm o sufixo `scss`.

### CSS

O código CSS é expresso da seguinte formaː

```css
#header {
    margin: 0;
    border: 1px solid blue;
}
#header p {
    font-size: 14px;
    color: blue;
}
#header a {
    text-decoration: none;
}
```

### SCSS

`SCSS` é uma extensão da sintaxe do CSS. É usado no núcleo do Joomlaǃ

```css
$color:    blue;
#header {
    margin: 0;
    border: 1px solid $color;
    p {
        color: $colorRed;
        font: {
            size: 14px;
        }
    }
    a {
        text-decoration: none;
    }
}
```

Uma sintaxe mais antiga do `Sass` oferece uma maneira mais concisa de escrever CSS.

```css
$color:    blue
#header
    margin: 0
    border: 1px solid $color
        p
            color: $colorRed
            font:
                size: 14px
        a
            text-decoration: none
```

Você pode encontrar mais informações na [Documentação do Sass](http://sass-lang.com/documentation/syntax/).

## De CSS existente para SCSS

Se você quiser personalizar o modelo Cassiopeia, é uma boa ideia copiar o modelo e personalizá-lo depois para que as atualizações do Joomla! não sobreponham suas personalizações. Para adicionar seus próprios arquivos CSS a uma cópia do modelo Cassiopeia, basta renomear seus arquivos `.css` para `.scss`. Você pode então aproveitar os recursos que o SCSS tem a oferecer:

- Extensões de linguagem, como variáveis, aninhamento e mixins
- Muitas funções úteis para manipular cores e outros valores
- Recursos avançados, como diretivas de controle para bibliotecas
- Saída bem formatada e personalizável

Veja o [site do Sass](https://sass-lang.com/) para mais detalhes.

### Importe seus arquivos .css como arquivos .scss

Supondo que você queira incluir seus arquivos personalizados e que eles sejam analisados pelo compilador SCSS - você NÃO precisa reescrever seu .css para SCSS porque `.css` simples também funciona. O que você precisa fazer:

- renomeie seus arquivos `.css` para `.scss`
- prefixe-os com um `_`
- adicione uma declaração `@import` na parte inferior de `media/templates/site/copy_of_cassiopeia/scss/template.scss` para que ela substitua as declarações existentes:

```css
// Bootstrap functions
@import "../../../media/vendor/bootstrap/scss/functions";
//...
// 50 or more lines of import statements
// Finally add the cassiopeia colours
:root {
  @each $color, $value in $cassiopeia-colors {
    --#{$color}: #{$value};
  }
// More lines containing scss color statements, then your own styles:
@import "mystyles";
}
```

Se agora você compilar seu arquivo main template.scss, você acabará com um único main template.css otimizado e minificado. Você também reduziu suas requisições http e o site deve carregar mais rápido.

*Traduzido por openai.com*

