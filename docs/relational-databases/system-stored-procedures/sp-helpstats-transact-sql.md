---
title: sp_helpstats (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpstats
- sp_helpstats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpstats
ms.assetid: 00ab3cfd-2736-4fc0-b1b2-16dd49fb2fe5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45d6df772da027568b1fbd7593e404f291246bb4
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpstats-transact-sql"></a>sp_helpstats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정된 테이블의 열과 인덱스에 대한 통계 정보를 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]통계에 대 한 정보, 쿼리는 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 및 [sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) 카탈로그 뷰.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpstats[ @objname = ] 'object_name'   
     [ , [ @results = ] 'value' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@objname=**] **'***object_name***'**  
 통계 정보를 제공할 테이블을 지정합니다. *object_name* 은 **nvarchar(520)** 이며 null 일 수 없습니다. 한 부분 또는 두 부분으로 이루어진 이름을 지정할 수 있습니다.  
  
 [  **@results=**] **'***값***'**  
 제공할 정보의 범위를 지정합니다. 유효한 항목은 **모든** 및 **STATS**합니다. **모든** 모든 인덱스 및 하며 생성 된 통계가 있는 열에 대 한 통계를 나열 합니다. **STATS** 인덱스와 연관 되지 않은 통계만 나열 합니다. *값* 은 **nvarchar (5)** 기본값은 STATS입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 표에서는 결과 집합의 열을 설명합니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**statistics_name**|통계의 이름입니다. 반환 **sysname** 이며 null 일 수 없습니다.|  
|**statistics_keys**|통계가 기반을 두고 있는 키입니다. 반환 **nvarchar(2078)** 이며 null 일 수 없습니다.|  
  
## <a name="remarks"></a>주의  
 특정 인덱스 또는 통계에 대한 자세한 통계 정보를 표시하려면 DBCC SHOW_STATISTICS를 사용합니다. 자세한 내용은 참조 [DBCC show_statistics&#40; Transact SQL &#41; ](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) 및 [sp_helpindex &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sp_createstats`를 실행하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 있는 모든 사용자 테이블에 대해 모든 해당 열에 관한 단일 열 통계를 만듭니다. 그 다음 `sp_helpstats`를 실행하여 `Customer` 테이블에서 생성된 통계 결과를 찾습니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_createstats;  
GO  
EXEC sp_helpstats   
@objname = 'Sales.Customer',  
@results = 'ALL';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `statistics_name               statistics_keys`  
  
 `----------------------------  ----------------`  
  
 `_WA_Sys_00000003_22AA2996     AccountNumber`  
  
 `AK_Customer_AccountNumber     AccountNumber`  
  
 `AK_Customer_rowguid           rowguid`  
  
 `CustomerType                  CustomerType`  
  
 `IX_Customer_TerritoryID       TerritoryID`  
  
 `ModifiedDate                  ModifiedDate`  
  
 `PK_Customer_CustomerID        CustomerID`  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
