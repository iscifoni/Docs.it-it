---
uid: whitepapers/ms03-32-issue
title: Correzione di errore "Applicazione Server non disponibile" dopo aver applicato l'aggiornamento della sicurezza per Internet Explorer | Documenti Microsoft
author: rick-anderson
description: Questo documento descrive la patch che corregge un problema con l'aggiornamento della sicurezza MS03-32 per Internet Explorer che influisce sulle applicazioni ASP.NET 1.0 in esecuzione nell'elemento di lavoro...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: 8658e387aeb4ea0340080666906b2b89db49a31a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/10/2017
---
<a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a><span data-ttu-id="1c223-103">Correggere l'errore "Applicazione Server non disponibile" dopo aver applicato l'aggiornamento della sicurezza per Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="1c223-103">Fix for 'Server Application Unavailable' Error after Applying Security Update for IE</span></span>
====================
> <span data-ttu-id="1c223-104">Questo documento descrive la patch che corregge un problema con l'aggiornamento della sicurezza MS03-32 per Internet Explorer che influisce sulle applicazioni ASP.NET 1.0 in esecuzione in Windows XP Professional.</span><span class="sxs-lookup"><span data-stu-id="1c223-104">This paper describes the patch that fixes an issue with the MS03-32 Security Update for Internet Explorer that affects ASP.NET 1.0 applications running on Windows XP Professional.</span></span>
> 
> <span data-ttu-id="1c223-105">Si applica a ASP.NET 1.0 e Windows XP Professional.</span><span class="sxs-lookup"><span data-stu-id="1c223-105">Applies to ASP.NET 1.0 and Windows XP Professional.</span></span>


<span data-ttu-id="1c223-106">Microsoft identificato un problema con l'aggiornamento della sicurezza per la patch di sicurezza di Internet Explorer MS03-32 e versione 1.0 di ASP.NET in esecuzione in Windows XP.</span><span class="sxs-lookup"><span data-stu-id="1c223-106">Microsoft identified an issue with the MS03-32 Security Update for Internet Explorer security patch and ASP.NET 1.0 running on Windows XP.</span></span> <span data-ttu-id="1c223-107">Questa patch può essere installata manualmente o per ottenere gli aggiornamenti critici di recente dal sito Windows Update.</span><span class="sxs-lookup"><span data-stu-id="1c223-107">This patch can be installed manually or by obtaining recent critical updates from the Windows Update site.</span></span>

<span data-ttu-id="1c223-108">Il sintomo di questo problema è che dopo l'installazione di patch in un computer Windows XP, tutte le richieste di applicazioni ASP.NET in esecuzione nel server web IIS 5.1 locale dare come risultato un messaggio di errore che indica "Applicazione Server non disponibile".</span><span class="sxs-lookup"><span data-stu-id="1c223-108">The symptom of this issue is that after installing the patch on a Windows XP machine, all requests to ASP.NET applications running on the local IIS 5.1 web server result in an error message saying "Server Application Unavailable".</span></span> <span data-ttu-id="1c223-109">Le richieste ai server web remoto non sono interessate.</span><span class="sxs-lookup"><span data-stu-id="1c223-109">Requests to remote web servers are unaffected.</span></span>

<span data-ttu-id="1c223-110">Questo problema influisce solo sulle installazioni in esecuzione ASP.NET 1.0 in Windows XP.</span><span class="sxs-lookup"><span data-stu-id="1c223-110">This issue only impacts installations running ASP.NET 1.0 on Windows XP.</span></span> <span data-ttu-id="1c223-111">Non influisce sulle macchine che eseguono Windows 2000 o Windows Server 2003.</span><span class="sxs-lookup"><span data-stu-id="1c223-111">It does not impact machines running Windows 2000 or Windows Server 2003.</span></span> <span data-ttu-id="1c223-112">Non influisce inoltre i computer che eseguono Windows XP con ASP.NET 1.1 installato.</span><span class="sxs-lookup"><span data-stu-id="1c223-112">It also does not impact machines running Windows XP with ASP.NET 1.1 installed.</span></span>

<span data-ttu-id="1c223-113">Si noti che questo problema **non** un bug di sicurezza con ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1c223-113">Please note that this issue **is not** a security bug with ASP.NET.</span></span> <span data-ttu-id="1c223-114">Si **non** aprire o consentire eventuali attacchi contro un server o un'applicazione ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1c223-114">It **does not** open up or allow any malicious attacks against an ASP.NET application or server.</span></span> <span data-ttu-id="1c223-115">Al contrario, è semplicemente un bug funzionale causato dalla patch stesso.</span><span class="sxs-lookup"><span data-stu-id="1c223-115">Instead, it is purely a functional bug caused by the patch itself.</span></span>

<span data-ttu-id="1c223-116">Si sta lavorando attivamente in una soluzione permanente per questo problema.</span><span class="sxs-lookup"><span data-stu-id="1c223-116">We are working hard on a permanent solution for this issue.</span></span> <span data-ttu-id="1c223-117">Nel frattempo, è possibile eseguire il seguente file batch come soluzione alternativa per il problema.</span><span class="sxs-lookup"><span data-stu-id="1c223-117">In the meantime, you can execute the following batch file as a workaround for the issue.</span></span> <span data-ttu-id="1c223-118">Il file batch effettua le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1c223-118">The batch file does the following:</span></span>

1. <span data-ttu-id="1c223-119">Arresta i servizi di stato IIS e ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1c223-119">Stops the IIS and ASP.NET state services</span></span>
2. <span data-ttu-id="1c223-120">Elimina e ricrea l'account ASPNET con una password temporanea nota</span><span class="sxs-lookup"><span data-stu-id="1c223-120">Deletes and recreates the ASPNET account with a known temporary password</span></span>
3. <span data-ttu-id="1c223-121">Usa Windows `runas` comando per avviare un eseguibile che consente di creare un profilo utente ASPNET</span><span class="sxs-lookup"><span data-stu-id="1c223-121">Uses the Windows `runas` command to launch an executable that creates an ASPNET user profile</span></span>
4. <span data-ttu-id="1c223-122">Registrare nuovamente ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1c223-122">Re-registers ASP.NET.</span></span> <span data-ttu-id="1c223-123">Verrà creata una nuova password casuale per l'account e si applica impostazioni di controllo di accesso predefinite ASP.NET per tale</span><span class="sxs-lookup"><span data-stu-id="1c223-123">This creates a new random password for the account and applies default ASP.NET access control settings for it</span></span>
5. <span data-ttu-id="1c223-124">Riavvia il servizio IIS</span><span class="sxs-lookup"><span data-stu-id="1c223-124">Restarts the IIS service</span></span>

<span data-ttu-id="1c223-125">Il file batch contiene una password temporanea hardcoded di "**1pass@word**" quale sarà chiesto di immettere per il runas comando quando viene eseguito il file batch.</span><span class="sxs-lookup"><span data-stu-id="1c223-125">The batch file contains a hardcoded temporary password of "**1pass@word**" which you will be prompted to enter for the runas command when the batch file is run.</span></span> <span data-ttu-id="1c223-126">Al termine dell'esecuzione del comando runas, la password dell'account ASPNET viene ricreata con un valore casuale complesso.</span><span class="sxs-lookup"><span data-stu-id="1c223-126">After the runas command completes, the ASPNET account password is recreated with a strong random value.</span></span> <span data-ttu-id="1c223-127">Si noti che il file batch potrebbe non riuscire se la password hardcoded non soddisfa i requisiti di complessità delle password nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="1c223-127">Note that the batch file may fail if the hardcoded password does not meet the password complexity requirements in your environment.</span></span> <span data-ttu-id="1c223-128">Se è questo il caso, è possibile modificarlo in un altro valore appropriato per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="1c223-128">If that's the case, you can change it to another value that is appropriate for your environment.</span></span>

<span data-ttu-id="1c223-129">*> [!IMPORTANT]*Se si hanno aggiunto le impostazioni di controllo di accesso personalizzati o autorizzazioni dell'account del database per l'account ASPNET, dovranno essere ricreati dopo il completamento di questo file batch.</span><span class="sxs-lookup"><span data-stu-id="1c223-129">*> [!IMPORTANT]* If you have added custom access control settings or database account permissions for the ASPNET account, they will need to be recreated after this batch file completes.</span></span> <span data-ttu-id="1c223-130">Infatti, quando viene ricreato l'account, riceverà un nuovo ID di sicurezza (SID).</span><span class="sxs-lookup"><span data-stu-id="1c223-130">This is because when the account is recreated, it will get a new security identifier (SID).</span></span>

<span data-ttu-id="1c223-131">*> [!IMPORTANT]*Se si esegue il processo di lavoro ASP.NET con un account personalizzato diverso dall'account ASPNET, non è necessario eseguire questo file batch.</span><span class="sxs-lookup"><span data-stu-id="1c223-131">*> [!IMPORTANT]* If you are running the ASP.NET worker process with a custom account other than the ASPNET account, then you should not run this batch file.</span></span> <span data-ttu-id="1c223-132">Invece, si deve accedere modo interattivo o utilizzare il comando runas con tale account verrà creato un profilo utente per tale account.</span><span class="sxs-lookup"><span data-stu-id="1c223-132">Instead, you should log in interactively or use the runas command with that account which will create a user profile for that account.</span></span>

<span data-ttu-id="1c223-133">Il file batch è incluso nell'archivio autoestraente riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1c223-133">The batch file is included in the self-extracting archive below.</span></span> <span data-ttu-id="1c223-134">Utilizzo:</span><span class="sxs-lookup"><span data-stu-id="1c223-134">To use it:</span></span>

1. <span data-ttu-id="1c223-135">È necessario essere in esecuzione come account con privilegi di amministratore</span><span class="sxs-lookup"><span data-stu-id="1c223-135">You must be running as an account with Administrator privileges</span></span>
2. [<span data-ttu-id="1c223-136">Scaricare e aprire il file eseguibile autoestraente</span><span class="sxs-lookup"><span data-stu-id="1c223-136">Download and open the self-extracting executable file</span></span>](ms03-32-issue/_static/fixup1.exe)
3. <span data-ttu-id="1c223-137">Estrarre il contenuto in c:\.</span><span class="sxs-lookup"><span data-stu-id="1c223-137">Extract the contents to c:\\</span></span>
4. <span data-ttu-id="1c223-138">Scegliere Esegui... dal menu start e immettere`cmd.exe`</span><span class="sxs-lookup"><span data-stu-id="1c223-138">Select Run... from the start menu, and enter `cmd.exe`</span></span>
5. <span data-ttu-id="1c223-139">Nella finestra comando Apri, digitare `c:\fixup.cmd`.</span><span class="sxs-lookup"><span data-stu-id="1c223-139">In the open command windows, type `c:\fixup.cmd`.</span></span>
6. <span data-ttu-id="1c223-140">Quando richiesto, immettere  **1pass@word**  come password.</span><span class="sxs-lookup"><span data-stu-id="1c223-140">When prompted, enter **1pass@word** as the password.</span></span>
7. <span data-ttu-id="1c223-141">Se si dispone di impostazioni di controllo di accesso personalizzate in precedenza o le autorizzazioni per l'account ASPNET account di database, è necessario riapplicare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="1c223-141">If you have previously custom access control settings or database account permissions for the ASPNET account, you'll need to re-apply these settings now.</span></span>

<span data-ttu-id="1c223-142">Molti scusiamo per l'inconveniente che questo ha causato.</span><span class="sxs-lookup"><span data-stu-id="1c223-142">Many apologies for the inconvenience that this has caused.</span></span> <span data-ttu-id="1c223-143">È possibile registrare informazioni aggiuntive appena sarà disponibile.</span><span class="sxs-lookup"><span data-stu-id="1c223-143">We'll post additional information as it becomes available.</span></span>

<span data-ttu-id="1c223-144">La matrice di seguito in dettaglio le piattaforme e versioni interessate dal problema.</span><span class="sxs-lookup"><span data-stu-id="1c223-144">The matrix below details platforms and versions impacted by this issue.</span></span>

| <span data-ttu-id="1c223-145">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="1c223-145">.NET Framework</span></span> | <span data-ttu-id="1c223-146">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="1c223-146">Platform</span></span> | <span data-ttu-id="1c223-147">Interessati</span><span class="sxs-lookup"><span data-stu-id="1c223-147">Affected</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1c223-148">Versione 1.0</span><span class="sxs-lookup"><span data-stu-id="1c223-148">Version 1.0</span></span> | <span data-ttu-id="1c223-149">Windows 2000 Professional</span><span class="sxs-lookup"><span data-stu-id="1c223-149">Windows 2000 Professional</span></span> | <span data-ttu-id="1c223-150">No</span><span class="sxs-lookup"><span data-stu-id="1c223-150">No</span></span> |
| <span data-ttu-id="1c223-151">Versione 1.0</span><span class="sxs-lookup"><span data-stu-id="1c223-151">Version 1.0</span></span> | <span data-ttu-id="1c223-152">Windows 2000 Server</span><span class="sxs-lookup"><span data-stu-id="1c223-152">Windows 2000 Server</span></span> | <span data-ttu-id="1c223-153">No</span><span class="sxs-lookup"><span data-stu-id="1c223-153">No</span></span> |
| <span data-ttu-id="1c223-154">Versione 1.0</span><span class="sxs-lookup"><span data-stu-id="1c223-154">Version 1.0</span></span> | <span data-ttu-id="1c223-155">Windows XP Professional</span><span class="sxs-lookup"><span data-stu-id="1c223-155">Windows XP Professional</span></span> | <span data-ttu-id="1c223-156">Sì</span><span class="sxs-lookup"><span data-stu-id="1c223-156">Yes</span></span> |
| <span data-ttu-id="1c223-157">Versione 1.0</span><span class="sxs-lookup"><span data-stu-id="1c223-157">Version 1.0</span></span> | <span data-ttu-id="1c223-158">Windows Server 2003</span><span class="sxs-lookup"><span data-stu-id="1c223-158">Windows Server 2003</span></span> | <span data-ttu-id="1c223-159">No</span><span class="sxs-lookup"><span data-stu-id="1c223-159">No</span></span> |
| <span data-ttu-id="1c223-160">Versione 1.0</span><span class="sxs-lookup"><span data-stu-id="1c223-160">Version 1.0</span></span> | <span data-ttu-id="1c223-161">Windows XP Home Edition con Cassini</span><span class="sxs-lookup"><span data-stu-id="1c223-161">Windows XP Home with Cassini</span></span> | <span data-ttu-id="1c223-162">No</span><span class="sxs-lookup"><span data-stu-id="1c223-162">No</span></span> |
| <span data-ttu-id="1c223-163">Versione 1.1</span><span class="sxs-lookup"><span data-stu-id="1c223-163">Version 1.1</span></span> | <span data-ttu-id="1c223-164">Windows 2000 Professional</span><span class="sxs-lookup"><span data-stu-id="1c223-164">Windows 2000 Professional</span></span> | <span data-ttu-id="1c223-165">No</span><span class="sxs-lookup"><span data-stu-id="1c223-165">No</span></span> |
| <span data-ttu-id="1c223-166">Versione 1.1</span><span class="sxs-lookup"><span data-stu-id="1c223-166">Version 1.1</span></span> | <span data-ttu-id="1c223-167">Windows 2000 Server</span><span class="sxs-lookup"><span data-stu-id="1c223-167">Windows 2000 Server</span></span> | <span data-ttu-id="1c223-168">No</span><span class="sxs-lookup"><span data-stu-id="1c223-168">No</span></span> |
| <span data-ttu-id="1c223-169">Versione 1.1</span><span class="sxs-lookup"><span data-stu-id="1c223-169">Version 1.1</span></span> | <span data-ttu-id="1c223-170">Windows XP Professional</span><span class="sxs-lookup"><span data-stu-id="1c223-170">Windows XP Professional</span></span> | <span data-ttu-id="1c223-171">No</span><span class="sxs-lookup"><span data-stu-id="1c223-171">No</span></span> |
| <span data-ttu-id="1c223-172">Versione 1.1</span><span class="sxs-lookup"><span data-stu-id="1c223-172">Version 1.1</span></span> | <span data-ttu-id="1c223-173">Windows Server 2003</span><span class="sxs-lookup"><span data-stu-id="1c223-173">Windows Server 2003</span></span> | <span data-ttu-id="1c223-174">No</span><span class="sxs-lookup"><span data-stu-id="1c223-174">No</span></span> |
| <span data-ttu-id="1c223-175">Versione 1.1</span><span class="sxs-lookup"><span data-stu-id="1c223-175">Version 1.1</span></span> | <span data-ttu-id="1c223-176">Windows XP Home Edition con Cassini</span><span class="sxs-lookup"><span data-stu-id="1c223-176">Windows XP Home with Cassini</span></span> | <span data-ttu-id="1c223-177">No</span><span class="sxs-lookup"><span data-stu-id="1c223-177">No</span></span> |

<span data-ttu-id="1c223-178">Grazie,</span><span class="sxs-lookup"><span data-stu-id="1c223-178">Thanks,</span></span>   
 <span data-ttu-id="1c223-179">Il Team di ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1c223-179">The ASP.NET Team</span></span>