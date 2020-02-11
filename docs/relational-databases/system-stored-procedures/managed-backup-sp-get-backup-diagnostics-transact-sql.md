---
title: managed_backup. sp_get_backup_diagnostics (Transact-sql) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942042"
---
# <a name="managed_backupsp_get_backup_diagnostics-transact-sql"></a>managed_backup. sp_get_backup_diagnostics (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  스마트 관리에 기록된 확장 이벤트를 반환합니다.  
  
 이 저장 프로시저를 사용 하 여 Smart Admin에서 기록한 확장 이벤트를 모니터링 합니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 이벤트는이 시스템에 기록 되며,이 저장 프로시저를 사용 하 여 검토 하 고 모니터링할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="Arguments"></a> 인수  
 @xevent_channel  
 확장 이벤트의 유형입니다. 기본값은 이전 30분 동안 기록된 모든 이벤트를 반환하도록 설정됩니다. 기록된 이벤트는 활성화된 확장 이벤트의 유형에 따라 달라집니다. 이 매개 변수를 사용하여 특정 유형의 이벤트만 표시되도록 저장 프로시저를 필터링할 수 있습니다. 전체 이벤트 이름을 지정 하거나 **' admin**', **' 분석 '**, **' 작동 '** 및 **' 디버그 '** 와 같은 부분 문자열을 지정할 수 있습니다. 는 @event_channel **VARCHAR (255)** 입니다.  
  
 현재 사용 하도록 설정 된 이벤트 유형 목록을 가져오려면 **managed_backup. fn_get_current_xevent_settings** 함수를 사용 합니다.  
  
 [@begin_time  
 이벤트가 표시되어야 하는 기간의 시작 시간입니다. @begin_time 매개 변수는 DATETIME 이며 기본값은 NULL입니다. 지정되지 않은 경우 이전 30분의 이벤트가 표시됩니다.  
  
 @end_time  
 이벤트가 표시되어야 하는 기간의 종료 시간입니다. @end_time 매개 변수는 DATATIME 이며 기본값은 NULL입니다.  지정하지 않은 경우 현재 시간까지의 이벤트가 표시됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
 이 저장 프로시저는 다음 정보와 함께 테이블을 반환합니다.  
  
||||  
|-|-|-|  
|열 이름|데이터 형식|Description|  
|event_type|NVARCHAR (512)|확장 이벤트 유형|  
|행사|NVARCHAR (512)|이벤트 로그의 요약입니다.|  
|타임스탬프|timestamp|이벤트 발생 시 표시되는 이벤트의 타임스탬프입니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 저장 프로시저에 대 한 **EXECUTE** 권한이 필요 합니다. 또한이 권한이 필요한 다른 시스템 개체를 내부적으로 호출 하기 때문에 **VIEW SERVER STATE** 권한도 필요 합니다.  
  
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
  
  
