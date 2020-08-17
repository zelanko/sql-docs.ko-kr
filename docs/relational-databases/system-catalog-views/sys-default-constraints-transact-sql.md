---
description: sys.default_constraints(Transact-SQL)
title: sys. default_constraints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.default_constraints
- sys.default_constraints_TSQL
- default_constraints
- default_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.default_constraints catalog view
ms.assetid: 096e3659-edeb-4440-a016-f847acd6166b
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 69d5d6f490e8ca96dfac93fabf5267e6963e07ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88378569"
---
# <a name="sysdefault_constraints-transact-sql"></a>sys.default_constraints(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  기본 정의 인 각 개체에 대 한 행을 포함 합니다 (CREATE DEFAULT 문 대신 CREATE TABLE 또는 ALTER TABLE 문의 일부로 만듦 **).**  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.|  
|**parent_column_id**|**int**|이 기본값이 속한 **parent_object_id** 의 열 ID입니다.|  
|**정의**|**nvarchar(max)**|이 기본값을 정의하는 SQL 식입니다.|  
|**is_system_named**|**bit**|1 = 시스템에서 이름을 생성했습니다.<br /><br /> 0 = 사용자가 제공한 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `VacationHours` 테이블의 `HumanResources.Employee` 열에 적용된 DEFAULT 제약 조건의 정의를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT d.definition   
FROM sys.default_constraints AS d  
INNER JOIN sys.columns AS c  
ON d.parent_object_id = c.object_id
AND d.parent_column_id = c.column_id  
WHERE d.parent_object_id = OBJECT_ID(N'HumanResources.Employee', N'U')  
AND c.name = 'VacationHours';  
```  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
