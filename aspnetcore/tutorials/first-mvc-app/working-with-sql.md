---
title: "使用 SQL Server LocalDB"
author: rick-anderson
description: "使用有簡單 MVC 應用程式的 SQL Server LocalDB"
keywords: ASP.NET Core,SQL Server LocalDB, SQL Server, LocalDB
ms.author: riande
manager: wpickett
ms.date: 03/07/2017
ms.topic: get-started-article
ms.assetid: ff8fd9b8-7c98-424d-8641-7524e23bf541
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/working-with-sql
ms.openlocfilehash: dd8b8603d8444c95f086fd593aabe86d60f93ad4
ms.sourcegitcommit: eb025f2166023e1c394a0213c7ed8a9ca7190da5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2017
---
# <a name="working-with-sql-server-localdb"></a><span data-ttu-id="2a8a5-104">使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="2a8a5-104">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="2a8a5-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2a8a5-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="2a8a5-106">`MvcMovieContext` 物件會處理連線到資料庫和將 `Movie` 物件對應至資料庫記錄的工作。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-106">The `MvcMovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="2a8a5-107">在 *Startup.cs* 檔案的 `ConfigureServices` 方法中，以[相依性插入](xref:fundamentals/dependency-injection)容器登錄資料庫內容：</span><span class="sxs-lookup"><span data-stu-id="2a8a5-107">The database context is registered with the [Dependency Injection](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

<span data-ttu-id="2a8a5-108">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=ConfigureServices&highlight=6-7)]</span><span class="sxs-lookup"><span data-stu-id="2a8a5-108">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=ConfigureServices&highlight=6-7)]</span></span>

<span data-ttu-id="2a8a5-109">ASP.NET Core [組態](xref:fundamentals/configuration)系統會讀取 `ConnectionString`。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-109">The ASP.NET Core [Configuration](xref:fundamentals/configuration) system reads the `ConnectionString`.</span></span> <span data-ttu-id="2a8a5-110">對於本機開發，它會從 *appsettings.json* 檔案取得連接字串：</span><span class="sxs-lookup"><span data-stu-id="2a8a5-110">For local development, it gets the connection string from the *appsettings.json* file:</span></span>

<span data-ttu-id="2a8a5-111">[!code-javascript[Main](start-mvc/sample/MvcMovie/appsettings.json?highlight=2&range=8-10)]</span><span class="sxs-lookup"><span data-stu-id="2a8a5-111">[!code-javascript[Main](start-mvc/sample/MvcMovie/appsettings.json?highlight=2&range=8-10)]</span></span>

<span data-ttu-id="2a8a5-112">當您將應用程式部署到測試或生產環境伺服器時，可以使用環境變數或另一個方法來設定實際 SQL Server 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-112">When you deploy the app to a test or production server, you can use an environment variable or another approach to set the connection string to a real SQL Server.</span></span> <span data-ttu-id="2a8a5-113">如需詳細資訊，請參閱[組態](xref:fundamentals/configuration)。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-113">See [Configuration](xref:fundamentals/configuration) for more information.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="2a8a5-114">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="2a8a5-114">SQL Server Express LocalDB</span></span>

<span data-ttu-id="2a8a5-115">LocalDB 是輕量版的 SQL Server Express Database Engine，以程式開發為目標。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-115">LocalDB is a lightweight version of the SQL Server Express Database Engine that is targeted for program development.</span></span> <span data-ttu-id="2a8a5-116">LocalDB 會視需要啟動，並以使用者模式執行，因此沒有複雜的組態。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-116">LocalDB starts on demand and runs in user mode, so there is no complex configuration.</span></span> <span data-ttu-id="2a8a5-117">根據預設，LocalDB 資料庫會在 *C:/Users/\<使用者\>* 目錄中建立 "\*.mdf" 檔案。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-117">By default, LocalDB database creates "\*.mdf" files in the *C:/Users/\<user\>* directory.</span></span>

* <span data-ttu-id="2a8a5-118">從 [檢視] 功能表中，開啟 [SQL Server 物件總管] (SSOX)。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-118">From the **View** menu, open **SQL Server Object Explorer** (SSOX).</span></span>

  ![檢視功能表](working-with-sql/_static/ssox.png)

* <span data-ttu-id="2a8a5-120">以滑鼠右鍵按一下 `Movie` 資料表 > [檢視表設計工具]</span><span class="sxs-lookup"><span data-stu-id="2a8a5-120">Right click on the `Movie` table **> View Designer**</span></span>

  ![在電影資料表上開啟操作功能表](working-with-sql/_static/design.png)

  ![在設計工具中開啟電影資料表](working-with-sql/_static/dv.png)

<span data-ttu-id="2a8a5-123">請注意 `ID` 旁的索引鍵圖示。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-123">Note the key icon next to `ID`.</span></span> <span data-ttu-id="2a8a5-124">根據預設，EF 會將名為 `ID` 的屬性設為主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-124">By default, EF will make a property named `ID` the primary key.</span></span>

* <span data-ttu-id="2a8a5-125">以滑鼠右鍵按一下 `Movie` 資料表 > [檢視資料]</span><span class="sxs-lookup"><span data-stu-id="2a8a5-125">Right click on the `Movie` table **> View Data**</span></span>

  ![在電影資料表上開啟操作功能表](working-with-sql/_static/ssox2.png)

  ![開啟的電影資料表顯示資料表資料](working-with-sql/_static/vd22.png)

## <a name="seed-the-database"></a><span data-ttu-id="2a8a5-128">植入資料庫</span><span class="sxs-lookup"><span data-stu-id="2a8a5-128">Seed the database</span></span>

<span data-ttu-id="2a8a5-129">在 *Models* 資料夾中建立名為 `SeedData` 的新類別。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-129">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="2a8a5-130">使用下列程式碼取代產生的程式碼：</span><span class="sxs-lookup"><span data-stu-id="2a8a5-130">Replace the generated code with the following:</span></span>

<span data-ttu-id="2a8a5-131">[!code-csharp[Main](start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]</span><span class="sxs-lookup"><span data-stu-id="2a8a5-131">[!code-csharp[Main](start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]</span></span>

<span data-ttu-id="2a8a5-132">如果資料庫中有任何電影，則種子初始設定式會返回，而且不會新增任何電影。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-132">If there are any movies in the DB, the seed initializer returns and no movies are added.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="2a8a5-133">新增種子初始設定式</span><span class="sxs-lookup"><span data-stu-id="2a8a5-133">Add the seed initializer</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2a8a5-134">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2a8a5-134">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="2a8a5-135">在 *Program.cs* 檔案中，將種子初始設定式新增至 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="2a8a5-135">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

<span data-ttu-id="2a8a5-136">[!code-csharp[Main](start-mvc/sample/MvcMovie/Program.cs?highlight=6,16-32)]</span><span class="sxs-lookup"><span data-stu-id="2a8a5-136">[!code-csharp[Main](start-mvc/sample/MvcMovie/Program.cs?highlight=6,16-32)]</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2a8a5-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2a8a5-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="2a8a5-138">在 *Startup.cs* 檔案中，將種子初始設定式新增至 `Configure` 方法的結尾處。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-138">Add the seed initializer to the end of the `Configure` method in the *Startup.cs* file.</span></span>

<span data-ttu-id="2a8a5-139">[!code-csharp[Main](start-mvc/sample/MvcMovie/Startup.cs?highlight=9&name=snippet_seed)]</span><span class="sxs-lookup"><span data-stu-id="2a8a5-139">[!code-csharp[Main](start-mvc/sample/MvcMovie/Startup.cs?highlight=9&name=snippet_seed)]</span></span>

---

<span data-ttu-id="2a8a5-140">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="2a8a5-140">Test the app</span></span>

* <span data-ttu-id="2a8a5-141">刪除資料庫中的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-141">Delete all the records in the DB.</span></span> <span data-ttu-id="2a8a5-142">您可以使用瀏覽器或 SSOX 的刪除連結來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-142">You can do this with the delete links in the browser or from SSOX.</span></span>
* <span data-ttu-id="2a8a5-143">強制應用程式初始化 (呼叫 `Startup` 類別中的方法)，以執行植入方法。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-143">Force the app to initialize (call the methods in the `Startup` class) so the seed method runs.</span></span> <span data-ttu-id="2a8a5-144">若要強制初始化，IIS Express 必須停止並重新啟動。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-144">To force initialization, IIS Express must be stopped and restarted.</span></span> <span data-ttu-id="2a8a5-145">您可以使用下列其中一個方法來執行此工作：</span><span class="sxs-lookup"><span data-stu-id="2a8a5-145">You can do this with any of the following approaches:</span></span>

  * <span data-ttu-id="2a8a5-146">以滑鼠右鍵按一下通知區域中的 IIS Express 系統匣圖示，然後點選 [結束] 或 [停止站台]。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-146">Right click the IIS Express system tray icon in the notification area and tap **Exit** or **Stop Site**</span></span>

    ![IIS Express 系統匣圖示](working-with-sql/_static/iisExIcon.png)

    ![操作功能表](working-with-sql/_static/stopIIS.png)

   * <span data-ttu-id="2a8a5-149">如果您已在非偵錯模式中執行 VS，請按 F5 以偵錯模式執行。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-149">If you were running VS in non-debug mode, press F5 to run in debug mode</span></span>
   * <span data-ttu-id="2a8a5-150">如果您已在偵錯模式中執行 VS，請停止偵錯工具，然後按 F5。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-150">If you were running VS in debug mode, stop the debugger and press F5</span></span>
   
<span data-ttu-id="2a8a5-151">應用程式會顯示植入的資料。</span><span class="sxs-lookup"><span data-stu-id="2a8a5-151">The app shows the seeded data.</span></span>

![在 Microsoft Edge 中開啟 MVC 電影應用程式顯示電影資料](working-with-sql/_static/m55.png)

>[!div class="step-by-step"]
<span data-ttu-id="2a8a5-153">[上一頁](adding-model.md)
[下一頁](controller-methods-views.md)</span><span class="sxs-lookup"><span data-stu-id="2a8a5-153">[Previous](adding-model.md)
[Next](controller-methods-views.md)</span></span>  