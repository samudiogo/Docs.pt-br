---
title: "Introdução ao ASP.NET Core MVC e ao Visual Studio para Mac"
author: rick-anderson
description: "Introdução ao ASP.NET Core MVC e ao Visual Studio"
ms.author: riande
manager: wpickett
ms.date: 8/23/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app-mac/start-mvc
ms.openlocfilehash: 51c0477c40885d3aaaa7562f8baba0a94cb4f920
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-with-aspnet-core-mvc-and-visual-studio-for-mac"></a>Introdução ao ASP.NET Core MVC e ao Visual Studio para Mac

Por [Rick Anderson](https://twitter.com/RickAndMSFT)

Este tutorial ensina os conceitos básicos da criação de um aplicativo Web ASP.NET Core MVC usando o [Visual Studio para Mac](https://www.visualstudio.com/vs/visual-studio-mac/). 

[!INCLUDE[consider RP](../../includes/razor.md)]

Há três versões deste tutorial:

* macOS: [Compilar um aplicativo ASP.NET Core MVC com o Visual Studio para Mac](xref:tutorials/first-mvc-app-mac/start-mvc)
* Windows: [Compilar um aplicativo ASP.NET Core MVC com o Visual Studio](xref:tutorials/first-mvc-app/start-mvc)
* Linux, macOS e Windows: [Compilar um aplicativo ASP.NET Core MVC com o Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial exige o [SDK do .NET Core 2.0.0](https://www.microsoft.com/net/core) ou posterior.

Instale o seguinte:

- [SDK do .NET Core 2.0.0](https://www.microsoft.com/net/core) ou posterior
- [Visual Studio para Mac](https://www.visualstudio.com/vs/visual-studio-mac/)

## <a name="create-a-web-app"></a>Criar um aplicativo Web

No Visual Studio, selecione **Arquivo > Nova Solução**.

![Nova solução do macOS](../first-web-api-mac/_static/sln.png)

Selecione **Aplicativo .NET Core > ASP.NET Core > Aplicativo Web > Avançar**.

![Caixa de diálogo Novo projeto do macOS](start-mvc/1.png)

Nomeie o projeto **MvcMovie** e, em seguida, selecione **Criar**.

![Caixa de diálogo Novo projeto do macOS](start-mvc/2.png)

### <a name="launch-the-app"></a>Iniciar o aplicativo

No Visual Studio, selecione **Executar > Iniciar Sem Depuração** para iniciar o aplicativo. O Visual Studio inicia o [Kestrel](xref:fundamentals/servers/index#kestrel), inicia um navegador e navega para `http://localhost:port`, em que *porta* é um número da porta escolhido aleatoriamente.

![Navegador com novo projeto](start-mvc/b1.png)

* A barra de endereços mostra `localhost:port#` e não algo como `example.com`. Isso ocorre porque `localhost` é o nome do host padrão do computador local. Quando o Visual Studio cria um projeto Web, uma porta aleatória é usada para o servidor Web. Quando você executar o aplicativo, verá um número da porta diferente.
* Você pode iniciar o aplicativo no modo de depuração ou sem depuração no item de menu **Executar**.

O modelo padrão fornece os links **Página Inicial, Sobre** e **Contato**. A imagem do navegador acima não mostra esses links. Dependendo do tamanho do navegador, talvez você precise clicar no ícone de navegação para mostrá-los.

![Navegador com Novo projeto](start-mvc/b2.png)

Na próxima parte deste tutorial, você saberá mais sobre o MVC e começará a escrever um pouco de código.

>[!div class="step-by-step"]
[Avançar](adding-controller.md)  
