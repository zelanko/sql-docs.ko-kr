---
title: 원격 서버 연결 옵션 보기 또는 구성(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- remote servers [SQL Server], connection options
- servers [SQL Server], remote
- connections [SQL Server], remote servers
ms.assetid: 356d3e6b-8514-4bd2-a683-9de147949b2b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5dfc0aa145f106fc57c25a6249b928ee27ab4b87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62757201"
---
# <a name="view-or-configure-remote-server-connection-options-sql-server"></a>원격 서버 연결 옵션 보기 또는 구성(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 서버 수준에서 원격 서버 연결 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **원격 서버 연결 옵션을 보거나 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [원격 서버 연결 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 **sp_serveroption** 을 실행하려면 서버에 대한 ALTER ANY LINKED SERVER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-or-configure-remote-server-connection-options"></a>원격 서버 연결 옵션을 보거나 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **SQL Server 속성 - \<***server_name***>** 대화 상자에서 **연결**을 클릭합니다.  
  
3.  **연결** 페이지에서 **원격 서버 연결** 설정을 확인한 다음 필요한 경우 수정합니다.  
  
4.  원격 서버 쌍의 다른 서버에 대해 1단계에서 3단계까지 반복합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-remote-server-connection-options"></a>원격 서버 연결 옵션을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 [sp_helpserver](/sql/relational-databases/system-stored-procedures/sp-helpserver-transact-sql) 를 사용하여 모든 원격 서버에 대한 정보를 반환합니다.  
  
```sql  
USE master;  
GO  
EXEC sp_helpserver ;  
```  
  
#### <a name="to-configure-remote-server-connection-options"></a>원격 서버 연결 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 [sp_serveroption](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql) 을 사용하여 원격 서버를 구성하는 방법을 보여 줍니다. 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스인 `SEATTLE3`에 해당하는 원격 서버를 구성하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스와 데이터 정렬이 호환되도록 합니다.  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
##  <a name="FollowUp"></a> 후속 작업: 원격 서버 연결 옵션을 구성한 후  
 설정을 적용하려면 원격 서버를 중지한 후 다시 시작해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [원격 서버](remote-servers.md)   
 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_linkedservers&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-linkedservers-transact-sql)   
 [sp_helpserver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpserver-transact-sql)   
 [sp_serveroption&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-serveroption-transact-sql)  
  
  
