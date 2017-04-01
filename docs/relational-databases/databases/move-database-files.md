---
title: "데이터베이스 파일 이동 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "재해 복구 [SQL Server], 데이터베이스 파일 이동"
  - "파일 [SQL Server], 이동"
  - "데이터 파일 [SQL Server], 이동"
  - "파일 이동 [SQL Server]"
  - "전체 텍스트 카탈로그 이동"
  - "데이터베이스 이동"
  - "전체 텍스트 카탈로그 [SQL Server], 이동"
  - "데이터베이스 파일 이동"
  - "예약된 디스크 유지 관리 [SQL Server]"
  - "파일 이동"
  - "데이터베이스 파일 재배치"
  - "계획된 데이터베이스 재배치 [SQL Server]"
  - "데이터베이스 [SQL Server], 이동"
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 데이터베이스 파일 이동
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문의 FILENAME 절에 새 파일 위치를 지정하여 시스템 및 사용자 데이터베이스를 이동할 수 있습니다. 데이터, 로그 및 전체 텍스트 카탈로그 파일도 이런 식으로 이동할 수 있습니다. 이 방법은 다음과 같은 경우 유용합니다.  
  
-   오류 복구. 하드웨어 오류로 인해 데이터베이스가 주의 대상 모드에 있거나 종료된 경우를 예로 들 수 있습니다.  
  
-   계획된 재배치  
  
-   예약된 디스크 유지 관리를 위한 재배치  
  
## 섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[사용자 데이터베이스 이동](../../relational-databases/databases/move-user-databases.md)|사용자 데이터베이스 파일과 전체 텍스트 카탈로그 파일을 새 위치로 이동하는 절차에 대해 설명합니다.|  
|[시스템 데이터베이스 이동](../../relational-databases/databases/move-system-databases.md)|시스템 데이터베이스 파일을 새 위치로 이동하는 절차에 대해 설명합니다.|  
  
## 참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  