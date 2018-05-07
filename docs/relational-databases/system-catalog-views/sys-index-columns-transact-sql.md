---
title: sys.index_columns (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.index_columns
- sys.index_columns_TSQL
- index_columns
- index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.index_columns catalog view
ms.assetid: 211471aa-558a-475c-9b94-5913c143ed12
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: eb87377beeff12c6071ace2f03fee14ba9d92bf5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysindexcolumns-transact-sql"></a>sys.index_columns(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  일부인 열 하나당 하나의 행을 포함 한 **sys.indexes** 인덱스 또는 정렬 되지 않은 테이블 (힙).  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|인덱스가 정의되는 개체의 ID입니다.|  
|**index_id**|**int**|열이 정의되는 인덱스의 ID입니다.|  
|**index_column_id**|**int**|인덱스 열의 ID입니다. **index_column_id** 내 에서만 고유 **index_id**합니다.|  
|**column_id**|**int**|에 있는 열의 ID **object_id**합니다.<br /><br /> 0 = 비클러스터형 인덱스의 RID(행 식별자)<br /><br /> **column_id** 내 에서만 고유 **object_id**합니다.|  
|**key_ordinal**|**tinyint**|키 열 집합 내에서의 서수(1부터 시작)입니다.<br /><br /> 0 = 키 열이 아니거나, XML 인덱스, columnstore 인덱스 또는 공간 인덱스입니다.<br /><br /> 참고: XML 또는 공간 인덱스 키 일 수 없습니다는 기본 열은 비교할 수 있으므로 즉 해당 값을 정렬할 수 없습니다.|  
|**partition_ordinal**|**tinyint**|분할 열 집합 내에 있는 서수(1부터 시작)입니다. 클러스터형 columnstore 인덱스는 하나의 분할 열만 가질 수 있습니다.<br /><br /> 0 = 분할 열 아님|  
|**is_descending_key**|**bit**|1 = 인덱스 키 열이 내림차순으로 정렬됩니다.<br /><br /> 0 = 인덱스 키 열이 오름차순으로 정렬되거나 열이 columnstore 또는 해시 인덱스의 일부입니다.|  
|**is_included_column**|**bit**|1 = 열이 CREATE INDEX INCLUDE 절을 사용하여 인덱스에 추가된 키가 아닌 열이거나 columnstore 인덱스의 일부인 열입니다.<br /><br /> 0 = 열이 포괄 열이 아닙니다.<br /><br /> 클러스터링 키의 일부 이므로 암시적으로 추가 된 열에 나열 되지 않은 **sys.index_columns**합니다.<br /><br /> 분할 열이어서 암시적으로 추가된 열은 0으로 반환됩니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예는 `Production.BillOfMaterials` 테이블에 대한 모든 인덱스 및 인덱스 열을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,ic.key_ordinal  
,ic.is_included_column  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.object_id = OBJECT_ID('Production.BillOfMaterials');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
index_name                                                 column_name        index_column_id key_ordinal is_included_column  
---------------------------------------------------------- -----------------  --------------- ----------- -------------  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ProductAssemblyID  1               1           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ComponentID        2               2           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate StartDate          3               3           0  
PK_BillOfMaterials_BillOfMaterialsID                       BillOfMaterialsID  1               1           0  
IX_BillOfMaterials_UnitMeasureCode                         UnitMeasureCode    1               1           0  
  
(5 row(s) affected)  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
