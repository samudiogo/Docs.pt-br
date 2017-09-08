---
title: "Migrando configuração"
author: ardalis
description: 
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 8468d859-ff32-4a92-9e62-08c4a9e36594
ms.technology: aspnet
ms.prod: asp.net-core
uid: migration/configuration
ms.openlocfilehash: f19a8389bd8c4035292306216522994b1dbdc506
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/11/2017
---
# <a name="migrating-configuration"></a><span data-ttu-id="92d89-103">Migrando configuração</span><span class="sxs-lookup"><span data-stu-id="92d89-103">Migrating Configuration</span></span>

<span data-ttu-id="92d89-104">Por [Steve Smith](http://ardalis.com) e [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="92d89-104">By [Steve Smith](http://ardalis.com) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="92d89-105">O artigo anterior, começamos [migrando um projeto ASP.NET MVC para MVC do ASP.NET Core](mvc.md).</span><span class="sxs-lookup"><span data-stu-id="92d89-105">In the previous article, we began [migrating an ASP.NET MVC project to ASP.NET Core MVC](mvc.md).</span></span> <span data-ttu-id="92d89-106">Neste artigo, vamos migrar a configuração.</span><span class="sxs-lookup"><span data-stu-id="92d89-106">In this article, we migrate configuration.</span></span>

[<span data-ttu-id="92d89-107">Exibir ou baixar o código de exemplo</span><span class="sxs-lookup"><span data-stu-id="92d89-107">View or download sample code</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/configuration/samples)

## <a name="setup-configuration"></a><span data-ttu-id="92d89-108">Configuração da instalação</span><span class="sxs-lookup"><span data-stu-id="92d89-108">Setup Configuration</span></span>

<span data-ttu-id="92d89-109">ASP.NET Core não usa mais o *global. asax* e *Web. config* arquivos utilizadas de versões anteriores do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="92d89-109">ASP.NET Core no longer uses the *Global.asax* and *web.config* files that previous versions of ASP.NET utilized.</span></span> <span data-ttu-id="92d89-110">Em versões anteriores do ASP.NET, a lógica de inicialização do aplicativo foi colocada em uma `Application_StartUp` método *global. asax*.</span><span class="sxs-lookup"><span data-stu-id="92d89-110">In earlier versions of ASP.NET, application startup logic was placed in an `Application_StartUp` method within *Global.asax*.</span></span> <span data-ttu-id="92d89-111">Posteriormente, no ASP.NET MVC, um *Startup.cs* arquivo foi incluído na raiz do projeto; e ele foi chamado quando o aplicativo foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="92d89-111">Later, in ASP.NET MVC, a *Startup.cs* file was included in the root of the project; and, it was called when the application started.</span></span> <span data-ttu-id="92d89-112">ASP.NET Core adotou essa abordagem completamente colocando toda lógica de inicialização no *Startup.cs* arquivo.</span><span class="sxs-lookup"><span data-stu-id="92d89-112">ASP.NET Core has adopted this approach completely by placing all startup logic in the *Startup.cs* file.</span></span>

<span data-ttu-id="92d89-113">O *Web. config* arquivo também foi substituído no núcleo do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="92d89-113">The *web.config* file has also been replaced in ASP.NET Core.</span></span> <span data-ttu-id="92d89-114">Configuração propriamente dita agora pode ser configurada como parte do procedimento de inicialização de aplicativo descrito em *Startup.cs*.</span><span class="sxs-lookup"><span data-stu-id="92d89-114">Configuration itself can now be configured, as part of the application startup procedure described in *Startup.cs*.</span></span> <span data-ttu-id="92d89-115">Configuração ainda pode utilizar para arquivos XML, mas normalmente projetos do ASP.NET Core colocará os valores de configuração em um arquivo no formato JSON, como *appSettings. JSON*.</span><span class="sxs-lookup"><span data-stu-id="92d89-115">Configuration can still utilize XML files, but typically ASP.NET Core projects will place configuration values in a JSON-formatted file, such as *appsettings.json*.</span></span> <span data-ttu-id="92d89-116">Sistema de configuração do ASP.NET Core pode acessar facilmente as variáveis de ambiente, que podem fornecer um local mais seguro e robusto para valores específicos do ambiente.</span><span class="sxs-lookup"><span data-stu-id="92d89-116">ASP.NET Core's configuration system can also easily access environment variables, which can provide a more secure and robust location for environment-specific values.</span></span> <span data-ttu-id="92d89-117">Isso é especialmente verdadeiro para segredos, como cadeias de caracteres de conexão e chaves de API que não devem ser verificadas no controle de origem.</span><span class="sxs-lookup"><span data-stu-id="92d89-117">This is especially true for secrets like connection strings and API keys that should not be checked into source control.</span></span> <span data-ttu-id="92d89-118">Consulte [configuração](../fundamentals/configuration.md) para saber mais sobre a configuração no núcleo do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="92d89-118">See [Configuration](../fundamentals/configuration.md) to learn more about configuration in ASP.NET Core.</span></span>

<span data-ttu-id="92d89-119">Neste artigo, estamos começando com o projeto do ASP.NET Core parcialmente migrados de [artigo anterior](mvc.md).</span><span class="sxs-lookup"><span data-stu-id="92d89-119">For this article, we are starting with the partially-migrated ASP.NET Core project from [the previous article](mvc.md).</span></span> <span data-ttu-id="92d89-120">Para configurar a configuração, adicione o seguinte construtor e propriedade para o *Startup.cs* arquivo localizado na raiz do projeto:</span><span class="sxs-lookup"><span data-stu-id="92d89-120">To setup configuration, add the following constructor and property to the *Startup.cs* file located in the root of the project:</span></span>

<span data-ttu-id="92d89-121">[!code-csharp[Main](configuration/samples/WebApp1/src/WebApp1/Startup.cs?range=11-21)]</span><span class="sxs-lookup"><span data-stu-id="92d89-121">[!code-csharp[Main](configuration/samples/WebApp1/src/WebApp1/Startup.cs?range=11-21)]</span></span>

<span data-ttu-id="92d89-122">Observe que neste ponto, o *Startup.cs* arquivo não será compilado, pois precisamos adicionar o seguinte `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="92d89-122">Note that at this point, the *Startup.cs* file will not compile, as we still need to add the following `using` statement:</span></span>

```csharp
using Microsoft.Extensions.Configuration;
```

<span data-ttu-id="92d89-123">Adicionar uma *appSettings. JSON* arquivo para a raiz do projeto usando o modelo de item apropriado:</span><span class="sxs-lookup"><span data-stu-id="92d89-123">Add an *appsettings.json* file to the root of the project using the appropriate item template:</span></span>

![Adicionar AppSettings JSON](configuration/_static/add-appsettings-json.png)

## <a name="migrate-configuration-settings-from-webconfig"></a><span data-ttu-id="92d89-125">Migrar configurações de Web. config</span><span class="sxs-lookup"><span data-stu-id="92d89-125">Migrate Configuration Settings from web.config</span></span>

<span data-ttu-id="92d89-126">Nosso projeto ASP.NET MVC incluído a cadeia de caracteres de conexão de banco de dados necessários no *Web. config*, além de `<connectionStrings>` elemento.</span><span class="sxs-lookup"><span data-stu-id="92d89-126">Our ASP.NET MVC project included the required database connection string in *web.config*, in the `<connectionStrings>` element.</span></span> <span data-ttu-id="92d89-127">Em nosso projeto do ASP.NET Core, vamos armazenar essas informações no *appSettings. JSON* arquivo.</span><span class="sxs-lookup"><span data-stu-id="92d89-127">In our ASP.NET Core project, we are going to store this information in the *appsettings.json* file.</span></span> <span data-ttu-id="92d89-128">Abra *appSettings. JSON*e observe que ele já inclui o seguinte:</span><span class="sxs-lookup"><span data-stu-id="92d89-128">Open *appsettings.json*, and note that it already includes the following:</span></span>

<span data-ttu-id="92d89-129">[!code-json[Main](../migration/configuration/samples/WebApp1/src/WebApp1/appsettings.json?highlight=4)]</span><span class="sxs-lookup"><span data-stu-id="92d89-129">[!code-json[Main](../migration/configuration/samples/WebApp1/src/WebApp1/appsettings.json?highlight=4)]</span></span>


<span data-ttu-id="92d89-130">Na linha realçada descrita acima, altere o nome do banco de dados **_CHANGE_ME** para o nome do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="92d89-130">In the highlighted line depicted above, change the name of the database from **_CHANGE_ME** to the name of your database.</span></span>

## <a name="summary"></a><span data-ttu-id="92d89-131">Resumo</span><span class="sxs-lookup"><span data-stu-id="92d89-131">Summary</span></span>

<span data-ttu-id="92d89-132">ASP.NET Core coloca toda a lógica de inicialização para o aplicativo em um único arquivo, no qual os serviços necessários e dependências podem ser definidas e configuradas.</span><span class="sxs-lookup"><span data-stu-id="92d89-132">ASP.NET Core places all startup logic for the application in a single file, in which the necessary services and dependencies can be defined and configured.</span></span> <span data-ttu-id="92d89-133">Ele substitui o *Web. config* arquivo com um recurso de configuração flexíveis que pode aproveitar uma variedade de formatos de arquivo, como JSON, bem como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="92d89-133">It replaces the *web.config* file with a flexible configuration feature that can leverage a variety of file formats, such as JSON, as well as environment variables.</span></span>