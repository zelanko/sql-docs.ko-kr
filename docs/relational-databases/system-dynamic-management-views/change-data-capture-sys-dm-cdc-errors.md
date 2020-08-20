---
description: 변경 데이터 캡처-sys. dm_cdc_errors
title: sys. dm_cdc_errors (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cdc_errors_TSQL
- dm_cdc_errors
- sys.dm_cdc_errors
- sys.dm_cdc_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cdc_errors dynamic management view
- change data capture [SQL Server], error reporting
ms.assetid: 898f2d76-9e63-45ef-94da-8034e86004ab
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b34623ac9b7732faff5b1f29e6a154dddf79dd78
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482050"
---
# <a name="change-data-capture---sysdm_cdc_errors"></a>변경 데이터 캡처-sys. dm_cdc_errors
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  변경 데이터 캡처 로그 검색 세션 중 발생한 각 오류마다 한 개의 행을 반환합니다.  
 
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|세션의 ID입니다.<br /><br /> 0 = 로그 검색 세션 내에서 오류가 발생하지 않았습니다.|  
|**phase_number**|**int**|오류 발생한 시점의 세션 단계를 나타내는 번호입니다. 각 단계에 대 한 설명은 [dm_cdc_log_scan_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)을 참조 하십시오.|  
|**entry_time**|**datetime**|오류가 기록된 날짜 및 시간입니다. 이 값은 SQL 오류 로그의 타임스탬프와 일치합니다.|  
|**error_number**|**int**|오류 메시지 ID입니다.|  
|**error_severity**|**int**|1에서 25 사이의 메시지 심각도입니다.|  
|**error_state**|**int**|오류의 상태 번호입니다.|  
|**error_message**|**nvarchar(1024)**|오류의 메시지 텍스트입니다.|  
|**start_lsn**|**nvarchar (23)**|오류가 발생한 시점에 처리 중이었던 행의 시작 LSN 값입니다.<br /><br /> 0 = 로그 검색 세션 내에서 오류가 발생하지 않았습니다.|  
|**begin_lsn**|**nvarchar (23)**|오류가 발생한 시점에 처리 중이었던 트랜잭션의 시작 LSN 값입니다.<br /><br /> 0 = 로그 검색 세션 내에서 오류가 발생하지 않았습니다.|  
|**sequence_value**|**nvarchar (23)**|오류가 발생한 시점에 처리 중이었던 행의 LSN 값입니다.<br /><br /> 0 = 로그 검색 세션 내에서 오류가 발생하지 않았습니다.|  
  
## <a name="remarks"></a>설명  
 **dm_cdc_errors** 이전 32 세션에 대 한 오류 정보를 포함 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sys. dm_cdc_errors** 동적 관리 뷰를 쿼리하려면 VIEW DATABASE STATE 권한이 필요 합니다. 동적 관리 뷰 사용 권한에 대 한 자세한 내용은 [동적 관리 뷰 및 함수 &#40;transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [dm_cdc_log_scan_sessions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)   
 [dm_repl_traninfo &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-repl-traninfo-transact-sql.md)  
  
  

