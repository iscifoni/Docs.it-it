---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: Esaminare i dettagli e i metodi di eliminazione | Documenti Microsoft
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 6d7d0fe5bd2f6a6bd7f9c7ca04a8f142223ccf8e
ms.sourcegitcommit: d1d8071d4093bf2444b5ae19d6e45c3d187e338b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/19/2017
---
<a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="5910d-102">Esaminare i dettagli e i metodi di eliminazione</span><span class="sxs-lookup"><span data-stu-id="5910d-102">Examining the Details and Delete Methods</span></span>
====================
<span data-ttu-id="5910d-103">Da [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="5910d-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE[Tutorial Note](sample/code-location.md)]

<span data-ttu-id="5910d-104">In questa parte dell'esercitazione, si esamineranno generato automaticamente `Details` e `Delete` metodi.</span><span class="sxs-lookup"><span data-stu-id="5910d-104">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="5910d-105">Esaminare i dettagli e i metodi di eliminazione</span><span class="sxs-lookup"><span data-stu-id="5910d-105">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="5910d-106">Aprire il `Movie` controller ed esaminare il `Details` metodo.</span><span class="sxs-lookup"><span data-stu-id="5910d-106">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="5910d-107">Il motore di scaffolding MVC che ha creato questo metodo di azione aggiunge un commento che mostra una richiesta HTTP che richiama il metodo.</span><span class="sxs-lookup"><span data-stu-id="5910d-107">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="5910d-108">In questo caso è un `GET` richiesta con tre segmenti di URL, il `Movies` controller, il `Details` (metodo) e un `ID` valore.</span><span class="sxs-lookup"><span data-stu-id="5910d-108">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="5910d-109">Codice innanzitutto semplifica la ricerca di dati utilizzando il `Find` metodo.</span><span class="sxs-lookup"><span data-stu-id="5910d-109">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="5910d-110">Un'importante funzionalità di protezione creata nel metodo è che il codice verifica che il `Find` metodo ha trovato un filmato prima che il codice tenta di utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="5910d-110">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="5910d-111">Ad esempio, un pirata informatico potrebbe causare errori nel sito modificando l'URL creato per i collegamenti da `http://localhost:xxxx/Movies/Details/1` esempio `http://localhost:xxxx/Movies/Details/12345` (o altri valori che non rappresentano un filmato effettivo).</span><span class="sxs-lookup"><span data-stu-id="5910d-111">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="5910d-112">Se non è stata selezionata per un filmato null, un film null restituirà un errore di database.</span><span class="sxs-lookup"><span data-stu-id="5910d-112">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="5910d-113">Esaminare i metodi `Delete` e `DeleteConfirmed`.</span><span class="sxs-lookup"><span data-stu-id="5910d-113">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="5910d-114">Si noti che il `HTTP Get``Delete` metodo non comporta l'eliminazione del filmato specificato, restituisce una visualizzazione del film in cui è possibile inviare (`HttpPost`) l'eliminazione...</span><span class="sxs-lookup"><span data-stu-id="5910d-114">Note that the `HTTP Get``Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion..</span></span> <span data-ttu-id="5910d-115">L'esecuzione di un'operazione di eliminazione in risposta a una richiesta GET (o l'esecuzione di un'operazione di modifica, di creazione o di qualsiasi altra azione che modifica i dati) introduce un problema di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5910d-115">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="5910d-116">Per ulteriori informazioni, vedere il post di blog di Stephen Walther [ASP.NET MVC suggerimento #46-non usare eliminare collegamenti poiché creano problemi di sicurezza](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span><span class="sxs-lookup"><span data-stu-id="5910d-116">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="5910d-117">Il metodo `HttpPost` che elimina i dati è denominato `DeleteConfirmed` per fornire al metodo HTTP POST un nome o una firma univoca.</span><span class="sxs-lookup"><span data-stu-id="5910d-117">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="5910d-118">Le firme dei due metodi sono illustrate di seguito:</span><span class="sxs-lookup"><span data-stu-id="5910d-118">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="5910d-119">Il Common Language Runtime (CLR) richiede metodi in rapporto di overload per disporre di una firma di parametro univoca, ovvero lo stesso nome di metodo ma un elenco diverso di parametri.</span><span class="sxs-lookup"><span data-stu-id="5910d-119">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="5910d-120">Tuttavia, in questo caso è necessario due metodi di eliminazione: uno per GET - e uno per POST che entrambi abbiano la stessa firma del parametro.</span><span class="sxs-lookup"><span data-stu-id="5910d-120">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="5910d-121">Entrambi devono accettare un singolo intero come parametro.</span><span class="sxs-lookup"><span data-stu-id="5910d-121">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="5910d-122">Per ordinare la natura, è possibile eseguire alcune operazioni.</span><span class="sxs-lookup"><span data-stu-id="5910d-122">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="5910d-123">Uno consiste nell'assegnare i metodi di nomi diversi.</span><span class="sxs-lookup"><span data-stu-id="5910d-123">One is to give the methods different names.</span></span> <span data-ttu-id="5910d-124">Questa operazione è stata eseguita dal meccanismo di scaffolding nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="5910d-124">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="5910d-125">Tuttavia in questo modo si introduce un piccolo problema: ASP.NET esegue il mapping dei segmenti di un URL ai metodi di azione in base al nome e, se si rinomina un metodo, generalmente il routing non è in grado di trovare questo metodo.</span><span class="sxs-lookup"><span data-stu-id="5910d-125">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="5910d-126">La soluzione è mostrata nell'esempio e consiste nell'aggiungere l'attributo `ActionName("Delete")` al metodo `DeleteConfirmed`.</span><span class="sxs-lookup"><span data-stu-id="5910d-126">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="5910d-127">Questo in modo efficace esegue il mapping per il sistema di routing in modo che un URL che includa */Delete/* disponibili per un POST di richiesta di `DeleteConfirmed` metodo.</span><span class="sxs-lookup"><span data-stu-id="5910d-127">This effectively performs mapping for the routing system so that a URL that includes */Delete/* for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="5910d-128">Un altro modo comune per evitare un problema con metodi che hanno firme e i nomi identici consiste nel modificare artificialmente la firma del metodo POST per includere un parametro non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5910d-128">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="5910d-129">Ad esempio, alcuni sviluppatori aggiungono un parametro di tipo `FormCollection` che viene passato al metodo POST e quindi semplicemente non usa il parametro:</span><span class="sxs-lookup"><span data-stu-id="5910d-129">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="5910d-130">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5910d-130">Summary</span></span>

<span data-ttu-id="5910d-131">Ora è un'applicazione ASP.NET MVC completa che archivia i dati in un database di database locale.</span><span class="sxs-lookup"><span data-stu-id="5910d-131">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="5910d-132">È possibile creare, leggere, aggiornare, eliminare e cercare film.</span><span class="sxs-lookup"><span data-stu-id="5910d-132">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="5910d-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5910d-133">Next Steps</span></span>

<span data-ttu-id="5910d-134">Dopo aver compilato e testato un'applicazione web, il passaggio successivo è per renderlo disponibile ad altri utenti per l'utilizzo su Internet.</span><span class="sxs-lookup"><span data-stu-id="5910d-134">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="5910d-135">A tale scopo, è necessario distribuirla in un provider di hosting web.</span><span class="sxs-lookup"><span data-stu-id="5910d-135">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="5910d-136">Microsoft offre l'hosting web gratuito per fino a 10 siti web in un [senza account di valutazione Azure](https://www.windowsazure.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="5910d-136">Microsoft offers free web hosting for up to 10 web sites in a [free Azure trial account](https://www.windowsazure.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="5910d-137">È consigliabile quindi seguire l'esercitazione [distribuire un'app protetta ASP.NET MVC con appartenenza, OAuth e il Database SQL in Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="5910d-137">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="5910d-138">Un'ottima esercitazione è di livello intermedio di Tom Dykstra [la creazione di un modello di dati di Entity Framework per un'applicazione MVC ASP.NET](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="5910d-138">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="5910d-139">[StackOverflow](http://stackoverflow.com/help) e [forum di ASP.NET MVC](https://forums.asp.net/1146.aspx) sono inserisce un'eccellente per porre domande.</span><span class="sxs-lookup"><span data-stu-id="5910d-139">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="5910d-140">Seguire [me](https://twitter.com/RickAndMSFT) su twitter, pertanto è possibile ottenere gli aggiornamenti in my esercitazioni più recente.</span><span class="sxs-lookup"><span data-stu-id="5910d-140">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="5910d-141">Commenti e suggerimenti sono ben accetti.</span><span class="sxs-lookup"><span data-stu-id="5910d-141">Feedback is welcome.</span></span>

<span data-ttu-id="5910d-142">- [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter:[@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5910d-142">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="5910d-143">- [Scott Hanselman](http://www.hanselman.com/blog/) twitter:[@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="5910d-143">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="5910d-144">Precedente</span><span class="sxs-lookup"><span data-stu-id="5910d-144">Previous</span></span>](adding-validation.md)