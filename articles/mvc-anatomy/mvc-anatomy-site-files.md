<!-- Filename: J4.x:MVC_Anatomy:_Site_Files / Display title: Anatomia MVC: Arquivos do Site -->

## Estrutura de Arquivos

Há menos arquivos na parte do Site do componente do que na parte do Administrador, então parece um bom lugar para começar. Somente as partes de cada arquivo que necessitam de explicação serão abordadas. É melhor abrir cada arquivo mencionado, dar uma olhada no conteúdo geral e depois encontrar as partes explicadas. A ordem alfabética da estrutura dos arquivos é a seguinte:

```bash
    site
    |- forms
        |- filter_countries.xml
    |- language
        |- en-GB
           |- com_countrybase.ini
    |- src
        |- Controller
           |- DisplayController
        |- Model
           |- CountriesModel.php
        |- Service
           |- Router.php
        |- View
           |- Countries
              |- HtmlView.php
    |- tmpl
        |- countries
           |- default.php
           |- default.xml
```

## DisplayController.php

```php
<?php

/**
 * @package     Countrybase.Site
 * @subpackage  com_countrybase
 *
 * @copyright   (C) 2025 Clifford E Ford
 * @license     GNU General Public License version 3 or later; see LICENSE.txt
 */

namespace Cefjdemos\Component\Countrybase\Site\Controller;

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects

use Joomla\CMS\MVC\Controller\BaseController;
use Joomla\CMS\Router\Route;
use Joomla\CMS\Session\Session;

/**
 * Countrybase Component Controller
 *
 * @since  1.0.0
 */
class DisplayController extends BaseController
{
    /**
     * The default view.
     *
     * @var    string
     */
    protected $default_view = 'countries';
}
```

Partes deste arquivo são explicadas da seguinte forma:

### Aviso de Direitos Autorais

Cada arquivo php deve começar com um aviso de direitos autorais como o seguinte:

```php
<?php

/**
 * @package     Countrybase.Site
 * @subpackage  com_countrybase
 *
 * @copyright   (C) 2025 Clifford E Ford
 * @license     GNU General Public License version 3 or later; see LICENSE.txt
 */
```

Se você frequentemente cria novos arquivos e copia/cola esta seção, lembre-se de atualizar o nome do componente e o aviso de direitos autorais. Além disso, o sniffer de código exige uma linha em branco antes de um bloco de documentação.

### Namespace e verificação definida

Após o aviso de direitos autorais, todo arquivo php deve ter uma linha contendo defined('_JEXEC') ou die; exceto que arquivos com namespace devem declarar o namespace antes de qualquer outro código php, então antes da verificação definida. Arquivos php com namespace são aqueles que contêm classes php de componentes na pasta src ou suas subpastas.

```php
namespace Cefjemos\Component\Countrybase\Site\Controller;

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects
```

O check `defined` impede que um arquivo PHP seja executado chamando-o diretamente através de sua URL. A constante `_JEXEC` é definida quando a aplicação é iniciada via o arquivo index.php da raiz ou do administrador. É uma importante ajuda de segurança.

O controle `defined` é envolvido em `phpcs:disable` e `phpcs:enable` para permitir uma violação do padrão de codificação PSR12.

Combinado com o namespace declarado no arquivo de manifesto countrybase.xml, o Joomla procurará qualquer classe declarada no arquivo atual em root/components/com_countrybase/src/Controller - neste caso, anexando o nome deste arquivo, DisplayController.php.

### declarações use

As declarações de uso geralmente seguem a verificação definida e muitas vezes são listadas em ordem alfabética. As declarações de uso definem os locais das classes utilizadas por este arquivo PHP. Às vezes, as declarações de uso estão lá por engano, sendo declaradas, mas não usadas. Isso não causa dano, mas deve ser corrigido. Há duas declarações não utilizadas aqui:

```php
    use Joomla\CMS\Router\Route;
    use Joomla\CMS\Session\Session;
```

### Classe Controladora

O controlador de exibição tem quase nada a fazer, já que todo o trabalho é realizado na classe pai. A única coisa importante que ele faz é definir a visão padrão, neste caso, **countries**. Isso fará com que a visão padrão do componente utilize os arquivos Countries/HtmlView.php e tmpl/countries/default.php para exibir os dados dos países.

```php
/**
 * Countrybase Component Controller
 *
 * @since  1.0.0 Created for first release.
 */
class DisplayController extends BaseController
{
    /**
     * The default view.
     *
     * @var    string
     */
    protected $default_view = 'countries';
}
```

O bloco de documentação (DocBlock) que precede a declaração de `class` é usado para documentação automática com ferramentas como o *Doxygen*. A declaração `@since` é uma *tag* que indica o número da versão da extensão onde este elemento foi introduzido. Ela pode ser seguida por uma explicação em texto simples. Qualquer elemento pode ter um DocBlock com qualquer número de tags padrão. É uma boa prática manter seu próprio código bem documentado!

Não se esqueça de definir o \$default_view para este controlador. Sem isso, o DisplayController usará a visualização padrão definida no arquivo de configuração do componente ou, se isso não existir, o nome do componente.

## src/View/Countries/HtmlView.php

O controlador definiu a visualização padrão para **countries**, então o próximo passo é carregar o código correspondente do HtmlView.php. Partes deste arquivo exigem alguma explicação.

### Variáveis de classe

```php
class HtmlView extends BaseHtmlView
{
    /**
     * The model state
     *
     * @var  \Joomla\CMS\Object\CMSObject
     */
    protected $state = null;
    ...
    protected $items = null;
    ...
    protected $pagination = null;
    ...
    public $filterForm;
    ...
    public $activeFilters;
```

As variáveis de classe são usadas para armazenar informações sobre a página a ser exibida:

- `$state` - o estado do modelo, frequentemente inicializado por formulário ou entrada de string de consulta.
- `$items` - a lista de dados de países recuperados do banco de dados.
- `$pagination` - um objeto usado para exibir um mecanismo de navegação de página se houver mais páginas do que o limite da lista, normalmente 20 itens.
- `$filterForm` - geralmente não encontrado nas páginas do site, mas usado em com_countrybase para filtrar por nome do país ou estado publicado.
- `$activeFilters` - usado para manter o controle de quais filtros estão em uso.

### função de exibição

Este é um padrão bastante comum para a visualização de um site, exceto pelas partes filterForm e activeFilters:

```php
    public function display($tpl = null)
    {
        $this->state      = $this->get('State');
        $this->items      = $this->get('Items');
        $this->pagination = $this->get('Pagination');
        $this->filterForm    = $this->get('FilterForm');
        $this->activeFilters = $this->get('ActiveFilters');

        // Flag indicates to not add limitstart=0 to URL
        $this->pagination->hideEmptyLimitstart = true;

        // Check for errors.
        if (count($errors = $this->get('Errors')))
        {
            throw new GenericDataException(implode("\n", $errors), 500);
        }

        parent::display($tpl);
    }
```

As instruções da forma `$this->get('Xxxx')` fazem com que o Joomla procure em `CountriesModel.php` uma função chamada `getXxxx()` e retorne qualquer dado produzido por esse código para armazenamento e uso na visualização. Frequentemente, a função está no pai de CountriesModel. Por exemplo, a função getItems não está presente em CountriesModel.php, mas está presente em ListModel, que ele estende.

Em resumo, a classe de visualização recupera dados do modelo e, em seguida, chama sua classe pai para exibir os dados.

## Model/CountriesModel.php

Existem um pequeno número de funções no Modelo que você geralmente precisa completar por conta própria. Outras são herdadas do ListModel pai.

### __construct

É prática comum incluir no construtor quaisquer campos de filtro que você possa desejar usar. Sem eles, os filtros podem parecer não ter efeito. Eles são frequentemente esquecidos quando você deseja adicionar um filtro algum tempo depois. Cada campo é dado como seu nome de campo com um alias de nome de tabela, geralmente a, b, c e assim por diante, mas pode ser qualquer coisa que você escolha que seja consistente com o código em outros lugares.

```php
       public function __construct($config = array())
        {
            if (empty($config['filter_fields']))
            {
                $config['filter_fields'] = array(
                        'id', 'a.id',
                        'title', 'a.title',
                        'iso_2', 'a.iso_2',
                        'iso_3', 'a.iso_3',
                        'country_code', 'a.country_code',
                        'region_code', 'a.region_code',
                        'state', 'a.state',
                        'subregion_code', 'a.subregion_code',
                        'phone_prefix', 'a.phone_prefix',
                        'currency_code', 'a.currency_code',
                );
            }

            parent::__construct($config);
        }
```

### populateState

Esta função recebe parâmetros de entrada e os prepara para uso em uma consulta de banco de dados. Alguns parâmetros são manipulados no principal, então não há necessidade de fazer nada aqui. Por exemplo, se o campo de pesquisa for **título**, ele é manipulado pelo principal, assim como os campos **estado** e de paginação **início** e **limite**.

```php
       protected function populateState($ordering = 'title', $direction = 'ASC')
        {
            // List state information.
            parent::populateState($ordering, $direction);
        }
```

### obterIdLoja

Esta função cria um hash para armazenar uma consulta para uso em outro lugar.

```php
       protected function getStoreId($id = '')
        {
            // Compile the store id.
            $id .= ':' . $this->getState('filter.search');
            $id .= ':' . $this->getState('filter.published');

            return parent::getStoreId($id);
        }
```

### getListQuery

É aqui que a consulta é criada para extrair dados do banco de dados. Isso requer algum entendimento de como as consultas são construídas.

```php
    protected function getListQuery()
    {
        // Create a new query object.
        $db = $this->getDatabase();
        $query = $db->getQuery(true);

        // Select the required fields from the table.
        $query->select(
            $this->getState(
                'list.select',
                [
                    $db->quoteName('a.title'),
                    $db->quoteName('a.iso_2'),
                    $db->quoteName('a.iso_3'),
                    $db->quoteName('a.country_code'),
                    $db->quoteName('a.region_code'),
                    $db->quoteName('a.subregion_code'),
                    $db->quoteName('a.phone_prefix'),
                    $db->quoteName('a.currency_code'),
                    $db->quoteName('a.state'),
                    $db->quoteName('b.title') . ' AS currency_title',
                    $db->quoteName('b.symbol'),
                    $db->quoteName('b.dollar_exchange_rate'),
                ]
            )
        )
            ->from($db->quoteName('#__countrybase_countries', 'a'))
            ->leftjoin($db->quoteName('#__countrybase_currencies', 'b') . 'ON a.currency_code = b.currency_code');

        // Filter by search in title.
        $search = $this->getState('filter.search');

        if (!empty($search)) {
            $search = '%' . str_replace(' ', '%', trim($search) . '%');
            $query->where($db->quoteName('a.title') . ' LIKE :search')
            ->bind(':search', $search, ParameterType::STRING);
        }

        // Filter by published state
        $published = (string) $this->getState('filter.published');

        if ($published !== '*') {
            if (is_numeric($published)) {
                $state = (int) $published;
                $query->where($db->quoteName('a.state') . ' = :state')
                    ->bind(':state', $state, ParameterType::INTEGER);
            }
        }

        // Add the list ordering clause.
        $orderCol = $this->state->get('list.ordering', 'a.title');
        $orderDirn = $this->state->get('list.direction', 'ASC');

        $query->order($db->escape($orderCol) . ' ' . $db->escape($orderDirn));
        return $query;
    }
```

Explicação

- **getQuery(true)** obtém um novo objeto de consulta vazio.
- **\$query-\>select()** adiciona uma instrução SELECT. Pode haver várias instruções SELECT - o Joomla as concatena.
- **aliases de tabela a e b** observe que algumas colunas vêm de tabelas diferentes.
- **-\>from()** define qual tabela é a tabela a. isso pode estar em uma declaração separada: \$query-\>from();
- **-\>leftjoin()** define a tabela b e como ela deve ser unida à tabela a.
- **\$query-\>where()** faz uso de quaisquer filtros definidos, um para **search** e outro para **state**.
- **return \$query** não há chamada pai, tudo na consulta deve ser configurado aqui.

## tmpl/países/default.php

Esta é a parte do código onde o conteúdo HTML é criado. Para a lista de países, é necessário uma tabela com uma linha de cabeçalho e uma linha para dados de cada país. Como há 250 países, um mecanismo de paginação é necessário para exibir um subconjunto de países alguns de cada vez. Isso requer um formulário. E, neste caso, uma barra padrão **searchtools** do Joomla é útil. Aqui está:

```php
<?php

/**
 * @package     Countrybase.Site
 * @subpackage  com_countrybase
 *
 * @copyright   (C) 2025 Clifford E Ford
 * @license     GNU General Public License version 3 or later; see LICENSE.txt
 */

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects

use Joomla\CMS\HTML\HTMLHelper;
use Joomla\CMS\Language\Text;
use Joomla\CMS\Layout\LayoutHelper;
use Joomla\CMS\Router\Route;

$listOrder = $this->escape($this->state->get('list.ordering'));
$listDirn  = $this->escape($this->state->get('list.direction'));

?>
<h1><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES'); ?></h1>

<form action="<?php echo Route::_('index.php?option=com_countrybase'); ?>"
    method="post" name="adminForm" id="adminForm">

<?php echo LayoutHelper::render('joomla.searchtools.default', array('view' => $this)); ?>

<div class="table-responsive">
    <table class="table table-striped">
    <caption><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_TABLE_CAPTION'); ?></caption>
    <thead>
    <tr>
        <th scope="col">
            <?php echo HTMLHelper::_(
                'searchtools.sort',
                'COM_COUNTRYBASE_COUNTRIES_COUNTRY',
                'a.title',
                $listDirn,
                $listOrder
            ); ?>
        </th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_ISO_2'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_ISO_3'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_CURRENCY_TITLE'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_CURRENCY_SYMBOL'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_CURRENCY_CODE'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_XRATE'); ?></th>
    </tr>
    </thead>
    <tbody>
    <?php foreach ($this->items as $id => $item) : ?>
    <tr>
        <td><?php echo $item->title; ?></td>
        <td><?php echo $item->iso_2; ?></td>
        <td><?php echo $item->iso_3; ?></td>
        <td><?php echo $item->currency_title; ?></td>
        <td><?php echo $item->symbol; ?></td>
        <td><?php echo $item->currency_code; ?></td>
        <td><?php echo $item->dollar_exchange_rate; ?></td>
    </tr>
    <?php endforeach; ?>
    </tbody>
    </table>
</div>

<?php echo $this->pagination->getListFooter(); ?>

<input type="hidden" name="task" value="">
<input type="hidden" name="boxchecked" value="0">
<?php echo HTMLHelper::_('form.token'); ?>

</form>
```

Pontos a observar:

- **\$listOrder** e **\$listDirection** são usados para ordenar por cabeçalho de coluna. Apenas o título foi configurado para fazer isso.
- **form action** é tipicamente configurado para se referir a si mesmo.
- **LayoutHelper::render('joomla.searchtools.default',...)** cria uma barra de busca do tipo visto nas páginas de lista do administrador. **Precisa de um formulário de filtro!**
- **\$this-\>pagination-\>getListFooter()** busca o código HTML para o widget de paginação.
- **task** este campo oculto é preenchido por JavaScript quando o formulário é enviado.
- **boxchecked** este campo oculto é usado quando uma ou mais caixas de seleção de linha são marcadas para operação em lote. Não é realmente necessário aqui!
- **HTMLHelper::\_('form.token');** obtém o código para um token de formulário usado como dispositivo de segurança para envios de formulário que envolvem envio de dados.

## tmpl/countries/default.xml

Este arquivo é utilizado para criar um item de menu. Ele tem o mesmo nome que o arquivo php, portanto, default.xml neste caso.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<metadata>
    <layout title="COM_COUNTRYBASE_VIEW_DEFAULT_MENU_LABEL"
        option="COM_COUNTRYBASE_VIEW_DEFAULT_OPTION">
        <help
            url="components/com_countrybase/help/en-GB/countrybase.html"
        />
        <message>
            <![CDATA[COM_COUNTRYBASE_VIEW_DEFAULT_MENU_DESC]]>
        </message>
    </layout>

    <!-- Add fields to the parameters object for the layout. -->
    <fields name="params">

        <!-- Options -->
        <fieldset name="options">
        </fieldset>

    </fields>
</metadata>
```

Notas:

- **ajuda url** aponta para um arquivo de ajuda na pasta do administrador. Permite criar seus próprios arquivos de ajuda locais, acionados a partir do botão de ajuda no formulário de edição do menu após selecionar o tipo de menu Countrybase Default View.
- **parâmetros** permitem o uso de parâmetros, por exemplo, se deve ou não mostrar uma coluna específica na lista de países. Nenhum parâmetro foi especificado ainda.
- As traduções da **chave** precisam estar no arquivo administrator/language/en-GB/countrybase.sys.ini. A chave *COM_COUNTRYBASE_VIEW_DEFAULT_MENU_DESC*, traduzida para *Mostra uma página de Países.*, aparece como uma descrição no formulário de seleção do Tipo de Item de Menu.

## forms/filter_countries.xml

Este arquivo é necessário para a barra de pesquisa. Sem ele, o Joomla exibirá um erro fatal. O nome do arquivo deve ser exatamente como mostrado: o nome da visualização precedido por filter\_. O conteúdo é simples, apenas definições para o campo de pesquisa e quaisquer outros filtros que você deseje usar.

```xml
<?xml version="1.0" encoding="utf-8"?>
<form>
    <fields name="filter">
        <field
            name="search"
            type="text"
            label="COM_COUNTRYBASE_COUNTRIES_FILTER_SEARCH_LABEL"
            description="COM_COUNTRYBASE_COUNTRIES_FILTER_SEARCH_DESC"
            hint="JSEARCH_FILTER"
        />

        <field
            name="published"
            type="status"
            label="JOPTION_SELECT_PUBLISHED"
            onchange="this.form.submit();"
            >
            <option value="">JOPTION_SELECT_PUBLISHED</option>
        </field>

    </fields>

    <fields name="list">
        <field
            name="fullordering"
            type="list"
            label="JGLOBAL_SORT_BY"
            default="a.title ASC"
            onchange="this.form.submit();"
            >
            <option value="">JGLOBAL_SORT_BY</option>
            <option value="a.title ASC">COM_COUNTRYBASE_COUNTRIES_FILTER_COUNTRY_ASC</option>
            <option value="a.title DESC">COM_COUNTRYBASE_COUNTRIES_FILTER_COUNTRY_DESC</option>
            <option value="a.iso_2 ASC">ISO2 ASC</option>
            <option value="a.iso_2 DESC">ISO2 DESC</option>
            <option value="a.iso_3 ASC">ISO3 ASC</option>
            <option value="a.iso_3 DESC">ISO3 DESC</option>
            <option value="a.currency_code ASC">COM_COUNTRYBASE_COUNTRIES_FILTER_CURRENCY_CODE_ASC</option>
            <option value="a.currency_code DESC">COM_COUNTRYBASE_COUNTRIES_FILTER_CURRENCY_CODE_DESC</option>
            <option value="a.id ASC">JGRID_HEADING_ID_ASC</option>
            <option value="a.id DESC">JGRID_HEADING_ID_DESC</option>
        </field>

        <field
            name="limit"
            type="limitbox"
            label="JGLOBAL_LIST_LIMIT"
            default="25"
            onchange="this.form.submit();"
        />
    </fields>
</form>
```

Observe que qualquer chave de string começando com J é definida pelo Joomla e você não deve incluí-las nos seus arquivos de idioma.

## language/pt-BR/com_countrybase.ini

Joomla sempre carrega traduções de chave de idioma em inglês antes de qualquer outro idioma. Isso garante que as chaves não apareçam na saída se um idioma estiver incompletamente traduzido. Como as chaves de idioma são palavras longas em pseudo-inglês, é considerado melhor ter uma mistura de inglês e outro idioma do que uma mistura de chaves e outro idioma. Se outro idioma estiver em uso, o Joomla sobrescreve as strings em inglês com as daquele outro idioma.

Observe que é prática comum listar as strings em ordem alfabética de chaves:

```ini
    ; Joomla! Project
    ; (C) 2005 Open Source Matters, Inc. https://www.joomla.org
    ; License GNU General Public License version 2 or later; see LICENSE.txt
    ; Note : All ini files need to be saved as UTF-8

    COM_COUNTRYBASE_COUNTRIES_COUNTRY="Country"
    COM_COUNTRYBASE_COUNTRIES_CURRENCY_CODE="Code"
    COM_COUNTRYBASE_COUNTRIES_CURRENCY_SYMBOL="Symbol"
    COM_COUNTRYBASE_COUNTRIES_CURRENCY_TITLE="Currency"
    COM_COUNTRYBASE_COUNTRIES_FILTER_COUNTRY_ASC="Country ASC"
    COM_COUNTRYBASE_COUNTRIES_FILTER_COUNTRY_DESC="Country DESC"
    COM_COUNTRYBASE_COUNTRIES_FILTER_CURRENCY_CODE_ASC="Currency code ASC"
    COM_COUNTRYBASE_COUNTRIES_FILTER_CURRENCY_CODE_DESC="Currency code DESC"
    COM_COUNTRYBASE_COUNTRIES_FILTER_SEARCH_DESC="Search in Country Name"
    COM_COUNTRYBASE_COUNTRIES_FILTER_SEARCH_LABEL="Search"
    COM_COUNTRYBASE_COUNTRIES_ISO_2="ISO2"
    COM_COUNTRYBASE_COUNTRIES_ISO_3="ISO3"
    COM_COUNTRYBASE_COUNTRIES_TABLE_CAPTION="Table of Country Currencies"
    COM_COUNTRYBASE_COUNTRIES_XRATE="Exchange Rate"
    COM_COUNTRYBASE_COUNTRIES="Countries"
```

## src/Service/Router.php

O Roteador é necessário para URLs de SEO. Sem ele, um link de menu pode aparecer como option=com_countrybase&view=countries. Com ele, um link aparecerá como country-base.html ou qualquer nome que você escolha para o alias do título do link.

```php
    public function __construct(
        SiteApplication $app,
        AbstractMenu $menu
    ) {

        $countries = new RouterViewConfiguration('countries');
        $countries->setKey('id');
        $this->registerView($countries);

        parent::__construct($app, $menu);

        $this->attachRule(new MenuRules($this));
        $this->attachRule(new StandardRules($this));
        $this->attachRule(new NomenuRules($this));
    }
```

Se houver mais visualizações, por exemplo, uma tabela de moedas, você definiria cada visualização aqui antes da declaração parent::\_\_construct().

*Traduzido por openai.com*

