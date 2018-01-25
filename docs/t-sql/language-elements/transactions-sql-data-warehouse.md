---
title: "트랜잭션 (SQL 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4ea7244857dcd25b1e36f3420811ef035d4ee3b2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="transactions-sql-data-warehouse"></a>트랜잭션 (SQL 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  트랜잭션이 완전히 커밋되거나 롤백 전체적으로 하는 하나 이상의 데이터베이스 문 그룹입니다. 각 트랜잭션에 원자성, 일관성, 격리성 및 내구성 (ACID). 트랜잭션이 성공 하면 그에 속한 모든 문이 커밋됩니다. 트랜잭션이 실패 하면 하에 있으면 그룹에는 문 중 하나 이상 실패 하면 전체 그룹이 롤백됩니다.  
  
 트랜잭션의 시작과 끝은 자동 커밋 설정과 BEGIN TRANSACTION, COMMIT 및 ROLLBACK 문을에 따라 달라 집니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]다음과 같은 유형의 트랜잭션 지원합니다.  
  
-   *명시적 트랜잭션을* 는 BEGIN TRANSACTION 문 및 COMMIT 또는 ROLLBACK 문 사용 하 여 종료로 시작 합니다.  
  
-   *자동 커밋 트랜잭션을* 세션 내에서 자동으로 시작 하 고 BEGIN TRANSACTION 문을 사용 하 여 시작 되지 않습니다. 자동 커밋 설정이 ON 이면 각 문에 트랜잭션에서 실행 되며 없는 명시적 COMMIT 또는 ROLLBACK 필요. 자동 커밋 설정이 OFF 이면 COMMIT 또는 ROLLBACK 문은 트랜잭션의 결과 결정 해야 합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], 자동 커밋 트랜잭션 COMMIT 또는 ROLLBACK 문을 직후 또는 SET 자동 커밋 OFF 문 다음 시작 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>인수  
 BEGIN TRANSACTION  
 명시적 트랜잭션의 시작 위치를 표시 합니다.  
  
 커밋 [작업]  
 명시적 또는 자동 커밋 트랜잭션의 끝을 표시합니다. 이 문은 하면 트랜잭션에서 데이터베이스에 영구적으로 커밋할 수로 변경 합니다. 문이 커밋은 COMMIT WORK, COMMIT TRAN 및 COMMIT TRANSACTION 동일 합니다.  
  
 롤백 [작업]  
 트랜잭션의 시작 부분에는 트랜잭션을 롤백합니다. 트랜잭션에 대 한 변경 내용이 없습니다 데이터베이스에 커밋됩니다. 문이 ROLLBACK는 ROLLBACK WORK, ROLLBACK TRAN 및 ROLLBACK TRANSACTION 동일 합니다.  
  
 자동 커밋 집합 { **ON** | OFF}  
 트랜잭션이 수 시작 하 고 종료 하는 방법을 결정 합니다.  
  
 ON  
 각 문에 자체 트랜잭션에서 실행 되며 명시적 COMMIT 또는 ROLLBACK 문이 없는 필요 합니다. 자동 커밋 ON 일 때 명시적 트랜잭션이 허용 됩니다.  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]트랜잭션이 없는 경우 이미 진행 중에서에 자동으로 트랜잭션을 시작 합니다. 모든 후속 문이 트랜잭션의 일부로 실행 되며 COMMIT 또는 ROLLBACK 트랜잭션의 결과 확인할 필요가 있습니다. 모드는 OFF 상태로 유지 됩니다 트랜잭션을 커밋하거나 롤백하면에서이 작업 모드를 즉시 및 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 새로운 트랜잭션을 시작 합니다. 자동 커밋 옵션이 OFF 명시적 트랜잭션은 허용 되지 않습니다.  
  
 활성화 된 트랜잭션 내에서 자동 커밋 설정을 변경 하면은 현재 트랜잭션이 영향이 설정과 트랜잭션이 완료 될 때까지 적용 되지 않습니다.  
  
 자동 커밋이 ON 이면 다른 SET 자동 커밋 ON 문을 실행 효과가 없습니다. 마찬가지로, 자동 커밋 옵션이 OFF 면 다른 SET 자동 커밋 OFF 실행 효과가 없습니다.  
  
 SET IMPLICIT_TRANSACTIONS {ON | **OFF** }  
 자동 커밋 설정 같은 모드를 전환합니다. SET IMPLICIT_TRANSACTIONS 옵션을 ON으로 설정하면 연결이 암시적 트랜잭션 모드로 설정됩니다. 때 off로 설정한 연결 자동 커밋 모드로 돌아갑니다.  자세한 내용은 참조 [SET implicit_transactions&#40; Transact SQL &#41; ](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 특정 사용 권한 없음 트랜잭션 관련 문을 실행 해야 합니다. 트랜잭션 내에서 문을 실행할 권한이 필요 합니다.  
  
## <a name="error-handling"></a>오류 처리  
 COMMIT 또는 ROLLBACK을 실행 하 고 활성 트랜잭션이 없는 경우 오류가 발생 합니다.  
  
 BEGIN TRANSACTION은 트랜잭션이 이미 진행 중이면를 실행 하는 경우 오류가 발생 합니다. 이 BEGIN TRANSACTION 성공적인 BEGIN TRANSACTION 문 또는 세션 SET 자동 커밋 OFF 부족할 때 발생 하는 경우 발생할 수 있습니다.  
  
 런타임 문 오류가 아닌 다른 오류로 인해 명시적 트랜잭션의 성공적으로 완료 하는 경우 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 자동으로 트랜잭션을 롤백하고 하 고 트랜잭션에서 보유 하는 모든 리소스를 해제 합니다. 예를 들어 경우 클라이언트의 네트워크 연결의 인스턴스로 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 끊어지면 또는 클라이언트 응용 프로그램이 저속, 네트워크 구분선의 인스턴스를 알려 줍니다. 때 연결에 커밋되지 않은 모든 트랜잭션이 롤백됩니다.  
  
 런타임 문 오류가 발생 한 경우 일괄 처리에서 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 와 일치 하 게 작동 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **XACT_ABORT** 로 설정 **ON** 전체 트랜잭션이 롤백됩니다. 에 대 한 자세한 내용은 **XACT_ABORT** 참조 설정, [SET XACT_ABORT (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms188792.aspx)합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 세션; 한 번에 하나의 트랜잭션만 에서만 실행할 수 있습니다. 저장 지점 및 중첩 된 트랜잭션은 지원 되지 않습니다.  
  
 책임은 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 모든 데이터는 트랜잭션에서 참조 하는 경우 커밋 점에서 발급 하는 프로그래머는 논리적으로 정확할 합니다.  
  
 세션 트랜잭션이 완료 되기 전에 종료 되 면 트랜잭션이 롤백됩니다.  
  
 트랜잭션 모드 세션 수준에서 관리 됩니다. 예를 들어 하나의 명시적 트랜잭션을 시작 또는 OFF로 설정 하는 자동 커밋 이거나 IMPLICIT_TRANSACTIONS가 ON으로 설정, 주지 다른 세션의 트랜잭션 모드에 영향을 주지 않습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 롤백할 수 없습니다 트랜잭션이 데이터 수정 내용을 되었기 때문에 데이터베이스의 영구적인 부분이 COMMIT 문이 실행 된 후입니다.  
  
 [데이터베이스 만들기 &#40; Azure SQL 데이터 웨어하우스 &#41; ](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) 및 [DROP database&#40; Transact SQL &#41; ](../../t-sql/statements/drop-database-transact-sql.md) 명시적 트랜잭션 내 명령을 사용할 수 없습니다.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]공유 메커니즘 트랜잭션을 없습니다. 이 특정 시점에 하나의 세션 작업을 수행할 수 모든 트랜잭션 시스템에서 의미 합니다.  
  
## <a name="locking-behavior"></a>잠금 동작  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서는 트랜잭션 무결성을 보장 하 고 여러 사용자가 동시에 데이터에 액세스 하는 데이터베이스의 일관성을 유지 관리에 대 한 잠금이 사용 합니다. 암시적 및 명시적 트랜잭션에 의해 잠금이 사용 됩니다. 각 트랜잭션은 테이블 또는 데이터베이스 트랜잭션이 종속 되는 등의 리소스에 대해 서로 다른 유형의 잠금을 요청 합니다. 모든 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 잠금은 테이블 수준 이상. 잠금은 다른 트랜잭션의 리소스 수정을 차단하여 잠금을 요청하는 트랜잭션에 문제가 발생하지 않도록 합니다. 각 트랜잭션은 잠긴된 리소스;에 더 이상 종속 되어 때 잠금을 해제합니다 명시적 트랜잭션을 커밋 또는 롤백 것 트랜잭션이 완료 될 때까지 잠금을 유지 합니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>1. 명시적 트랜잭션을 사용 하 여  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>2. 트랜잭션 롤백  
 다음 예제에서는 트랜잭션을 롤백하면 결과 보여 줍니다.  이 예제에서는 ROLLBACK 문을 롤백합니다 INSERT 문이 되지만 만든된 테이블은 계속 존재 합니다.  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>3. 자동 커밋 설정  
 다음 예제에서는 자동 커밋 설정이 설정 `ON`합니다.  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 다음 예제에서는 자동 커밋 설정이 설정 `OFF`합니다.  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>4. 암시적 다중 문 트랜잭션을 사용 하 여  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SET implicit_transactions 옵션 &#40; Transact SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION level&#40; Transact SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
