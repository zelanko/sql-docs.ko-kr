---
title: "이름 바꾸기 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 11/20/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
caps.latest.revision: "15"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3c08b4d991717d877ca33cd2d136d0dbf0d30483
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="rename-transact-sql"></a>이름 바꾸기 (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  사용자가 만든 테이블의 이름을 바꿉니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다. 사용자가 만든 테이블 또는 데이터베이스의 이름을 바꿉니다 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
> [!NOTE]  
>  데이터베이스의 이름을 바꾸려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 저장된 프로시저를 사용 하 여 [sp_renamedb &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md). Azure SQL Database에서 데이터베이스의 이름을 바꾸려면 [ALTER DATABASE(Azure SQL Database)](/statements/alter-database-azure-sql-database.md) 문을 사용합니다. 
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
-- Rename a table.  
RENAME OBJECT [ :: ]  [ [ database_name .  [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name  
[;]  
  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- Rename a table  
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name  
[;]  
  
-- Rename a database  
RENAME DATABASE [::] database_name TO new_database_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 개체 [:] 이름 바꾸기   
          [ [*database_name* . [ *schema_name* ] . ] | [ *schema_name* . ] ]*table_name* TO *new_table_name*  
 **적용 대상:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 사용자 정의 테이블의 이름을 변경 합니다. 1, 2 개 또는 세 부분으로 된 이름으로 이름을 변경 하려면 테이블을 지정 합니다.    새 테이블을 지정 *new_table_name* 한 부분 이름으로 합니다.  
  
 [:] 데이터베이스 이름 바꾸기   
          [ *database_name* TO *new_database_name*  
 **적용 대상:**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 사용자 정의 데이터베이스의 이름을 변경 *database_name* 를 *new_database_name*합니다.  이러한 항목 중 하나에 데이터베이스를 이름을 바꿀 수 없습니다 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]예약 된 데이터베이스 이름:  
  
-   master  
  
-   model  
  
-   msdb  
  
-   tempdb  
  
-   pdwtempdb1  
  
-   pdwtempdb2  
  
-   DWConfiguration  
  
-   DWDiagnostics  
  
-   Dwqueue를 설치  
  
## <a name="permissions"></a>Permissions  
 이 명령을 실행 하려면이 권한이 필요 합니다.  
  
-   **ALTER** 테이블에 대 한  
   
  
## <a name="limitations-and-restrictions"></a>제한 사항  
  
### <a name="cannot-rename-an-external-table-indexes-or-views"></a>외부 테이블, 인덱스 또는 뷰 이름을 바꿀 수 없습니다.
외부 테이블, 인덱스 또는 뷰를 바꿀 수 없습니다. 이름을 바꾸는 것 보다 외부 테이블, 인덱스 또는 뷰를 삭제 하 고 새 이름으로 다시 만들 수 있습니다.

### <a name="cannot-rename-a-table-in-use"></a>사용 중인 테이블 이름을 바꿀 수 없습니다.  
 사용 중인 동안 테이블 또는 데이터베이스를 바꿀 수 없습니다. 테이블 이름 바꾸기는 테이블에 대해 배타적 잠금이 필요 합니다. 표를 사용 하는 경우 테이블을 사용 하는 세션을 종료 해야 합니다. 세션을 종료 하려면 KILL 명령을 사용할 수 있습니다. 세션이 종료 될 때 커밋되지 않은 모든 작업은 롤백할 수 있으므로 신중 하 게 KILL을 사용 합니다. SQL 데이터 웨어하우스에 세션에는 'SID' 접두사로 합니다. KILL 명령을 호출할 때이 및 세션 수를 포함 해야 합니다. 이 예제에서는 활성 또는 유휴 세션의 목록을 볼 하 고 'SID1234' 세션을 종료 합니다.  
  
### <a name="views-are-not-updated"></a>뷰는 업데이트 되지 않습니다.  
 데이터베이스의 이름을 바꾸면 이전 데이터베이스 이름을 사용 하는 모든 보기 무효화 됩니다. 이 보기 내부 및 외부 데이터베이스 모두에 적용 됩니다. 예를 들어 판매 데이터베이스의 이름을 바꿀 뷰 포함 된 `SELECT * FROM Sales.dbo.table1` 유효 하지 않게 됩니다. 이 해결 하려면이 터 뷰에서 세 부분으로 된 이름을 사용 하지 않도록 또는 뷰 이름을 참조 하는 새 데이터베이스를 업데이트 합니다.  
  
 테이블의 이름을 바꾸면 뷰 이름을 참조 하는 새 테이블에 업데이트 되지 않습니다. 각 보기의 내부 또는 외부 이전 테이블 이름을 참조 하는 데이터베이스에서 유효 하지 않게 됩니다. 이 해결 하려면 각 보기 이름을 참조 하는 새 테이블을 업데이트할 수 있습니다.  
  
## <a name="locking"></a>잠금  
 테이블 이름 바꾸기는 데이터베이스 개체에 대 한 공유 잠금을, 스키마 개체의 공유 잠금 및 테이블에 대 한 배타적 잠금을 사용 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-rename-a-database"></a>1. 데이터베이스 이름 바꾸기  
 **적용 대상:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 만  
  
 이 예제에서는 AdWorks2에 사용자 정의 데이터베이스를 AdWorks 이름을 바꿉니다.  
  
```  
-- Rename the user defined database AdWorks  
RENAME DATABASE AdWorks to AdWorks2;  
  
```  
  
 테이블 이름 바꾸기, 모든 개체 및 해당 테이블과 연결 된 속성 이름을 참조 하는 새 테이블 업데이트 됩니다. 예를 들어, 정의 인덱스, 제약 조건, 테이블 및 사용 권한을 업데이트 합니다. 뷰 업데이트 되지 않습니다.  
  
### <a name="b-rename-a-table"></a>2. 테이블 이름 바꾸기  
 **적용 대상:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 이 예제에서는 고객 1에는 Customer 테이블을 이름을 바꿉니다.  
  
```  
-- Rename the customer table  
RENAME OBJECT Customer TO Customer1;  
  
RENAME OBJECT mydb.dbo.Customer TO Customer1;  
```  
  
 테이블 이름 바꾸기, 모든 개체 및 해당 테이블과 연결 된 속성 이름을 참조 하는 새 테이블 업데이트 됩니다. 예를 들어, 정의 인덱스, 제약 조건, 테이블 및 사용 권한을 업데이트 합니다. 뷰 업데이트 되지 않습니다.  
   
  
### <a name="c-move-a-table-to-a-different-schema"></a>3. 다른 스키마 테이블 이동  
 **적용 대상:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 사용 하 여 의도 다른 스키마로 개체를 이동 하려는 경우, [ALTER SCHEMA &#40; Transact SQL &#41; ](../../t-sql/statements/alter-schema-transact-sql.md). 예를 들어,이 테이블에서에서 항목을 이동 제품 스키마의 dbo 스키마.  
  
```  
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;  
```  
  
### <a name="d-terminate-sessions-before-renaming-a-table"></a>4. 테이블 이름 바꾸기 전에 세션을 종료 합니다.  
 **적용 대상:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 사용 중인 동안에 테이블을 바꿀 수 없습니다 기억 하는 것이 유용 합니다. 테이블의 이름 바꾸기를 테이블에 대 한 단독 잠금이 필요합니다. 표를 사용 하는 경우 테이블을 사용 하 여 세션을 종료 해야 합니다. 세션을 종료 하려면 KILL 명령을 사용할 수 있습니다. 세션이 종료 될 때 커밋되지 않은 모든 작업은 롤백할 수 있으므로 신중 하 게 KILL을 사용 합니다. SQL 데이터 웨어하우스에 세션에는 'SID' 접두사로 합니다. KILL 명령을 호출할 때이 및 세션 수를 포함 해야 합니다. 이 예제에서는 활성 또는 유휴 세션의 목록을 볼 하 고 'SID1234' 세션을 종료 합니다.  
  
```  
-- View a list of the current sessions  
SELECT session_id, login_name, status   
FROM sys.dm_pdw_exec_sessions   
WHERE status='Active' OR status='Idle';  
  
-- Terminate a session using the session_id.  
KILL 'SID1234';  
```  
  
  
