---
title: sys. computed_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.computed_columns_TSQL
- sys.computed_columns
- computed_columns_TSQL
- computed_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.computed_columns catalog view
ms.assetid: c962c619-e18f-4315-9251-8d9862462299
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1bbb4ef33cd640c8fe90f886f98eb966791e7003
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003064"
---
# <a name="syscomputed_columns-transact-sql"></a>sys.computed_columns(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **Sys.** 열에 있는 각 열에 대해 계산 열을 포함 하는 행을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Inherited columns>**||**Computed_columns** 뷰는 **sys. columns** 뷰의 모든 열을 반환 합니다. 또한 아래에 설명된 추가 열도 반환합니다. **Computed_columns** 뷰가 **sys.debug**에서 상속 하는 열에 대 한 설명은 [&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)을 참조 하십시오. **Is_computed** 열의 값은 항상 **computed_columns** 뷰에서 1로 설정 됩니다.|  
|**정의**|**nvarchar(max)**|이 계산 열을 정의하는 SQL 텍스트입니다.|  
|**uses_database_collation**|**bit**|1 = 열 정의는 정확한 평가를 위해 데이터베이스의 기본 데이터 정렬에 의존합니다. 그렇지 않으면 0입니다. 이러한 종속성으로 인해 데이터베이스의 기본 데이터 정렬을 바꿀 수 없습니다.|  
|**is_persisted**|**bit**|계산 열이 유지됩니다.|  
  
## <a name="permissions"></a>권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
