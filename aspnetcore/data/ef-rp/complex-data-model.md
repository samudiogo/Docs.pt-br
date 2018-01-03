---
title: "Páginas Razor com núcleo EF – modelo de dados - 5 de 8"
author: rick-anderson
description: "Neste tutorial, você adiciona mais entidades e relações e personalizar o modelo de dados especificando a formatação, validação e regras de mapeamento de banco de dados."
keywords: "Anotações de dados do ASP.NET Core, Entity Framework Core,"
ms.author: riande
manager: wpickett
ms.date: 10/25/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/complex-data-model
ms.openlocfilehash: c2761f79fa4836d29541526782969bb0fd47778b
ms.sourcegitcommit: 6e46abd65973dea796d364a514de9ec2e3e1c1ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2017
---
# <a name="creating-a-complex-data-model---ef-core-with-razor-pages-tutorial-5-of-8"></a><span data-ttu-id="fd235-104">Criar um modelo de dados complexos - Core EF com tutorial páginas Razor (5 de 8)</span><span class="sxs-lookup"><span data-stu-id="fd235-104">Creating a complex data model - EF Core with Razor Pages tutorial (5 of 8)</span></span>

<span data-ttu-id="fd235-105">Por [Tom Dykstra](https://github.com/tdykstra) e [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="fd235-105">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="fd235-106">Os tutoriais anteriores trabalharam com um modelo de dados básico composto de três entidades.</span><span class="sxs-lookup"><span data-stu-id="fd235-106">The previous tutorials worked with a basic data model that was composed of three entities.</span></span> <span data-ttu-id="fd235-107">Neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="fd235-107">In this tutorial:</span></span>

* <span data-ttu-id="fd235-108">Mais de entidades e relações são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="fd235-108">More entities and relationships are added.</span></span>
* <span data-ttu-id="fd235-109">O modelo de dados é personalizado com a especificação de formatação, validação e regras de mapeamento de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-109">The data model is customized by specifying formatting, validation, and database mapping rules.</span></span>

<span data-ttu-id="fd235-110">As classes de entidade para o modelo de dados completo é mostrado na ilustração a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-110">The entity classes for the completed data model is shown in the following illustration:</span></span>

![Diagrama de entidade](complex-data-model/_static/diagram.png)

<span data-ttu-id="fd235-112">Se você tiver problemas, você não conseguir resolver, baixe o [aplicativo concluído para este estágio](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part5-complex).</span><span class="sxs-lookup"><span data-stu-id="fd235-112">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part5-complex).</span></span>

## <a name="customize-the-data-model-with-attributes"></a><span data-ttu-id="fd235-113">Personalizar o modelo de dados com atributos</span><span class="sxs-lookup"><span data-stu-id="fd235-113">Customize the data model with attributes</span></span>

<span data-ttu-id="fd235-114">Nesta seção, o modelo de dados personalizado usando atributos.</span><span class="sxs-lookup"><span data-stu-id="fd235-114">In this section, the data model is customized using attributes.</span></span>

### <a name="the-datatype-attribute"></a><span data-ttu-id="fd235-115">O atributo de tipo de dados</span><span class="sxs-lookup"><span data-stu-id="fd235-115">The DataType attribute</span></span>

<span data-ttu-id="fd235-116">As páginas do aluno atualmente exibe a hora da data de registro.</span><span class="sxs-lookup"><span data-stu-id="fd235-116">The student pages currently displays the time of the enrollment date.</span></span> <span data-ttu-id="fd235-117">Normalmente, os campos de data mostram apenas a data e não o tempo.</span><span class="sxs-lookup"><span data-stu-id="fd235-117">Typically, date fields show only the date and not the time.</span></span>

<span data-ttu-id="fd235-118">Atualização *Models/Student.cs* com o seguinte realçado código:</span><span class="sxs-lookup"><span data-stu-id="fd235-118">Update *Models/Student.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_DataType&highlight=3,12-13)]

<span data-ttu-id="fd235-119">O [DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1) atributo especifica um tipo de dados que é mais específico que o tipo de banco de dados intrínseco.</span><span class="sxs-lookup"><span data-stu-id="fd235-119">The [DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1) attribute specifies a data type that is more specific than the database intrinsic type.</span></span> <span data-ttu-id="fd235-120">Neste caso, que apenas a data deve ser exibida, não a data e hora.</span><span class="sxs-lookup"><span data-stu-id="fd235-120">In this case only the date should be displayed, not the date and time.</span></span> <span data-ttu-id="fd235-121">O [enumeração DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1) fornece para muitos tipos de dados, como data, hora, PhoneNumber, moeda, endereço de email, etc. O `DataType` atributo também pode habilitar o aplicativo fornecer automaticamente os recursos de um tipo específico.</span><span class="sxs-lookup"><span data-stu-id="fd235-121">The [DataType Enumeration](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1) provides for many data types, such as Date, Time, PhoneNumber, Currency, EmailAddress, etc. The `DataType` attribute can also enable the app to automatically provide type-specific features.</span></span> <span data-ttu-id="fd235-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fd235-122">For example:</span></span>

* <span data-ttu-id="fd235-123">O `mailto:` link é criado automaticamente para `DataType.EmailAddress`.</span><span class="sxs-lookup"><span data-stu-id="fd235-123">The `mailto:` link is automatically created for `DataType.EmailAddress`.</span></span>
* <span data-ttu-id="fd235-124">O seletor de data é fornecido para `DataType.Date` na maioria dos navegadores.</span><span class="sxs-lookup"><span data-stu-id="fd235-124">The date selector is provided for `DataType.Date` in most browsers.</span></span>

<span data-ttu-id="fd235-125">O `DataType` atributo emite HTML 5 `data-` atributos (pronunciado dados dash) que consomem os navegadores HTML 5.</span><span class="sxs-lookup"><span data-stu-id="fd235-125">The `DataType` attribute emits HTML 5 `data-` (pronounced data dash) attributes that HTML 5 browsers consume.</span></span> <span data-ttu-id="fd235-126">O `DataType` atributos não fornecem validação.</span><span class="sxs-lookup"><span data-stu-id="fd235-126">The `DataType` attributes do not provide validation.</span></span>

<span data-ttu-id="fd235-127">`DataType.Date` não especifica o formato da data exibida.</span><span class="sxs-lookup"><span data-stu-id="fd235-127">`DataType.Date` does not specify the format of the date that is displayed.</span></span> <span data-ttu-id="fd235-128">Por padrão, o campo de data será exibido conforme os formatos padrão com base no servidor de [CultureInfo](https://docs.microsoft.com/aspnet/core/fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support).</span><span class="sxs-lookup"><span data-stu-id="fd235-128">By default, the date field is displayed according to the default formats based on the server's [CultureInfo](https://docs.microsoft.com/aspnet/core/fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support).</span></span>

<span data-ttu-id="fd235-129">O atributo `DisplayFormat` é usado para especificar explicitamente o formato de data:</span><span class="sxs-lookup"><span data-stu-id="fd235-129">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

<span data-ttu-id="fd235-130">O `ApplyFormatInEditMode` configuração especifica que a formatação também deve ser aplicada para a edição da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="fd235-130">The `ApplyFormatInEditMode` setting specifies that the formatting should also be applied to the edit UI.</span></span> <span data-ttu-id="fd235-131">Alguns campos não devem usar `ApplyFormatInEditMode`.</span><span class="sxs-lookup"><span data-stu-id="fd235-131">Some fields should not use `ApplyFormatInEditMode`.</span></span> <span data-ttu-id="fd235-132">Por exemplo, o símbolo de moeda deve geralmente não ser exibido em uma caixa de texto de edição.</span><span class="sxs-lookup"><span data-stu-id="fd235-132">For example, the currency symbol should generally not be displayed in an edit text box.</span></span>

<span data-ttu-id="fd235-133">O `DisplayFormat` atributo pode ser usado por si só.</span><span class="sxs-lookup"><span data-stu-id="fd235-133">The `DisplayFormat` attribute can be used by itself.</span></span> <span data-ttu-id="fd235-134">Geralmente, é recomendável usar o `DataType` atributo com o `DisplayFormat` atributo.</span><span class="sxs-lookup"><span data-stu-id="fd235-134">It's generally a good idea to use the `DataType` attribute with the `DisplayFormat` attribute.</span></span> <span data-ttu-id="fd235-135">O `DataType` atributo transmite a semântica dos dados em vez de como renderizá-lo em uma tela.</span><span class="sxs-lookup"><span data-stu-id="fd235-135">The `DataType` attribute conveys the semantics of the data as opposed to how to render it on a screen.</span></span> <span data-ttu-id="fd235-136">O `DataType` atributo fornece os seguintes benefícios que não estão disponíveis em `DisplayFormat`:</span><span class="sxs-lookup"><span data-stu-id="fd235-136">The `DataType` attribute provides the following benefits that are not available in `DisplayFormat`:</span></span>

* <span data-ttu-id="fd235-137">O navegador pode habilitar recursos do HTML5.</span><span class="sxs-lookup"><span data-stu-id="fd235-137">The browser can enable HTML5 features.</span></span> <span data-ttu-id="fd235-138">Por exemplo, mostra um controle de calendário, o símbolo de moeda local apropriado, links de email, validação de entrada do lado do cliente, etc.</span><span class="sxs-lookup"><span data-stu-id="fd235-138">For example, show a calendar control, the locale-appropriate currency symbol, email links, client-side input validation, etc.</span></span>
* <span data-ttu-id="fd235-139">Por padrão, o navegador renderiza dados usando o formato correto com base na localidade.</span><span class="sxs-lookup"><span data-stu-id="fd235-139">By default, the browser renders data using the correct format based on the locale.</span></span>

<span data-ttu-id="fd235-140">Para obter mais informações, consulte o [ \<entrada > documentação do auxiliar de marca](xref:mvc/views/working-with-forms#the-input-tag-helper).</span><span class="sxs-lookup"><span data-stu-id="fd235-140">For more information, see the [\<input> Tag Helper documentation](xref:mvc/views/working-with-forms#the-input-tag-helper).</span></span>

<span data-ttu-id="fd235-141">Execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd235-141">Run the app.</span></span> <span data-ttu-id="fd235-142">Navegue até a página de índice de alunos.</span><span class="sxs-lookup"><span data-stu-id="fd235-142">Navigate to the Students Index page.</span></span> <span data-ttu-id="fd235-143">Vezes não são mais exibidos.</span><span class="sxs-lookup"><span data-stu-id="fd235-143">Times are no longer displayed.</span></span> <span data-ttu-id="fd235-144">Cada modo de exibição que usa o `Student` modelo exibe a data sem tempo.</span><span class="sxs-lookup"><span data-stu-id="fd235-144">Every view that uses the `Student` model displays the date without time.</span></span>

![Página de índice de alunos mostrando datas sem vezes](complex-data-model/_static/dates-no-times.png)

### <a name="the-stringlength-attribute"></a><span data-ttu-id="fd235-146">O atributo StringLength</span><span class="sxs-lookup"><span data-stu-id="fd235-146">The StringLength attribute</span></span>

<span data-ttu-id="fd235-147">Regras de validação de dados e mensagens de erro de validação podem ser especificadas com atributos.</span><span class="sxs-lookup"><span data-stu-id="fd235-147">Data validation rules and validation error messages can be specified with attributes.</span></span> <span data-ttu-id="fd235-148">O [StringLength](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1) atributo especifica o comprimento mínimo e máximo de caracteres que são permitidos em um campo de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-148">The [StringLength](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1) attribute specifies the minimum and maximum length of characters that are allowed in a data field.</span></span> <span data-ttu-id="fd235-149">O `StringLength` atributo também fornece a validação do lado do cliente e do servidor.</span><span class="sxs-lookup"><span data-stu-id="fd235-149">The `StringLength` attribute also provides client-side and server-side validation.</span></span> <span data-ttu-id="fd235-150">O valor mínimo não tem impacto sobre o esquema de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-150">The minimum value has no impact on the database schema.</span></span>

<span data-ttu-id="fd235-151">Atualização de `Student` modelo com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-151">Update the `Student` model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_StringLength&highlight=10,12)]

<span data-ttu-id="fd235-152">O código anterior limita os nomes a não mais que 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="fd235-152">The preceding code limits names to no more than 50 characters.</span></span> <span data-ttu-id="fd235-153">O `StringLength` atributo não impede que um usuário inserir espaços em branco para um nome.</span><span class="sxs-lookup"><span data-stu-id="fd235-153">The `StringLength` attribute doesn't prevent a user from entering white space for a name.</span></span> <span data-ttu-id="fd235-154">O [RegularExpression](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1) atributo é usado para aplicar restrições para a entrada.</span><span class="sxs-lookup"><span data-stu-id="fd235-154">The [RegularExpression](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1) attribute is used to apply restrictions to the input.</span></span> <span data-ttu-id="fd235-155">Por exemplo, o código a seguir exige que o primeiro caractere a ser maiuscula e os caracteres restantes para estar em ordem alfabética:</span><span class="sxs-lookup"><span data-stu-id="fd235-155">For example, the following code requires the first character to be upper case and the remaining characters to be alphabetical:</span></span>

```csharp
[RegularExpression(@"^[A-Z]+[a-zA-Z''-'\s]*$")]
```

<span data-ttu-id="fd235-156">Execute o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="fd235-156">Run the app:</span></span>

* <span data-ttu-id="fd235-157">Navegue até a página de alunos.</span><span class="sxs-lookup"><span data-stu-id="fd235-157">Navigate to the Students page.</span></span>
* <span data-ttu-id="fd235-158">Selecione **criar novo**e digite um nome mais de 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="fd235-158">Select **Create New**, and enter a name longer than 50 characters.</span></span>
* <span data-ttu-id="fd235-159">Selecione **criar**, validação do lado do cliente mostra uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="fd235-159">Select **Create**, client-side validation shows an error message.</span></span>

![Os alunos mostrando erros de comprimento de cadeia de caracteres de página de índice](complex-data-model/_static/string-length-errors.png)

<span data-ttu-id="fd235-161">Em **Pesquisador de objetos do SQL Server** (SSOX), abra o designer de tabela do aluno clicando duas vezes o **aluno** tabela.</span><span class="sxs-lookup"><span data-stu-id="fd235-161">In **SQL Server Object Explorer** (SSOX), open the Student table designer by double-clicking the **Student** table.</span></span>

![Tabela de alunos em SSOX antes da migração](complex-data-model/_static/ssox-before-migration.png)

<span data-ttu-id="fd235-163">A imagem anterior mostra o esquema para o `Student` tabela.</span><span class="sxs-lookup"><span data-stu-id="fd235-163">The preceding image shows the schema for the `Student` table.</span></span> <span data-ttu-id="fd235-164">Os campos nome tem tipo `nvarchar(MAX)` porque migrações não tiver sido executada no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-164">The name fields have type `nvarchar(MAX)` because migrations has not been run on the DB.</span></span> <span data-ttu-id="fd235-165">Quando as migrações são executadas em breve neste tutorial, os campos de nome se tornam `nvarchar(50)`.</span><span class="sxs-lookup"><span data-stu-id="fd235-165">When migrations are run later in this tutorial, the name fields become `nvarchar(50)`.</span></span>

### <a name="the-column-attribute"></a><span data-ttu-id="fd235-166">O atributo de coluna</span><span class="sxs-lookup"><span data-stu-id="fd235-166">The Column attribute</span></span>

<span data-ttu-id="fd235-167">Atributos podem controlar como as classes e propriedades são mapeadas para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-167">Attributes can control how classes and properties are mapped to the database.</span></span> <span data-ttu-id="fd235-168">Nesta seção, o `Column` atributo é usado para mapear o nome do `FirstMidName` propriedade como "FirstName" no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-168">In this section, the `Column` attribute is used to map the name of the `FirstMidName` property to "FirstName" in the DB.</span></span>

<span data-ttu-id="fd235-169">Quando o banco de dados é criado, os nomes de propriedade no modelo são usados para nomes de coluna (exceto quando o `Column` atributo é usado).</span><span class="sxs-lookup"><span data-stu-id="fd235-169">When the DB is created, property names on the model are used for column names (except when the `Column` attribute is used).</span></span>

<span data-ttu-id="fd235-170">O `Student` modelo usa `FirstMidName` para o nome do primeiro campo porque o campo também pode conter um nome do meio.</span><span class="sxs-lookup"><span data-stu-id="fd235-170">The `Student` model uses `FirstMidName` for the first-name field because the field might also contain a middle name.</span></span>

<span data-ttu-id="fd235-171">Atualização de *Student.cs* arquivo com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="fd235-171">Update the *Student.cs* file with the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Column&highlight=4,14)]

<span data-ttu-id="fd235-172">Com a alteração anterior, `Student.FirstMidName` no aplicativo mapeia para o `FirstName` coluna o `Student` tabela.</span><span class="sxs-lookup"><span data-stu-id="fd235-172">With the preceding change, `Student.FirstMidName` in the app maps to the `FirstName` column of the `Student` table.</span></span>

<span data-ttu-id="fd235-173">A adição do `Column` atributo altera o backup do modelo de `SchoolContext`.</span><span class="sxs-lookup"><span data-stu-id="fd235-173">The addition of the `Column` attribute changes the model backing the `SchoolContext`.</span></span> <span data-ttu-id="fd235-174">O backup do modelo de `SchoolContext` não coincide mais com o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-174">The model backing the `SchoolContext` no longer matches the database.</span></span> <span data-ttu-id="fd235-175">Se o aplicativo é executado antes de aplicar as migrações, a seguinte exceção será gerada:</span><span class="sxs-lookup"><span data-stu-id="fd235-175">If the app is run before applying migrations, the following exception is generated:</span></span>

```SQL
SqlException: Invalid column name 'FirstName'.
```
<span data-ttu-id="fd235-176">Para atualizar o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="fd235-176">To update the DB:</span></span>

* <span data-ttu-id="fd235-177">Compile o projeto.</span><span class="sxs-lookup"><span data-stu-id="fd235-177">Build the project.</span></span>
* <span data-ttu-id="fd235-178">Abra uma janela de comando na pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="fd235-178">Open a command window in the project folder.</span></span> <span data-ttu-id="fd235-179">Digite os comandos a seguir para criar uma nova migração e atualizar o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="fd235-179">Enter the following commands to create a new migration and update the DB:</span></span>

    ```console
    dotnet ef migrations add ColumnFirstName
    dotnet ef database update
    ```

<span data-ttu-id="fd235-180">O `dotnet ef migrations add ColumnFirstName` comando gera a seguinte mensagem de aviso:</span><span class="sxs-lookup"><span data-stu-id="fd235-180">The `dotnet ef migrations add ColumnFirstName` command generates the following warning message:</span></span>

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
```

<span data-ttu-id="fd235-181">O aviso é gerado porque os campos de nome agora estão limitado a 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="fd235-181">The warning is generated because the name fields are now limited to 50 characters.</span></span> <span data-ttu-id="fd235-182">Se um nome de banco de dados tiver mais de 50 caracteres, 51 último caractere seriam perdidos.</span><span class="sxs-lookup"><span data-stu-id="fd235-182">If a name in the DB had more than 50 characters, the 51 to last character would be lost.</span></span>

* <span data-ttu-id="fd235-183">Teste o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd235-183">Test the app.</span></span>

<span data-ttu-id="fd235-184">Abra a tabela de alunos em SSOX:</span><span class="sxs-lookup"><span data-stu-id="fd235-184">Open the Student table in SSOX:</span></span>

![Tabela de alunos em SSOX após a migração](complex-data-model/_static/ssox-after-migration.png)

<span data-ttu-id="fd235-186">Antes da migração foi aplicada, as colunas de nome forem do tipo [nvarchar (max)](https://docs.microsoft.com/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="fd235-186">Before migration was applied, the name columns were of type [nvarchar(MAX)](https://docs.microsoft.com/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql).</span></span> <span data-ttu-id="fd235-187">As colunas de nome agora são `nvarchar(50)`.</span><span class="sxs-lookup"><span data-stu-id="fd235-187">The name columns are now `nvarchar(50)`.</span></span> <span data-ttu-id="fd235-188">O nome da coluna foi alterado de `FirstMidName` para `FirstName`.</span><span class="sxs-lookup"><span data-stu-id="fd235-188">The column name has changed from `FirstMidName` to `FirstName`.</span></span>

> [!Note]
> <span data-ttu-id="fd235-189">Na seção a seguir, criar o aplicativo em alguns estágios gera erros de compilador.</span><span class="sxs-lookup"><span data-stu-id="fd235-189">In the following section, building the app at some stages generates compiler errors.</span></span> <span data-ttu-id="fd235-190">As instruções especifiquem quando compilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd235-190">The instructions specify when to build the app.</span></span>

## <a name="student-entity-update"></a><span data-ttu-id="fd235-191">Atualização da entidade aluno</span><span class="sxs-lookup"><span data-stu-id="fd235-191">Student entity update</span></span>

![Entidade do aluno](complex-data-model/_static/student-entity.png)

<span data-ttu-id="fd235-193">Atualização *Models/Student.cs* com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-193">Update *Models/Student.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_BeforeInheritance&highlight=11,13,15,18,22,24-31)]

### <a name="the-required-attribute"></a><span data-ttu-id="fd235-194">O atributo necessário</span><span class="sxs-lookup"><span data-stu-id="fd235-194">The Required attribute</span></span>

<span data-ttu-id="fd235-195">O `Required` atributo faz com que os campos obrigatórios de propriedades de nome.</span><span class="sxs-lookup"><span data-stu-id="fd235-195">The `Required` attribute makes the name properties required fields.</span></span> <span data-ttu-id="fd235-196">O `Required` atributo não é necessária para tipos não anuláveis, como tipos de valor (`DateTime`, `int`, `double`, etc.).</span><span class="sxs-lookup"><span data-stu-id="fd235-196">The `Required` attribute is not needed for non-nullable types such as value types (`DateTime`, `int`, `double`, etc.).</span></span> <span data-ttu-id="fd235-197">Tipos que não podem ser nulos automaticamente são tratados como campos obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="fd235-197">Types that can't be null are automatically treated as required fields.</span></span>

<span data-ttu-id="fd235-198">O `Required` atributo pode ser substituído com um parâmetro de comprimento mínimo de `StringLength` atributo:</span><span class="sxs-lookup"><span data-stu-id="fd235-198">The `Required` attribute could be replaced with a minimum length parameter in the `StringLength` attribute:</span></span>

```csharp
[Display(Name = "Last Name")]
[StringLength(50, MinimumLength=1)]
public string LastName { get; set; }
```

### <a name="the-display-attribute"></a><span data-ttu-id="fd235-199">O atributo de exibição</span><span class="sxs-lookup"><span data-stu-id="fd235-199">The Display attribute</span></span>

<span data-ttu-id="fd235-200">O `Display` atributo especifica que a legenda para as caixas de texto deve ser "Nome", "Sobrenome", "Nome completo" e "Data de inscrição".</span><span class="sxs-lookup"><span data-stu-id="fd235-200">The `Display` attribute specifies that the caption for the text boxes should be "First Name", "Last Name", "Full Name", and "Enrollment Date."</span></span> <span data-ttu-id="fd235-201">As legendas padrão não tinham dividindo as palavras, por exemplo, "Sobrenome".</span><span class="sxs-lookup"><span data-stu-id="fd235-201">The default captions had no space dividing the words, for example "Lastname."</span></span>

### <a name="the-fullname-calculated-property"></a><span data-ttu-id="fd235-202">A propriedade FullName calculada</span><span class="sxs-lookup"><span data-stu-id="fd235-202">The FullName calculated property</span></span>

<span data-ttu-id="fd235-203">`FullName`é uma propriedade calculada que retorna um valor que é criado pela concatenação de duas outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="fd235-203">`FullName` is a calculated property that returns a value that's created by concatenating two other properties.</span></span> <span data-ttu-id="fd235-204">`FullName`não pode ser definida, que ela tem um acessador get.</span><span class="sxs-lookup"><span data-stu-id="fd235-204">`FullName` cannot be set, it has only a get accessor.</span></span> <span data-ttu-id="fd235-205">Não `FullName` coluna é criada no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-205">No `FullName` column is created in the database.</span></span>

## <a name="create-the-instructor-entity"></a><span data-ttu-id="fd235-206">Criar a entidade do instrutor</span><span class="sxs-lookup"><span data-stu-id="fd235-206">Create the Instructor Entity</span></span>

![Entidade instrutor](complex-data-model/_static/instructor-entity.png)

<span data-ttu-id="fd235-208">Criar *Models/Instructor.cs* com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-208">Create *Models/Instructor.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Instructor.cs?name=snippet_BeforeInheritance)]

<span data-ttu-id="fd235-209">Observe que várias propriedades são os mesmos no `Student` e `Instructor` entidades.</span><span class="sxs-lookup"><span data-stu-id="fd235-209">Notice that several properties are the same in the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="fd235-210">No tutorial implementando herança posteriormente na série, esse código é refatorado para eliminar a redundância.</span><span class="sxs-lookup"><span data-stu-id="fd235-210">In the Implementing Inheritance tutorial later in this series, this code is refactored to eliminate the redundancy.</span></span>

<span data-ttu-id="fd235-211">Vários atributos podem estar em uma linha.</span><span class="sxs-lookup"><span data-stu-id="fd235-211">Multiple attributes can be on one line.</span></span> <span data-ttu-id="fd235-212">O `HireDate` atributos podem ser escritos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="fd235-212">The `HireDate` attributes could be written as follows:</span></span>

```csharp
[DataType(DataType.Date),Display(Name = "Hire Date"),DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

### <a name="the-courseassignments-and-officeassignment-navigation-properties"></a><span data-ttu-id="fd235-213">As propriedades de navegação CourseAssignments e OfficeAssignment</span><span class="sxs-lookup"><span data-stu-id="fd235-213">The CourseAssignments and OfficeAssignment navigation properties</span></span>

<span data-ttu-id="fd235-214">O `CourseAssignments` e `OfficeAssignment` propriedades são propriedades de navegação.</span><span class="sxs-lookup"><span data-stu-id="fd235-214">The `CourseAssignments` and `OfficeAssignment` properties are navigation properties.</span></span>

<span data-ttu-id="fd235-215">Um instrutor pode ensinar a qualquer número de cursos, portanto `CourseAssignments` é definido como uma coleção.</span><span class="sxs-lookup"><span data-stu-id="fd235-215">An instructor can teach any number of courses, so `CourseAssignments` is defined as a collection.</span></span>

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

<span data-ttu-id="fd235-216">Se uma propriedade de navegação contém várias entidades:</span><span class="sxs-lookup"><span data-stu-id="fd235-216">If a navigation property holds multiple entities:</span></span>

* <span data-ttu-id="fd235-217">Ele deve ser um tipo de lista onde as entradas podem ser adicionadas, excluídas e atualizadas.</span><span class="sxs-lookup"><span data-stu-id="fd235-217">It must be a list type where the entries can be added, deleted, and updated.</span></span>

<span data-ttu-id="fd235-218">Tipos de propriedade de navegação:</span><span class="sxs-lookup"><span data-stu-id="fd235-218">Navigation property types include:</span></span>

* `ICollection<T>`
*  `List<T>`
*  `HashSet<T>`

<span data-ttu-id="fd235-219">Se `ICollection<T>` for especificado, Core EF cria um `HashSet<T>` coleção por padrão.</span><span class="sxs-lookup"><span data-stu-id="fd235-219">If `ICollection<T>` is specified, EF Core creates a `HashSet<T>` collection by default.</span></span>

<span data-ttu-id="fd235-220">O `CourseAssignment` entidade é explicada na seção em relações muitos-para-muitos.</span><span class="sxs-lookup"><span data-stu-id="fd235-220">The `CourseAssignment` entity is explained in the section on many-to-many relationships.</span></span>

<span data-ttu-id="fd235-221">Estado que instrutor pode ter no máximo um escritório de regras de negócio de Contoso University.</span><span class="sxs-lookup"><span data-stu-id="fd235-221">Contoso University business rules state that an instructor can have at most one office.</span></span> <span data-ttu-id="fd235-222">O `OfficeAssignment` propriedade contém um único `OfficeAssignment` entidade.</span><span class="sxs-lookup"><span data-stu-id="fd235-222">The `OfficeAssignment` property holds a single `OfficeAssignment` entity.</span></span> <span data-ttu-id="fd235-223">`OfficeAssignment`será null se o office não está atribuído.</span><span class="sxs-lookup"><span data-stu-id="fd235-223">`OfficeAssignment` is null if no office is assigned.</span></span>

```csharp
public OfficeAssignment OfficeAssignment { get; set; }
```

## <a name="create-the-officeassignment-entity"></a><span data-ttu-id="fd235-224">Criar a entidade OfficeAssignment</span><span class="sxs-lookup"><span data-stu-id="fd235-224">Create the OfficeAssignment entity</span></span>

![Entidade OfficeAssignment](complex-data-model/_static/officeassignment-entity.png)

<span data-ttu-id="fd235-226">Criar *Models/OfficeAssignment.cs* com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-226">Create *Models/OfficeAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/OfficeAssignment.cs)]

### <a name="the-key-attribute"></a><span data-ttu-id="fd235-227">O atributo de chave</span><span class="sxs-lookup"><span data-stu-id="fd235-227">The Key attribute</span></span>

<span data-ttu-id="fd235-228">O `[Key]` atributo é usado para identificar uma propriedade como a chave primária (PK) quando o nome da propriedade é algo diferente de classnameID ou ID.</span><span class="sxs-lookup"><span data-stu-id="fd235-228">The `[Key]` attribute is used to identify a property as the primary key (PK) when the property name is something other than classnameID or ID.</span></span>

<span data-ttu-id="fd235-229">Há uma relação um-para-zero-ou-um entre o `Instructor` e `OfficeAssignment` entidades.</span><span class="sxs-lookup"><span data-stu-id="fd235-229">There's a one-to-zero-or-one relationship between the `Instructor` and `OfficeAssignment` entities.</span></span> <span data-ttu-id="fd235-230">Uma atribuição de office existe apenas em relação ao instrutor a que é atribuído.</span><span class="sxs-lookup"><span data-stu-id="fd235-230">An office assignment only exists in relation to the instructor it's assigned to.</span></span> <span data-ttu-id="fd235-231">O `OfficeAssignment` PK também é a chave estrangeira (FK) para o `Instructor` entidade.</span><span class="sxs-lookup"><span data-stu-id="fd235-231">The `OfficeAssignment` PK is also its foreign key (FK) to the `Instructor` entity.</span></span> <span data-ttu-id="fd235-232">EF principal não pode reconhecer `InstructorID` como PK de `OfficeAssignment` porque:</span><span class="sxs-lookup"><span data-stu-id="fd235-232">EF Core can't automatically recognize `InstructorID` as the PK of `OfficeAssignment` because:</span></span>

* <span data-ttu-id="fd235-233">`InstructorID`não siga a convenção de nomenclatura de ID ou classnameID.</span><span class="sxs-lookup"><span data-stu-id="fd235-233">`InstructorID` doesn't follow the ID or classnameID naming convention.</span></span>

<span data-ttu-id="fd235-234">Portanto, o `Key` atributo é usado para identificar `InstructorID` como o PK:</span><span class="sxs-lookup"><span data-stu-id="fd235-234">Therefore, the `Key` attribute is used to identify `InstructorID` as the PK:</span></span>

```csharp
[Key]
public int InstructorID { get; set; }
```

<span data-ttu-id="fd235-235">Por padrão, o núcleo de EF trata a chave como não gerado pelo banco de dados porque a coluna é uma relação de identificação.</span><span class="sxs-lookup"><span data-stu-id="fd235-235">By default, EF Core treats the key as non-database-generated because the column is for an identifying relationship.</span></span>

### <a name="the-instructor-navigation-property"></a><span data-ttu-id="fd235-236">A propriedade de navegação do instrutor</span><span class="sxs-lookup"><span data-stu-id="fd235-236">The Instructor navigation property</span></span>

<span data-ttu-id="fd235-237">O `OfficeAssignment` propriedade de navegação para o `Instructor` entidade é anulável porque:</span><span class="sxs-lookup"><span data-stu-id="fd235-237">The `OfficeAssignment` navigation property for the `Instructor` entity is nullable because:</span></span>

* <span data-ttu-id="fd235-238">Tipos de referência (como classes são nulas).</span><span class="sxs-lookup"><span data-stu-id="fd235-238">Reference types (such as classes are nullable).</span></span>
* <span data-ttu-id="fd235-239">Um instrutor pode não ter uma atribuição de escritório.</span><span class="sxs-lookup"><span data-stu-id="fd235-239">An instructor might not have an office assignment.</span></span>


<span data-ttu-id="fd235-240">O `OfficeAssignment` entidade tem uma não-anulável `Instructor` propriedade de navegação porque:</span><span class="sxs-lookup"><span data-stu-id="fd235-240">The `OfficeAssignment` entity has a non-nullable `Instructor` navigation property because:</span></span>

* <span data-ttu-id="fd235-241">`InstructorID`é não anulável.</span><span class="sxs-lookup"><span data-stu-id="fd235-241">`InstructorID` is non-nullable.</span></span>
* <span data-ttu-id="fd235-242">Uma atribuição de office não pode existir sem um instrutor.</span><span class="sxs-lookup"><span data-stu-id="fd235-242">An office assignment can't exist without an instructor.</span></span>

<span data-ttu-id="fd235-243">Quando um `Instructor` entidade tem um relacionados `OfficeAssignment` entidade, cada entidade tem uma referência para um em sua propriedade de navegação.</span><span class="sxs-lookup"><span data-stu-id="fd235-243">When an `Instructor` entity has a related `OfficeAssignment` entity, each entity has a reference to the other one in its navigation property.</span></span>

<span data-ttu-id="fd235-244">O `[Required]` atributo pode ser aplicado para o `Instructor` propriedade de navegação:</span><span class="sxs-lookup"><span data-stu-id="fd235-244">The `[Required]` attribute could be applied to the `Instructor` navigation property:</span></span>

```csharp
[Required]
public Instructor Instructor { get; set; }
```

<span data-ttu-id="fd235-245">O código anterior Especifica que deve ser um instrutor relacionado.</span><span class="sxs-lookup"><span data-stu-id="fd235-245">The preceding code specifies that there must be a related instructor.</span></span> <span data-ttu-id="fd235-246">O código anterior é desnecessário porque o `InstructorID` chave estrangeira (que é também o PK) é não anulável.</span><span class="sxs-lookup"><span data-stu-id="fd235-246">The preceding code is unnecessary because the `InstructorID` foreign key (which is also the PK) is non-nullable.</span></span>

## <a name="modify-the-course-entity"></a><span data-ttu-id="fd235-247">Modificar a entidade de curso</span><span class="sxs-lookup"><span data-stu-id="fd235-247">Modify the Course Entity</span></span>

![Entidade de curso](complex-data-model/_static/course-entity.png)

<span data-ttu-id="fd235-249">Atualização *Models/Course.cs* com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-249">Update *Models/Course.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Final&highlight=2,10,13,16,19,21,23)]

<span data-ttu-id="fd235-250">O `Course` entidade tem uma propriedade de chave estrangeira (FK) `DepartmentID`.</span><span class="sxs-lookup"><span data-stu-id="fd235-250">The `Course` entity has a foreign key (FK) property `DepartmentID`.</span></span> <span data-ttu-id="fd235-251">`DepartmentID`aponta para relacionado `Department` entidade.</span><span class="sxs-lookup"><span data-stu-id="fd235-251">`DepartmentID` points to the related `Department` entity.</span></span> <span data-ttu-id="fd235-252">O `Course` entidade tem um `Department` propriedade de navegação.</span><span class="sxs-lookup"><span data-stu-id="fd235-252">The `Course` entity has a `Department` navigation property.</span></span>

<span data-ttu-id="fd235-253">Núcleo EF não requer uma propriedade FK para um modelo de dados quando o modelo tem uma propriedade de navegação para uma entidade relacionada.</span><span class="sxs-lookup"><span data-stu-id="fd235-253">EF Core doesn't require a FK property for a data model when the model has a navigation property for a related entity.</span></span>

<span data-ttu-id="fd235-254">EF Core cria automaticamente FKs no banco de dados sempre que forem necessários.</span><span class="sxs-lookup"><span data-stu-id="fd235-254">EF Core automatically creates FKs in the database wherever they are needed.</span></span> <span data-ttu-id="fd235-255">Cria Core EF [propriedades de sombra](https://docs.microsoft.com/ef/core/modeling/shadow-properties) para FKs criados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fd235-255">EF Core creates [shadow properties](https://docs.microsoft.com/ef/core/modeling/shadow-properties) for automatically created FKs.</span></span> <span data-ttu-id="fd235-256">Ter FK no modelo de dados pode fazer atualizações mais simples e mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="fd235-256">Having the FK in the data model can make updates simpler and more efficient.</span></span> <span data-ttu-id="fd235-257">Por exemplo, considere um modelo em que a propriedade FK `DepartmentID` é *não* incluídos.</span><span class="sxs-lookup"><span data-stu-id="fd235-257">For example, consider a model where the FK property `DepartmentID` is *not* included.</span></span> <span data-ttu-id="fd235-258">Quando uma entidade de curso é buscada para editar:</span><span class="sxs-lookup"><span data-stu-id="fd235-258">When a course entity is fetched to edit:</span></span>

* <span data-ttu-id="fd235-259">O `Department` entidade será null se ele não foi explicitamente é carregado.</span><span class="sxs-lookup"><span data-stu-id="fd235-259">The `Department` entity is null if it's not explicitly loaded.</span></span>
* <span data-ttu-id="fd235-260">Para atualizar a entidade de curso, o `Department` primeiro deve ser buscada de entidade.</span><span class="sxs-lookup"><span data-stu-id="fd235-260">To update the course entity, the `Department` entity must first be fetched.</span></span>

<span data-ttu-id="fd235-261">Quando a propriedade FK `DepartmentID` está incluído no modelo de dados, não é necessário para buscar o `Department` entidade antes de uma atualização.</span><span class="sxs-lookup"><span data-stu-id="fd235-261">When the FK property `DepartmentID` is included in the data model, there is no need to fetch the `Department` entity before an update.</span></span>

### <a name="the-databasegenerated-attribute"></a><span data-ttu-id="fd235-262">O atributo DatabaseGenerated</span><span class="sxs-lookup"><span data-stu-id="fd235-262">The DatabaseGenerated attribute</span></span>

<span data-ttu-id="fd235-263">O `[DatabaseGenerated(DatabaseGeneratedOption.None)]` atributo especifica que o PK é fornecida pelo aplicativo em vez de gerado pelo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-263">The `[DatabaseGenerated(DatabaseGeneratedOption.None)]` attribute specifies that the PK is provided by the application rather than generated by the database.</span></span>

```csharp
[DatabaseGenerated(DatabaseGeneratedOption.None)]
[Display(Name = "Number")]
public int CourseID { get; set; }
```

<span data-ttu-id="fd235-264">Por padrão, o EF Core assume que os valores de PK são gerados pelo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-264">By default, EF Core assumes that PK values are generated by the DB.</span></span> <span data-ttu-id="fd235-265">Banco de dados gerado PK valores geralmente é a melhor abordagem.</span><span class="sxs-lookup"><span data-stu-id="fd235-265">DB generated PK values is generally the best approach.</span></span> <span data-ttu-id="fd235-266">Para `Course` entidades, o usuário Especifica o PK.</span><span class="sxs-lookup"><span data-stu-id="fd235-266">For `Course` entities, the user specifies the PK.</span></span> <span data-ttu-id="fd235-267">Por exemplo, um número de curso como uma série de 1000 para o departamento de matemática, uma série de 2000 para o departamento em inglês.</span><span class="sxs-lookup"><span data-stu-id="fd235-267">For example, a course number such as a 1000 series for the math department, a 2000 series for the English department.</span></span>

<span data-ttu-id="fd235-268">O `DatabaseGenerated` atributo também pode ser usado para gerar valores padrão.</span><span class="sxs-lookup"><span data-stu-id="fd235-268">The `DatabaseGenerated` attribute can also be used to generate default values.</span></span> <span data-ttu-id="fd235-269">Por exemplo, o banco de dados pode gerar automaticamente um campo de data para registrar a data em que uma linha foi criada ou atualizada.</span><span class="sxs-lookup"><span data-stu-id="fd235-269">For example, the DB can automatically generate a date field to record the date a row was created or updated.</span></span> <span data-ttu-id="fd235-270">Para obter mais informações, consulte [propriedades gerado](https://docs.microsoft.com/ef/core/modeling/generated-properties).</span><span class="sxs-lookup"><span data-stu-id="fd235-270">For more information, see [Generated Properties](https://docs.microsoft.com/ef/core/modeling/generated-properties).</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="fd235-271">Propriedades de navegação e de chave estrangeira</span><span class="sxs-lookup"><span data-stu-id="fd235-271">Foreign key and navigation properties</span></span>

<span data-ttu-id="fd235-272">As propriedades de chave estrangeira (FK) e propriedades de navegação no `Course` entidade refletem as relações a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-272">The foreign key (FK) properties and navigation properties in the `Course` entity reflect the following relationships:</span></span>

<span data-ttu-id="fd235-273">Um curso é atribuído a um departamento, para que haja um `DepartmentID` FK e um `Department` propriedade de navegação.</span><span class="sxs-lookup"><span data-stu-id="fd235-273">A course is assigned to one department, so there's a `DepartmentID` FK and a `Department` navigation property.</span></span>

```csharp
public int DepartmentID { get; set; }
public Department Department { get; set; }
```

<span data-ttu-id="fd235-274">Um curso pode ter qualquer número de alunos inscritos, portanto, o `Enrollments` propriedade de navegação é uma coleção:</span><span class="sxs-lookup"><span data-stu-id="fd235-274">A course can have any number of students enrolled in it, so the `Enrollments` navigation property is a collection:</span></span>

```csharp
public ICollection<Enrollment> Enrollments { get; set; }
```

<span data-ttu-id="fd235-275">Um curso pode ser ensinado por vários instrutores, portanto, o `CourseAssignments` propriedade de navegação é uma coleção:</span><span class="sxs-lookup"><span data-stu-id="fd235-275">A course may be taught by multiple instructors, so the `CourseAssignments` navigation property is a collection:</span></span>

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

<span data-ttu-id="fd235-276">`CourseAssignment`é explicado [posteriormente](#many-to-many-relationships).</span><span class="sxs-lookup"><span data-stu-id="fd235-276">`CourseAssignment` is explained [later](#many-to-many-relationships).</span></span>

## <a name="create-the-department-entity"></a><span data-ttu-id="fd235-277">Criar a entidade de departamento</span><span class="sxs-lookup"><span data-stu-id="fd235-277">Create the Department entity</span></span>

![Entidade Department](complex-data-model/_static/department-entity.png)

<span data-ttu-id="fd235-279">Criar *Models/Department.cs* com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-279">Create *Models/Department.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Department.cs?name=snippet_Begin)]

### <a name="the-column-attribute"></a><span data-ttu-id="fd235-280">O atributo de coluna</span><span class="sxs-lookup"><span data-stu-id="fd235-280">The Column attribute</span></span>

<span data-ttu-id="fd235-281">Anteriormente a `Column` atributo foi usado para alterar o mapeamento de nome de coluna.</span><span class="sxs-lookup"><span data-stu-id="fd235-281">Previously the `Column` attribute was used to change column name mapping.</span></span> <span data-ttu-id="fd235-282">No código para o `Department` entidade, o `Column` atributo é usado para alterar o mapeamento de tipo de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="fd235-282">In the code for the `Department` entity, the `Column` attribute is used to change SQL data type mapping.</span></span> <span data-ttu-id="fd235-283">O `Budget` coluna é definida usando o tipo de dinheiro do SQL Server no banco de dados:</span><span class="sxs-lookup"><span data-stu-id="fd235-283">The `Budget` column is defined using the SQL Server money type in the DB:</span></span>

```csharp
[Column(TypeName="money")]
public decimal Budget { get; set; }
```

<span data-ttu-id="fd235-284">Mapeamento de coluna, geralmente não é necessário.</span><span class="sxs-lookup"><span data-stu-id="fd235-284">Column mapping is generally not required.</span></span> <span data-ttu-id="fd235-285">Núcleo EF geralmente escolhe o tipo de dados do SQL Server apropriado com base no tipo CLR para a propriedade.</span><span class="sxs-lookup"><span data-stu-id="fd235-285">EF Core generally chooses the appropriate SQL Server data type based on the CLR type for the property.</span></span> <span data-ttu-id="fd235-286">O CLR `decimal` tipo é mapeado para um SQL Server `decimal` tipo.</span><span class="sxs-lookup"><span data-stu-id="fd235-286">The CLR `decimal` type maps to a SQL Server `decimal` type.</span></span> <span data-ttu-id="fd235-287">`Budget`para moeda, e o tipo de dados money é mais apropriado para moeda.</span><span class="sxs-lookup"><span data-stu-id="fd235-287">`Budget` is for currency, and the money data type is more appropriate for currency.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="fd235-288">Propriedades de navegação e de chave estrangeira</span><span class="sxs-lookup"><span data-stu-id="fd235-288">Foreign key and navigation properties</span></span>

<span data-ttu-id="fd235-289">As propriedades de navegação e FK refletem as relações a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-289">The FK and navigation properties reflect the following relationships:</span></span>

* <span data-ttu-id="fd235-290">Um departamento pode ou não ter um administrador.</span><span class="sxs-lookup"><span data-stu-id="fd235-290">A department may or may not have an administrator.</span></span>
* <span data-ttu-id="fd235-291">Um administrador é sempre um instrutor.</span><span class="sxs-lookup"><span data-stu-id="fd235-291">An administrator is always an instructor.</span></span> <span data-ttu-id="fd235-292">Portanto, o `InstructorID` propriedade está incluída como FK para o `Instructor` entidade.</span><span class="sxs-lookup"><span data-stu-id="fd235-292">Therefore the `InstructorID` property is included as the FK to the `Instructor` entity.</span></span>

<span data-ttu-id="fd235-293">A propriedade de navegação é denominada `Administrator` , mas contém um `Instructor` entidade:</span><span class="sxs-lookup"><span data-stu-id="fd235-293">The navigation property is named `Administrator` but holds an `Instructor` entity:</span></span>

```csharp
public int? InstructorID { get; set; }
public Instructor Administrator { get; set; }
```

<span data-ttu-id="fd235-294">O ponto de interrogação (?) no código anterior Especifica que a propriedade é anulável.</span><span class="sxs-lookup"><span data-stu-id="fd235-294">The question mark (?) in the preceding code specifies the property is nullable.</span></span>

<span data-ttu-id="fd235-295">Um departamento pode ter vários cursos, portanto, há uma propriedade de navegação de cursos:</span><span class="sxs-lookup"><span data-stu-id="fd235-295">A department may have many courses, so there's a Courses navigation property:</span></span>

```csharp
public ICollection<Course> Courses { get; set; }
```

<span data-ttu-id="fd235-296">Observação: Por convenção, o núcleo do EF permite a exclusão em cascata para FKs não anuláveis em relações muitos-para-muitos.</span><span class="sxs-lookup"><span data-stu-id="fd235-296">Note: By convention, EF Core enables cascade delete for non-nullable FKs and for many-to-many relationships.</span></span> <span data-ttu-id="fd235-297">Exclusão em cascata pode resultar em regras de exclusão em cascata circular.</span><span class="sxs-lookup"><span data-stu-id="fd235-297">Cascading delete can result in circular cascade delete rules.</span></span> <span data-ttu-id="fd235-298">Circular exclusão em cascata causas regras uma exceção quando uma migração é adicionada.</span><span class="sxs-lookup"><span data-stu-id="fd235-298">Circular cascade delete rules causes an exception when a migration is added.</span></span>

<span data-ttu-id="fd235-299">Por exemplo, se o `Department.InstructorID` propriedade não foi definida como anulável:</span><span class="sxs-lookup"><span data-stu-id="fd235-299">For example, if the `Department.InstructorID` property was not defined as nullable:</span></span>

* <span data-ttu-id="fd235-300">Núcleo EF configura uma regra de exclusão em cascata para excluir o instrutor quando o departamento é excluído.</span><span class="sxs-lookup"><span data-stu-id="fd235-300">EF Core configures a cascade delete rule to delete the instructor when the department is deleted.</span></span>
* <span data-ttu-id="fd235-301">Excluir o instrutor quando o departamento é excluído não é o comportamento desejado.</span><span class="sxs-lookup"><span data-stu-id="fd235-301">Deleting the instructor when the department is deleted is not the intended behavior.</span></span>

<span data-ttu-id="fd235-302">Se as regras de negócio é necessário o `InstructorID` propriedade ser não anuláveis, use a seguinte instrução API fluente:</span><span class="sxs-lookup"><span data-stu-id="fd235-302">If business rules required the `InstructorID` property be non-nullable, use the following fluent API statement:</span></span>

 ```csharp
 modelBuilder.Entity<Department>()
    .HasOne(d => d.Administrator)
    .WithMany()
    .OnDelete(DeleteBehavior.Restrict)
 ```

<span data-ttu-id="fd235-303">O código anterior desabilita a exclusão em cascata na relação instrutor departamento.</span><span class="sxs-lookup"><span data-stu-id="fd235-303">The preceding code disables cascade delete on the department-instructor relationship.</span></span>

## <a name="update-the-enrollment-entity"></a><span data-ttu-id="fd235-304">Atualizar a entidade de registro</span><span class="sxs-lookup"><span data-stu-id="fd235-304">Update the Enrollment entity</span></span>

<span data-ttu-id="fd235-305">Um registro é um curso uma tomada por um aluno.</span><span class="sxs-lookup"><span data-stu-id="fd235-305">An enrollment record is for a one course taken by one student.</span></span>

![Entidade de registro](complex-data-model/_static/enrollment-entity.png)

<span data-ttu-id="fd235-307">Atualização *Models/Enrollment.cs* com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-307">Update *Models/Enrollment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Final&highlight=1-2,16)]

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="fd235-308">Propriedades de navegação e de chave estrangeira</span><span class="sxs-lookup"><span data-stu-id="fd235-308">Foreign key and navigation properties</span></span>

<span data-ttu-id="fd235-309">As propriedades FK e propriedades de navegação refletem as relações a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-309">The FK properties and navigation properties reflect the following relationships:</span></span>

<span data-ttu-id="fd235-310">Um registro é um curso, portanto, há um `CourseID` propriedade FK e um `Course` propriedade de navegação:</span><span class="sxs-lookup"><span data-stu-id="fd235-310">An enrollment record is for one course, so there's a `CourseID` FK property and a `Course` navigation property:</span></span>

```csharp
public int CourseID { get; set; }
public Course Course { get; set; }
```

<span data-ttu-id="fd235-311">Um registro é para um aluno, portanto, há um `StudentID` propriedade FK e um `Student` propriedade de navegação:</span><span class="sxs-lookup"><span data-stu-id="fd235-311">An enrollment record is for one student, so there's a `StudentID` FK property and a `Student` navigation property:</span></span>

```csharp
public int StudentID { get; set; }
public Student Student { get; set; }
```

## <a name="many-to-many-relationships"></a><span data-ttu-id="fd235-312">Relações muitos-para-muitos</span><span class="sxs-lookup"><span data-stu-id="fd235-312">Many-to-Many Relationships</span></span>

<span data-ttu-id="fd235-313">Há uma relação muitos-para-muitos entre o `Student` e `Course` entidades.</span><span class="sxs-lookup"><span data-stu-id="fd235-313">There's a many-to-many relationship between the `Student` and `Course` entities.</span></span> <span data-ttu-id="fd235-314">O `Enrollment` entidade funciona como uma tabela de junção de muitos-para-muitos *com carga* no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-314">The `Enrollment` entity functions as a many-to-many join table *with payload* in the database.</span></span> <span data-ttu-id="fd235-315">"Com carga" significa que o `Enrollment` tabela contém dados adicionais além FKs para tabelas unidas (nesse caso, a CP e `Grade`).</span><span class="sxs-lookup"><span data-stu-id="fd235-315">"With payload" means that the `Enrollment` table contains additional data besides FKs for the joined tables (in this case, the PK and `Grade`).</span></span>

<span data-ttu-id="fd235-316">A ilustração a seguir mostra a aparência dessas relações em um diagrama de entidade.</span><span class="sxs-lookup"><span data-stu-id="fd235-316">The following illustration shows what these relationships look like in an entity diagram.</span></span> <span data-ttu-id="fd235-317">(Esse diagrama foi gerado usando EF Power Tools para EF 6. x.</span><span class="sxs-lookup"><span data-stu-id="fd235-317">(This diagram was generated using EF Power Tools for EF 6.x.</span></span> <span data-ttu-id="fd235-318">Criar o diagrama não faz parte do tutorial.)</span><span class="sxs-lookup"><span data-stu-id="fd235-318">Creating the diagram isn't part of the tutorial.)</span></span>

![Curso de aluno muitos para muitos](complex-data-model/_static/student-course.png)

<span data-ttu-id="fd235-320">Cada linha de relação tem um 1 em uma extremidade e um asterisco (*) em outro, indicando uma relação um-para-muitos.</span><span class="sxs-lookup"><span data-stu-id="fd235-320">Each relationship line has a 1 at one end and an asterisk (*) at the other, indicating a one-to-many relationship.</span></span>

<span data-ttu-id="fd235-321">Se o `Enrollment` tabela não incluir informações de classificação, ele apenas precisa conter os dois FKs (`CourseID` e `StudentID`).</span><span class="sxs-lookup"><span data-stu-id="fd235-321">If the `Enrollment` table didn't include grade information, it would only need to contain the two FKs (`CourseID` and `StudentID`).</span></span> <span data-ttu-id="fd235-322">Uma tabela de junção de muitos-para-muitos sem carga às vezes é chamada de uma tabela de junção puro (PJT).</span><span class="sxs-lookup"><span data-stu-id="fd235-322">A many-to-many join table without payload is sometimes called a pure join table (PJT).</span></span>

<span data-ttu-id="fd235-323">O `Instructor` e `Course` as entidades têm uma relação muitos-para-muitos usando uma tabela de junção puro.</span><span class="sxs-lookup"><span data-stu-id="fd235-323">The `Instructor` and `Course` entities have a many-to-many relationship using a pure join table.</span></span>

<span data-ttu-id="fd235-324">Observação: EF 6. x oferece suporte a tabelas de junção implícita para relações muitos-para-muitos, mas Core EF não.</span><span class="sxs-lookup"><span data-stu-id="fd235-324">Note: EF 6.x supports implicit join tables for many-to-many relationships, but EF Core does not.</span></span> <span data-ttu-id="fd235-325">Para obter mais informações, consulte [muitos-para-muitos relações no EF Core 2.0](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/).</span><span class="sxs-lookup"><span data-stu-id="fd235-325">For more information, see [Many-to-many relationships in EF Core 2.0](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/).</span></span>

## <a name="the-courseassignment-entity"></a><span data-ttu-id="fd235-326">A entidade CourseAssignment</span><span class="sxs-lookup"><span data-stu-id="fd235-326">The CourseAssignment entity</span></span>

![Entidade CourseAssignment](complex-data-model/_static/courseassignment-entity.png)

<span data-ttu-id="fd235-328">Criar *Models/CourseAssignment.cs* com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-328">Create *Models/CourseAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/CourseAssignment.cs)]

### <a name="instructor-to-courses"></a><span data-ttu-id="fd235-329">Instrutor para cursos</span><span class="sxs-lookup"><span data-stu-id="fd235-329">Instructor-to-Courses</span></span>

![M:M instrutor para cursos](complex-data-model/_static/courseassignment.png)

<span data-ttu-id="fd235-331">A relação de muitos-para-muitos instrutor para cursos:</span><span class="sxs-lookup"><span data-stu-id="fd235-331">The Instructor-to-Courses many-to-many relationship:</span></span>

* <span data-ttu-id="fd235-332">Requer uma tabela de junção que deve ser representada por um conjunto de entidades.</span><span class="sxs-lookup"><span data-stu-id="fd235-332">Requires a join table that must be represented by an entity set.</span></span>
* <span data-ttu-id="fd235-333">É uma tabela de junção puro (tabela sem carga).</span><span class="sxs-lookup"><span data-stu-id="fd235-333">Is a pure join table (table without payload).</span></span>

<span data-ttu-id="fd235-334">É comum para nomear uma entidade de junção `EntityName1EntityName2`.</span><span class="sxs-lookup"><span data-stu-id="fd235-334">It's common to name a join entity `EntityName1EntityName2`.</span></span> <span data-ttu-id="fd235-335">Por exemplo, a tabela de junção instrutor para cursos usando esse padrão é `CourseInstructor`.</span><span class="sxs-lookup"><span data-stu-id="fd235-335">For example, the Instructor-to-Courses join table using this pattern is `CourseInstructor`.</span></span> <span data-ttu-id="fd235-336">No entanto, é recomendável usar um nome que descreve a relação.</span><span class="sxs-lookup"><span data-stu-id="fd235-336">However, we recommend using a name that describes the relationship.</span></span>

<span data-ttu-id="fd235-337">Modelos de dados começam simples e crescem.</span><span class="sxs-lookup"><span data-stu-id="fd235-337">Data models start out simple and grow.</span></span> <span data-ttu-id="fd235-338">Nenhuma carga junções (PJTs) evoluem com frequência para incluir a carga.</span><span class="sxs-lookup"><span data-stu-id="fd235-338">No-payload joins (PJTs) frequently evolve to include payload.</span></span> <span data-ttu-id="fd235-339">Iniciando com um nome descritivo de entidade, o nome não precisa alterar quando a tabela de junção é alterado.</span><span class="sxs-lookup"><span data-stu-id="fd235-339">By starting with a descriptive entity name, the name doesn't need to change when the join table changes.</span></span> <span data-ttu-id="fd235-340">Idealmente, a entidade de junção terá seu próprio nome (possivelmente única palavra) natural no domínio da empresa.</span><span class="sxs-lookup"><span data-stu-id="fd235-340">Ideally, the join entity would have its own natural (possibly single word) name in the business domain.</span></span> <span data-ttu-id="fd235-341">Por exemplo, manuais e clientes foi vinculados com uma entidade de associação chamada classificações.</span><span class="sxs-lookup"><span data-stu-id="fd235-341">For example, Books and Customers could be linked with a join entity called Ratings.</span></span> <span data-ttu-id="fd235-342">Para a relação de muitos-para-muitos instrutor para cursos, `CourseAssignment` é preferencial em `CourseInstructor`.</span><span class="sxs-lookup"><span data-stu-id="fd235-342">For the Instructor-to-Courses many-to-many relationship, `CourseAssignment` is preferred over `CourseInstructor`.</span></span>

### <a name="composite-key"></a><span data-ttu-id="fd235-343">Chave composta</span><span class="sxs-lookup"><span data-stu-id="fd235-343">Composite key</span></span>

<span data-ttu-id="fd235-344">FKs não são nulas.</span><span class="sxs-lookup"><span data-stu-id="fd235-344">FKs are not nullable.</span></span> <span data-ttu-id="fd235-345">Os dois FKs em `CourseAssignment` (`InstructorID` e `CourseID`) juntas identificam exclusivamente cada linha do `CourseAssignment` tabela.</span><span class="sxs-lookup"><span data-stu-id="fd235-345">The two FKs in `CourseAssignment` (`InstructorID` and `CourseID`) together uniquely identify each row of the `CourseAssignment` table.</span></span> <span data-ttu-id="fd235-346">`CourseAssignment`não requer um PK. dedicado</span><span class="sxs-lookup"><span data-stu-id="fd235-346">`CourseAssignment` doesn't require a dedicated PK.</span></span> <span data-ttu-id="fd235-347">O `InstructorID` e `CourseID` propriedades funcionam como um PK de composição.</span><span class="sxs-lookup"><span data-stu-id="fd235-347">The `InstructorID` and `CourseID` properties function as a composite PK.</span></span> <span data-ttu-id="fd235-348">A única maneira de especificar PKs compostos Core EF é com o *API fluente*.</span><span class="sxs-lookup"><span data-stu-id="fd235-348">The only way to specify composite PKs to EF Core is with the *fluent API*.</span></span> <span data-ttu-id="fd235-349">A próxima seção mostra como configurar o PK de composição.</span><span class="sxs-lookup"><span data-stu-id="fd235-349">The next section shows how to configure the composite PK.</span></span>

<span data-ttu-id="fd235-350">A chave composta garante:</span><span class="sxs-lookup"><span data-stu-id="fd235-350">The composite key ensures:</span></span>

* <span data-ttu-id="fd235-351">São permitidas várias linhas para um curso.</span><span class="sxs-lookup"><span data-stu-id="fd235-351">Multiple rows are allowed for one course.</span></span>
* <span data-ttu-id="fd235-352">São permitidas várias linhas para um instrutor.</span><span class="sxs-lookup"><span data-stu-id="fd235-352">Multiple rows are allowed for one instructor.</span></span>
* <span data-ttu-id="fd235-353">Várias linhas para o mesmo instrutor e curso não é permitido.</span><span class="sxs-lookup"><span data-stu-id="fd235-353">Multiple rows for the same instructor and course is not allowed.</span></span>

<span data-ttu-id="fd235-354">O `Enrollment` junção entidade define seu próprio PK, portanto, duplicatas desse tipo são possíveis.</span><span class="sxs-lookup"><span data-stu-id="fd235-354">The `Enrollment` join entity defines its own PK, so duplicates of this sort are possible.</span></span> <span data-ttu-id="fd235-355">Para evitar tais duplicatas:</span><span class="sxs-lookup"><span data-stu-id="fd235-355">To prevent such duplicates:</span></span>

* <span data-ttu-id="fd235-356">Adicionar um índice exclusivo nos campos de FK, ou</span><span class="sxs-lookup"><span data-stu-id="fd235-356">Add a unique index on the FK fields, or</span></span>
* <span data-ttu-id="fd235-357">Configurar `Enrollment` com uma chave primária composta semelhante ao `CourseAssignment`.</span><span class="sxs-lookup"><span data-stu-id="fd235-357">Configure `Enrollment` with a primary composite key similar to `CourseAssignment`.</span></span> <span data-ttu-id="fd235-358">Para obter mais informações, consulte [índices](https://docs.microsoft.com/ef/core/modeling/indexes).</span><span class="sxs-lookup"><span data-stu-id="fd235-358">For more information, see [Indexes](https://docs.microsoft.com/ef/core/modeling/indexes).</span></span>

## <a name="update-the-db-context"></a><span data-ttu-id="fd235-359">Atualizar o contexto do banco de dados</span><span class="sxs-lookup"><span data-stu-id="fd235-359">Update the DB context</span></span>

<span data-ttu-id="fd235-360">Adicione o seguinte código realçado para *Data/SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="fd235-360">Add the following highlighted code to *Data/SchoolContext.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_BeforeInheritance&highlight=15-18,25-31)]

<span data-ttu-id="fd235-361">O código anterior adiciona novas entidades e configura o `CourseAssignment` PK. de composição da entidade</span><span class="sxs-lookup"><span data-stu-id="fd235-361">The preceding code adds the new entities and configures the `CourseAssignment` entity's composite PK.</span></span>

## <a name="fluent-api-alternative-to-attributes"></a><span data-ttu-id="fd235-362">Alternativa de API fluente para atributos</span><span class="sxs-lookup"><span data-stu-id="fd235-362">Fluent API alternative to attributes</span></span>

<span data-ttu-id="fd235-363">O `OnModelCreating` método anterior de código usa o *API fluente* para configurar o comportamento de EF Core.</span><span class="sxs-lookup"><span data-stu-id="fd235-363">The `OnModelCreating` method in the preceding code uses the *fluent API* to configure EF Core behavior.</span></span> <span data-ttu-id="fd235-364">A API é chamada "fluente" porque ele geralmente é usado pelo encadeamento uma série de chamadas de método em uma única instrução.</span><span class="sxs-lookup"><span data-stu-id="fd235-364">The API is called "fluent" because it's often used by stringing a series of method calls together into a single statement.</span></span> <span data-ttu-id="fd235-365">O [código a seguir](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration) é um exemplo de como a API fluente:</span><span class="sxs-lookup"><span data-stu-id="fd235-365">The [following code](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration) is an example of the fluent API:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .IsRequired();
}
```

<span data-ttu-id="fd235-366">Neste tutorial, a API fluente é usada apenas para mapeamento de banco de dados que não pode ser feito com atributos.</span><span class="sxs-lookup"><span data-stu-id="fd235-366">In this tutorial, the fluent API is used only for DB mapping that can't be done with attributes.</span></span> <span data-ttu-id="fd235-367">No entanto, a API fluente pode especificar mais de formatação, validação e regras de mapeamento que podem ser feitas com os atributos.</span><span class="sxs-lookup"><span data-stu-id="fd235-367">However, the fluent API can specify most of the formatting, validation, and mapping rules that can be done with attributes.</span></span>

<span data-ttu-id="fd235-368">Alguns atributos como `MinimumLength` não pode ser aplicado com a API fluente.</span><span class="sxs-lookup"><span data-stu-id="fd235-368">Some attributes such as `MinimumLength` can't be applied with the fluent API.</span></span> <span data-ttu-id="fd235-369">`MinimumLength`não altera o esquema, ela só se aplica a uma regra de validação de comprimento mínimo.</span><span class="sxs-lookup"><span data-stu-id="fd235-369">`MinimumLength` doesn't change the schema, it only applies a minimum length validation rule.</span></span>

<span data-ttu-id="fd235-370">Alguns desenvolvedores preferem usar a API fluente exclusivamente para que eles podem manter suas classes de entidade "normal".</span><span class="sxs-lookup"><span data-stu-id="fd235-370">Some developers prefer to use the fluent API exclusively so that they can keep their entity classes "clean."</span></span> <span data-ttu-id="fd235-371">Atributos e a API fluente podem ser mesclados.</span><span class="sxs-lookup"><span data-stu-id="fd235-371">Attributes and the fluent API can be mixed.</span></span> <span data-ttu-id="fd235-372">Há algumas configurações que só podem ser feitas com a API fluente (especificando uma CP composto).</span><span class="sxs-lookup"><span data-stu-id="fd235-372">There are some configurations that can only be done with the fluent API (specifying a composite PK).</span></span> <span data-ttu-id="fd235-373">Há algumas configurações que só podem ser feitas com os atributos (`MinimumLength`).</span><span class="sxs-lookup"><span data-stu-id="fd235-373">There are some configurations that can only be done with attributes (`MinimumLength`).</span></span> <span data-ttu-id="fd235-374">A prática recomendada para o uso de atributos ou API fluente:</span><span class="sxs-lookup"><span data-stu-id="fd235-374">The recommended practice for using fluent API or attributes:</span></span>

* <span data-ttu-id="fd235-375">Escolha uma destas duas abordagens.</span><span class="sxs-lookup"><span data-stu-id="fd235-375">Choose one of these two approaches.</span></span>
* <span data-ttu-id="fd235-376">Use a abordagem escolhida consistentemente tanto quanto possível.</span><span class="sxs-lookup"><span data-stu-id="fd235-376">Use the chosen approach consistently as much as possible.</span></span>

<span data-ttu-id="fd235-377">Alguns dos atributos usados neste tutorial são usados para:</span><span class="sxs-lookup"><span data-stu-id="fd235-377">Some of the attributes used in the this tutorial are used for:</span></span>

* <span data-ttu-id="fd235-378">Somente validação (por exemplo, `MinimumLength`).</span><span class="sxs-lookup"><span data-stu-id="fd235-378">Validation only (for example, `MinimumLength`).</span></span>
* <span data-ttu-id="fd235-379">Apenas para a configuração de núcleo EF (por exemplo, `HasKey`).</span><span class="sxs-lookup"><span data-stu-id="fd235-379">EF Core configuration only (for example, `HasKey`).</span></span>
* <span data-ttu-id="fd235-380">Configuração de validação e EF Core (por exemplo, `[StringLength(50)]`).</span><span class="sxs-lookup"><span data-stu-id="fd235-380">Validation and EF Core configuration (for example, `[StringLength(50)]`).</span></span>

<span data-ttu-id="fd235-381">Para obter mais informações sobre atributos versus API fluente, consulte [métodos de configuração](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration).</span><span class="sxs-lookup"><span data-stu-id="fd235-381">For more information about attributes vs. fluent API, see [Methods of configuration](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration).</span></span>

## <a name="entity-diagram-showing-relationships"></a><span data-ttu-id="fd235-382">Relações de exibição de diagrama de entidade</span><span class="sxs-lookup"><span data-stu-id="fd235-382">Entity Diagram Showing Relationships</span></span>

<span data-ttu-id="fd235-383">A ilustração a seguir mostra o diagrama que criar EF Power Tools para o modelo de escola concluído.</span><span class="sxs-lookup"><span data-stu-id="fd235-383">The following illustration shows the diagram that EF Power Tools create for the completed School model.</span></span>

![Diagrama de entidade](complex-data-model/_static/diagram.png)

<span data-ttu-id="fd235-385">O diagrama anterior mostra:</span><span class="sxs-lookup"><span data-stu-id="fd235-385">The preceding diagram shows:</span></span>

* <span data-ttu-id="fd235-386">Várias linhas de relação um-para-muitos (1 a \*).</span><span class="sxs-lookup"><span data-stu-id="fd235-386">Several one-to-many relationship lines (1 to \*).</span></span>
* <span data-ttu-id="fd235-387">A linha de relação um-para-zero-ou-um (1 para entre 0 e 1) entre o `Instructor` e `OfficeAssignment` entidades.</span><span class="sxs-lookup"><span data-stu-id="fd235-387">The one-to-zero-or-one relationship line (1 to 0..1) between the `Instructor` and `OfficeAssignment` entities.</span></span>
* <span data-ttu-id="fd235-388">A linha de relação de zero-ou-um-para-muitos (entre 0 e 1 para *) entre o `Instructor` e `Department` entidades.</span><span class="sxs-lookup"><span data-stu-id="fd235-388">The zero-or-one-to-many relationship line (0..1 to *) between the `Instructor` and `Department` entities.</span></span>

## <a name="seed-the-db-with-test-data"></a><span data-ttu-id="fd235-389">O banco de dados com dados de teste de propagação</span><span class="sxs-lookup"><span data-stu-id="fd235-389">Seed the DB with Test Data</span></span>

<span data-ttu-id="fd235-390">Atualize o código em *Data/DbInitializer.cs*:</span><span class="sxs-lookup"><span data-stu-id="fd235-390">Update the code in *Data/DbInitializer.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Final)]

<span data-ttu-id="fd235-391">O código anterior fornece dados de propagação de novas entidades.</span><span class="sxs-lookup"><span data-stu-id="fd235-391">The preceding code provides seed data for the new entities.</span></span> <span data-ttu-id="fd235-392">A maioria do código cria novos objetos de entidade e carrega dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="fd235-392">Most of this code creates new entity objects and loads sample data.</span></span> <span data-ttu-id="fd235-393">Os dados de exemplo são usados para teste.</span><span class="sxs-lookup"><span data-stu-id="fd235-393">The sample data is used for testing.</span></span> <span data-ttu-id="fd235-394">O código anterior cria as seguintes relações muitos-para-muitos:</span><span class="sxs-lookup"><span data-stu-id="fd235-394">The preceding code creates the following many-to-many relationships:</span></span>

* `Enrollments`
* `CourseAssignment`

<span data-ttu-id="fd235-395">Observação: [EF Core 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap) dará suporte [propagação de dados](https://github.com/aspnet/EntityFrameworkCore/issues/629).</span><span class="sxs-lookup"><span data-stu-id="fd235-395">Note: [EF Core 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap) will support [data seeding](https://github.com/aspnet/EntityFrameworkCore/issues/629).</span></span>

## <a name="add-a-migration"></a><span data-ttu-id="fd235-396">Adicionar uma migração</span><span class="sxs-lookup"><span data-stu-id="fd235-396">Add a migration</span></span>

<span data-ttu-id="fd235-397">Compile o projeto.</span><span class="sxs-lookup"><span data-stu-id="fd235-397">Build the project.</span></span> <span data-ttu-id="fd235-398">Abra uma janela de comando na pasta do projeto e digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="fd235-398">Open a command window in the project folder and enter the following command:</span></span>

```console
dotnet ef migrations add ComplexDataModel
```

<span data-ttu-id="fd235-399">O comando anterior exibe um aviso sobre a possível perda de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-399">The preceding command displays a warning about possible data loss.</span></span>

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
Done. To undo this action, use 'ef migrations remove'
```

<span data-ttu-id="fd235-400">Se o `database update` comando é executado, o seguinte erro é gerado:</span><span class="sxs-lookup"><span data-stu-id="fd235-400">If the `database update` command is run, the following error is produced:</span></span>

```text
The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK_dbo.Course_dbo.Department_DepartmentID". The conflict occurred in
database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.
```

<span data-ttu-id="fd235-401">Quando as migrações são executadas com os dados existentes, pode haver restrições FK que não são atendidas com os dados existentes.</span><span class="sxs-lookup"><span data-stu-id="fd235-401">When migrations are run with existing data, there may be FK constraints that are not satisfied with the exiting data.</span></span> <span data-ttu-id="fd235-402">Para este tutorial, um novo banco de dados é criado, portanto, não há nenhuma violação de restrição FK.</span><span class="sxs-lookup"><span data-stu-id="fd235-402">For this tutorial, a new DB is created, so there are no FK constraint violations.</span></span> <span data-ttu-id="fd235-403">Consulte [corrigir restrições de chave estrangeira com dados herdados](#fk) para obter instruções sobre como corrigir as violações de FK no banco de dados atual.</span><span class="sxs-lookup"><span data-stu-id="fd235-403">See [Fixing foreign key constraints with legacy data](#fk) for instructions on how to fix the FK violations on the current DB.</span></span>

## <a name="change-the-connection-string-and-update-the-db"></a><span data-ttu-id="fd235-404">Altere a cadeia de caracteres de conexão e atualize o banco de dados</span><span class="sxs-lookup"><span data-stu-id="fd235-404">Change the connection string and update the DB</span></span>

<span data-ttu-id="fd235-405">O código atualizado `DbInitializer` adiciona dados de propagação de novas entidades.</span><span class="sxs-lookup"><span data-stu-id="fd235-405">The code in the updated `DbInitializer` adds seed data for the new entities.</span></span> <span data-ttu-id="fd235-406">Para forçar o EF principal para criar um novo banco de dados vazio:</span><span class="sxs-lookup"><span data-stu-id="fd235-406">To force EF Core to create a new empty DB:</span></span>

* <span data-ttu-id="fd235-407">Alterar o nome de cadeia de caracteres de conexão de banco de dados no *appSettings. JSON* para ContosoUniversity3.</span><span class="sxs-lookup"><span data-stu-id="fd235-407">Change the DB connection string name in *appsettings.json* to ContosoUniversity3.</span></span> <span data-ttu-id="fd235-408">O novo nome deve ser um nome que ainda não foi usado no computador.</span><span class="sxs-lookup"><span data-stu-id="fd235-408">The new name must be a name that hasn't been used on the computer.</span></span>

    ```json
    {
      "ConnectionStrings": {
        "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ContosoUniversity3;Trusted_Connection=True;MultipleActiveResultSets=true"
      },
    ```

* <span data-ttu-id="fd235-409">Como alternativa, exclua o banco de dados usando:</span><span class="sxs-lookup"><span data-stu-id="fd235-409">Alternatively, delete the DB using:</span></span>

    * <span data-ttu-id="fd235-410">**Pesquisador de objetos do SQL Server** (SSOX).</span><span class="sxs-lookup"><span data-stu-id="fd235-410">**SQL Server Object Explorer** (SSOX).</span></span>
    * <span data-ttu-id="fd235-411">O `database drop` comando CLI:</span><span class="sxs-lookup"><span data-stu-id="fd235-411">The `database drop` CLI command:</span></span>

   ```console
   dotnet ef database drop
   ```

<span data-ttu-id="fd235-412">Executar `database update` na janela de comando:</span><span class="sxs-lookup"><span data-stu-id="fd235-412">Run `database update` in the command window:</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="fd235-413">O comando anterior é executado todas as migrações.</span><span class="sxs-lookup"><span data-stu-id="fd235-413">The preceding command runs all the migrations.</span></span>

<span data-ttu-id="fd235-414">Execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fd235-414">Run the app.</span></span> <span data-ttu-id="fd235-415">Executando o aplicativo será executado o `DbInitializer.Initialize` método.</span><span class="sxs-lookup"><span data-stu-id="fd235-415">Running the app runs the `DbInitializer.Initialize` method.</span></span> <span data-ttu-id="fd235-416">O `DbInitializer.Initialize` preenche o novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-416">The `DbInitializer.Initialize` populates the new DB.</span></span>

<span data-ttu-id="fd235-417">Abra o banco de dados SSOX:</span><span class="sxs-lookup"><span data-stu-id="fd235-417">Open the DB in SSOX:</span></span>

* <span data-ttu-id="fd235-418">Expanda o **tabelas** nó.</span><span class="sxs-lookup"><span data-stu-id="fd235-418">Expand the **Tables** node.</span></span> <span data-ttu-id="fd235-419">As tabelas criadas são exibidas.</span><span class="sxs-lookup"><span data-stu-id="fd235-419">The created tables are displayed.</span></span>
* <span data-ttu-id="fd235-420">Se SSOX foi aberto anteriormente, clique o **atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="fd235-420">If SSOX was opened previously, click the **Refresh** button.</span></span>

![Tabelas no SSOX](complex-data-model/_static/ssox-tables.png)

<span data-ttu-id="fd235-422">Examine o **CourseAssignment** tabela:</span><span class="sxs-lookup"><span data-stu-id="fd235-422">Examine the **CourseAssignment** table:</span></span>

* <span data-ttu-id="fd235-423">Clique com botão direito do **CourseAssignment** de tabela e selecione **exibir dados**.</span><span class="sxs-lookup"><span data-stu-id="fd235-423">Right-click the **CourseAssignment** table and select **View Data**.</span></span>
* <span data-ttu-id="fd235-424">Verifique se o **CourseAssignment** tabela contiver dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-424">Verify the **CourseAssignment** table contains data.</span></span>

![Dados CourseAssignment SSOX](complex-data-model/_static/ssox-ci-data.png)

<a name="fk"></a>

## <a name="fixing-foreign-key-constraints-with-legacy-data"></a><span data-ttu-id="fd235-426">Correção de restrições de chave estrangeira com dados herdados</span><span class="sxs-lookup"><span data-stu-id="fd235-426">Fixing foreign key constraints with legacy data</span></span>

<span data-ttu-id="fd235-427">Esta seção é opcional.</span><span class="sxs-lookup"><span data-stu-id="fd235-427">This section is optional.</span></span>

<span data-ttu-id="fd235-428">Quando as migrações são executadas com os dados existentes, pode haver restrições FK que não são atendidas com os dados existentes.</span><span class="sxs-lookup"><span data-stu-id="fd235-428">When migrations are run with existing data, there may be FK constraints that are not satisfied with the exiting data.</span></span> <span data-ttu-id="fd235-429">Com dados de produção, as etapas devem ser executadas para migrar os dados existentes.</span><span class="sxs-lookup"><span data-stu-id="fd235-429">With production data, steps must be taken to migrate the existing data.</span></span> <span data-ttu-id="fd235-430">Esta seção fornece um exemplo de correção de violações de restrição FK.</span><span class="sxs-lookup"><span data-stu-id="fd235-430">This section provides an example of fixing FK constraint violations.</span></span> <span data-ttu-id="fd235-431">Não fazer essas alterações de código sem um backup.</span><span class="sxs-lookup"><span data-stu-id="fd235-431">Don't make these code changes without a backup.</span></span> <span data-ttu-id="fd235-432">Não fazer essas alterações de código se você concluir a seção anterior e atualizar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fd235-432">Don't make these code changes if you completed the previous section and updated the database.</span></span>

<span data-ttu-id="fd235-433">O *{timestamp}_ComplexDataModel.cs* arquivo contém o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd235-433">The *{timestamp}_ComplexDataModel.cs* file contains the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_DepartmentID)]

<span data-ttu-id="fd235-434">O código anterior adiciona uma não-anulável `DepartmentID` FK para o `Course` tabela.</span><span class="sxs-lookup"><span data-stu-id="fd235-434">The preceding code adds a non-nullable `DepartmentID` FK to the `Course` table.</span></span> <span data-ttu-id="fd235-435">O banco de dados do tutorial anterior contém linhas de `Course`, portanto, essa tabela não pode ser atualizada por migrações.</span><span class="sxs-lookup"><span data-stu-id="fd235-435">The DB from the previous tutorial contains rows in `Course`, so that table cannot be updated by migrations.</span></span>

<span data-ttu-id="fd235-436">Para fazer o `ComplexDataModel` trabalho de migração com dados existentes:</span><span class="sxs-lookup"><span data-stu-id="fd235-436">To make the `ComplexDataModel` migration work with existing data:</span></span>

* <span data-ttu-id="fd235-437">Altere o código para dar a nova coluna (`DepartmentID`) um valor padrão.</span><span class="sxs-lookup"><span data-stu-id="fd235-437">Change the code to give the new column (`DepartmentID`) a default value.</span></span>
* <span data-ttu-id="fd235-438">Crie um departamento falso chamado "Temp" para agir como o departamento de padrão.</span><span class="sxs-lookup"><span data-stu-id="fd235-438">Create a fake department named "Temp" to act as the default department.</span></span>

### <a name="fix-the-foreign-key-constraints"></a><span data-ttu-id="fd235-439">Corrija as restrições de chave estrangeiras</span><span class="sxs-lookup"><span data-stu-id="fd235-439">Fix the foreign key constraints</span></span>

<span data-ttu-id="fd235-440">Atualização de `ComplexDataModel` classes `Up` método:</span><span class="sxs-lookup"><span data-stu-id="fd235-440">Update the `ComplexDataModel` classes `Up` method:</span></span>

* <span data-ttu-id="fd235-441">Abra o *{timestamp}_ComplexDataModel.cs* arquivo.</span><span class="sxs-lookup"><span data-stu-id="fd235-441">Open the *{timestamp}_ComplexDataModel.cs* file.</span></span>
* <span data-ttu-id="fd235-442">Comente a linha de código que adiciona o `DepartmentID` coluna para o `Course` tabela.</span><span class="sxs-lookup"><span data-stu-id="fd235-442">Comment out the line of code that adds the `DepartmentID` column to the `Course` table.</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CommentOut&highlight=9-13)]

<span data-ttu-id="fd235-443">Adicione o seguinte código realçado.</span><span class="sxs-lookup"><span data-stu-id="fd235-443">Add the following highlighted code.</span></span> <span data-ttu-id="fd235-444">O novo código é após o `.CreateTable( name: "Department"` bloco:[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]</span><span class="sxs-lookup"><span data-stu-id="fd235-444">The new code goes after the `.CreateTable( name: "Department"` block: [!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]</span></span>

<span data-ttu-id="fd235-445">Com as alterações anteriores, existente `Course` linhas estão relacionadas ao departamento "Temp" após o `ComplexDataModel` `Up` execuções do método.</span><span class="sxs-lookup"><span data-stu-id="fd235-445">With the preceding changes, existing `Course` rows will be related to the "Temp" department after the `ComplexDataModel` `Up` method runs.</span></span>

<span data-ttu-id="fd235-446">Um aplicativo de produção seria:</span><span class="sxs-lookup"><span data-stu-id="fd235-446">A production app would:</span></span>

* <span data-ttu-id="fd235-447">Incluir código ou scripts para adicionar `Department` linhas e relacionadas `Course` linhas para o novo `Department` linhas.</span><span class="sxs-lookup"><span data-stu-id="fd235-447">Include code or scripts to add `Department` rows and related `Course` rows to the new `Department` rows.</span></span>
* <span data-ttu-id="fd235-448">Não use o departamento de "Temp" ou o valor padrão para `Course.DepartmentID `.</span><span class="sxs-lookup"><span data-stu-id="fd235-448">Would not use the "Temp" department or the default value for `Course.DepartmentID `.</span></span>

<span data-ttu-id="fd235-449">O seguinte tutorial abrange os dados relacionados.</span><span class="sxs-lookup"><span data-stu-id="fd235-449">The next tutorial covers related data.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="fd235-450">[Anterior](xref:data/ef-rp/migrations)
[Próximo](xref:data/ef-rp/read-related-data)</span><span class="sxs-lookup"><span data-stu-id="fd235-450">[Previous](xref:data/ef-rp/migrations)
[Next](xref:data/ef-rp/read-related-data)</span></span>