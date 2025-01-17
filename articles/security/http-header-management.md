<!-- Filename: J4.x:Http_Header_Management / Display title: Cabeçalhos HTTP -->

## Introdução

Joomla 4 introduziu um sistema de Cabeçalhos HTTP projetado para ajudar os proprietários de sites a configurar Cabeçalhos de Segurança HTTP. Ele é implementado usando um plugin *System - HTTP Headers*. Há um tutorial [User](jdocmanual?article=user/security/http-headers) abrangente sobre este tópico. Este tutorial é mais curto e cobre alguns pontos relevantes para desenvolvedores.

## O Sistema - Plugin de Cabeçalhos HTTP

### Guia de plugin

Navegue para **Sistema → Plugins → Sistema - Cabeçalhos HTTP** para acessar o formulário de configuração do plugin.

![System http headers plugin form](../../../en/images/security/security-http-headers-plugin.png)

- **Opções X-Frame** Isso é ativado por padrão, mas a [documentação](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options) diz que está obsoleto e uma política de *frame-ancestors* deve ser usada em vez disso.
- **Política de Referência** O padrão é *strict-origin-when-cross-origin*.
- **Política de Abertura entre Origens** O valor padrão do Joomla é `same-origin`.
- **Forçar Cabeçalhos HTTP** Não há cabeçalhos forçados definidos por padrão. Aqui é onde pode ser especificada uma alternativa às *Opções X-Frame*. O valor de `Content-Security-Policy` pode ser um dos seguintes:
    - `'none'`
    - `'self' https://www.example.org;`
    - `'self' https://example.org https://example.com https://store.example.com;`

Usando o subformulário **Forçar Cabeçalhos HTTP**, você também pode forçar os seguintes cabeçalhos:

- [Política de Segurança de Conteúdo](https://scotthelme.co.uk/content-security-policy-an-introduction/)
- [Política de Segurança de Conteúdo Somente para Relatório](https://scotthelme.co.uk/content-security-policy-an-introduction/#testingapolicy)
- [Política de Abridor entre Origens](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cross-Origin-Opener-Policy)
- [Expect-CT](https://scotthelme.co.uk/a-new-security-header-expect-ct/)
- [Política de Recursos & Política de Permissões](https://scotthelme.co.uk/a-new-security-header-feature-policy/)
- [NEL (Registro de Resposta de Rede)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/NEL)
- [Política de Referência](https://scotthelme.co.uk/a-new-security-header-referrer-policy/)
- [Reportar-para](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-to)
- [Segurança de Transporte Estrita](https://scotthelme.co.uk/hsts-the-missing-link-in-tls/)
- [Opções de Quadro X](https://scotthelme.co.uk/hardening-your-http-response-headers/#x-frame-options)

### Guia de Segurança de Transporte Estrita (HSTS)

![strict transport security settings](../../../en/images/security/security-http-headers-hsts.png)

Use o botão *Alternar Ajuda Inline* para obter informações sobre cada parâmetro. Referência ilustrada:

[Formulário para verificar ou definir o status e a elegibilidade de pré-carregamento HSTS](https://hstspreload.org/)

### Guia de Políticas de Segurança de Conteúdo (CSP)

![Content security policy options](../../../en/images/security/security-http-headers-csp.png)

Uma vez habilitado, você pode definir o cliente onde deseja aplicar a CSP configurada, permitindo definir `site`, `administrador` ou `ambos`. Uma CSP deve ser aplicada tanto no frontend quanto no backend. Referências ilustradas:

- [Política de Segurança de Conteúdo](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
- [Nonce](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/nonce)
- [Hashes de Script e Estilo](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/script-src)
- Descrições de origem de [Diretiva de Política](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/child-src) estão disponíveis no menu desta página.

A opção final chamada *Adicionar Diretiva* permite que você configure a lista de permissões por diretiva conforme necessário. Por exemplo, para a diretiva *script-src*, o campo *Valor* deve conter as origens que você deseja permitir o carregamento de scripts.

## Notas

Quando você configurou alguns Cabeçalhos de Segurança HTTP diretamente no servidor, pode haver entradas duplicadas.

Verifique a saída dos seus Cabeçalhos HTTP no console do navegador. No Google Chrome ou Firefox: Inspecionar → Rede → a saída em Cabeçalhos. Você pode então desativar os cabeçalhos que causam entradas duplas. Também verifique o console do seu navegador para possíveis erros.

## Desenvolvedores de Extensões

A grande vantagem de uma Política de Segurança de Conteúdo ocorre quando o Cabeçalho bloqueia todo JavaScript inline e CSS inline afetando manipuladores de eventos JavaScript via atributos HTML. Com a proteção do navegador ativada, JavaScript inline e CSS inline também são bloqueados para extensões. Essa proteção não está ativada por padrão, mas pode ser habilitada pelos usuários.

Onde JavaScript e CSS inline são necessários, suporte para nonce e hash estão incluídos nas APIs de Documento. Quando usados, o núcleo garantirá que eles estejam na lista de permissões, mas ainda bloqueará códigos maliciosos.

### Notas importantes para Desenvolvedores de Extensões

A partir do Joomla 4.0, a Política de Segurança de Conteúdo:

- é enviado com o núcleo.
- está desativado por padrão.
- pode ser habilitado por administradores do site.
- é fortemente recomendável que o frontend e o backend da sua extensão funcionem com a Política de Segurança de Conteúdo ativada.

Com a Política de Segurança de Conteúdo estrita habilitada, os seguintes recursos serão bloqueados:

- A execução de JavaScript através dos manipuladores de eventos HTML (manipuladores onXXX como onClick e similares).
- A execução de JavaScript na página que não é passada para a página através da API do Documento.
- A execução de código JavaScript injetado em APIs do DOM, como eval().
- O uso de CSS embutido na página que não é passado para a página através da API do Documento.
- O uso de CSS embutido utilizando o atributo style do HTML.

Para fazer suas extensões funcionarem mesmo com uma política de segurança de conteúdo estrita habilitada, a maneira mais fácil é usar a API do Documento para aplicar seu JavaScript e CSS embutidos. Veja os exemplos abaixo.

### Adicionando JavaScript usando a API do Joomla

```php
    use Joomla\CMS\Factory;

    /** @var Joomla\CMS\WebAsset\WebAssetManager $wa */
    $wa = Factory::getApplication()->getDocument()->getWebAssetManager();

    // Add JavaScript from URL
    $wa->registerAndUseScript('com_example.sample', 'https://example.org/sample.js', [], ['defer' => true]);

    // Add inline JavaScript
    $wa->addInlineScript('
        document.addEventListener("DOMContentLoaded", function(event) {
            alert("An inline JavaScript Declaration");
        });
    ');
```

### Adicionando CSS usando a API do Joomla

```php
    use Joomla\CMS\Factory;

    /** @var Joomla\CMS\WebAsset\WebAssetManager $wa */
    $wa = Factory::getApplication()->getDocument()->getWebAssetManager();

    // Add Style from URL
    $wa->registerAndUseStyle('com_example.sample', 'https://example.org/sample.css');

    // Add inline Style
    $wa->addInlineStyle('
        body {
            background: #00ff00;
            color: rgb(0,0,255);
        }
    ');
```

## Recursos adicionais

- [CSP Cheat Sheet](https://scotthelme.co.uk/csp-cheat-sheet/)
- [Política de Segurança de Conteúdo - Uma Introdução](https://scotthelme.co.uk/content-security-policy-an-introduction/)
- [Security Headers](https://securityheaders.com/) é parte do Probely e foi originalmente criado por Scott Helme! É uma ferramenta gratuita e fácil de usar, projetada para ajudar você a implementar e compreender melhor os recursos de segurança modernos disponíveis para o seu site.
- [CSP Evaluator](https://csp-evaluator.withgoogle.com/)
- [Política de Segurança de Conteúdo do Web Fundamentals](https://developers.google.com/web/fundamentals/security/csp)
- [Documentação de CSP do Google](https://csp.withgoogle.com/docs/index.html)
- [CSP Está Morto, Viva o CSP!](https://research.google/pubs/pub45542/) Sobre a Insegurança das Listas Brancas e o Futuro da Política de Segurança de Conteúdo
- [Pesquisa de Segurança do web.dev](https://web.dev/s/results?q=security#gsc.tab=0&gsc.q=security&gsc.sort=)

*Traduzido por openai.com*

