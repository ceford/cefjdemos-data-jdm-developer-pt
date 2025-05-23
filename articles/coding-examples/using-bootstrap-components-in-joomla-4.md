<!-- Filename: J4.x:Using_Bootstrap_Components_in_Joomla_4 / Display title: Usando Componentes do Bootstrap no Joomla 4 -->

## Introdução

### Componentes do Bootstrap

Alguns dos componentes descritos na documentação do Bootstrap usam apenas CSS. Por exemplo, o componente Breadcrumbs é renderizado com CSS e não requer suporte para JavaScript. Outros respondem a ações do usuário, como clique ou passar o cursor, e precisam de suporte para JavaScript. Estes últimos são referidos aqui como Componentes Interativos. Este artigo explica como usá-los em Artigos e em um Módulo Personalizado.

Veja a [Documentação do Bootstrap](https://getbootstrap.com/docs/5.0/getting-started/introduction/)

### Joomla 4 Introduz uma Abordagem Modular para Componentes Interativos

- O que é uma abordagem modular?
- A funcionalidade é dividida em componentes individuais suportados por arquivos individuais. Não há uma abordagem de **um arquivo só** como era com o Bootstrap no Joomla 3. A abordagem modular é mais eficiente e oferece ganhos de desempenho (envie apenas o código necessário em vez de entregar tudo no caso de alguma página precisar de algum componente).

### Usando Componentes Interativos: Codificadores

- Carregue o que você precisa por caso! Existem funções auxiliares para configurar componentes individuais com argumentos apropriados.
- Veja a lista de Componentes Interativos do Bootstrap.

### Usando Componentes Interativos: Não Programadores

- Usar componentes em artigos não é tão fácil porque as funções auxiliares não podem ser chamadas de um artigo ou módulo HTML personalizado padrão. Três soluções possíveis são sugeridas mais adiante neste tutorial:
  - Um módulo personalizado
  - Um plugin personalizado
  - Uma substituição de módulo personalizado
- Pule ou escaneie a lista de Componentes Interativos do Bootstrap. Você não usará essas chamadas de função diretamente.

## Componentes Interativos do Bootstrap

### Alerta

Presumindo que você já tenha a parte HTML em seu layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.alert', '.selector');
```

- O **.selector** refere-se ao seletor CSS para o alerta. Você pode chamar esta função várias vezes com diferentes seletores CSS.
- Nenhuma opção extra disponível

### Botão

Supondo que você já tenha a parte HTML em seu Layout, você também precisará incluir a interatividade (a parte em JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.button', '.selector');
```

- O **.selector** refere-se ao seletor CSS para o botão. Você pode chamar esta função várias vezes com seletores CSS diferentes
- Nenhuma opção extra disponível

### Carrossel

Assumindo que você já tenha a parte HTML no seu Layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.carousel', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para o carrossel. Você pode chamar esta função várias vezes com diferentes seletores CSS
- O terceiro argumento refere-se às opções disponíveis para o carrossel

Opções para o carrossel podem ser:

- **interval**, número, padrão:**5000**, A quantidade de tempo para atrasar entre a rotação automática de um item. Se falso, o carrossel não ciclará automaticamente.
- **keyboard**, booleano, padrão:**true** Indica se o carrossel deve reagir a eventos de teclado.
- **pause**, string\|booleano, **hover** Pausa a rotação do carrossel ao passar o mouse e retoma a rotação ao sair com o mouse.
- **slide**, string\|booleano, padrão:**false** Reproduz automaticamente o carrossel após o usuário girar manualmente o primeiro item. Se "carousel", reproduz automaticamente o carrossel ao carregar.

### Recolher

Supondo que você já tenha a parte HTML no seu layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.collapse', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para o colapso. Você pode chamar esta função várias vezes com diferentes seletores CSS.
- O terceiro argumento refere-se às opções disponíveis para o colapso.

Opções para o colapso podem ser:

- **parent**, string, padrão:**false** Se um pai for fornecido, todos os elementos recolhíveis sob o pai especificado serão fechados quando este item recolhível for exibido.
- **toggle**, booleano padrão:**true** Alterna o elemento recolhível ao ser invocado.

### Menu Suspenso

Presumindo que você já tenha a parte HTML em seu Layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.dropdown', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para o dropdown. Você pode chamar esta função várias vezes com diferentes seletores CSS.
- O terceiro argumento refere-se às opções disponíveis para o dropdown.

Opções para o colapso podem ser:

- **flip**, booleano, padrão:**true** Permite que o Dropdown inverta em caso de sobreposição no elemento de referência.
- **boundary**, string, padrão:**scrollParent** Limite de restrição de transbordamento do menu suspenso.
- **reference**, string, padrão:**toggle** Elemento de referência do menu suspenso. Aceita **toggle** ou **parent**.
- **display**, string, padrão:**dynamic** Por padrão, usamos Popper para posicionamento dinâmico. Desative isso com **static**.

### Modal

Assumindo que você já tenha a parte HTML no seu Layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.modal', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para o modal. Você pode chamar esta função várias vezes com seletores CSS diferentes.
- O terceiro argumento refere-se às opções disponíveis para o modal.

Opções para o modal podem ser:

- **backdrop**, string\|boolean padrão:**true** Inclui um elemento modal-backdrop. Alternativamente, especifique static para um fundo que não feche o modal ao clicar.
- **keyboard**, boolean padrão:**true** Fecha o modal quando a tecla escape é pressionada.
- **focus**, boolean padrão:**true** Fecha o modal quando a tecla escape é pressionada.

### Fora do Canvas

Supondo que você já tenha a parte HTML no seu Layout, também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.offcanvas', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para o offcanvas. Você pode chamar esta função várias vezes com diferentes seletores CSS.
- O terceiro argumento refere-se às opções disponíveis para o offcanvas.

Opções para o offcanvas podem ser:

- **backdrop**, booleano, padrão:**true** Aplica um pano de fundo no corpo enquanto o offcanvas está aberto.
- **keyboard**, booleano, padrão:**true** Fecha o offcanvas quando a tecla de escape é pressionada.
- **scroll**, booleano, padrão:**false** Permite rolagem do corpo enquanto o offcanvas está aberto.

### Popover

Supondo que você já tenha a parte HTML no seu Layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.popover', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para o popover. Você pode chamar esta função várias vezes com diferentes seletores CSS.
- O terceiro argumento refere-se às opções disponíveis para o popover.

Opções para o popover podem ser:

- **animation**, booleano, padrão:**true** Aplica uma transição de desvanecimento CSS ao popover.
- **container**, string\|booleano, padrão:**false** Anexa o popover a um elemento específico. Ex.: **body**.
- **content**, string, padrão:**null** Valor de conteúdo padrão se o atributo data-bs-content não estiver presente.
- **delay**, número, padrão:**0** Atrasa o mostrar e ocultar do popover (ms) não se aplica ao tipo de disparo manual.
- **html**, booleano, padrão:**true** Insere HTML no popover. Se **false**, a propriedade innerText será usada para inserir conteúdo no DOM.
- **placement**, string, padrão:**right** Como posicionar o popover - **auto** \| **top** \| **bottom** \| **left** \| **right**. Quando auto é especificado, ele reorientará dinamicamente o popover.
- **selector**, string, padrão:**false** Se um seletor for fornecido, objetos popover serão delegados aos alvos especificados.
- **template**, string, padrão:**null** HTML base a ser usado ao criar o popover.
- **title**, string, padrão:**null** Valor de título padrão se a tag **title** não estiver presente.
- **trigger**, string, padrão:**click** Como o popover é disparado - **click** \| **hover** \| **focus** \| **manual**.
- **offset**, inteiro, padrão:**0** Deslocamento do popover em relação ao seu alvo.

### Scrollspy

Assumindo que você já tenha a parte HTML no seu Layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.scrollspy', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para o scrollspy. Você pode chamar esta função várias vezes com diferentes seletores CSS.
- O terceiro argumento refere-se às opções disponíveis para o scrollspy.

Opções para o Scrollspy podem ser:

- **offset** número de Pixels para deslocar do topo ao calcular a posição da rolagem.
- **method** string Descobre em qual seção o elemento espiado está.
- **target** string Especifica o elemento para aplicar o plugin Scrollspy.

### Aba

Supondo que você já tenha a parte HTML no seu Layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tab', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para a aba. Você pode chamar esta função várias vezes com diferentes seletores CSS.
- O terceiro argumento refere-se às opções disponíveis para a aba.

Opções para a Guia podem ser:

### Dica de Ferramenta

Supondo que você já tenha a parte HTML no seu Layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tooltip', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para a dica de ferramenta. Você pode chamar esta função várias vezes com seletores CSS diferentes.
- O terceiro argumento refere-se às opções disponíveis para a dica de ferramenta.

Opções para a dica de ferramenta podem ser:

- **animation**, boolean aplica uma transição de desvanecimento CSS ao popover.
- **container**, string\|boolean Anexa o popover a um elemento específico: { container: **body** }.
- **delay**, number\|object atraso para mostrar e ocultar o popover (ms) - não se aplica ao tipo de acionamento manual. Se um número for fornecido, o atraso é aplicado tanto para ocultar quanto para mostrar. A estrutura do objeto é: delay: { show: 500, hide: 100 }.
- **html**, boolean Insere HTML no popover. Se for falso, o método de texto do jQuery será usado para inserir o conteúdo no dom.
- **placement**, string\|function como posicionar o popover - **top** \| **bottom** \| **left** \| **right**.
- **selector** string Se um seletor for fornecido, os objetos popover serão delegados aos alvos especificados.
- **template**, string HTML base a ser usado ao criar o popover.
- **title**, string\|function valor padrão do título se a tag **title** não estiver presente.
- **trigger**, string como o popover é acionado - hover \| focus \| manual.
- **constraints**, array Um array de restrições - passado para o Popper.
- **offset**, string Deslocamento do popover em relação ao seu alvo.

### Torrada

Supondo que você já tenha a parte HTML no seu Layout, você também precisará incluir a interatividade (a parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.toast', '.selector', []);
```

- O **.selector** refere-se ao seletor CSS para o toast. Você pode chamar esta função várias vezes com diferentes seletores CSS.
- O terceiro argumento refere-se às opções disponíveis para o toast.

Opções para a torrada podem ser:

- **animation**, booleano, padrão:**true** Aplica uma transição fade CSS ao toast.
- **autohide**, booleano, padrão:**true** Ocultar automaticamente o toast.
- **delay**, número, padrão:**5000** Atraso para ocultar o toast (ms).

### Veja Também

- **Acordeão** usa Collapse para exibir painéis de dados.
- **Grupo de Lista** pode ser combinado com Tab para exibir conteúdo em abas.

## Usando Componentes do Bootstrap em Artigos

A marcação HTML para a maioria dos componentes pode ser incluída em um artigo ou em um módulo que pode, por sua vez, ser incluído em um artigo. O problema é que a chamada do HTMLHelper para configurar o suporte JavaScript não pode ser incluída ali. Existem várias abordagens possíveis para esse problema. Três abordagens são sugeridas aqui, usando um Módulo personalizado, usando um Plugin ou usando uma sobreposição de Template.

**Cuidado:** Os editores TinyMCE e JCE removem os espaços em branco ao salvar e dificultam a edição de código! A solução simples é ir para o canto superior direito da tela do Administrador e selecionar **Menu do Usuário → Editar Conta** e definir o Editor para Code Mirror.

## Abordagem 1: Usando um Módulo Personalizado

Este é provavelmente o método menos propenso a erros, pois as opções de suporte do componente Bootstrap são selecionadas com caixas de seleção. As etapas envolvidas são as seguintes:

- Baixe, instale e ative este [Custom Module](https://github.com/ceford/j4xdemos-mod-custom-bscompos/raw/master/mod_custom_bscompos.zip)
- No menu do Administrador, vá para **Conteúdo**→** Módulos do Site → Novo**
- Selecione **Custom BS Components**
- Insira um Título
- Altere o Editor para o modo de texto simples e cole ou digite o código HTML do componente que você deseja usar.
- Na aba Opções, role para baixo até a lista de BS Components e selecione o tipo de componente nesta instância do módulo. Note que você pode selecionar mais de um se estiver usando mais de um componente.
- Selecione uma Posição do módulo: ou
  - uma posição definida pelo template se você quiser usar o módulo em um local específico ou
  - digite uma posição se desejar usar o módulo dentro de um artigo específico: no artigo digite {loadposition whatever}
- Salve e vá para o site para Testar!

### Seletores

Para alguns componentes, a ação do JavaScript é desencadeada por uma **classe** específica no código HTML. Em outros componentes, a ação é desencadeada por um atributo **data-bs-whatever**. A seguir estão os gatilhos atuais e podem mudar:

- **Alerta** acionado por class="alert ..."
- **Botão** acionado por data-bs-toggle="button"
- **Carrossel** acionado por data-bs-ride="whatever"
- **Colapso** acionado por data-bs-toggle="collapse"
- **Dropdown** acionado por data-bs-toggle="dropdown"
- **Modal** acionado por data-bs-toggle="modal"
- **Offcanvas** acionado por data-bs-toggle="offcanvas"
- **Popover** acionado por class="btn ..." ou
    - tag (poderia ser alterado para class="haspopover ...") E
    - data-bs-toggle="popover"
- **Scrollspy** acionado por data-bs-spy="scroll"
- **Aba** acionada por data-bs-toggle="tab"
- **Toast** acionado por class="toast ..."
- **Tooltip** acionado por class="btn ..." ou
    - tag (poderia ser alterado para class="hastooltip ...") E
    - data-bs-toggle="tooltip"

### Exemplo 1: Alerta

Os alertas podem ser usados em código HTML sem suporte a JavaScript. Isso é necessário apenas para a funcionalidade de fechar. Exemplo de código HTML:

```html
<div class="alert alert-warning alert-dismissible fade show" role="alert">
  <strong>Holy guacamole!</strong> You should check in on some of those fields below.
  <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
</div>
```

Exemplo de resultado ao incluir um módulo em um artigo:

![Bootstrap alert](../../../en/images/coding-examples/coding-examples-alert.png)

Note que, sem suporte a JavaScript, o alerta aparecerá exatamente como acima, mas um clique no botão de fechar \[X\] não irá dispensar o alerta. Além disso, o alerta aparecerá a cada carregamento de página.

### Exemplo 2: Botões

Botões podem ser usados no código HTML sem suporte a JavaScript. Isso é necessário apenas para a mudança sutil de estilo aplicada a botões com uma mudança de estado, estilizado ativo. Exemplo de código Bootstrap:

```html
<p><button type="button" class="btn btn-primary" data-bs-toggle="button" autocomplete="off">Toggle button</button>
<button type="button" class="btn btn-primary active" data-bs-toggle="button" autocomplete="off" aria-pressed="true">Active toggle button</button>
<button type="button" class="btn btn-primary" disabled data-bs-toggle="button" autocomplete="off">Disabled toggle button</button></p>
```

```html
<p><a href="#" class="btn btn-primary" role="button" data-bs-toggle="button">Toggle link</a>
<a href="#" class="btn btn-primary active" role="button" data-bs-toggle="button" aria-pressed="true">Active toggle link</a>
<a href="#" class="btn btn-primary disabled" tabindex="-1" aria-disabled="true" role="button" data-bs-toggle="button">Disabled toggle link</a></p>
```

Com este estilo no modelo user.css:

```css
    .btn.btn-primary.active {
        background-color: green;
    }
```

![Bootstrap buttons](../../../en/images/coding-examples/coding-examples-buttons.png)

Os botões alternam entre azul e verde.

### Exemplo 3: Carrossel

O Carrossel oferece uma apresentação de slides que passa por uma série de imagens ou painéis de texto. O exemplo a seguir usou imagens do Joomla 4 Sample. Código do Bootstrap:

```html
<div id="carouselExampleCaptions" class="carousel slide" data-bs-ride="carousel">
    <div class="carousel-indicators">
        <button class="active" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="0" aria-current="true" aria-label="Slide 1"></button>
        <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="1" aria-label="Slide 2"></button>
        <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="2" aria-label="Slide 3"></button>
    </div>
    <div class="carousel-inner">
        <div class="carousel-item active"><img class="d-block w-100" src="images/sampledata/cassiopeia/nasa1-1200.jpg" alt="..." />
            <div class="carousel-caption d-none d-md-block">
                <h5>First slide label</h5>
                <p>Some representative placeholder content for the first slide.</p>
            </div>
        </div>
        <div class="carousel-item"><img class="d-block w-100" src="images/sampledata/cassiopeia/nasa2-1200.jpg" alt="..." />
            <div class="carousel-caption d-none d-md-block">
                <h5>Second slide label</h5>
                <p>Some representative placeholder content for the second slide.</p>
            </div>
        </div>
        <div class="carousel-item"><img class="d-block w-100" src="images/sampledata/cassiopeia/nasa3-1200.jpg" alt="..." />
            <div class="carousel-caption d-none d-md-block">
                <h5>Third slide label</h5>
                <p>Some representative placeholder content for the third slide.</p>
            </div>
        </div>
    </div>
    <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="prev">
        <span class="visually-hidden">Previous</span>
    </button>
    <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="next">
        <span class="visually-hidden">Next</span>
    </button>
</div>
```

Resultado:

![Bootstrap carousel](../../../en/images/coding-examples/coding-examples-carousel.jpg)

### Exemplo 4: Colapso

Colapso é amplamente utilizado no Joomla e você pode não precisar usar um módulo ou plugin para acionar a ação. O clique abre um painel com informações extras. Exemplo de código Bootstrap:

```html
<p>
    <a class="btn btn-primary" role="button" href="#collapseExample" data-bs-toggle="collapse" aria-expanded="false" aria-controls="collapseExample"> Link with href </a>
    <button class="btn btn-primary" type="button" data-bs-toggle="collapse" data-bs-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">
        Button with data-bs-target
    </button>
</p>
<div id="collapseExample" class="collapse">
    <div class="card card-body">
        Some placeholder content for the collapse component. This panel is hidden by default but revealed when the user activates the relevant trigger.
    </div>
</div>
```

Resultado:

![Bootstrap collapse](../../../en/images/coding-examples/coding-examples-collapse.png)

### Exemplo 5: Menu Suspenso

Os menus suspensos são sobreposições contextuais alternáveis para exibir listas de links e mais. Código de exemplo do Bootstrap:

```html
<div class="btn-group">
    <button class="btn btn-danger dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false"> Action </button>
    <ul class="dropdown-menu">
        <li><a class="dropdown-item" href="#">Action</a></li>
        <li><a class="dropdown-item" href="#">Another action</a></li>
        <li><a class="dropdown-item" href="#">Something else here</a></li>
        <li><hr class="dropdown-divider" /></li>
        <li><a class="dropdown-item" href="#">Separated link</a></li>
    </ul>
</div>
```

Resultado:

![Bootstrap dropdown](../../../en/images/coding-examples/coding-examples-dropdown.png)

### Exemplo 6: Modal

O componente Modal abre uma caixa de diálogo no meio da tela. Há várias opções para controlar o tamanho e o conteúdo do modal. Consulte a documentação do Bootstrap para mais detalhes. Exemplo de código do Bootstrap:

```html
<p><button class="btn btn-primary" type="button" data-bs-toggle="modal" data-bs-target="#exampleModal"> Launch demo modal </button></p>
<div id="exampleModal" class="modal fade" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 id="exampleModalLabel" class="modal-title">Modal title</h5>
                <button class="btn-close" type="button" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                ...
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" type="button" data-bs-dismiss="modal">Close</button>
                <button class="btn btn-primary" type="button">Save changes</button>
            </div>
        </div>
    </div>
</div>
```

Resultado:

![Bootstrap modal](../../../en/images/coding-examples/coding-examples-modal.png)

### Exemplo 7: Offcanvas

No momento, este componente não é suportado no Joomla. Fique atento - em breve!

### Exemplo 8: Popover

Os Popovers são como Tooltips, mas com um Título. Eles têm alguns problemas de acessibilidade e desempenho, portanto devem ser usados com cautela. Código de exemplo do Bootstrap:

```html
<p><button class="btn btn-lg btn-danger" title="Popover title" type="button" data-bs-toggle="popover" data-bs-content="And here's some amazing content. It's very engaging. Right?">Click to toggle popover</button></p>
```

Resultado:

![Bootstrap alert](../../../en/images/coding-examples/coding-examples-popover.png)

### Exemplo 9: Scrollspy

Exemplo de código:

```html
<div class="row">
    <div class="col-4">
        <nav id="navbar-example3" class="navbar navbar-light bg-light flex-column">
            <a class="navbar-brand" href="#">Navbar</a><nav class="nav nav-pills flex-column">
            <a class="nav-link active" href="#item-1">Item 1</a>
            <nav class="nav nav-pills flex-column">
                <a class="nav-link ms-3 my-1" href="#item-1-1">Item 1-1</a>
                <a class="nav-link ms-3 my-1" href="#item-1-2">Item 1-2</a>
            </nav>
            <a class="nav-link" href="#item-2">Item 2</a>
            <a class="nav-link" href="#item-3">Item 3</a>
            <nav class="nav nav-pills flex-column">
                <a class="nav-link ms-3 my-1" href="#item-3-1">Item 3-1</a>
                <a class="nav-link ms-3 my-1" href="#item-3-2">Item 3-2</a>
            </nav>
        </nav>
    </div>
    <div class="col-8">
        <div class="scrollspy-example" tabindex="0" data-bs-spy="scroll" data-bs-target="#navbar-example3" data-bs-offset="0">
            <h4 id="item-1">Item 1</h4>
            <p>Placeholder content for the scrollspy example. This one relates to item 1. Takes you miles high, so high, 'cause she’s got that one international smile. There's a stranger in my bed, there's a pounding in my head. Oh, no. In another life I would make you stay. ‘Cause I, I’m capable of anything. Suiting up for my crowning battle. Used to steal your parents' liquor and climb to the roof. Tone, tan fit and ready, turn it up cause its gettin' heavy. Her love is like a drug. I guess that I forgot I had a choice.</p>
            <h5 id="item-1-1">Item 1-1</h5>
            <p>Placeholder content for the scrollspy example. This one relates to the item 1-1. You got the finest architecture. Passport stamps, she's cosmopolitan. Fine, fresh, fierce, we got it on lock. Never planned that one day I'd be losing you. She eats your heart out. Your kiss is cosmic, every move is magic. I mean the ones, I mean like she's the one. Greetings loved ones let's take a journey. Just own the night like the 4th of July! But you'd rather get wasted.</p>
            <h5 id="item-1-2">Item 1-2</h5>
            <p>Placeholder content for the scrollspy example. This one relates to the item 1-2. Her love is like a drug. All my girls vintage Chanel baby. Got a motel and built a fort out of sheets. 'Cause she's the muse and the artist. (This is how we do) So you wanna play with magic. So just be sure before you give it all to me. I'm walking, I'm walking on air (tonight). Skip the talk, heard it all, time to walk the walk. Catch her if you can. Stinging like a bee I earned my stripes.</p>
            <h4 id="item-2">Item 2</h4>
            <p>Placeholder content for the scrollspy example. This one relates to item 2. Don't need apologies. There is no fear now, let go and just be free, I will love you unconditionally. Last Friday night. Don't be a shy kinda guy I'll bet it's beautiful. Summer after high school when we first met. 'Cause she's the muse and the artist. What? Wait. No, no, no, no. Thought that I was the exception.</p>
            <h4 id="item-3">Item 3</h4>
            <p>Placeholder content for the scrollspy example. This one relates to item 3. Word on the street, you got somethin' to show me, me. All this money can't buy me a time machine. Make it like your birthday everyday. So we hit the boulevard. You make me feel like I'm livin' a teenage dream, the way you turn me on Skip the talk, heard it all, time to walk the walk. Word on the street, you got somethin' to show me, me. It's no big deal, it's no big deal, it's no big deal.</p>
            <h5 id="item-3-1">Item 3-1</h5>
            <p>Placeholder content for the scrollspy example. This one relates to item 3-1. Baby do you dare to do this? This is no big deal. Yeah, you're lucky if you're on her plane. Just own the night like the 4th of July! Standing on the frontline when the bombs start to fall. So just be sure before you give it all to me.</p>
            <h5 id="item-3-2">Item 3-2</h5>
            <p>Placeholder content for the scrollspy example. This one relates to item 3-2. You're original, cannot be replaced. All night they're playing, your song. California girls we're undeniable. Like a bird without a cage. There is no fear now, let go and just be free, I will love you unconditionally. I can see the writing on the wall. You could travel the world but nothing comes close to the golden coast.</p>
        </div>
    </div>
</div>
```

Resultado:

![Bootstrap scrollspy](../../../en/images/coding-examples/coding-examples-scrollspy.png)

Além disso, é necessário algum estilo em user.css:

```css
    .scrollspy-example {
        height: 350px;
        overflow-y: scroll;
    }
```

Espreitar: o menu não se coordena bem com o conteúdo neste exemplo!

### Exemplo 10: Aba

As abas são frequentemente usadas como elementos de navegação combinados com menus suspensos. Código de exemplo Bootstrap:

```html
<ul class="nav nav-tabs">
    <li class="nav-item"><a class="nav-link active" href="#" aria-current="page">Active</a></li>
    <li class="nav-item dropdown"><a class="nav-link dropdown-toggle" role="button" href="#" data-bs-toggle="dropdown" aria-expanded="false">Dropdown</a>
        <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Action</a></li>
            <li><a class="dropdown-item" href="#">Another action</a></li>
            <li><a class="dropdown-item" href="#">Something else here</a></li>
            <li><hr class="dropdown-divider" /></li>
            <li><a class="dropdown-item" href="#">Separated link</a></li>
        </ul>
    </li>
    <li class="nav-item"><a class="nav-link" href="#">Link</a></li>
    <li class="nav-item"><a class="nav-link disabled" tabindex="-1" href="#" aria-disabled="true">Disabled</a></li>
</ul>
```

Resultado:

![Bootstrap tab](../../../en/images/coding-examples/coding-examples-tab.png)

Lembre-se de verificar as opções de Aba e Dropdown para que a parte do menu suspenso funcione.

### Exemplo 11: Brinde

Os toasts são notificações leves projetadas para imitar as notificações push que foram popularizadas por sistemas operacionais móveis e de desktop. Elas são construídas com flexbox, portanto são fáceis de alinhar e posicionar. Código de exemplo Bootstrap:

```html
<div class="toast fade show" role="alert" aria-live="assertive" aria-atomic="true">
    <div class="toast-header">
        <img class="rounded me-2" src="..." alt="..." />
        <strong class="me-auto">Bootstrap</strong> <small>11 mins ago</small>
        <button class="btn-close" type="button" data-bs-dismiss="toast" aria-label="Close"></button>
    </div>
    <div class="toast-body">Hello, world! This is a toast message.</div>
</div>
```

Resultado:

![Bootstrap toast](../../../en/images/coding-examples/coding-examples-toast.png)

Observe que a demonstração do Bootstrap que usa um botão para mostrar a mensagem Toast precisa de algum JavaScript extra. Parece que este componente precisa de um programador para ser bem utilizado!

### Exemplo 12: Dica de Ferramenta

Uma dica de ferramenta é um pequeno pedaço de texto que aparece ao passar o cursor sobre um botão ou link para explicar o que é ou o que faz. A dica de ferramenta pode ser posicionada acima, abaixo, à esquerda ou à direita do elemento. Se não especificado, a posição padrão é no topo. A dica de ferramenta mudará para outra posição se não houver espaço suficiente na posição especificada. Código de exemplo do Bootstrap:

```html
<p><button class="btn btn-secondary" title="Tooltip on left" type="button" data-bs-toggle="tooltip" data-bs-placement="left"> Tooltip on left </button>
<button class="btn btn-secondary" title="Tooltip" type="button" data-bs-toggle="tooltip"> Tooltip </button>
<button class="btn btn-secondary" title="Tooltip on top" type="button" data-bs-toggle="tooltip" data-bs-placement="top"> Tooltip on top </button>
<button class="btn btn-secondary" title="Tooltip on right" type="button" data-bs-toggle="tooltip" data-bs-placement="right"> Tooltip on right </button>
<button class="btn btn-secondary" title="Tooltip on bottom" type="button" data-bs-toggle="tooltip" data-bs-placement="bottom"> Tooltip on bottom </button>
<button class="btn btn-secondary" title="<em>Tooltip</em> <u>with</u> <b>HTML</b>" type="button" data-bs-toggle="tooltip" data-bs-html="true"> Tooltip with HTML </button></p>
<p>Tooltip triggered by class: <button class="btn btn-warning" title="Tooltip Message">Alert!</button></p>
```

Resultado:

![Bootstrap tooltip](../../../en/images/coding-examples/coding-examples-tooltip.png)

## Abordagem 2: Usando um Plugin de Conteúdo

Os passos envolvidos:

- Baixe, instale e ative este [plugin](https://github.com/ceford/j4xdemos-plg-bscompos/raw/master/plg_j4xdemos_bscompos.zip)
- No artigo, adicione o texto sobre o qual o plugin atua, por exemplo, {bscompos modal carousel} acionará o carregamento do JavaScript necessário para suportar um diálogo modal e um carrossel. O plugin remove o texto de disparo e as tags vazias (agora) envolventes.
- Inclua o código HTML do Componente Bootstrap diretamente no artigo ou em um módulo incluído no artigo. Há um exemplo de código HTML abaixo para um Modal simples e um Modal contendo um Carrossel. Note que isso não funcionará se o código HTML estiver em um módulo em uma localização de template.
- Isso também funcionará para um módulo Custom padrão se a Opção Preparar Conteúdo estiver definida como Sim.
- Teste!

## Abordagem 3: Usando uma Substituição de Modelo

Os passos envolvidos:

- Crie uma substituição de template para mod_custom.
- Adicione um módulo mod_custom contendo a marcação do componente e classes de gatilho.
- Inclua o módulo em um artigo.

### A substituição de modelo mod_custom

- Na interface do Administrador, vá para **Sistema → Modelos de Site → Detalhes e Arquivos do Cassiopeia**.
- Selecione **Criar Substituições** → **mod_custom** → **default.php**.
- Na linha após defined('\_JEXEC') or die; adicione o seguinte código:

```php
    $module_class = $params->get('moduleclass_sfx');
    if (!empty($module_class))
    {
        $classes = explode(' ', $module_class);
        foreach ($classes as $class)
        {
        switch ($class)
            {
              case 'bs-alert':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.alert', '.alert');
                break;
              case 'bs-button':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.button', '.btn');
                break;
              case 'bs-carousel':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.carousel', '.selector', []);
                break;
              case 'bs-collapse':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.collapse', '.selector', []);
                break;
              case 'bs-dropdown':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.dropdown', '.selector', []);
                break;
              case 'bs-modal':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.modal', '.selector', []);
                break;
              case 'bs-offcanvas':
                // Not Found
                //\Joomla\CMS\HTML\HTMLHelper::_('bootstrap.offcanvas', '.btn', []);
                break;
              case 'bs-popover':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.popover', '.btn', []);
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.popover', 'a', []);
                break;
              case 'bs-scrollspy':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.scrollspy', '.selector', []);
                break;
              case 'bs-tab':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tab', '.selector', []);
                break;
              case 'bs-tooltip':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tooltip', '.btn', []);
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tooltip', 'a', []);
                break;
              case 'bs-toast':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.toast', '.selector', []);
                break;
              default:
                // do nothing
            }
        }
    }
```

Este código busca nomes de classes definidos em mod_custom e faz a chamada do HTMLHelper para configurar o suporte ao JavaScript. Note que o último item em cada chamada é um seletor que pode ou não ser usado para acionar a ação. Muitos dos componentes são acionados por atributos de dados no mark-up e não usam os seletores aqui. Para alguns, o seletor é necessário. Por exemplo, faz sentido usar a classe **.btn** e a tag **a** para acionar Tooltips.

### Um Módulo mod_custom para um Componente Modal

- Vá para **Conteúdo**→**Módulos do Site**→**Novo**.
- Selecione o módulo **Personalizado**.
- Preencha o formulário:
  - Título: Demo Modal
  - No campo Posição, digite **demomodal** para uso em um artigo;
  - Conteúdo do Módulo: Alterne o Editor para entrada de texto simples.
  - Cole o seguinte código da documentação do Bootstrap:

```html
<h2>Modal</h2>
<!-- Button trigger modal -->
<p><button class="btn btn-primary" type="button" data-bs-toggle="modal" data-bs-target="#exampleModal"> Launch demo modal </button></p>
<!-- Modal -->
<div id="exampleModal" class="modal fade" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 id="exampleModalLabel" class="modal-title">Modal title</h5>
                <button class="btn-close" type="button" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                ...
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" type="button" data-bs-dismiss="modal">Close</button>
                <button class="btn btn-primary" type="button">Save changes</button>
            </div>
        </div>
    </div>
</div>
```

- Selecione a guia Avançado e no campo Classe do Módulo, insira **bs-modal**
- Opcional: defina Título como Ocultar para usar o H2 no código colado.
- Salve e Feche (não se preocupe se o modal parecer errado no editor).

### Criar um Artigo e Item de Menu

- Crie um novo artigo, Demo Modal, e no modo de entrada de texto simples defina o conteúdo para

```html
<div>{loadposition demomodal}</div>
```

- Criar um item de menu de Artigo Único.
- Teste:

![Bootstrap modal module in article](../../../en/images/coding-examples/coding-examples-modal-module.png)

### Um Componente Modal Contendo um Carrossel

- Crie um novo módulo Custom com um novo título: Demo Modal Carousel
- Posição: demomodalcarousel
- **Aba Avançada** → **Classe do Módulo**: bs-modal bs-carousel
- Conteúdo personalizado do módulo em texto simples:

```html
<h2>Modal with Carousel</h2>
<div class="mod-custom custom">
    <!-- Button trigger modal -->
    <button class="btn btn-primary" type="button" data-bs-toggle="modal" data-bs-target="#exampleModal"> Launch demo modal </button>
</div>
<div id="exampleModal" class="modal fade" style="display: none;" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <button class="close" type="button" data-bs-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">×</span>
                </button>
            </div>
            <div class="modal-body">
                <div id="carouselExampleCaptions" class="carousel slide" data-bs-ride="carousel">
                    <div class="carousel-indicators">
                        <button class="active" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="0" aria-current="true" aria-label="Slide 1"></button>
                        <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="1" aria-label="Slide 2"></button>
                        <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="2" aria-label="Slide 3"></button>
                    </div>
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img class="d-block w-100" src="images/sampledata/cassiopeia/nasa1-1200.jpg" alt="..." />
                            <div class="carousel-caption d-none d-md-block">
                                <h5>First slide label</h5>
                                <p>Some representative placeholder content for the first slide.</p>
                            </div>
                        </div>
                        <div class="carousel-item">
                            <img class="d-block w-100" src="images/sampledata/cassiopeia/nasa2-1200.jpg" alt="..." />
                            <div class="carousel-caption d-none d-md-block">
                                <h5>Second slide label</h5>
                                <p>Some representative placeholder content for the second slide.</p>
                            </div>
                        </div>
                        <div class="carousel-item">
                            <img class="d-block w-100" src="images/sampledata/cassiopeia/nasa3-1200.jpg" alt="..." />
                            <div class="carousel-caption d-none d-md-block">
                                <h5>Third slide label</h5>
                                <p>Some representative placeholder content for the third slide.</p>
                            </div>
                        </div>
                    </div>
                    <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="prev">
                        <span class="visually-hidden">Previous</span>
                    </button>
                    <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="next">
                        <span class="visually-hidden">Next</span>
                    </button>
                </div>
            </div>
        </div>
    </div>
</div>
```

- Crie um novo Artigo com {loadposition demomodalcarousel} no conteúdo.
- Crie um novo item de menu de artigo único: Demo Modal Carousel
- Teste:

![Bootstrap modal carousel](../../../en/images/coding-examples/coding-examples-modal-carousel.png)

*Traduzido por openai.com*
