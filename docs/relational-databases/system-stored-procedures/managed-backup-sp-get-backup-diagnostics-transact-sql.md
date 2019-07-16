---
title: managed_backup.sp_get_backup_diagnostics (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_get_backup_diagnostics_TSQL
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics_TSQL
- smart_admin.sp_get_backup_diagnostics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics
ms.assetid: 2266a233-6354-464b-91ec-824ca4eb9ceb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5e967ae5b46ec703da4e8b1fff64f298fdf8a081
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942042"
---
# <a name="managedbackupspgetbackupdiagnostics-transact-sql"></a>managed_backup.sp_get_backup_diagnostics (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  스마트 관리에 기록된 확장 이벤트를 반환합니다.  
  
 이 저장된 프로시저를 사용 하 여 스마트 관리자가 기록 된 확장 이벤트를 모니터링 하려면 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이벤트를 검토할 수 있습니다 및이 저장된 프로시저를 사용 하 여 모니터링이 시스템에 기록 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="Arguments"></a> 인수  
 @xevent_channel  
 확장 이벤트의 유형입니다. 기본값은 이전 30분 동안 기록된 모든 이벤트를 반환하도록 설정됩니다. 기록된 이벤트는 활성화된 확장 이벤트의 유형에 따라 달라집니다. 이 매개 변수를 사용하여 특정 유형의 이벤트만 표시되도록 저장 프로시저를 필터링할 수 있습니다. 전체 이벤트 이름을 지정 하거나 같은 부분 문자열을 지정할 수 있습니다. **'Admin'** , **'분석'** 합니다 **'Operational'** , 및 **'Debug'** 합니다. 합니다 @event_channel 됩니다 **VARCHAR (255)** 합니다.  
  
 현재 사용 가능한 형식 사용 이벤트의 목록을 가져오려면 합니다 **managed_backup.fn_get_current_xevent_settings** 함수입니다.  
  
 [@begin_time  
 이벤트가 표시되어야 하는 기간의 시작 시간입니다. @begin_time 매개 변수는 DATETIME 이며 기본값은 NULL입니다. 지정되지 않은 경우 이전 30분의 이벤트가 표시됩니다.  
  
 @end_time  
 이벤트가 표시되어야 하는 기간의 종료 시간입니다. @end_time 매개 변수는 DATATIME 이며 기본값은 NULL입니다.  지정하지 않은 경우 현재 시간까지의 이벤트가 표시됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
 이 저장 프로시저는 다음 정보와 함께 테이블을 반환합니다.  
  
||||  
|-|-|-|  
|열 이름|데이터 형식|설명|  
|event_type|NVARCHAR(512)|확장 이벤트 유형|  
|이벤트|NVARCHAR(512)|이벤트 로그의 요약입니다.|  
|타임 스탬프|timestamp|이벤트 발생 시 표시되는 이벤트의 타임스탬프입니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 필요 **EXECUTE** 저장된 프로시저에 대 한 권한. 또한 필요 **VIEW SERVER STATE** 권한을 내부적으로 다른 시스템 개체를 호출 하므로이 권한이 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이전 30분 동안 기록된 모든 이벤트를 반환합니다.  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics  
  
```  
  
 다음 예에서는 특정 시간 범위 동안 기록된 모든 이벤트를 반환합니다.  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Admin',  
  @begin_time = '2013-06-01', @end_time = '2013-06-10'  
  
```  
  
 다음 예에서는 이전 30분 동안 기록된 모든 분석 이벤트를 반환합니다.  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Analytic'  
  
```  
  
  
