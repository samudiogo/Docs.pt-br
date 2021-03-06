---
title: Limitar o tempo de vida das cargas protegidos
author: rick-anderson
description: "Este documento explica como limitar o tempo de vida de uma carga protegido usando as APIs de proteção de dados ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/limited-lifetime-payloads
ms.openlocfilehash: 144097cd1551c1d0aece5df20ce01e14146a41d1
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="limiting-the-lifetime-of-protected-payloads"></a>Limitar o tempo de vida das cargas protegidos

Há cenários onde quer que o desenvolvedor do aplicativo para criar uma carga protegida que expira após um período de tempo definido. Por exemplo, a carga protegida pode representar um token de redefinição de senha que deve ser válido somente por uma hora. É certamente possível para o desenvolvedor criar seu próprio formato de carga que contém uma data de expiração incorporados e os desenvolvedores avançados talvez queira fazer isso mesmo assim, mas para a maioria dos desenvolvedores gerenciar esses expirações pode crescer entediante.

Para facilitar isso para nossos público de desenvolvedor, o pacote [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) contém APIs do utilitário para criar cargas expirarem automaticamente após um período de tempo definido. Essas APIs de suspensão do `ITimeLimitedDataProtector` tipo.

## <a name="api-usage"></a>Uso de API

O `ITimeLimitedDataProtector` interface é a interface principal para proteger e ao desproteger cargas de tempo limitado / expiração automática. Para criar uma instância de um `ITimeLimitedDataProtector`, você precisará de uma instância de uma expressão [IDataProtector](overview.md) construído com uma finalidade específica. Uma vez o `IDataProtector` instância estiver disponível, chame o `IDataProtector.ToTimeLimitedDataProtector` método de extensão para retornar um protetor com recursos internos de expiração.

`ITimeLimitedDataProtector`apresenta os seguintes métodos de extensão e de superfície de API:

* CreateProtector (objetivo de cadeia de caracteres): ITimeLimitedDataProtector - esta API é semelhante à existente `IDataProtectionProvider.CreateProtector` em que ele pode ser usado para criar [finalidade cadeias](purpose-strings.md) de um protetor de tempo limite de raiz.

* Proteger (byte [] texto sem formatação, expiração de DateTimeOffset): byte]

* Proteger (texto sem formatação do byte [], tempo de vida de TimeSpan): byte]

* Proteger (byte [] texto sem formatação): byte]

* Proteger (cadeia de caracteres em texto sem formatação, expiração de DateTimeOffset): cadeia de caracteres

* Proteger (texto sem formatação de cadeia de caracteres, tempo de vida de TimeSpan): cadeia de caracteres

* Proteger (cadeia de caracteres em texto sem formatação): cadeia de caracteres

Além das principais `Protect` métodos que levam apenas o texto não criptografado, não há novas sobrecargas que permitem especificar a data de validade da carga. A data de validade pode ser especificada como uma data absoluta (por meio de um `DateTimeOffset`) ou como uma hora relativa (do sistema atual de tempo, por meio de um `TimeSpan`). Se uma sobrecarga que não tem uma expiração é chamada, a carga será considerada nunca para expirar.

* Desproteger (byte [] protectedData, limite de expiração de DateTimeOffset): byte]

* Desproteger (byte [] protectedData): byte]

* Desproteger (protectedData de cadeia de caracteres, limite de expiração de DateTimeOffset): cadeia de caracteres

* Desproteger (cadeia de caracteres protectedData): cadeia de caracteres

O `Unprotect` métodos retornam os dados desprotegidos originais. Se a carga ainda não tiver expirado, a expiração absoluta é retornada como um parâmetro junto com os dados desprotegidos originais out opcional. Se a carga tiver expirada, todas as sobrecargas do método Desproteger lançará CryptographicException.

>[!WARNING]
> Não é recomendável usar essas APIs para proteger cargas que requerem a persistência de longo prazo ou indefinida. "Pode suportar para as cargas protegidas sejam irrecuperáveis permanentemente após um mês?" pode servir como uma boa regra prática; Se a resposta for nenhum desenvolvedores, em seguida, considere APIs alternativas.

O exemplo abaixo usa o [caminhos de código não DI](../configuration/non-di-scenarios.md) para instanciar o sistema de proteção de dados. Para executar este exemplo, certifique-se de que você adicionou uma referência ao pacote Microsoft.AspNetCore.DataProtection.Extensions primeiro.

[!code-csharp[Main](limited-lifetime-payloads/samples/limitedlifetimepayloads.cs)]
