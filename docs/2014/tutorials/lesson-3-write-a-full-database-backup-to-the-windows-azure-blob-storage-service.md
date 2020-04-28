---
title: '3 단원: Azure Blob Storage 서비스에 전체 데이터베이스 백업 작성 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 454c8296-64e9-46ed-b141-5ebfbc8a4fe2
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 1d5a749c61a3bc97de841e1149dd1539cbc990f2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70153472"
---
# <a name="lesson-3-write-a-full-database-backup-to-the-azure-blob-storage-service"></a>3단원: Azure Blob Storage Service로 전체 데이터베이스 백업 작성
  이 단원에서는 tsql 문을 사용 하 여 Azure Blob storage 서비스에 대 한 전체 데이터베이스 백업을 수행 하는 방법을 보여 줍니다.  
  
## <a name="perform-a-full-database-backup-to-the-azure-blob-storage-service"></a>Azure Blob Storage 서비스에 대 한 전체 데이터베이스 백업 수행  
 전체 데이터베이스 백업을 만들려면 다음 절차를 따르세요.  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 연결합니다.  
  
2.  **개체 탐색기**에서 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]인스턴스에 연결합니다.  
  
3.  표준 메뉴 모음에서 **새 쿼리**를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 창에 붙여 넣고 필요한 대로 수정한 다음 **실행**을 클릭합니다.  
  
    ```  
    BACKUP DATABASE[AdventureWorks2012]   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/   
    WITH CREDENTIAL = 'mycredential';  
    /* name of the credential you created in the previous step */   
    GO  
  
    ```  
  
5.  개체 탐색기에서 Azure Storage에 연결합니다. 컨테이너 및 새로 만든 백업 파일을 찾아봅니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [4 단원: 전체 데이터베이스 백업에서 복원 수행](../../2014/tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)  
  
  
