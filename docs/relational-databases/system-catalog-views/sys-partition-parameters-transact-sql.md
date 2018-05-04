---
title: sys.partition_parameters (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- partition_parameters_TSQL
- partition_parameters
- sys.partition_parameters_TSQL
- sys.partition_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_parameters catalog view
ms.assetid: 2012ed9d-3ea3-4c29-9b78-dfa54a392dce
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d829b581083cdb434270a58aa276404050011882
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syspartitionparameters-transact-sql"></a>sys.partition_parameters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  파티션 함수의 각 매개 변수당 하나의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|이 매개 변수가 속한 파티션 함수의 ID입니다.|  
|**parameter_id**|**int**|매개 변수의 ID입니다. 파티션 함수 내에서 고유하며 1로 시작됩니다.|  
|**system_type_id**|**tinyint**|매개 변수 시스템 유형의 ID입니다. 에 해당 하는 **system_type_id** 의 열은 **sys.types** 카탈로그 뷰.|  
|**max_length**|**smallint**|매개 변수의 최대 길이(바이트)입니다.|  
|**전체 자릿수**|**tinyint**|숫자 기반일 경우 매개 변수의 전체 자릿수이고 그렇지 않으면 0입니다.|  
|**소수 자릿수**|**tinyint**|숫자 기반일 경우 매개 변수의 소수 자릿수이고 그렇지 않으면 0입니다.|  
|**collation_name**|**sysname**|문자 기반일 경우 매개 변수의 데이터 정렬 이름이고 그렇지 않으면 NULL입니다.|  
|**user_type_id**|**int**|유형 ID입니다. 데이터베이스 내에서 고유합니다. 시스템 데이터 형식에 대 한 **user_type_id** = **system_type_id**합니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [파티션 함수 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_range_values &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  
