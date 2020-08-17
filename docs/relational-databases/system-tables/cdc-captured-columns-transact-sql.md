---
description: cdc.captured_columns(Transact-SQL)
title: cdc. captured_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.captured_columns
- cdc.captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.captured_columns
ms.assetid: 7bb4d408-d764-4ef6-802c-f271c8d39c2a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1f97c0f9f8836a1ef0115a93d9cfae882cbaac05
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88374125"
---
# <a name="cdccaptured_columns-transact-sql"></a>cdc.captured_columns(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  캡처 인스턴스에서 추적된 각 열에 대해 하나의 행을 반환합니다. 기본적으로 원본 테이블의 모든 열이 캡처됩니다. 하지만 원본 테이블에서 변경 데이터 캡처가 활성화된 경우 열 목록을 지정하여 열을 포함하거나 제외할 수 있습니다. 자세한 내용은 [sp_cdc_enable_table &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)을 참조 하십시오.  
  
 **시스템 테이블을 직접 쿼리하지**않는 것이 좋습니다. 대신, [sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md) 저장 프로시저를 실행 합니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|캡처된 열이 속해 있는 원본 테이블의 ID입니다.|  
|**column_name**|**sysname**|캡처된 열의 이름입니다.|  
|**column_id**|**int**|원본 테이블 내 캡처된 열의 ID입니다.|  
|**column_type**|**sysname**|캡처된 열의 유형입니다.|  
|**column_ordinal**|**int**|변경 테이블의 열 서수(1부터 시작)입니다. 변경 테이블의 메타데이터 열은 제외됩니다. 서수 1은 첫 번째 캡처된 열에 할당됩니다.|  
|**is_computed**|**bit**|캡처된 열이 원본 테이블에서 계산 열임을 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [change_tables &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
