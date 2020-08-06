---
title: CLR 整合程式設計模型限制 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
author: rothja
ms.author: jroth
ms.openlocfilehash: 01a32e1460ad9c49061b39b1bdc419c7cd2f1342
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87584579"
---
# <a name="clr-integration-programming-model-restrictions"></a>CLR 整合程式設計模型限制
  當您建立 managed 預存程式或其他 managed 資料庫物件時，會執行特定的程式碼檢查， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 其會在第一次於資料庫中註冊、使用 `CREATE ASSEMBLY` 語句，以及在執行時間時，對 managed 程式碼元件執行檢查。 也會在執行階段檢查 Managed 程式碼，因為在組件中，可能會有執行階段絕對無法到達的程式碼路徑。  特別是這樣提供了註冊協力廠商組件的彈性，如此一來，當組件中的不安全程式碼設計為在用戶端環境中執行，但是絕對不會在主控的 CLR 內執行時，就不會封鎖該組件。 Managed 程式碼必須符合的需求取決於元件是否註冊為 `SAFE` 、 `EXTERNAL_ACCESS` 、或，是否為 `UNSAFE` `SAFE` 最嚴格的，並且如下所示。  
  
 除了對 Managed 程式碼組件所加諸的限制以外，也有授與的程式碼安全性權限。 Common Language Runtime (CLR) 支援稱為 Managed 程式碼之程式碼存取安全性 (CAS) 的安全性模型。 在此模型中，將會根據程式碼的識別來授與權限給組件。 `SAFE`、`EXTERNAL_ACCESS` 和 `UNSAFE` 組件有不同的 CAS 權限。 如需詳細資訊，請參閱[CLR 整合代碼啟用安全性](../security/clr-integration-code-access-security.md)。  
  
## <a name="create-assembly-checks"></a>CREATE ASSEMBLY 檢查  
 當執行 `CREATE ASSEMBLY` 陳述式時，將會針對每一個安全性層級執行下列檢查。  如果任何檢查失敗，`CREATE ASSEMBLY` 將會失敗，並傳回錯誤訊息。  
  
### <a name="global-any-security-level"></a>全域 (任何安全性層級)  
 所有參考的組件都必須符合下列其中一個或多個準則：  
  
-   此組件已經在資料庫中註冊。  
  
-   此組件是其中一個支援的組件。 如需詳細資訊，請參閱[支援的 .NET Framework 程式庫](supported-net-framework-libraries.md)。  
  
-   您正在使用 `CREATE ASSEMBLY FROM` * \<location> ，* 而且所有參考的元件及其相依性都可在中取得 *\<location>* 。  
  
-   您使用的是 `CREATE ASSEMBLY FROM` * \<bytes ...> ，* 而且所有的參考都是透過以空格分隔的位元組來指定。  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 所有 `EXTERNAL_ACCESS` 組件都必須符合下列準則：  
  
-   靜態欄位無法用來儲存資訊。 允許唯讀靜態欄位。  
  
-   通過 PEVerify 測試。 用來檢查 MSIL 程式碼及關聯的中繼資料確實符合類型安全需求的 PEVerify 工具 (peverify.exe) 隨附在 .NET Framework SDK 中。  
  
-   例如，將不會使用與 `SynchronizationAttribute` 類別的同步處理。  
  
-   不會使用 Finalizer 方法。  
  
 `EXTERNAL_ACCESS` 組件中不允許下列自訂屬性：  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   所有 `EXTERNAL_ACCESS` 組件條件都會檢查。  
  
## <a name="runtime-checks"></a>執行階段檢查  
 執行階段會檢查程式碼組件是否有下列條件。 如果找到這些條件的任何一個，將不允許執行 Managed 程式碼，而且將會擲回例外狀況。  
  
### <a name="unsafe"></a>UNSAFE  
 不允許載入元件（不論是 `System.Reflection.Assembly.Load()` 從位元組陣列呼叫方法，或是透過使用 `Reflection.Emit` 命名空間隱含）。  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 所有 `UNSAFE` 條件都會檢查。  
  
 不允許在支援的組件清單中使用下列主機保護屬性 (HPA) 值當做註解的所有類型和方法。  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Synchronization  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 如需 Hpa 的詳細資訊，以及支援的元件中不允許的類型和成員清單，請參閱[主控制項保護屬性和 CLR 整合程式設計](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)。  
  
### <a name="safe"></a>SAFE  
 所有 `EXTERNAL_ACCESS` 條件都會檢查。  
  
## <a name="see-also"></a>另請參閱  
 [支援的 .NET Framework 程式庫](supported-net-framework-libraries.md)   
 [CLR 整合代碼啟用安全性](../security/clr-integration-code-access-security.md)   
 [主機保護屬性和 CLR 整合程式設計](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [建立組件](../assemblies/creating-an-assembly.md)  
  
  
