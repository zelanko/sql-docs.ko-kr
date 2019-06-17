---
title: max text repl size 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- max text repl size option
ms.assetid: 3056cf64-621d-4996-9162-3913f6bc6d5b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e55268f499069fb6714aa07944997e1e92e7fc23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811577"
---
# <a name="configure-the-max-text-repl-size-server-configuration-option"></a>max text repl size 서버 구성 옵션 구성
  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 최대 텍스트 복제 크기 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **최대 텍스트 복제 크기** 옵션의 최대 크기 (메가바이트 단위)를 지정 `text`, `ntext`, `varchar(max)`를 `nvarchar(max)`, `varbinary(max)`를 `xml`, 및 `image` 에 추가할 수 있는 데이터 복제 된 열 또는 단일 INSERT, UPDATE, WRITETEXT 또는 UPDATETEXT 문에서 캡처된 열입니다. 기본값은 65536 바이트입니다. 값이 -1이면 데이터 형식에서 요구하는 한도 이외의 크기 제한이 없음을 나타냅니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **최대 텍스트 복제 크기 옵션을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [최대 텍스트 복제 크기 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   이 옵션은 트랜잭션 복제와 변경 데이터 캡처에 적용됩니다. 서버에 트랜잭션 복제 및 변경 데이터 캡처가 모두 구성되어 있는 경우 지정한 값이 두 기능에 모두 적용됩니다. 이 옵션은 스냅숏 복제 및 병합 복제에서는 무시됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-max-text-repl-size-option"></a>최대 텍스트 복제 크기 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **고급** 노드를 클릭합니다.  
  
3.  **기타**에서 **최대 텍스트 복제 크기** 옵션을 원하는 값으로 변경합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-max-text-repl-size-option"></a>최대 텍스트 복제 크기 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 를 사용하여 `max text repl size` 옵션을 `-1`으로 구성하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;   
RECONFIGURE ;   
GO  
EXEC sp_configure 'max text repl size', -1 ;   
GO  
RECONFIGURE;   
GO  
  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: Max text repl size 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 복제](../../relational-databases/replication/sql-server-replication.md)   
 [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [UPDATE&#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)   
 [UPDATETEXT&#40;Transact-SQL&#41;](/sql/t-sql/queries/updatetext-transact-sql)   
 [WRITETEXT&#40;Transact-SQL&#41;](/sql/t-sql/queries/writetext-transact-sql)  
  
  
