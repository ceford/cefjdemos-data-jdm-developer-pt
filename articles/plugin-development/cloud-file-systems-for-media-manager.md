<!-- Filename: J4.x:Cloud_File_Systems_for_Media_Manager / Display title: Sistemas de Arquivos em Nuvem para Gerenciamento de Mídia -->

<span id="main-portal-heading">GSoC 2017
Sistemas de Arquivos em Nuvem para Gerenciador de Mídia
Documentação</span> [<img
src="https://docs.joomla.org/images/thumb/7/7d/Gsoc2016.png/75px-Gsoc2016.png"
decoding="async"
srcset="https://docs.joomla.org/images/thumb/7/7d/Gsoc2016.png/113px-Gsoc2016.png 1.5x, https://docs.joomla.org/images/thumb/7/7d/Gsoc2016.png/150px-Gsoc2016.png 2x"
data-file-width="373" data-file-height="373" width="75" height="75"
alt="Gsoc2016.png" />](https://docs.joomla.org/GSOC_2017 "GSOC 2017")
Joomla!  4.x

## Introdução

**Joomla! 4.x** é fornecido com sistemas de arquivos em nuvem para o **Media Manager** por padrão. Com a API anterior, criar sistemas de arquivos personalizados era uma tarefa difícil. Graças à nova API, agora é fácil criar um sistema de arquivos personalizado. Se você quiser usar um Serviço de Nuvem com o novo Media Manager, é recomendado usar **OAuth2.0**.

Este documento irá guiá-lo através de etapas importantes para criar seu próprio **Plugin de Sistema de Arquivos** para estender o **Gerenciador de Mídia**. Antes de prosseguir, certifique-se de ter o conhecimento básico sobre como desenvolver um plugin para Joomla. [Este tutorial](https://docs.joomla.org/J3.x:Creating_a_Plugin_for_Joomla) deve ajudar.

## Crie seu plugin de sistema de arquivos

### Configuração

Primeiramente, precisamos criar um plugin de **sistema de arquivos** para expandir o Gerenciador de Mídia. Este plugin deve conter alguns atributos importantes para que possa funcionar com o Gerenciador de Mídia.

Certifique-se de que seu plugin contém `group="filesystem"`. Assim, em seu
`[plugin-name].xml`, você deve ter:

```xml
<?xml version="1.0" encoding="utf-8"?>
<extension version="4.0" type="plugin" group="filesystem" method="upgrade">
    <name>plg_filesystem_myplugin</name>
    <author>Joomla! Project</author>
    <creationDate>April 2017</creationDate>
    <copyright>Copyright (C) 2005 - 2017 Open Source Matters. All rights reserved.</copyright>
    <license>GNU General Public License version 2 or later; see LICENSE.txt</license>
    <authorEmail>admin@joomla.org</authorEmail>
    <authorUrl>www.joomla.org</authorUrl>
    <version>__DEPLOY_VERSION__</version>
    <description>Description</description>
    <files>
        <filename plugin="myplugin">myplugin.php</filename>
        <folder>SomeFolder</folder>
    </files>

    <config>
        <fields name="params">
            <fieldset name="basic">
                <field
                    name="display_name"
                    type="text"
                    label="YOUR_LABEL"
                    description="YOUR_DESCRIPTION"
                    default="DEFAULT_VALUE"
                />
            </fieldset>
        </fields>
    </config>
</extension>
```

O parâmetro **display_name** ajuda o Gerenciador de Mídia a exibir o nome do seu **Sistema de Arquivos** como um nó raiz no Navegador de Arquivos. Qualquer adaptador pertencente ao seu Sistema de Arquivos será exibido como filhos sob o nó raiz.

Inclua todos os parâmetros necessários, como `App Secret`, com Campos de Formulário apropriados.

### Eventos do Plugin

- `onFileSystemGetAdapters()`
- `onFileSystemOAuthCallback(\Joomla\Component\Media\Administrator\Event\OAuthCallbackEvent $event)`

#### onFileSystemGetAdapters()

Qualquer plugin de sistema de arquivos deve conter um evento chamado `onFileSystemGetAdapters()` para funcionalidade. Este evento deve retornar um **array** de `Joomla\Component\Media\Administrator\Adapter\AdapterInterface` quando for chamado. O evento é acionado quando você abre o Gerenciador de Mídia. Cada `AdapterInterface` será montado sob o nó raiz do seu sistema de arquivos.

#### onFileSystemOAuthCallback()

Este evento é acionado quando você usa o **OAuthCallbackHandler** do Media Manager para o processo de Autorização e Autenticação OAuth2.0 descrito abaixo no documento. O evento é acionado somente no plugin solicitado. Portanto, não há necessidade de verificar o `$context` em um cenário típico.

Um exemplo de uso do evento se parece com:

```php
    public function onFileSystemOAuthCallback(\Joomla\Component\Media\Administrator\Event\OAuthCallbackEvent $event)
    {
        // Your context
        $context = $event->getContext();

        // Get the input
        $data = $event->getInput();

        // Your code goes here

        // Set result to be returned
        $result = [
            "action" => "control-panel"
        ];

        // Pass back the result to event
        $event->setArgument('result', $result);
    }
```

**OAuthCallbackEvent** contém a entrada encaminhada para o URI OAuthCallback do Gerenciador de Mídia. `$event->getInput()` retorna um objeto de entrada.

`$result` define como o Joomla se comporta após um redirecionamento para o callback. Existem várias soluções possíveis disponíveis:

- `action`
  - close: Fecha uma janela que é aberta por um JavaScript **usando window.open()**
  - redirect: Redireciona para a página especificada pelo **redirect_uri**
  - control-panel: Redirecionar para o painel de controle
  - media-manager: Redirecionar para o Gerenciador de Mídia
- `redirect_uri`
  - Usado com a ação **redirect** (obrigatório)
- `message`
  - Mensagem que precisa ser exibida após uma ação
- `message_type`
  - warning
  - notice
  - error
  - message(ou deixar vazio)

Após definir tudo, defina o argumento `$result` do `$event` para passá-lo de volta ao chamador.

Um exemplo para exibir uma mensagem ao usuário seria:

```php
    $result = [
        "action" => "media-manager",
        "message" => "Some message",
        "message-type" => "notice"
    ];
```

Isso redirecionará para o Gerenciador de Mídia e exibirá uma notificação com o texto em **mensagem**.

Este método pode ser normalmente usado para obter códigos de autorização para o processo **OAuth2.0**. Em caso de **erro**, o Joomla! retornará ao painel de controle e exibirá uma mensagem de erro.

## Autenticação e Autorização

Joomla! 4.x aconselha você a usar OAuth2.0 para este processo. É um cenário comum que o OAuth2.0 requeira uma **URL de redirecionamento** para passar os dados de autenticação para o Aplicativo. Isso é tipicamente feito por um manipulador de retorno de chamada. Para o seu plugin, não há necessidade de reinventar a roda, você pode usar o **Manipulador de Retorno de Chamada** do **Gerenciador de Mídia** para realizar a tarefa.

Tudo o que você precisa fazer é definir o **URI de Redirecionamento** para o seguinte no seu provedor OAuth2.0 e implementar o `onFileSystemOAuthCallback(\Joomla\Component\Media\Administrator\Event\OAuthCallbackEvent $event)` no seu plugin.

`[site-name]/administrator/index.php?option=com_media&task=plugin.oauthcallback&plugin=[seu-nome-de-plugin]`

Neste exemplo:
`[site-name]/administrator/index.php?option=com_media&task=plugin.oauthcallback&plugin=myplugin`

Agora, quando você faz um redirecionamento do seu provedor, assim que ele atingir a URL fornecida, o **Controlador** para o Gerenciador de Mídia garantirá que seu plugin implemente `onFileSystemOAuthCallback(\Joomla\Component\Media\Administrator\Event\OAuthCallbackEvent $event)` antes de passar qualquer dado para ele. Caso contrário, você será redirecionado para o Painel de Controle com uma mensagem de erro.

Se você implementou todas as entradas que são passadas, o Provedor de Nuvem será incluído no `$event`. Você pode acessá-las usando `$event->getInput()` e tratá-las como uma `input` usual para o Joomla.

Após receber o `input`, você pode usá-lo para obter os detalhes do seu serviço em nuvem, como **Token de Acesso**, **Token de Renovação** etc.

Se você quiser distinguir várias contas, pode usar `Session` para isso.

**Nota**: É aconselhável verificar o **token CSRF** antes de prosseguir com seu pedido. A maioria dos provedores de nuvem suporta o parâmetro `state` que pode ser usado para cumprir a tarefa.

### Armadilhas Comuns

É necessário `urlencode()` seu URI de redirecionamento quando você estiver enviando-o
para o provedor de nuvem. Por favor, use-o para evitar mau funcionamento da
sua nuvem.

## Arquivo Servir do seu Adaptador

Para servir seus arquivos de mídia do Media Manager para o **Site Joomla!** `Joomla\Component\Media\Administrator\Adapter\AdapterInterface` ajuda você. Esta Interface contém um método especial chamado `getUrl($path)`.

`$path : O caminho é relativo à sua raiz`

A intenção do método é fornecer uma **URL Absoluta Pública** para o arquivo que você solicitou inserir no site. Por exemplo, suponha que o caminho do seu arquivo seja `/path/to/me.png` no servidor em nuvem. Agora, uma URL pública pode ser algo como `mycloud.com/share/u/myusername/path/to/me.png`. Como ela será servida, depende totalmente de você. Quando um usuário quiser inserir uma URL de mídia gerada, este método será usado.

Mais detalhes sobre `Adapter Interface` podem ser encontrados em `administrator/componenents/com_media/Adapter/AdapterInterface.php`

*Traduzido por openai.com*

