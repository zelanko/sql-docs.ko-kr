---
title: 트랜잭션(SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 583e8146a43ea88066a5e0ac223ab2088c0c61ed
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33702766"
---
# <a name="transactions-sql-data-warehouse"></a>트랜잭션(SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  트랜잭션은 완전히 커밋되거나 롤백되는 하나 이상의 데이터베이스 문 그룹입니다. 각각의 트랜잭션은 ACID(원자성, 일관성, 격리성 및 내구성)입니다. 트랜잭션이 성공하면 그 안의 모든 문이 커밋됩니다. 트랜잭션이 실패하면 그룹의 문 중 하나 이상이 실패하는 것이며 전체 그룹이 롤백됩니다.  
  
 트랜잭션의 시작과 끝은 AUTOCOMMIT 설정 및 BEGIN TRANSACTION, COMMIT 및 ROLLBACK 문에 따라 결정됩니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서는 다음과 같은 유형의 트랜잭션을 지원합니다.  
  
-   *명시적 트랜잭션*은 BEGIN TRANSACTION 문으로 시작되어 COMMIT 또는 ROLLBACK 문으로 끝납니다.  
  
-   *자동 커밋 트랜잭션*은 세션 안에서 자동으로 시작되며 BEGIN TRANSACTION 문으로 시작되지 않습니다. AUTOCOMMIT 설정이 ON이면 각 문은 트랜잭션 안에서 실행되며 명시적 COMMIT 또는 ROLLBACK이 필요하지 않습니다. AUTOCOMMIT 설정이 OFF이면 트랜잭션 결과를 판단하기 위해 COMMIT 또는 ROLLBACK 문이 필요합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 자동 커밋 트랜잭션은 COMMIT 또는 ROLLBACK 문 직후 또는 SET AUTOCOMMIT OFF 문 다음에서 시작됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 명시적 트랜잭션의 시작 위치를 표시합니다.  
  
 COMMIT [ WORK ]  
 명시적 또는 자동 커밋 트랜잭션의 끝을 표시합니다. 이 문에서는 트랜잭션의 변경 내용이 데이터베이스에 영구적으로 커밋됩니다. COMMIT 문은 COMMIT WORK, COMMIT TRAN 및 COMMIT TRANSACTION과 같습니다.  
  
 ROLLBACK [ WORK ]  
 트랜잭션을 시작 부분으로 롤백합니다. 트랜잭션의 변경 내용은 데이터베이스에 커밋되지 않습니다. ROLLBACK 문은 ROLLBACK WORK, ROLLBACK TRAN 및 ROLLBACK TRANSACTION과 동일합니다.  
  
 SET AUTOCOMMIT { **ON** | OFF }  
 트랜잭션의 시작과 종료 방법을 결정합니다.  
  
 ON  
 각 문은 자체 트랜잭션에서 실행되며 COMMIT 또는 ROLLBACK 문이 필요하지 않습니다. AUTOCOMMIT이 ON일 때 명시적 트랜잭션이 허용됩니다.  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 트랜잭션이 아직 진행 중이 아니면 트랜잭션을 시작합니다. 모든 후속 문은 트랜잭션의 ㅇ리부로 실행되며 트랜잭션 결과를 판단하기 위해 COMMIT 또는 ROLLBACK이 필요합니다. 이 작업 모드에서 트랜잭션 커밋 또는 롤백 즉시 모드가 OFF로 유지되며 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]가 새로운 트랜잭션을 시작합니다. AUTOCOMMIT이 OFF이면 명시적 트랜잭션이 허용되지 않습니다.  
  
 트랜잭션 내 AUTOCOMMIT 설정을 변경하면 이 설정이 현재 트랜잭션에 영향을 미치지 않고, 트랜잭션이 완료되어야 적용됩니다.  
  
 AUTOCOMMIT이 ON이면 다른 SET AUTOCOMMIT ON 문 실행이 효과가 없습니다. 마찬가지로 AUTOCOMMIT이 OFF이면 다른 SET AUTOCOMMIT OFF 문 실행이 효과가 없습니다.  
  
 SET IMPLICIT_TRANSACTIONS { ON | **OFF** }  
 SET AUTOCOMMIT과 같은 모드로 전환됩니다. SET IMPLICIT_TRANSACTIONS 옵션을 ON으로 설정하면 연결이 암시적 트랜잭션 모드로 설정됩니다. OFF이면 연결이 다시 자동 커밋 모드로 돌아갑니다.  자세한 내용은 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 트랜잭션 관련 문 실행에는 특정 권한이 필요하지 않습니다. 트랜잭션 안에서 문을 실행하려면 권한이 필요합니다.  
  
## <a name="error-handling"></a>오류 처리  
 COMMIT 또는 ROLLBACK을 실행하고 활성 트랜잭션이 없는 경우 오류가 발생합니다.  
  
 트랜잭션이 실행되는 도중에 BEGIN TRANSACTION이 실행되면 오류가 발생합니다. BEGIN TRANSACTION 문에 성공한 후 BEGIN TRANSACTION이 발생하거나 세션이 SET AUTOCOMMIT OFF 상태인 경우 이 상황이 일어날 수 있습니다.  
  
 런타임 문 오류 이외의 오류로 인해 명시적 트랜잭션이 제대로 완료되지 않은 경우 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서는 자동으로 트랜잭션을 롤백하고 해당 트랜잭션에 보유 중인 모든 리소스를 해제합니다. 예를 들어, 클라이언트와 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 인스턴스 간의 네트워크 연결이 끊어진 경우 네트워크에서 이 인스턴스에게 연결이 끊어진 것을 알릴 때 이 연결에 대한 커밋되지 않은 모든 트랜잭션은 롤백됩니다.  
  
 일괄 처리에서 런타임 문 오류가 발생할 경우 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 **ON**으로 설정된[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**XACT_ABORT**와 일관되게 작동하며 전체 트랜잭션이 롤백됩니다. **XACT_ABORT** 설정에 대한 자세한 내용은 [SET XACT_ABORT (Transact-SQL)](http://msdn.microsoft.com/library/ms188792.aspx)를 참조하세요.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 한 세션은 특정 시점에 한 트랜잭션만 실행할 수 있고 저장 지점과 중첩 트랜잭션은 지원되지 않습니다.  
  
 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 프로그래머는 트랜잭션에서 참조되는 모든 데이터가 논리적으로 정확할 때만 COMMIT을 실행해야 합니다.  
  
 트랜잭션 완료 전에 세션이 종료되면 트랜잭션이 롤백됩니다.  
  
 트랜잭션 모드는 세션 수준에서 관리됩니다. 예를 들어, 한 세션이 명시적 트랜잭션을 시작하거나, AUTOCOMMIT을 OFF로 설정하거나, IMPLICIT_TRANSACTIONS를 ON으로 설정할 경우 다른 세션의 트랜잭션 모드에는 영향이 없습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 COMMIT 문을 실행한 후에는 데이터 수정 내용이 데이터베이스에 영구적으로 반영되므로 트랜잭션을 롤백할 수 없습니다.  
  
 [CREATE DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) 및 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md) 명령은 명시적 트랜잭션 안에서 사용할 수 없습니다.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에는 트랜잭션 공유 메커니즘이 없습니다. 즉 어느 특정 시점에 시스템에서 한 세션만 트랜잭션에 대한 작업을 수행할 수 있습니다.  
  
## <a name="locking-behavior"></a>잠금 동작  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서는 여러 사용자가 동시에 데이터를 액세스하는 경우 잠금을 사용하여 트랜잭션의 무결성을 확인하고 데이터베이스의 일관성을 유지합니다. 잠금은 암시적 및 명시적 트랜잭션 모두에서 사용됩니다. 각 트랜잭션은 해당 트랜잭션이 종속되는 테이블, 데이터베이스 등의 리소스에 대해 서로 다른 유형의 잠금을 요청합니다. 모든 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 잠금은 테이블 수준 이상입니다. 잠금은 다른 트랜잭션의 리소스 수정을 차단하여 잠금을 요청하는 트랜잭션에 문제가 발생하지 않도록 합니다. 각 트랜잭션은 더 이상 잠긴 리소스에 종속되지 않게 되면 잠금을 해제합니다. 명시적 트랜잭션은 커밋 또는 롤백되어 트랜잭션이 완료될 때까지 잠금을 유지합니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>1. 명시적 트랜잭션 사용  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>2. 트랜잭션 롤백  
 다음 예제에서는 트랜잭션 롤백의 결과를 보여 줍니다.  이 예제에서는 ROLLBACK 문이 INSERT 문을 롤백하지만 만들어진 테이블은 그대로 있습니다.  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>3. AUTOCOMMIT 설정  
 다음 예제에서는 AUTOCOMMIT 설정을 `ON`으로 설정합니다.  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 다음 예제에서는 AUTOCOMMIT 설정을 `OFF`로 설정합니다.  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>4. 암시적 다중 문 트랜잭션 사용  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>참고 항목  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
