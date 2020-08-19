---
description: sp_depends(Transact-SQL)
title: sp_depends (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_depends
- sp_depends_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_depends
ms.assetid: d9934590-c6ae-4936-91c3-146055ef2c57
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ba819cdb8b3e9108fbae3e6405a87b78964931a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447274"
---
# <a name="sp_depends-transact-sql"></a>sp_depends(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  테이블 또는 뷰에 종속되는 뷰 및 프로시저, 뷰 또는 프로시저에 종속되는 테이블 및 뷰와 같은 데이터베이스 개체 종속성에 대한 정보를 표시합니다. 현재 데이터베이스 외부의 개체에 대한 참조는 보고되지 않습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md) 와 [dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) 를 사용 하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_depends [ @objname = ] '<object>'   
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name.  
    object_name  
}  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 개체가 속한 스키마의 이름입니다.  
  
 *object_name*  
 종속성을 검사할 데이터베이스 개체입니다. 개체는 테이블, 뷰, 저장 프로시저, 사용자 정의 함수 또는 트리거일 수 있습니다. o*bject_name* 은 **nvarchar (776)** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 **sp_depends** 는 두 개의 결과 집합을 표시 합니다.  
  
 다음 결과 집합은가 종속 된 개체를 표시 합니다 *\<object>* .  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar (257** **)**|종속성이 있는 항목의 이름입니다.|  
|**type**|**nvarchar (16)**|항목의 유형입니다.|  
|**updated**|**nvarchar (7)**|항목의 업데이트 여부를 결정합니다.|  
|**선택**|**nvarchar(8)**|SELECT 문에서 항목의 사용 여부를 결정합니다.|  
|**column**|**sysname**|종속성이 있는 열 또는 매개 변수입니다.|  
  
 다음 결과 집합은에 종속 된 개체를 표시 합니다 *\<object>* .  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar (257** **)**|종속성이 있는 항목의 이름입니다.|  
|**type**|**nvarchar (16)**|항목의 유형입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-listing-dependencies-on-a-table"></a>A. 테이블에 대한 종속성 나열  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `Sales.Customer` 테이블에 종속된 데이터베이스 개체를 나열합니다. 스키마 이름 및 테이블 이름 모두를 지정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_depends @objname = N'Sales.Customer' ;  
```  
  
### <a name="b-listing-dependencies-on-a-trigger"></a>B. 트리거에 대한 종속성 나열  
 다음 예에서는 `iWorkOrder` 트리거가 종속된 데이터베이스 개체를 나열합니다.  
  
```  
EXEC sp_depends @objname = N'AdventureWorks2012.Production.iWorkOrder' ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sql_dependencies &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
