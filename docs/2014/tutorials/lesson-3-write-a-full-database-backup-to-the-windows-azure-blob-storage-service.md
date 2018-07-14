---
title: '3 단원: Windows Azure Blob Storage 서비스에 전체 데이터베이스 백업을 작성 하 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 454c8296-64e9-46ed-b141-5ebfbc8a4fe2
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 4a28465f0175be0bfc12e5c9d51a267ae6597ec6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236083"
---
# <a name="lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>Lesson 3: Write a Full Database Backup to the Windows Azure Blob Storage Service
  이 단원에서는 Windows Azure Blob 저장소 서비스로 전체 데이터베이스 백업을 수행하는 tsql 문을 사용하는 방법을 보여 줍니다.  
  
## <a name="perform-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>Windows Azure Blob 저장소 서비스로 전체 데이터베이스 백업 수행  
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
  
5.  개체 탐색기에서 Azure 저장소에 연결합니다. 컨테이너 및 새로 만든 백업 파일을 찾아봅니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [Lesson 4: Perform a Restore From a Full Database Backup](../../2014/tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)입니다.  
  
  
