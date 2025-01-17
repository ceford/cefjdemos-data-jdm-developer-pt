<!-- Filename: J4.x:Joomla_Core_APIs / Display title: APIs Core do Joomla -->

Esta página lista os endpoints disponíveis no Joomla por exemplo de comandos curl. Foi preparada para o Joomla 4 e requer verificação de conformidade com as versões atuais do Joomla.

Toda URL requer autenticação, a menos que seja designada como uma URL pública. Para segurança no Joomla 4.0.0, planejamos fazer com que o aplicativo padrão da API exija uma conta de Superusuário (já que o aplicativo da API é totalmente novo), isso pode ser flexibilizado à medida que a API se estabiliza e é bem testada na comunidade. Se você estiver usando o plugin de autenticação básica (atualmente o único plugin fornecido a partir do Joomla 4 alpha 10), é necessário adicionar aos comandos curl abaixo usando --user nome_usuario:senha

Cada URL precisa ser precedida pelo host do Joomla antes do caminho (por exemplo, em vez de `/api/index.php/v1/article`, você precisa de `http://example.com/api/index.php/v1/article`).

Qualquer nome de propriedade entre chaves ({}) indica que a propriedade é uma variável que deve ser substituída.

A menos que indicado de outra forma, essas APIs foram introduzidas no Joomla 4. Para mais informações sobre a Especificação da API do Joomla (em oposição a esta lista de URLs e opções), por favor visite a [Especificação da API do Joomla](https://docs.joomla.org/Joomla_Api_Specification).

Onde os pontos de extremidade exigem o valor de {app}, a variável atualmente assume dois valores: site (front end) ou administrador (back end).

## Recursos Úteis

Um número de recursos complementares foi criado para introduzir os Serviços Web do Joomla e ajudá-lo a aprender como implementar Serviços Web em seu projeto.

- Coleção Postman das chamadas da [Joomla Web Services API](https://github.com/alexandreelise/j4x-api-collection) por Alexandre Elise.
- Tutorial do Youtube Joomla 4: [Utilizando a API de Serviços Web](https://www.youtube.com/watch?v=lT9qodsvfZg) com Eoin Oliver.
- Revista da Comunidade Joomla: [Joomla Web Services API 101](https://magazine.joomla.org/all-issues/august-2020/joomla-web-services-api-101-tokens,-testing-and-a-taste-test) por Patrick Jackson.

## Componente de Banners

### Banners

#### Obter Lista de Banners

curl -X GET /api/index.php/v1/banners

#### Obter Banner Único

curl -X GET /api/index.php/v1/banners/{banner_id}

#### Excluir Banner

`curl -X DELETE /api/index.php/v1/banners/{banner_id}`

#### Criar Banner

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/banners -d

{
    "catid": 3,
    "clicks": 0,
    "custombannercode": "",
    "description": "Texto",
    "metakey": "",
    "name": "Nome",
    "params": {
        "alt": "",
        "height": "",
        "imageurl": "",
        "width": ""
    }
}

#### Atualizar Banner

```
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/banners/{banner_id} -d
```

{
    "alias": "nome",
    "catid": 3,
    "description": "Novo Texto",
    "name": "Novo Nome"
}

### Clientes

#### Obter Lista de Clientes

curl -X GET /api/index.php/v1/banners/clientes

#### Obter Cliente Único

curl -X GET /api/index.php/v1/banners/clientes/{client_id}

#### Excluir Cliente

curl -X DELETE /api/index.php/v1/banners/clientes/{client_id}

#### Criar Cliente

curl -X POST -H "Content-Type: application/json" /api/index.php/v1/banners/clientes -d

```json
{
    "contacto": "Nome",
    "email": "email@mail.com",
    "extrainfo": "",
    "metakey": "",
    "nome": "Clientes",
    "estado": 1
}
```

#### Atualizar Cliente

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/banners/clients/{client_id} -d

{
    "contact": "novo Nome",
    "email": "novoe-mail@mail.com",
    "name": "Clientes"
}

### Categorias de Banners

#### Obter Lista de Categorias

`curl -X GET /api/index.php/v1/banners/categories`

#### Obter Categoria Única

curl -X GET /api/index.php/v1/banners/categories/{category_id}

#### Excluir Categoria

curl -X DELETE /api/index.php/v1/banners/categorias/{category_id}

#### Criar Categoria

```
curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/banners/categories -d
```

{
    "access": 1,
    "alias": "gato",
    "extension": "com_banners",
    "language": "*",
    "note": "",
    "parent_id": 1,
    "published": 1,
    "title": "Título"
}

#### Atualizar Categoria

curl -X PATCH -H "Content-Type: application/json" /api/index.php/v1/banners/categories/{category_id} -d

```json
{
    "alias": "gato",
    "note": "Algum texto",
    "parent_id": 1,
    "title": "Novo Título"
}
```

### Histórico de Conteúdo dos Banners

#### Obter Lista de Históricos de Conteúdo

curl -X GET /api/index.php/v1/banners/contenthistory/{banner_id}

#### Alternar Manter Histórico de Conteúdo

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/banners/historicoconteudo/manter/{historicoconteudo_id}

#### Excluir Histórico de Conteúdo

curl -X DELETE
/api/index.php/v1/banners/históriadeconteúdo/{contenthistory_id}

## Componente de Configuração

### Aplicativo

#### Obter Lista de Configurações de Aplicações

curl -X GET /api/index.php/v1/config/aplicativo

#### Atualizar Configuração do Aplicativo

```
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/config/application -d
```

{
    "debug": true,
    "sitename": "123"
}

### Componente

#### Obter Lista de Configurações de Componentes

`curl -X GET /api/index.php/v1/config/{component_name}`

Exemplo “component_name” é “com_content”.

#### Atualizar Configuração do Componente de Aplicação

```bash
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/config/application -d
```

{
    "link_titles": 1
}

## Componente de Contato

### Contato

#### Obter Lista de Contatos

curl -X GET /api/index.php/v1/contact

#### Obter Contato Único

`curl -X GET /api/index.php/v1/contact/{contact_id}`

#### Excluir Contato

```
curl -X DELETE /api/index.php/v1/contact/{contact_id}
```

#### Criar Contato

Não há texto específico que precise ser traduzido. O comando é técnico e deve permanecer como está.

```json
{
    "alias": "contato",
    "catid": 4,
    "language": "*",
    "name": "Contato"
}
```

#### Atualizar Contato

```
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/contact/{contact_id} -d
```

{
        "alias": "contato",
        "catid": 4,
        "name": "Novo Contato"
}

#### Enviar Formulário de Contato

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/contact/form/{contact_id} -d

{
    "contact_email": "email@mail.com",
    "contact_message": "algum texto",
    "contact_name": "nome",
    "contact_subject": "assunto"
}

### Categorias de Contato

1. A Rota Categorias de Contato é: "v1/contact/categories"
2. Trabalhar com ela é similar às Categorias de Banners.

### Campos de Contato

#### Obter Lista de Campos de Contato

```
curl -X GET /api/index.php/v1/fields/contato/contato
```

#### Obter Contato de Campo Único

`curl -X GET /api/index.php/v1/fields/contact/contact/{field_id}`

#### Excluir Campo Contato

Por favor, forneça o texto em inglês que você gostaria que fosse traduzido para o português, para que eu possa ajudá-lo.

#### Criar Contato de Campo

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/fields/contact/contact -d

```json
{
    "accesso": 1,
    "contexto": "com_contact.contact",
    "valor_padrao": "",
    "descrição": "",
    "id_grupo": 0,
    "etiqueta": "campo de contato",
    "idioma": "*",
    "nome": "campo-de-contato",
    "nota": "",
    "parâmetros": {
        "classe": "",
        "exibir": "2",
        "exibir_apenas_leitura": "2",
        "dica": "",
        "classe_etiqueta": "",
        "classe_renderização_etiqueta": "",
        "layout": "",
        "prefixo": "",
        "classe_renderização": "",
        "mostrar_em": "",
        "mostrar_etiqueta": "1",
        "sufixo": ""
    },
    "obrigatório": 0,
    "estado": 1,
    "título": "campo de contato",
    "tipo": "texto"
}
```

#### Atualizar Campo Contato

```markdown
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/fields/contact/contact/{field_id} -d
```

```json
{
    "title": "novo campo de contato",
    "name": "campo-de-contato",
    "label": "campo de contato",
    "default_value": "",
    "type": "texto",
    "note": "",
    "description": "Algum Texto Novo"
}
```

### Campos de Contato por E-mail

1. Os campos da rota Contato Mail são: "v1/fields/contact/mail"
2. Trabalhar com ele é semelhante aos Campos de Contato.

### Categorias de Contato de Campos

1. Os Campos de Rota das Categorias de Contato são: "v1/fields/contact/categories"
2. Trabalhar com isso é semelhante a Campos de Contato.

### Grupos Campos Contato

#### Obter Lista de Campos de Contatos dos Grupos

curl -X GET /api/index.php/v1/fields/groups/contact/contact

#### Obter Campos de Contato de Grupo Único

curl -X GET /api/index.php/v1/fields/groups/contact/contact/{group_id}

#### Excluir Contato de Campos do Grupo

curl -X DELETE
/api/index.php/v1/fields/groups/contact/contact/{group_id}

#### Criar Campos de Grupo de Contato

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/campos/grupos/contato/contato -d

```json
{
    "access": 1,
    "context": "com_contact.contact",
    "default_value": "",
    "description": "",
    "group_id": 0,
    "label": "campo de contato",
    "language": "*",
    "name": "campo-contato3",
    "note": "",
    "params": {
        "class": "",
        "display": "2",
        "display_readonly": "2",
        "hint": "",
        "label_class": "",
        "label_render_class": "",
        "layout": "",
        "prefix": "",
        "render_class": "",
        "show_on": "",
        "showlabel": "1",
        "suffix": ""
    },
    "required": 0,
    "state": 1,
    "title": "campo de contato",
    "type": "texto"
}
```

#### Atualizar Campos de Contato do Grupo

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/fields/groups/contact/contact/{group_id} -d

{
        "title": "novo grupo de contato",
        "note": "",
        "description": "nova descrição"
}

### Contato dos Campos do Grupo

1. O campo de grupos de rota para contato de e-mail é: "v1/fields/groups/contact/mail"
2. Trabalhar com isso é similar ao campo de grupos de contato.

### Categorias de Contato de Campos de Grupo

1.  Os Campos de Grupo de Rota Categorias de Contato são:
    "v1/fields/groups/contact/categories"
2.  Trabalhar com isso é similar a Campos de Grupo de Contato.

### Histórico de Conteúdo de Contato

1. O Histórico do Conteúdo da Rota é: "v1/contact/contenthistory"
2. Trabalhar com isso é semelhante ao Histórico de Conteúdo de Banners.

## Componente de Conteúdo

### Artigos

#### Obter Lista de Artigos

curl -X GET /api/index.php/v1/content/articles

#### Obter Artigo Único

curl -X GET /api/index.php/v1/content/articles/{article_id}

#### Excluir Artigo

curl -X DELETE /api/index.php/v1/content/articles/{article_id}

#### Criar Artigo

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/content/articles -d

{
    "alias": "meu-artigo",
    "articletext": "Meu texto",
    "catid": 64,
    "language": "*",
    "metadesc": "",
    "metakey": "",
    "title": "Aqui está um artigo"
}

Atualmente, as opções mencionadas aqui são propriedades obrigatórias. No entanto, a intenção é, atualmente, tornar PELO MENOS metakey e metadesc opcionais na API.

#### Atualizar Artigo

```
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/content/articles/{article_id} -d
```

{
        "catid": 64,
        "title": "Artigo atualizado"
}

### Categorias de Conteúdo

1. As categorias de conteúdo da rota são: "v1/content/categories"
2. Trabalhar com ele é similar a trabalhar com Categorias de Banners. Nota: se os fluxos de trabalho estiverem ativados, então especificar um fluxo de trabalho é necessário (similarmente à interface do usuário)

### Artigos de Campos

1. Os Artigos dos Campos de Rota são: "v1/fields/content/articles"
2. Trabalhar com isso é semelhante ao Campos de Contato.

### Grupos Campos Artigos

1.  A rota de Artigos em Grupos de Campos é: "v1/fields/groups/content/articles"
2.  Trabalhar com ela é semelhante a Grupos de Campos de Contato.

### Categorias de Campos

1. A categoria dos campos de rota é: "v1/fields/groups/content/categories"
2. Trabalhar com isso é semelhante a Campos de Contato.

### Histórico de Conteúdo do Componente de Conteúdo

1. O Histórico de Conteúdo da Rota é:
    "v1/content/articles/{article_id}/contenthistory"
2. Trabalhar com isso é semelhante ao Histórico de Conteúdo de Banners.

## Componente de Idiomas

### Idiomas

#### Obter Lista de Idiomas

`curl -X GET /api/index.php/v1/languages`

#### Instalar Idioma

```
curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/languages -d
```

{
    "package": "pkg_fr-FR"
}

### Idiomas de Conteúdo

#### Obter Lista de Idiomas de Conteúdo

curl -X GET /api/index.php/v1/languages/conteúdo

#### Obter Idioma Único do Conteúdo

curl -X GET /api/index.php/v1/v1/languages/content/{language_id}

#### Excluir Idioma do Conteúdo

curl -X DELETE /api/index.php/v1/languages/content/{language_id}

#### Criar Idioma do Conteúdo

```
curl -X POST -H "Content-Type: application/json" /api/index.php/v1/languages/content -d
```

{
    "access": 1,
    "description": "",
    "image": "fr_FR",
    "lang_code": "fr-FR",
    "metadesc": "",
    "metakey": "",
    "ordering": 1,
    "published": 0,
    "sef": "fk",
    "sitename": "",
    "title": "Francês (FR)",
    "title_native": "Français (France)"
}

#### Atualizar Idioma do Conteúdo

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/languages/content/{language_id} -d

```json
{
    "description": "",
    "lang_code": "pt-BR",
    "metadesc": "",
    "metakey": "",
    "sitename": "",
    "title": "Português (pt-BR)",
    "title_native": "Português (Brasil)"
}
```

### Substitui Idiomas

#### Obter Lista de Constantes de Idiomas Substituídas

curl -X GET /api/index.php/v1/languages/overrides/{app}/{lang_code}

#### Obter Constante de Linguagem de Substituição Única

curl -X GET
/api/index.php/v1/languages/overrides/{app}/{lang_code}/{constant_id}

#### Excluir Substituições de Idioma de Conteúdo

curl -X DELETE
/api/index.php/v1/languages/overrides/{app}/{lang_code}/{constant_id}

#### Criar Substituições de Idioma de Conteúdo

```
curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/languages/overrides/{app}/{lang_code} -d
```

```json
{
    "key":"nova_chave",
    "override": "texto"
}
```

#### Atualizar Substituições de Idioma do Conteúdo

```markdown
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/languages/overrides/{app}/{lang_code}/{constant_id} -d
```

{
    "key":"new_key",
    "override": "novo texto"
}

var app - enum {"site", "administrador"}

var lang_code - string Exemplo: “fr-FR“, “en-GB“ você pode obter lang_code
de v1/languages/content

#### Constante de Sobrescrição de Pesquisa

curl -X POST -H "Content-Type: application/json"  
/api/index.php/v1/idiomas/substituicoes/procurar -d

{
    "searchstring": "JLIB_APPLICATION_ERROR_SAVE_FAILED",
    "searchtype": "constante"
}

var searchtype - enum {“constant”, “value”}. “constant” busca por nome constante, “value” - busca por valor constante

#### Atualizar Cache de Pesquisa de Substituição

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/languages/overrides/search/cache/refresh

## Componente de Menus

### Menus

#### Obter Lista de Menus

curl -X GET /api/index.php/v1/menus/{app}

#### Obter Menu Único

curl -X GET /api/index.php/v1/menus/{app}/{menu_id}

#### Excluir Menu

curl -X DELETE /api/index.php/v1/menus/{app}/{menu_id}

#### Criar Menu

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/menus/{app} -d

{
    "client_id": 0,
    "description": "O menu para o site",
    "menutype": "menu",
    "title": "Menu"
}

#### Atualizar Menu

```
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/menus/{app}/{menu_id} -d
```

{
    "menutype": "menu",
    "title": "Novo Menu"
}

### Itens do Menu

#### Obter Lista de Tipos de Itens de Menus

curl -X GET /api/index.php/v1/menus/{app}/itens/tipos

#### Obter Lista de Itens de Menu

curl -X GET /api/index.php/v1/menus/{app}/items

#### Obter Item Único do Menu

```markdown
curl -X GET /api/index.php/v1/menus/{app}/items/{menu_item_id}
```

#### Excluir Item do Menu

curl -X DELETE /api/index.php/v1/menus/{app}/itens/{menu_item_id}

#### Criar Item de Menu

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/menus/{app}/items -d

```json
{
    "accesso": "1",
    "alias": "",
    "associações": {
        "en-GB": "",
        "fr-FR": ""
    },
    "navegaçãoNavegador": "0",
    "id_componente": "20",
    "casa": "0",
    "idioma": "*",
    "link": "index.php?option=com_content&view=form&layout=edit",
    "tipo_menu": "menuprincipal",
    "nota": "",
    "parâmetros": {
        "cancelar_redirecionamento_item_menu": "",
        "id_categoria": "",
        "cancelar_redirecionamento_personalizado": "0",
        "habilitar_categoria": "0",
        "css_âncora_menu": "",
        "título_âncora_menu": "",
        "descrição_meta_menu": "",
        "palavras_chave_meta_menu": "",
        "imagem_menu": "",
        "css_imagem_menu": "",
        "mostrar_menu": "1",
        "texto_menu": "1",
        "cabeçalho_página": "",
        "título_página": "",
        "sufixo_classe_página": "",
        "redirecionar_item_menu": "",
        "robôs": "",
        "mostrar_cabeçalho_página": ""
    },
    "id_pai": "1",
    "publicar_baixa": "",
    "publicar_alta": "",
    "publicado": "1",
    "id_estilo_template": "0",
    "título": "título",
    "alternar_módulos_atribuídos": "1",
    "alternar_módulos_publicados": "1",
    "tipo": "componente"
}
```

Exemplo para "Criar Página de Artigo"

#### Atualizar Item do Menu

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/menus/{app}/items/{menu_item_id} -d

{
    "component_id": "20",
    "language": "*",
    "link": "index.php?option=com_content&view=form&layout=edit",
    "menutype": "mainmenu",
    "note": "",
    "title": "novo título",
    "type": "componente"
}

Exemplo para "Criar Página de Artigo"

## Componente de Mensagens

### Mensagens

#### Obter Lista de Mensagens

curl -X GET /api/index.php/v1/mensagens

#### Obter Mensagem Única

curl -X GET /api/index.php/v1/messages/{message_id}

#### Excluir Mensagem

curl -X DELETE /api/index.php/v1/mensagens/{message_id}

#### Criar Mensagem

```markdown
curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/messages -d
```

```json
{
    "message": "texto",
    "state": 0,
    "subject": "texto",
    "user_id_from": 773,
    "user_id_to": 772
}
```

#### Mensagem de Atualização

```markdown
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/messages/{message_id} -d
```

{
    "mensagem": "novo texto",
    "assunto": "novo texto",
    "user_id_from": 773,
    "user_id_to": 772
}

## Componente de Módulos

### Módulos

#### Obter Lista de Tipos de Módulos

curl -X GET /api/index.php/v1/modules/types/{app}

#### Obter lista de módulos

curl -X GET /api/index.php/v1/modules/{app}

#### Obter Módulo Único

curl -X GET /api/index.php/v1/módulos/{app}/{module_id}

#### Excluir Módulo

curl -X DELETE /api/index.php/v1/modules/{app}/{module_id}

#### Criar Módulo

curl -X POST -H "Content-Type: application/json"  
/api/index.php/v1/modules/{app} -d

```json
{
    "acesso": "1",
    "atribuído": [
        "101",
        "105"
    ],
    "atribuição": "0",
    "cliente_id": "0",
    "idioma": "*",
    "módulo": "mod_articles_archive",
    "nota": "",
    "ordenamento": "1",
    "parâmetros": {
        "tamanho_bootstrap": "0",
        "cache": "1",
        "tempo_cache": "900",
        "modo_cache": "estático",
        "contagem": "10",
        "classe_cabeçalho": "",
        "tag_cabeçalho": "h3",
        "layout": "_:default",
        "tag_módulo": "div",
        "sfx_classemodule": "",
        "estilo": "0"
    },
    "posição": "",
    "publicar_abaixo": "",
    "publicar_acima": "",
    "publicado": "1",
    "mostrar_título": "1",
    "título": "Título"
}
```

Exemplo de "Artigos - Arquivados"

#### Atualizar Módulo

curl -X PATCH -H "Content-Type: application/json"  
/api/index.php/v1/modules/{app}/{module_id} -d

```json
{
    "access": "1",
    "client_id": "0",
    "language": "*",
    "module": "mod_articles_archive",
    "note": "",
    "ordering": "1",
    "title": "Novo Título"
}
```

Exemplo para "Artigos - Arquivados"

## Componente de Notícias

### Feeds

#### Obter Lista de Feeds

curl -X GET /api/index.php/v1/newsfeeds/feeds

#### Obter Feed Único

curl -X GET /api/index.php/v1/newsfeeds/feeds/{feed_id}

#### Excluir Feed

curl -X DELETE /api/index.php/v1/newsfeeds/feeds/{feed_id}

#### Criar Feed

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/newsfeeds/feeds -d

```json
{
    "acesso": 1,
    "alias": "alias",
    "catid": 5,
    "descrição": "",
    "imagens": {
        "float_first": "",
        "float_second": "",
        "image_first": "",
        "image_first_alt": "",
        "image_first_caption": "",
        "image_second": "",
        "image_second_alt": "",
        "image_second_caption": ""
    },
    "idioma": "*",
    "link": "http://samoylov/joomla/gsoc19_webservices/index.php",
    "metadata": {
        "hits": "",
        "direitos": "",
        "robôs": "",
        "tags": {
            "tags": "",
            "tipoAlias": null
        }
    },
    "metadesc": "",
    "metakey": "",
    "nome": "Nome",
    "ordenação": 1,
    "parâmetros": {
        "feed_character_count": "",
        "feed_display_order": "",
        "newsfeed_layout": "",
        "mostrar_descrição_feed": "",
        "mostrar_imagem_feed": "",
        "mostrar_descrição_item": ""
    },
    "publicado": 1
}
```

#### Atualizar Feed

`curl -X PATCH -H "Content-Type: application/json" /api/index.php/v1/newsfeeds/feeds/{feed_id} -d`

{
    "acesso": 1,
    "alias": "test2",
    "catid": 5,
    "descrição": "",
    "link": "http://samoylov/joomla/gsoc19_webservices/index.php",
    "metadesc": "",
    "metakey": "",
    "nome": "Teste"
}

### Categorias de Noticiários

1. A rota para Categorias de Feeds de Notícias é: "v1/newsfeeds/categories"
2. Trabalhar com isso é semelhante a Categorias de Banners.

## Componente de Privacidade

### Solicitação

#### Obter Lista de Solicitações

curl -X GET /api/index.php/v1/privacy/request

#### Obter Solicitação Única

curl -X GET /api/index.php/v1/privacy/request/{request_id}

#### Obter Dados de Exportação de Pedido Único

Tradução não é necessária para blocos de código delimitados (fenced code blocks).

#### Criar Solicitação

curl -X POST -H "Content-Type: application/json"  
/api/index.php/v1/privacy/request -d

{
    "email":"somenewemail@com.ua",
    "request_type":"exportar"
}

### Consentimento

#### Obter Lista de Consentimentos

`curl -X GET /api/index.php/v1/privacy/consent`

#### Obter Consentimento Único

curl -X GET /api/index.php/v1/privacy/consent/{consent_id}

#### Excluir Consentimento

`curl -X DELETE /api/index.php/v1/privacy/consent/{consent_id}`

## Componente de Redirecionamento

### Redirecionar

#### Obter Lista de Redirecionamentos

`curl -X GET /api/index.php/v1/redirect`

#### Obter Redirecionamento Único

curl -X GET /api/index.php/v1/redirect/{id_do_redirecionamento}

#### Excluir Redirecionamento

curl -X DELETE /api/index.php/v1/redirect/{redirect_id}

#### Criar Redirecionamento

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/redirect -d

{
    "comentário": "",
    "cabeçalho": 301,
    "acessos": 0,
    "nova_url": "/content/art/99",
    "antiga_url": "/content/art/12",
    "publicado": 1,
    "referente": ""
}

#### Atualizar Redirecionamento

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/redirect/{redirect_id} -d

{
        "new_url": "/content/art/4",
        "old_url": "/content/art/132"
}

## Componente de Tags

### Tags

#### Obter Lista de Tags

`curl -X GET /api/index.php/v1/tags`

#### Obter Tag Única

```plaintext
curl -X GET /api/index.php/v1/tags/{tag_id}
```

#### Excluir Tag

curl -X DELETE /api/index.php/v1/tags/{tag_id}

#### Criar Tag

curl -X POST -H "Content-Type: application/json" /api/index.php/v1/tags -d

{
        "access": 1,
        "access_title": "Público",
        "alias": "teste",
        "description": "",
        "language": "*",
        "note": "",
        "parent_id": 1,
        "path": "teste",
        "published": 1,
        "title": "teste"
    }

#### Atualizar Tag

curl -X PATCH -H "Content-Type: application/json" /api/index.php/v1/tags/{tag_id} -d

{
    "alias": "teste",
    "title": "novo título"
}

## Modelos

### Estilos de Modelos

#### Obter Lista de Estilos de Modelos

```
curl -X GET /api/index.php/v1/templates/styles/{app}
```

#### Obter Estilo de Template Único

curl -X GET /api/index.php/v1/templates/styles/{app}/{template_style_id}

#### Excluir Estilo de Modelo

curl -X DELETE
/api/index.php/v1/templates/styles/{app}/{template_style_id}

#### Criar Estilo de Modelo

```
curl -X POST -H "Content-Type: application/json" /api/index.php/v1/templates/styles/{app} -d
```

{
    "home": "0",
    "params": {
        "fluidContainer": "0",
        "logoFile": "",
        "sidebarLeftWidth": "3",
        "sidebarRightWidth": "3"
    },
    "template": "cassiopeia",
    "title": "cassiopeia - Algum Texto"
}

#### Atualizar Estilo do Modelo

curl -X PATCH -H "Content-Type: application/json" /api/index.php/v1/templates/styles/{app}/{template_style_id} -d

{
    "template": "cassiopeia",
    "title": "novo cassiopeia - Padrão"
}

## Componente de Usuários

### Usuários

#### Obter Lista de Usuários

curl -X GET /api/index.php/v1/usuarios

#### Obter Usuário Único

curl -X GET /api/index.php/v1/usuarios/{user_id}

#### Excluir Usuário

curl -X DELETE /api/index.php/v1/usuarios/{user_id}

#### Criar Usuário

```plaintext
curl -X POST -H "Content-Type: application/json" /api/index.php/v1/users
-d
```

```json
{
    "bloqueio": "0",
    "email": "test@mail.com",
    "grupos": [
        "2"
    ],
    "id": "0",
    "ultimaHoraDeReset": "",
    "dataUltimaVisita": "",
    "nome": "nnn",
    "parametros": {
        "idioma_admin": "",
        "estilo_admin": "",
        "editor": "",
        "site_ajuda": "",
        "idioma": "",
        "fuso_horario": ""
    },
    "senha": "qwertyqwerty123",
    "senha2": "qwertyqwerty123",
    "dataRegistro": "",
    "requerReset": "0",
    "contadorReset": "0",
    "enviarEmail": "0",
    "nome_usuario": "ad"
}
```

#### Atualizar Usuário

```
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/users/{user_id} -d
```

{
    "email": "new@mail.com",
    "groups": [
        "2"
    ],
    "name": "nome",
    "username": "nome de usuário"
}

### Campos Usuários

1. A rota para Campos Usuários é: "v1/fields/users"
2. Trabalhar com isso é semelhante a trabalhar com Campos Contato.

### Grupos Campos Usuários

1. O Grupo de Rotas para Usuários de Campos é: "v1/fields/groups/users"
2. Trabalhar com isso é similar ao Grupos de Campos de Contato.

*Traduzido por openai.com*

