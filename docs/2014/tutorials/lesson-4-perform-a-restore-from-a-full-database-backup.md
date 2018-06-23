---
title: '4 단원: 전체 데이터베이스 백업에서 복원을 수행 하 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 580f76e6-9802-4abc-9043-db6de592c733
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8869fa4bba6050dd0c15b8b59b7f2d091902936f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079437"
---
# <a name="lesson-4-perform-a-restore-from-a-full-database-backup"></a>4 단원: 전체 데이터베이스 백업에서 복원 수행
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
    , STATS = 5 – use this to see monitor the progress  
    GO  
  
    ```  
  
5.  T-SQL 문을 확인 하 고 클릭 **Execute**  
  
### <a name="return-to-tutorials-portal"></a>자습서 포털로 돌아가기  
 [자습서: SQL Server 백업 및 복원 Windows azure Blob 저장소 서비스](../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)합니다.  
  
  