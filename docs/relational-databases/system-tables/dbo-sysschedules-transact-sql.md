---
title: dbo.sysschedules (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5a1922fd8b9cdfb327186afe453fc1904d698579
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470715"
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 일정에 대한 정보를 포함합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 일정의 ID입니다.|  
|**schedule_uid**|**uniqueidentifier**|작업 일정의 고유 식별자입니다. 이 값은 배포된 작업의 일정을 식별하는 데 사용됩니다.|  
|**originating_server_id**|**int**|작업 일정을 가져온 마스터 서버의 ID입니다.|  
|**name**|**sysname (nvarchar(128))**|작업 일정의 사용자 정의 이름입니다. 이 이름은 작업 내에서 고유해야 합니다.|  
|**owner_sid**|**varbinary(85)**|Microsoft Windows *security_identifier* 사용자 또는 작업 일정을 소유 하는 그룹입니다.|  
|**enabled**|**int**|작업 일정의 상태입니다.<br /><br /> **0** = 사용 안 함.<br /><br /> **1** = 사용 하도록 설정 합니다.<br /><br /> 일정을 사용할 수 없는 경우에는 작업이 일정에 따라 실행되지 않습니다.|  
|**freq_type**|**int**|이 일정에 따라 작업이 실행되는 빈도입니다.<br /><br /> **1** = 한 번만<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** = 매월, 상대적인 **freq_interval**<br /><br /> **64** = SQL Server 에이전트 서비스가 시작 될 때 실행<br /><br /> **128** = 컴퓨터가 유휴 상태일 때 실행|  
|**freq_interval**|**int**|작업이 실행되는 요일입니다. 값에 따라 달라 집니다 **freq_type**합니다. 기본값은 **0**를 나타내는 **freq_interval** 사용 되지 않습니다. 가능한 값 및 그 영향에 대 한 아래 표를 참조 하세요.|  
|**freq_subday_type**|**int**|에 대 한 단위를 **freq_subday_interval**합니다. 가능한 값 및 해당 설명을 보려면은 다음과 같습니다.<br /><br /> <br /><br /> **1** : 지정된 시간<br /><br /> **2** : 초<br /><br /> **4** : 분<br /><br /> **8** : 시간|  
|**freq_subday_interval**|**int**|수가 **freq_subday_type** 작업의 각 실행 간에 발생 하는 기간.|  
|**freq_relative_interval**|**int**|때 **freq_interval** 경우에 각 월에 발생 합니다. **freq_interval** 됩니다 **32** (매월 상대적)입니다. 다음 값 중 하나입니다.<br /><br /> **0** = **freq_relative_interval** 사용 되지 않습니다<br /><br /> **1** = 첫 번째<br /><br /> **2** = Second<br /><br /> **4** = Third<br /><br /> **8** = Fourth<br /><br /> **16** = Last|  
|**freq_recurrence_**<br /><br /> **factor**|**int**|예약된 작업 실행 간의 주 또는 월 수입니다. **freq_recurrence_factor** 경우에 사용 됩니다 **freq_type** 됩니다 **8**를 **16**, 또는 **32**합니다. 이 열이 있으면 **0**를 **freq_recurrence_factor** 사용 되지 않습니다.|  
|**active_start_date**|**int**|작업 실행이 시작되는 날짜입니다. 날짜 형식은 YYYYMMDD입니다. NULL은 오늘 날짜를 나타냅니다.|  
|**active_end_date**|**int**|작업 실행이 중지되는 날짜입니다. 날짜 형식은 YYYYMMDD입니다.|  
|**active_start_time**|**int**|사이의 임의의 날짜에서 시간 **active_start_date** 하 고 **active_end_date** 작업 실행을 시작 합니다. 시간 형식은 24시간제를 사용하는 HHMMSS입니다.|  
|**active_end_time**|**int**|사이의 임의의 날짜에서 시간 **active_start_date** 하 고 **active_end_date** 작업 실행을 중지 합니다. 시간 형식은 24시간제를 사용하는 HHMMSS입니다.|  
|**date_created**|**datetime**|일정을 작성한 날짜와 시간입니다.|  
|**date_modified**|**datetime**|일정을 마지막으로 수정한 날짜와 시간입니다.|  
|**version_number**|**int**|일정의 현재 버전 번호입니다. 예를 들어, 일정을 10 번 수정 된 경우는 **version_number** 은 10입니다.|  
  
|freq_type의 값|freq_interval에 미치는 영향|  
|-------------------------|------------------------------|  
|**1** (한 번)|**freq_interval** 사용 되지 않습니다 (**0**)|  
|**4** (매일)|모든 **freq_interval** 일|  
|**8** (매주)|**freq_interval** 은 다음 중 하나 이상을:<br /><br /> **1** = Sunday<br /><br /> **2** = Monday<br /><br /> **4** = 화요일<br /><br /> **8** = 수요일<br /><br /> **16** = 목요일<br /><br /> **32** = 금요일<br /><br /> **64** = 토요일|  
|**16** (매월)|에 **freq_interval** 월의 일|  
|**32** (월간, 상대)|**freq_interval** 다음 중 하나입니다.<br /><br /> **1** = Sunday<br /><br /> **2** = Monday<br /><br /> **3** = 화요일<br /><br /> **4** = 수요일<br /><br /> **5** = 목요일<br /><br /> **6** = 금요일<br /><br /> **7** = 토요일<br /><br /> **8** = Day<br /><br /> **9** = 평일<br /><br /> **10** = 주말|  
|**64** (SQL Server 에이전트 서비스가 시작 될 때 시작)|**freq_interval** 사용 되지 않습니다 (**0**)|  
|**128** (컴퓨터가 유휴 상태일 때 실행 됨)|**freq_interval** 사용 되지 않습니다 (**0**)|  
  
## <a name="see-also"></a>참고자료  
 [dbo.sysjobschedules &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  
