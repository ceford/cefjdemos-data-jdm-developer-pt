<!-- Filename: API_Guides / Display title: Guias de API -->

Esta página contém um índice para o conjunto de Guias de API do Joomla. Esses guias têm como objetivo ajudá-lo a entender como usar essas funções do Joomla em suas próprias extensões Joomla.

Cada guia de API inclui exemplos de código que você pode copiar e instalar no seu próprio ambiente de desenvolvimento. Geralmente, esses exemplos de código são escritos para serem incluídos e instalados como um módulo Joomla, então, se você não estiver familiarizado com o desenvolvimento de módulos Joomla, pode achar útil passar pela curta série [Criando um Módulo Simples](https://docs.joomla.org/Creating_a_simple_module).

Por volta do Joomla 3.8, a equipe de desenvolvimento do Joomla começou a mudar a convenção de nomenclatura das classes do Joomla para usar namespaces, de forma que, por exemplo, JFactory mudou para Factory no namespace Joomla\CMS. Ao ler o código e a documentação existentes do Joomla, você pode encontrar as classes seguindo o novo ou o antigo padrão de nomenclatura. Você pode encontrar o mapeamento entre as duas convenções de nomenclatura no arquivo `libraries/classmap.php` na sua instância do Joomla.

- As classes de aplicação base e sua hierarquia e propósitos são descritos em [Understanding the Application classes](https://docs.joomla.org/J3.x:Understanding_the_Application_classes)
- O manuseio de Ajax dentro de Componentes Joomla é descrito em [JSON Responses with JResponseJson](https://docs.joomla.org/JSON_Responses_with_JResponseJson "JSON Responses with JResponseJson"). Ajax também pode ser usado dentro de Módulos e Plugins Joomla como descrito em [Using Joomla Ajax Interface](https://docs.joomla.org/Using_Joomla_Ajax_Interface).
- [Cache](https://docs.joomla.org/Cache_Basic_API_Guide) - como usar cache de retorno de chamada dentro do seu código.
- [Categories](https://docs.joomla.org/Categories_and_CategoryNodes_API_Guide) Usando as classes `Categories` e `CategoryNode` para acessar dados relacionados às categorias do Joomla
- CSS pode ser adicionado conforme descrito em [Adding JavaScript and CSS to the page](https://docs.joomla.org/Adding_JavaScript_and_CSS_to_the_page)
- Banco de dados / JDatabase. Existem dois guias de API, cobrindo [Selecting data using JDatabase](https://docs.joomla.org/Selecting_data_using_JDatabase)
  e [Inserting, Updating and Removing data using JDatabase](https://docs.joomla.org/Inserting,_Updating_and_Removing_data_using_JDatabase)
- [Date/JDate](https://docs.joomla.org/How_to_use_JDate) é a classe de data do Joomla.
- Arquivos e Pastas. Veja [How to use the filesystem package](https://docs.joomla.org/How_to_use_the_filesystem_package).
- Formulário / JForm. Há um [Guia básico](https://docs.joomla.org/Basic_form_guide "Basic form guide") para usar a API de formulário do Joomla e incorporar formulários dentro de um componente Joomla, e também um [Guia avançado de formulários](https://docs.joomla.org/Advanced_form_guide) cobrindo aspectos mais avançados das APIs.
- FormField / JFormField. Esta classe e classes relacionadas, como JFormFieldList, que herdam dela, são principalmente úteis para definir campos de formulário personalizados, conforme descrito em [Creating a custom form field type](https://docs.joomla.org/Creating_a_custom_form_field_type).
- [Input / JInput](https://docs.joomla.org/Retrieving_request_data_using_JInput) Usando a classe `Input` para obter os valores dos parâmetros em solicitações HTTP GET e POST
- JavaScript pode ser adicionado conforme descrito em [Adding JavaScript and CSS to the page](https://docs.joomla.org/Adding_JavaScript_and_CSS_to_the_page)
- Usar Layouts Joomla é descrito em [Sharing layouts across views or extensions with JLayout](https://docs.joomla.org/J3.x:Sharing_layouts_across_views_or_extensions_with_JLayout "J3.x:Sharing layouts across views or extensions with JLayout"). A flexibilidade foi aumentada no Joomla 3.2, conforme descrito em [JLayout Improvements for Joomla!](https://docs.joomla.org/J3.x:JLayout_Improvements_for_Joomla!).
- [Log / JLog](https://docs.joomla.org/Using_JLog) Registrar mensagens (por exemplo, mensagens de erro, mensagens de depuração) em um arquivo de log e, opcionalmente, no console de depuração
- [Menu and Menuitems](https://docs.joomla.org/Menu_and_Menuitems_API_Guide)
- [Nested Sets](https://docs.joomla.org/Using_nested_sets), que permitem a implementação de uma hierarquia em árvore na tabela do banco de dados, são usados por menus, artigos, categorias do Joomla, etc.
- [Registry/JRegistry](https://github.com/joomla-framework/registry) é uma classe utilitária muito útil para manipular arrays PHP, converter para JSON, etc.
- [JResponseJson](https://docs.joomla.org/JSON_Responses_with_JResponseJson) suporta responder em formato JSON a solicitações Ajax.
- Route / JRoute veja [URLs in Joomla](https://docs.joomla.org/URLs_in_Joomla)
- Table / JTable fornece funcionalidade para realizar operações CRUD (e mais) nas tabelas do banco de dados. O guia é dividido em um [Guia Básico de API](https://docs.joomla.org/Table_Basic_API_Guide)
  e um [Guia Avançado de API](https://docs.joomla.org/Table_Advanced_API_Guide)
- Os [Controllers](https://docs.joomla.org/Controllers) (BaseController, AdminController, FormController, ApiController) são responsáveis por analisar a solicitação do usuário, verificar se o usuário tem permissão para realizar essa ação e determinar como satisfazer a solicitação.
- Os [Models](https://docs.joomla.org/Models) (BaseModel, BaseDatabaseModel, ItemModel, ListModel, FormModel, AdminModel) encapsulam os dados usados pelo componente. Eles também são responsáveis por atualizar o banco de dados quando apropriado.
- As [Views](https://docs.joomla.org/Views) (AbstractView, CategoriesView, CategoryFeedView, CategoryView, FormView, HtmlView, JsonApiView, JsonView, ListView) especificam o que deve aparecer na página web e reúnem todos os dados necessários para enviar a resposta HTTP.
- [Tags](https://docs.joomla.org/Tags_API_Guide).
- Uri / JUri veja [URLs in Joomla](https://docs.joomla.org/URLs_in_Joomla)
- [User / JUser](https://docs.joomla.org/Accessing_the_current_user_object) API relacionada ao Usuário do Joomla.

*Traduzido por openai.com*

