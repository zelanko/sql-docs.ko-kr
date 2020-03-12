---
title: dbo. sysschedules (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysschedules_TSQL
- sysschedules
- sysschedules_TSQL
- dbo.sysschedules
dev_langs:
- TSQL
helpviewer_keywords:
- sysschedules system table
ms.assetid: 4cac9237-7a69-4035-bb3e-928b76aad698
author: stevestein
ms.author: sstein
ms.openlocfilehash: cbf570a09f3316172a60206730b91644cc603f0b
ms.sourcegitcommit: 4bba3c8e3360bcbe269819d61f8898d0ad52c6e3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79090573"
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 일정에 대한 정보를 포함합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 일정의 ID입니다.|  
|**schedule_uid**|**uniqueidentifier**|작업 일정의 고유 식별자입니다. 이 값은 배포된 작업의 일정을 식별하는 데 사용됩니다.|  
|**originating_server_id**|**int**|작업 일정을 가져온 마스터 서버의 ID입니다.|  
|**name**|**sysname (nvarchar (128))**|작업 일정의 사용자 정의 이름입니다. 이 이름은 작업 내에서 고유해야 합니다.|  
|**owner_sid**|**varbinary (85)**|작업 일정을 소유 하는 사용자 또는 그룹의 Microsoft Windows *security_identifier* 입니다.|  
|**사용**|**int**|작업 일정의 상태입니다.<br /><br /> **0** = 사용 안 함<br /><br /> **1** = 사용<br /><br /> 일정을 사용할 수 없는 경우에는 작업이 일정에 따라 실행되지 않습니다.|  
|**freq_type**|**int**|이 일정에 따라 작업이 실행되는 빈도입니다.<br /><br /> **1** = 한 번만<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** = 매월, **freq_interval** 기준<br /><br /> **64** = SQL Server 에이전트 서비스가 시작 될 때 실행 됩니다.<br /><br /> **128** = 컴퓨터가 유휴 상태일 때 실행 됩니다.|  
|**freq_interval**|**int**|작업이 실행되는 요일입니다. **Freq_type**값에 따라 달라 집니다. 기본값은 **freq_interval** 이 사용 되지 않음을 나타내는 **0**입니다. 가능한 값과 그 영향에 대해서는 아래 표를 참조 하세요.|  
|**freq_subday_type**|**int**|**Freq_subday_interval**단위입니다. 다음은 가능한 값과 그에 대 한 설명입니다.<br /><br /> <br /><br /> **1** : 지정 된 시간에<br /><br /> **2** : 초<br /><br /> **4** : 분<br /><br /> **8** : 시간|  
|**freq_subday_interval**|**int**|각 작업 실행 사이에 발생 하는 **freq_subday_type** 기간 수입니다.|  
|**freq_relative_interval**|**int**|매월 **freq_interval** 발생 하는 경우 **freq_type** 는 **32** (매월 상대적)입니다. 다음 값 중 하나입니다.<br /><br /> **0** = **freq_relative_interval** 사용 되지 않습니다.<br /><br /> **1** = 첫 번째<br /><br /> **2** = 초<br /><br /> **4** = 세 번째<br /><br /> **8** = 네 번째<br /><br /> **16** = 마지막|  
|**freq_recurrence_**<br /><br /> **이용한**|**int**|예약된 작업 실행 간의 주 또는 월 수입니다. **freq_recurrence_factor** 는 **freq_type** 이 **8**, **16**또는 **32**인 경우에만 사용 됩니다. 이 열에 **0**이 있으면 **freq_recurrence_factor** 사용 되지 않습니다.|  
|**active_start_date**|**int**|작업 실행이 시작되는 날짜입니다. 날짜 형식은 YYYYMMDD입니다. NULL은 오늘 날짜를 나타냅니다.|  
|**active_end_date**|**int**|작업 실행이 중지되는 날짜입니다. 날짜 형식은 YYYYMMDD입니다.|  
|**active_start_time**|**int**|**Active_start_date** 와 해당 작업이 실행을 시작 하는 **active_end_date** 사이의 모든 날짜에 대 한 시간입니다. 시간 형식은 24시간제를 사용하는 HHMMSS입니다.|  
|**active_end_time**|**int**|**Active_start_date** 와 작업 실행이 중지 되는 **active_end_date** 사이의 모든 날짜에 대 한 시간입니다. 시간 형식은 24시간제를 사용하는 HHMMSS입니다.|  
|**date_created**|**datetime**|일정을 작성한 날짜와 시간입니다.|  
|**date_modified**|**datetime**|일정을 마지막으로 수정한 날짜와 시간입니다.|  
|**version_number**|**int**|일정의 현재 버전 번호입니다. 예를 들어 일정이 10 번 수정 된 경우 **version_number** 는 10입니다.|  
  
|freq_type의 값|freq_interval에 미치는 영향|  
|-------------------------|------------------------------|  
|**1** (한 번)|**freq_interval** 사용 되지 않음 (**0**)|  
|**4** (매일)|**Freq_interval** 일 마다|  
|**8** (매주)|**freq_interval** 은 다음 중 하나 이상입니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **4** = 화요일<br /><br /> **8** = 수요일<br /><br /> **16** = 목요일<br /><br /> **32** = 금요일<br /><br /> **64** = 토요일|  
|**16** (매월)|월 **freq_interval** 일|  
|**32** (매월, 상대)|**freq_interval** 은 다음 중 하나입니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **3** = 화요일<br /><br /> **4** = 수요일<br /><br /> **5** = 목요일<br /><br /> **6** = 금요일<br /><br /> **7** = 토요일<br /><br /> **8** = 일<br /><br /> **9** = 평일<br /><br /> **10** = 주말|  
|**64** (SQL Server 에이전트 서비스가 시작 될 때 시작)|**freq_interval** 사용 되지 않음 (**0**)|  
|**128** (컴퓨터가 유휴 상태일 때 실행)|**freq_interval** 사용 되지 않음 (**0**)|  
  
## <a name="see-also"></a>참고 항목  
 [&#40;Transact-sql&#41;에 대 한 dbo. sysjobschedules](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  
