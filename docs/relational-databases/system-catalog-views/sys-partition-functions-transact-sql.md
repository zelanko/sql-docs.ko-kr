---
title: sys.partition_functions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.partition_functions_TSQL
- partition_functions
- sys.partition_functions
- partition_functions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_functions catalog view
ms.assetid: 96515727-728b-4bea-804a-36ce915b8b75
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 55eec55a1fc0012520161a9587f4e3a4dffbef1a
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40393234"
---
# <a name="syspartitionfunctions-transact-sql"></a>sys.partition_functions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 각 파티션 함수에 대한 행을 하나씩 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|파티션 함수의 이름입니다. 데이터베이스 내에서 고유합니다.|  
|**function_id**|**int**|파티션 함수 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**type**|**char(2)**|함수 유형입니다.<br /><br /> R = 범위|  
|**type_desc**|**nvarchar(60)**|함수 유형입니다.<br /><br /> RANGE|  
|**팬아웃**|**int**|함수가 만든 파티션의 수입니다.|  
|**boundary_value_on_right**|**bit**|범위 분할입니다.<br /><br /> 1 = 경계 값이 경계의 오른쪽 범위에 포함됩니다.<br /><br /> 0 = 왼쪽 범위에 포함됩니다.|  
|**is_system**||**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 1 = 개체가 전체 텍스트 인덱스 조각에 사용됩니다.<br /><br /> 0 = 개체가 전체 텍스트 인덱스 조각에 사용되지 않습니다.|  
|**create_date**|**datetime**|함수가 생성된 날짜입니다.|  
|**modify_date**|**datetime**|ALTER 문을 사용하여 함수를 마지막으로 수정한 날짜입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [파티션 함수 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_range_values&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partition_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
