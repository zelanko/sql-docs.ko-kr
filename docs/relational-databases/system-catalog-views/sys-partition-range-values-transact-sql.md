---
description: sys.partition_range_values(Transact SQL)
title: sys.partition_range_values (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.partition_range_values
- partition_range_values_TSQL
- partition_range_values
- sys.partition_range_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_range_values catalog view
ms.assetid: 9aee483e-61f3-4613-bec6-f084161f45ac
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0617f01056af48341e616f10fca1cadabdf98299
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97458516"
---
# <a name="syspartition_range_values-transact-sql"></a>sys.partition_range_values(Transact SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  R 유형 파티션 함수의 각 범위 경계값당 한 개의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|이 범위 경계 값에 대한 파티션 함수의 ID입니다.|  
|**boundary_id**|**int**|경계 값 튜플의 ID(1부터 시작하는 서수)이며 맨 왼쪽 경계가 ID 1에서 시작합니다.|  
|**parameter_id**|**int**|이 값이 해당하는 함수의 매개 변수 ID입니다. 이 열의 값은 특정 **function_id** 에 대 한 **sys.partition_parameters** 카탈로그 뷰의 **parameter_id** 열에 있는 값과 일치 합니다.|  
|**value**|**sql_variant**|실제 경계 값입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;파티션 함수 카탈로그 뷰 ](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
