---
title: "데이터베이스 미러링 및 전체 텍스트 카탈로그(SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터베이스 미러링 [SQL Server], 상호 운용성"
  - "전체 텍스트 카탈로그 [SQL Server], 데이터베이스 미러링"
  - "카탈로그 [SQL Server], 데이터베이스 미러링"
ms.assetid: e34072ae-fe8a-462d-bb03-02fa0987f793
caps.latest.revision: 50
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 50
---
# 데이터베이스 미러링 및 전체 텍스트 카탈로그(SQL Server)
  전체 텍스트 카탈로그가 있는 데이터베이스를 미러링하려면 일반적인 백업을 사용하여 주 데이터베이스의 전체 데이터베이스 백업을 만든 다음 백업을 복원하여 데이터베이스를 미러 서버로 복사합니다. 자세한 내용은 [미러 데이터베이스에서 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)를 참조하세요.  
  
## 장애 조치(Failover) 이전의 전체 텍스트 카탈로그 및 인덱스  
 새로 생성된 미러 데이터베이스에서 전체 텍스트 카탈로그는 데이터베이스가 백업될 때와 동일합니다. 데이터베이스 미러링이 시작된 후 CREATE FULLTEXT CATALOG, ALTER FULLTEXT CATALOG, DROP FULLTEXT CATALOG 등과 같은 DDL 문으로 적용된 모든 카탈로그 수준 변경 내용은 기록되고 미러 서버로 전송되어 미러 데이터베이스에서 재생됩니다. 그러나 인덱스 수준 변경 내용은 주 서버에 기록되지 않으므로 미러 데이터베이스에서 재현되지 않습니다. 따라서 미러 데이터베이스의 전체 텍스트 카탈로그 내용은 주 데이터베이스의 전체 텍스트 카탈로그 내용이 변경됨에 따라 동기화되지 않습니다.  
  
## 장애 조치 이후의 전체 텍스트 인덱스  
 장애 조치 이후 새로운 주 서버에서 또는 다음 상황에서 전체 텍스트 인덱스의 전체 탐색이 필요하거나 유용할 수 있습니다.  
  
-   변경 추적이 전체 텍스트 인덱스에서 해제되어 있으면 다음 문을 사용하여 해당 인덱스에서 전체 탐색을 시작해야 합니다.  
  
     ALTER FULLTEXT INDEX ON *table_name* START FULL POPULATION  
  
-   전체 텍스트 인덱스가 변경 내용을 자동으로 추적하도록 구성되어 있으면 전체 텍스트 인덱스가 자동으로 동기화됩니다. 그러나 동기화로 인해 전체 텍스트 성능이 저하될 수 있습니다. 성능이 너무 저하될 경우에는 다음과 같이 변경 내용 추적을 해제하여 전체 탐색을 수행한 후 자동 추적을 다시 설정할 수 있습니다.  
  
    -   변경 내용 추적을 해제하려면  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING OFF  
  
    -   변경 내용 자동 추적을 자동으로 설정하려면  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING AUTO  
  
    > [!NOTE]  
    >  자동 변경 추적이 설정되어 있는지 확인하려면 [OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md) 함수를 사용하여 테이블의 **TableFullTextBackgroundUpdateIndexOn** 속성을 쿼리하세요.  
  
 자세한 내용은 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
>  장애 조치 이후의 탐색 시작은 복원 이후의 탐색 시작과 동일하게 작동합니다.  
  
## 서비스 강제 이후  
 미러 서버에 대해 서비스를 강제(데이터 손실 가능)한 후 전체 탐색을 시작합니다. 전체 탐색을 시작할 때 사용할 방법은 전체 텍스트 인덱스의 변경 내용 추적 여부에 따라 달라집니다. 자세한 내용은 이 항목의 앞부분에 나오는 "장애 조치 이후의 전체 텍스트 인덱스"를 참조하십시오.  
  
## 참고 항목  
 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [전체 텍스트 카탈로그와 인덱스 백업 및 복원](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
  