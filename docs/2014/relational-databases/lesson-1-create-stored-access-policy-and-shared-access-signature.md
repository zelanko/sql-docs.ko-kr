---
title: 2단원. 컨테이너에서 정책 만들기 및 공유 액세스 서명 (SAS) 키 생성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7ddcef5d5e0695041742784151103c358a973d55
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806734"
---
# <a name="lesson-2-create-a-policy-on-container-and-generate-a-shared-access-signature-sas-key"></a>2단원. 컨테이너에 정책 만들기 및 SAS(공유 액세스 서명) 키 생성
  이 단원에서는 Blob 컨테이너에서 정책을 만들고 SAS키를 생성하는 방법을 배웁니다.  
  
 저장된 액세스 정책은 서버 쪽에서 공유 액세스 서명에 대한 제어 수준을 추가로 제공합니다. 공유 액세스 서명은 컨테이너, Blob, 큐 및 테이블에 대한 제한된 액세스 권한을 부여하는 URI입니다. 이 새로운 향상된 기능을 사용하는 경우 읽기, 쓰기 및 나열 권한이 있는 컨테이너에 정책을 만들어야 합니다.  
  
 다음 방법 중 하나를 사용하여 정책과 공유 액세스 서명을 만들 수 있습니다.  
  
-   Windows Azure REST API 작업: [컨테이너를 만듭니다](https://msdn.microsoft.com/library/azure/dd179468.aspx), [컨테이너 ACL 설정](https://msdn.microsoft.com/library/azure/dd179391.aspx), 및 [컨테이너 ACL 가져오기](https://msdn.microsoft.com/library/azure/dd179469.aspx)합니다.  
  
-   Windows Azure SDK의[CloudBlobContainer.GetSharedAccessSignature 메서드](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storageclient.cloudblobcontainer.getsharedaccesssignature.aspx) .  
  
    ```  
  
       string signature = blob.GetSharedAccessSignature(new SharedAccessPolicy()   
        {   
            // Specify the expiration time for the signature.   
            SharedAccessExpiryTime = DateTime.Now.Years(1),   
            // Specify the permissions granted by the signature.    
            Permissions = SharedAccessPermissions.Write | SharedAccessPermissions.Read   
        });  
  
    ```  
  
-   [Azure 스토리지 탐색기](http://azurestorageexplorer.codeplex.com/)등의 타사 Windows Azure 탐색기 도구.  
  
 **다음 단원:**  
  
 [3단원: SQL Server 자격 증명 만들기](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
  
