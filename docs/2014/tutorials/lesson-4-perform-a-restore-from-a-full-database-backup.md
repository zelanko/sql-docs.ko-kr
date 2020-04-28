---
title: '4 단원: 전체 데이터베이스 백업에서 복원 수행 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 580f76e6-9802-4abc-9043-db6de592c733
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: de9a356589ac6bceb532ed4cecf509f957e3c337
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70153398"
---
# <a name="lesson-4-perform-a-restore-from-a-full-database-backup"></a>4단원: 전체 데이터베이스 백업에서 복원 수행
  이 단원에서는 이전 단원에서 만든 전체 데이터베이스 백업에서 복원을 수행하는 tsql 문을 사용하는 방법을 보여 줍니다.  
  
## <a name="perform-a-restore-of-a-database-backup"></a>데이터베이스 백업에서 복원 수행  
 전체 데이터베이스 백업을 복원하려면 다음 절차를 따르세요.  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 연결합니다.  
  
2.  **개체 탐색기**에서 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]인스턴스에 연결합니다.  
  
3.  표준 메뉴 모음에서 **새 쿼리**를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 창에 붙여 넣고 필요한 대로 수정합니다.  
  
    ```  
    RESTORE DATABASE AdventureWorks2012   
    FROM URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    WITH CREDENTIAL = 'mycredential';  
    , STATS = 5 - use this to see monitor the progress  
    GO  
  
    ```  
  
5.  T-sql 문을 확인 하 고 **실행** 을 클릭 합니다.  
  
### <a name="return-to-tutorials-portal"></a>자습서 포털로 돌아가기  
 [자습서: 백업 및 Azure Blob Storage 서비스에 SQL Server 복원](../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
  
