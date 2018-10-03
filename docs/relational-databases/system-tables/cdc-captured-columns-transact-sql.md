---
title: cdc.captured_columns (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fb9bc8d8fe92a53eace426080221c224e229a80b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620041"
---
# <a name="cdccapturedcolumns-transact-sql"></a>cdc.captured_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  캡처 인스턴스에서 추적된 각 열에 대해 하나의 행을 반환합니다. 기본적으로 원본 테이블의 모든 열이 캡처됩니다. 하지만 원본 테이블에서 변경 데이터 캡처가 활성화된 경우 열 목록을 지정하여 열을 포함하거나 제외할 수 있습니다. 자세한 내용은 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)합니다.  
  
 좋습니다 있습니다 **쿼리하지 않는 시스템 테이블을 직접**입니다. 대신 실행 합니다 [sys.sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md) 저장 프로시저입니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|캡처된 열이 속해 있는 원본 테이블의 ID입니다.|  
|**column_name**|**sysname**|캡처된 열의 이름입니다.|  
|**column_id**|**int**|원본 테이블 내 캡처된 열의 ID입니다.|  
|**column_type**|**sysname**|캡처된 열의 유형입니다.|  
|**column_ordinal**|**int**|변경 테이블의 열 서수(1부터 시작)입니다. 변경 테이블의 메타데이터 열은 제외됩니다. 서수 1은 첫 번째 캡처된 열에 할당됩니다.|  
|**is_computed**|**bit**|캡처된 열이 원본 테이블에서 계산 열임을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [cdc.change_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
