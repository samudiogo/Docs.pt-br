---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: "Introdução ao ASP.NET Web API 2 (c#)"
author: MikeWasson
description: "HTTP não é apenas para serviços de páginas da web. Também é uma plataforma poderosa para a criação de APIs que expõem os dados e serviços. O HTTP é simples, flexível e ubiq..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/28/2017
ms.topic: article
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: fa1cd068a7466e0b6b6fe7716090c8a7afd2a4d5
ms.sourcegitcommit: ec9371e2fbfcb8d62e7e7cae69e7752f3f205385
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2017
---
<a name="getting-started-with-aspnet-web-api-2-c"></a>Introdução ao ASP.NET Web API 2 (c#)
====================
por [Mike Wasson](https://github.com/MikeWasson)

[Baixe o projeto concluído](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

HTTP não é apenas para serviços de páginas da web. HTTP também é uma plataforma poderosa para a criação de APIs que expõem os dados e serviços. O HTTP é simples, flexível e de todos os lugares. Praticamente qualquer plataforma que você pode pensar tem uma biblioteca HTTP para que serviços HTTP podem atingir uma ampla gama de clientes, incluindo navegadores, dispositivos móveis e aplicativos de área de trabalho tradicionais.
 
A API Web ASP.NET é uma estrutura para a criação de APIs Web sobre o .NET Framework. Neste tutorial, você usará a API Web ASP.NET para criar uma API Web que retorna uma lista de produtos. 

 
 ## <a name="software-versions-used-in-the-tutorial"></a>Versões de software usadas no tutorial
  
 - [Visual Studio 2017](https://www.visualstudio.com/downloads/)
 - Web API 2

Consulte [criar uma API Web com o Visual Studio para Windows e o ASP.NET Core](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) para ver uma versão mais recente deste tutorial. 

## <a name="create-a-web-api-project"></a>Criar um projeto de API da Web

Neste tutorial, você usará a API Web ASP.NET para criar uma API Web que retorna uma lista de produtos. A página da Web front-end usa jQuery para exibir os resultados. 

![](tutorial-your-first-web-api/_static/image1.png)

Inicie o Visual Studio e selecione **Novo projeto** na página **Iniciar**. Ou, no menu **Arquivo**, selecione **Novo** e, em seguida, **Projeto**. 

No painel **Modelos**, selecione **Modelos Instalados** e expanda o nó **Visual C#**. Em **Visual C#**, selecione **Web**. Na lista de modelos de projeto, selecione **Aplicativo Web ASP.NET**. Dê ao projeto o nome de "ProductsApp" e clique em **OK**. 

![](tutorial-your-first-web-api/_static/image2.png)

Na caixa de diálogo **Novo Aplicativo Web ASP.NET**, selecione o modelo **Vazio**. Em &quot;adicionar pastas e referências de núcleo&quot;, verifique **Web API**. Clique em **OK**.

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> Você também pode criar um projeto de Web API usando o modelo &quot;Web API&quot;. O modelo de Web API usa o ASP.NET MVC para fornecer páginas de Ajuda da API. Estou usando o modelo vazio para este tutorial porque Mostrar Web API sem MVC. Em geral, você não precisa saber o ASP.NET MVC para usar a Web API.


## <a name="adding-a-model"></a>Adicionando um modelo

Um *modelo (model)* é um objeto que representa os dados em seu aplicativo. ASP.NET Web API pode serializar automaticamente seu modelo para outro formato, XML ou JSON, e, em seguida, gravar os dados serializados no corpo da mensagem de resposta HTTP. Como um cliente pode ler o formato de serialização, ele pode desserializar o objeto. A maioria dos clientes pode analisar XML ou JSON. Além disso, o cliente pode indicar qual formato ele deseja definindo o cabeçalho Accept na mensagem de solicitação HTTP.

Vamos começar criando um modelo simples que representa um produto.

Se o Gerenciador de Soluções não estiver visível, clique no menu **Exibir** e selecione **Gerenciador de Soluções**. No Gerenciador de Soluções, clique com o botão direito na pasta de modelos (Models). No menu de contexto, selecione **Adicionar** , em seguida, selecione **Classe**.

![](tutorial-your-first-web-api/_static/image4.png)

Nomeie a classe &quot;Produt&quot; (produto). Adicione as seguintes propriedades para a classe `Product`.

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a>Adicionando um controlador

Na Web API, um *controlador* (controller) é um objeto que manipula as solicitações HTTP. Vamos adicionar um controlador que pode retornar uma lista de produtos ou um único produto especificado por ID.

> [!NOTE]
> Se você tiver usado o ASP.NET MVC, você já está familiarizados com os controladores. Controladores de API da Web são semelhantes aos controladores MVC, mas herdam a classe **ApiController** em vez da classe **Controller**.

Em **Gerenciador de Soluções**, clique com o botão direito na pasta controllers (controladores). Selecione **Adicionar** e, em seguida, selecione **Controlador**.

![](tutorial-your-first-web-api/_static/image5.png)

Na caixa de diálogo **Adicionar scaffold**, selecione **Controlador de Web API - Vazio**. Clique em **Adicionar**.

![](tutorial-your-first-web-api/_static/image6.png)

Na caixa de diálogo **Adicionar controlador**, nomeie o controlador como &quot;ProductsController&quot;. Clique em **Adicionar**. 

![](tutorial-your-first-web-api/_static/image7.png)

O scaffolding cria um arquivo chamado ProductsController.cs na pasta controladores.

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> Não é necessário colocar os controladores em uma pasta chamada controladores. O nome da pasta é apenas uma maneira conveniente de organizar seus arquivos de origem.


Se esse arquivo não estiver aberto, clique duas vezes no arquivo para abri-lo. Substitua o código neste arquivo com o seguinte:

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

Para manter o exemplo simples, os produtos são armazenados em uma matriz fixa dentro da classe do controlador. É claro que, em um aplicativo real, você consulta um banco de dados ou usar outra fonte de dados externa.

O controlador define dois métodos que retornam produtos:

- O método `GetAllProducts` retorna a lista completa de produtos como um tipo **IEnumerable&lt;produto&gt;**. 
- O método `GetProduct` procura um único produto por sua ID. 

É só isso! Você está trabalhando em uma API Web. Cada método do controlador corresponde a um ou mais URIs: 

| Método do controlador | URI |
| --- | --- |
| GetAllProducts | produtos/api / |
| GetProduct | /API/produtos/*id* |

Para o método `GetProduct`, o *id* no URI é um espaço reservado. Por exemplo, para obter o produto com ID 5, o URI é `api/products/5`.

Para obter mais informações sobre como a API Web encaminha solicitações HTTP para os métodos do controlador, consulte [roteamento na API Web ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md). 

## <a name="calling-the-web-api-with-javascript-and-jquery"></a>Chamar a API Web com Javascript e jQuery 

Nesta seção, vamos adicionar uma página HTML que usa AJAX para chamar a API Web. Vamos usar jQuery para fazer chamadas AJAX e também para atualizar a página com os resultados.  

No Gerenciador de Soluções, clique com o botão direito e selecione **adicionar**, em seguida, selecione **Novo Item**.

![](tutorial-your-first-web-api/_static/image9.png)

Na caixa de diálogo **Adicionar Novo Item**, selecione o nó **Web** no **Visual C#** e, em seguida, selecione o item **Página HTML**. Nomeie a página &quot;index.html&quot;. 

![](tutorial-your-first-web-api/_static/image10.png)

Substitua tudo neste arquivo com o seguinte:

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

Há várias maneiras de obter jQuery. Neste exemplo, usei o [Microsoft Ajax CDN](../../../ajax/cdn/overview.md). Você também pode baixá-lo do [http://jquery.com/](http://jquery.com/), e o modelo de projeto ASP.NET "API Web" também inclui jQuery.

### <a name="getting-a-list-of-products"></a>Obtendo uma lista de produtos

Para obter uma lista de produtos, envie uma solicitação HTTP GET para &quot;/api/produtos&quot;.

A função jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) envia uma solicitação AJAX. A resposta contém uma matriz de objetos JSON. A função `done` especifica um retorno de chamada que é chamado quando a solicitação for bem-sucedida. No retorno de chamada, atualizamos o DOM com as informações de produto. 

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a>Um produto por ID

Para obter um produto por ID, envie uma solicitação HTTP GET para &quot;/api/produtos/*id*&quot;, onde *id* é a ID do produto.

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

Chamamos ainda `getJSON` para enviar a solicitação AJAX, mas desta vez colocamos a ID no URI de solicitação. A resposta dessa solicitação é uma representação JSON de um único produto.

## <a name="running-the-application"></a>Executando o aplicativo

Pressione F5 para iniciar a depuração do aplicativo. A página da web deve parecer com o seguinte:

![](tutorial-your-first-web-api/_static/image11.png)

Para obter um produto por ID, insira a ID e clique em Pesquisar:

![](tutorial-your-first-web-api/_static/image12.png)

Se você inserir uma ID inválida, o servidor retornará um erro HTTP:

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a>Usando a tecla F12 para exibir a solicitação e resposta HTTP

Quando você estiver trabalhando com um serviço HTTP, ele pode ser muito útil ver a solicitação HTTP e mensagens de solicitação. Você pode fazer isso usando as ferramentas de desenvolvedor F12 no Internet Explorer 9. No Internet Explorer 9, pressione **F12** para abrir as ferramentas. Clique na guia **rede** e pressione **iniciar captura**. Agora vá para a página da web e pressione **F5** para recarregar a página da web. Internet Explorer capturará o tráfego HTTP entre o navegador e o servidor web. O modo de exibição de resumo mostra todo o tráfego de rede para uma página:

![](tutorial-your-first-web-api/_static/image14.png)

Localize a entrada para o URI relativo "api/produtos /". Selecione esta opção e clique em **Acessar a exibição detalhada**. Na exibição detalhada, há guias para exibir os corpos e cabeçalhos de solicitação e resposta. Por exemplo, se você clicar na guia **Cabeçalhos de solicitação**, você pode ver que o cliente solicitou &quot;aplicativo/json&quot; no cabeçalho Aceitar. 

![](tutorial-your-first-web-api/_static/image15.png)

Se você clicar na guia de corpo de resposta, você pode ver como a lista de produtos foi serializada como JSON. Outros navegadores têm funcionalidade semelhante. Outra ferramenta útil é [Fiddler](http://www.fiddler2.com/fiddler2/), um web proxy de depuração. Você pode usar o Fiddler para exibir o tráfego HTTP e também para compor as solicitações HTTP, que lhe dá controle total sobre os cabeçalhos HTTP na solicitação.

## <a name="see-this-app-running-on-azure"></a>Consulte este aplicativo em execução no Azure

Você gostaria de ver o site concluído em execução como um aplicativo web em tempo real? Você pode implantar uma versão completa do aplicativo para sua conta do Azure, clicando no botão a seguir.

[![](http://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

Você precisa de uma conta do Azure para implantar essa solução no Azure. Se você não tiver uma conta, você tem as seguintes opções:

- [Abra uma conta do Azure gratuitamente](https://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604) -você obtém créditos você pode usar para experimentar os serviços do Azure pagos e mesmo depois que eles são usados até que você pode manter a conta e livre de usar os serviços do Azure.
- [Ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -assinatura do MSDN fornece créditos de cada mês em que você pode usar para os serviços do Azure pagos.

## <a name="next-steps"></a>Próximas etapas

- Para obter um exemplo mais completo de um serviço HTTP que dá suporte a ações de POST, PUT e DELETE e grava em um banco de dados, consulte [usando API Web 2 com o Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).
- Para obter mais informações sobre como criar aplicativos web flexível e responsivo sobre um serviço HTTP, consulte [único aplicativo de página ASP.NET](../../../single-page-application/index.md).
- Para obter informações sobre como implantar um projeto da web do Visual Studio para o serviço de aplicativo do Azure, consulte [criar um aplicativo web ASP.NET no serviço de aplicativo do Azure](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-get-started/).
