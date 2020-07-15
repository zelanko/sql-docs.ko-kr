---
title: 데이터베이스 삭제 | Microsoft 문서
description: SQL Server Management Studio 또는 Transact-SQL을 사용하여 SQL Server의 SQL Server Management Studio에 있는 사용자 정의 데이터베이스를 삭제하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database removal [SQL Server], SQL Server Management Studio
- removing databases
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- database removal [SQL Server]
ms.assetid: 1fd8c0f5-03e1-449a-af45-b8cacb479d9c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4a4665cd3b3f554c33a1c8640ee47dea94f911d6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85630663"
---
# <a name="delete-a-database"></a>데이터베이스 삭제
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 사용자 정의 데이터베이스를 삭제하는 방법을 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터베이스를 삭제하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [데이터베이스를 삭제한 후](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   시스템 데이터베이스는 삭제할 수 없습니다.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
  
-   데이터베이스에 있는 모든 데이터베이스 스냅샷을 삭제합니다. 자세한 내용은 [Drop a Database Snapshot &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
-   데이터베이스가 로그 전달과 관련되어 있으면 로그 전달을 제거합니다.  
  
-   데이터베이스가 트랜잭션 복제용으로 게시되거나 복제를 병합하기 위해 게시 또는 구독되는 경우 데이터베이스에서 복제를 제거합니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   데이터베이스 전체 백업을 고려합니다. 삭제된 데이터베이스는 백업 복원을 통해서만 다시 만들 수 있습니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 DROP DATABASE를 실행하려면 최소한 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-database"></a>데이터베이스를 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 삭제할 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
3.  올바른 데이터베이스가 선택되었는지 확인하고 **확인**을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-database"></a>데이터베이스를 삭제하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 `Sales` 및 `NewSales` 데이터베이스를 제거합니다.  
  
```sql  
USE master ;  
GO  
DROP DATABASE Sales, NewSales ;  
GO  
```  
  
##  <a name="follow-up-after-deleting-a-database"></a><a name="FollowUp"></a> 후속 작업: 데이터베이스를 삭제한 후  
 **master** 데이터베이스를 백업합니다. **master** 를 복원해야 할 경우 마지막 **master** 백업 이후 삭제된 모든 데이터베이스의 참조가 시스템 카탈로그 뷰에 아직 있어서 오류 메시지가 발생할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
