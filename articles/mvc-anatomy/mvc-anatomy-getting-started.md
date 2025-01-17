<!-- Filename: J4.x:MVC_Anatomy:_Getting_Started / Display title: Anatomia do MVC: Introdução -->

## Introdução

Os componentes do Joomla seguem a abordagem Modelo, Visão, Controlador, ou MVC para abreviar. O Modelo deve lidar com o carregamento e armazenamento de dados. A Visão deve lidar com a exibição de dados. E o Controlador deve lidar com o fluxo do programa, a interação entre o código do Modelo e da Visão do componente.

Se você deseja construir seu próprio componente, existem duas abordagens de aprendizado que você pode adotar:

- **Construa passo a passo:** seguindo um tutorial simples que descreve cada etapa.
- **Desmonte arquivo por arquivo:** desmontando um componente funcional para aprender como cada parte funciona.

Este tutorial utiliza a última abordagem. O componente usado para o tutorial é denominado com_countrybase. Ele é usado para gerenciar e exibir alguns dados básicos sobre os países do mundo. Ele é, na verdade, útil por si só e pode ser usado como base para construir algo mais sofisticado.

## Objetivos do Esboço

Seja qual for o seu projeto, você deve começar com um esboço de seus objetivos e talvez se perguntar se esses objetivos podem ser alcançados com os componentes principais do Joomla ou uma extensão disponível. Para o com_countrybase, é necessário uma tabela de dados de países, juntamente com páginas de entrada e saída. E talvez um módulo para exibir uma taxa de câmbio monetária diária. E até um plugin chamado por um comando cli para atualizar dados de câmbio em intervalos regulares. Este tutorial cobre apenas o componente.

O componente precisa de uma tabela de banco de dados para armazenar dados de países e uma tabela para armazenar dados de moedas. Cada uma precisará de uma visualização de lista e uma visualização de edição. Isso não é algo que possa ser realizado com componentes principais do Joomla, então é claramente um caso para um componente personalizado.

## Tabelas Iniciais

Há muitos dados sobre países disponíveis de diversas fontes e em diversos formatos. Como existem pelo menos 250 países no mundo, inserir dados para cada país um por um usando um formulário de entrada de dados seria bastante tedioso. Assim, preparei tabelas iniciais coletando dados de várias fontes, combinando-os em uma planilha e depois exportando instruções sql para criar as tabelas.

Os dados são baseados nos Códigos de País ISO 3166, mas alguns países muito conhecidos não estão incluídos, por exemplo, Inglaterra, Escócia e País de Gales. Você não precisa se preocupar com isso. As tabelas são fornecidas com o componente com_countrybase.

Os arquivos para o componente com_countrybase estão disponíveis no GitHub. Você pode baixar um [ZIP](https://github.com/ceford/j4xdemos-com-countrybase/archive/refs/heads/master.zip) e instalá-lo para vê-lo funcionando no menu do Administrador. Crie um item de menu se desejar vê-lo funcionando no seu modelo de Site. Além disso, descompacte o arquivo zip no espaço de arquivos do seu projeto, não na árvore do seu site de teste, para examinar a estrutura dos arquivos do componente e o conteúdo dos arquivos com seu IDE ou editor de texto favorito.

## Captura de Tela

Esta lista de Administradores de Países tem cinco itens para minimizar o tamanho da imagem. O Joomla normalmente exibe 20 itens.

![List of countries](../../../en/images/mvc-anatomy/com-countrybase-countries.png)

## Componente Boilerplate

Para ajudá-lo a começar com seu próprio componente, há um [componente modelo](https://github.com/ceford/j4xdemos-com-bpsrc/archive/refs/heads/master.zip) disponível no Github. Baixe e descompacte isso no espaço de arquivos do seu projeto, não na árvore do seu site de teste. Após o download, faça todas as alterações indicadas no README e você estará pronto para começar.

Há também vários geradores de extensões gratuitos e comerciais que você pode querer experimentar para gerar um componente esqueleto para seus próprios propósitos. O [Joomla! Component Builder](https://www.joomlacomponentbuilder.com/) é gratuito e parece abrangente.

*Traduzido por openai.com*

