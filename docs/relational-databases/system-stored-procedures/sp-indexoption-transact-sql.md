---
title: sp_indexoption (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexoption
- sp_indexoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexoption
ms.assetid: 75f836be-d322-4a53-a45d-25bee6b42a52
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cc11f219d98e4b8018bc7d763345feb279790e13
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893244"
---
# <a name="sp_indexoption-transact-sql"></a>sp_indexoption(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  사용자 정의 클러스터형 및 비클러스터형 인덱스 또는 클러스터형 인덱스가 없는 테이블에 대한 잠금 옵션 값을 설정합니다.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 자동으로 페이지, 행 또는 테이블 수준의 잠금을 선택합니다. 이러한 옵션을 수동으로 설정할 필요는 없습니다. 특정 유형의 잠금이 항상 적절 하다는 확신을 알고 있는 전문가 사용자를 위해 **sp_indexoption** 제공 됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]대신 [ALTER INDEX &#40;transact-sql&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 사용 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_indexoption [ @IndexNamePattern = ] 'table_or_index_name'   
    , [ @OptionName = ] 'option_name'   
    , [ @OptionValue = ] 'value'  
```  
  
## <a name="arguments"></a>인수  
`[ @IndexNamePattern = ] 'table_or_index_name'`사용자 정의 테이블이 나 인덱스의 정규화 된 이름 또는 정규화 되지 않은 이름입니다. *table_or_index_name* 은 **nvarchar (1035)** 이며 기본값은 없습니다. 정규화된 인덱스 또는 테이블 이름을 지정할 경우에만 따옴표가 필요합니다. 데이터베이스 이름을 포함한 정규화된 테이블 이름인 경우 데이터베이스 이름이 반드시 현재 데이터베이스의 이름이어야 합니다. 테이블 이름이 인덱스 없이 지정된 경우 지정된 옵션 값은 해당 테이블의 모든 인덱스에 대해 설정되며 테이블에 클러스터형 인덱스가 없는 경우 테이블 자체에 대해 설정됩니다.  
  
`[ @OptionName = ] 'option_name'`인덱스 옵션 이름입니다. *option_name* 는 **varchar (35)** 이며 기본값은 없습니다. *option_name* 는 다음 값 중 하나를 사용할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**AllowRowLocks**|TRUE인 경우 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다. FALSE로 설정된 경우 행 잠금을 사용하지 않습니다. 기본값은 TRUE입니다.|  
|**AllowPageLocks**|TRUE인 경우 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다. FALSE로 설정된 경우 페이지 잠금을 사용하지 않습니다. 기본값은 TRUE입니다.|  
|**DisAllowRowLocks**|TRUE로 설정된 경우 행 잠금을 사용하지 않습니다. FALSE인 경우 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.|  
|**DisAllowPageLocks**|TRUE로 설정된 경우 페이지 잠금을 사용하지 않습니다. FALSE인 경우 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.|  
  
`[ @OptionValue = ] 'value'`*Option_name* 설정을 사용할지 (TRUE, ON, yes 또는 1) 또는 해제 (FALSE, OFF, no 또는 0)를 지정 합니다. *값* 은 **varchar (12)** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0 초과(실패)  
  
## <a name="remarks"></a>설명  
 XML 인덱스는 지원되지 않습니다. XML 인덱스가 지정된 경우, 그리고 테이블 이름이 인덱스 이름 없이 지정되고 테이블에 XML 인덱스가 있는 경우 문이 실패합니다. 이러한 옵션을 설정 하려면 대신 [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) 를 사용 합니다.  
  
 현재 행 및 페이지 잠금 속성을 표시 하려면 [Indexproperty](../../t-sql/functions/indexproperty-transact-sql.md) 또는 [sys indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰를 사용 합니다.  
  
-   **Allowrowlocks** = True 또는 **DisAllowRowLocks** = False, **Allowrowlocks** = true 또는 **DisAllowPageLocks** = false 일 때 인덱스에 액세스할 때 행, 페이지 및 테이블 수준 잠금이 허용 됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 적절한 잠금을 선택하고 행 또는 페이지 잠금에서 테이블 잠금으로 잠금을 에스컬레이션할 수 있습니다.  
  
 **Allowrowlocks** = False 또는 **DisAllowRowLocks** = True 및 **Allowrowlocks** = false 또는 **DisAllowPageLocks** = true 일 때 인덱스에 액세스할 때 테이블 수준 잠금만 허용 됩니다.  
  
 테이블 이름이 인덱스 없이 지정된 경우 설정은 해당 테이블의 모든 인덱스에 적용됩니다. 기본 테이블에 클러스터형 인덱스가 없는 경우(힙) 다음과 같이 설정이 적용됩니다.  
  
-   **Allowrowlocks** 또는 **DisAllowRowLocks** 가 TRUE 또는 FALSE로 설정 된 경우이 설정은 힙 및 연결 된 모든 비클러스터형 인덱스에 적용 됩니다.  
  
-   **Allowpagelocks** 옵션을 TRUE로 설정 하거나 **DisAllowPageLocks** 을 FALSE로 설정 하면 힙 및 연결 된 모든 비클러스터형 인덱스에 설정이 적용 됩니다.  
  
-   **Allowpagelocks** 옵션이 FALSE로 설정 되거나 **DisAllowPageLocks** 가 TRUE로 설정 된 경우이 설정은 비클러스터형 인덱스에 완전히 적용 됩니다. 즉, 비클러스터형 인덱스에서는 모든 페이지 잠금이 허용되지 않습니다. 힙에서는 페이지에 대한 공유(S), 업데이트(U) 및 배타적(X) 잠금이 허용되지 않습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 내부에서 사용하기 위해 의도 페이지 잠금(IS, IU 또는 IX)을 획득할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-setting-an-option-on-a-specific-index"></a>A. 특정 인덱스에 대한 옵션 설정  
 다음 예에서는 테이블의 인덱스에 대 한 페이지 잠금을 허용 하지 `IX_Customer_TerritoryID` `Customer` 않습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_indexoption N'Sales.Customer.IX_Customer_TerritoryID',  
    N'disallowpagelocks', TRUE;  
```  
  
### <a name="b-setting-an-option-on-all-indexes-on-a-table"></a>B. 테이블의 모든 인덱스에 대한 옵션 설정  
 다음 예에서는 `Product` 테이블에 연결된 모든 인덱스에 대해 행 잠금을 허용하지 않습니다. 문의 결과를 표시하기 위해 `sys.indexes` 프로시저를 실행하기 전과 후에 `sp_indexoption` 카탈로그 뷰를 쿼리합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
-- Set the disallowrowlocks option on the Product table.   
EXEC sp_indexoption N'Production.Product',  
    N'disallowrowlocks', TRUE;  
GO  
--Verify the row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
```  
  
### <a name="c-setting-an-option-on-a-table-with-no-clustered-index"></a>C. 클러스터형 인덱스가 없는 테이블에 대한 옵션 설정  
 다음 예에서는 클러스터형 인덱스가 없는 테이블(힙)에 대해 페이지 잠금을 허용하지 않습니다. `sys.indexes` `sp_indexoption` 문 결과를 표시 하기 위해 프로시저를 실행 하기 전과 후에 카탈로그 뷰를 쿼리 합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options of the table.   
SELECT OBJECT_NAME (object_id) AS [Table], type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
-- Set the disallowpagelocks option on the table.   
EXEC sp_indexoption DatabaseLog,  
    N'disallowpagelocks', TRUE;  
GO  
--Verify the row and page lock settings of the table.  
SELECT OBJECT_NAME (object_id) AS [Table], allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [INDEXPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
