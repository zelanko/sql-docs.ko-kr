---
title: sysjobs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobs
- sysjobs_TSQL
- dbo.sysjobs
- dbo.sysjobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobs system table
ms.assetid: e244a6a5-54c2-47a6-8039-dd1852b0ae59
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8fe374a81fc88b6591da8fb0303d5ea490cccac0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807054"
---
# <a name="dbosysjobs-transact-sql"></a>dbo.sysjobs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 실행될 각 예약 작업의 정보를 저장합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|작업의 고유 ID입니다.|  
|**originating_server_id**|**int**|작업을 가져온 서버의 ID입니다.|  
|**name**|**sysname**|작업의 이름입니다.|  
|**사용**|**tinyint**|작업을 실행할 수 있는지를 표시합니다.|  
|**한**|**nvarchar(512)**|작업 설명입니다.|  
|**start_step_id**|**int**|실행을 시작해야 하는 작업 단계의 ID입니다.|  
|**category_id**|**int**|작업 범주의 ID입니다.|  
|**owner_sid**|**varbinary(85)**|작업 소유자의 보안 ID(SID)입니다.|  
|**notify_level_eventlog**|**int**|Microsoft Windows 응용 프로그램 로그에 알림 이벤트를 기록해 야 하는 상황을 나타내는 **비트 마스크** 입니다.<br /><br /> **0** = 안 함<br /><br /> **1** = 작업이 성공 하는 경우<br /><br /> **2** = 작업이 실패 하는 경우<br /><br /> **3** = 작업이 완료 될 때마다 (작업 결과에 관계 없음)|  
|**notify_level_email**|**int**|작업을 완료했을 때, 어떤 상황에서 알림 전자 메일을 전달해야 할지를 지정하는 비트 마스크입니다.<br /><br /> **0** = 안 함<br /><br /> **1** = 작업이 성공 하는 경우<br /><br /> **2** = 작업이 실패 하는 경우<br /><br /> **3** = 작업이 완료 될 때마다 (작업 결과에 관계 없음)|  
|**notify_level_netsend**|**int**|작업을 완료했을 때, 어떤 상황에서 네트워크 메시지를 전달해야 할지를 지정하는 비트 마스크입니다.<br /><br /> **0** = 안 함<br /><br /> **1** = 작업이 성공 하는 경우<br /><br /> **2** = 작업이 실패 하는 경우<br /><br /> **3** = 작업이 완료 될 때마다 (작업 결과에 관계 없음)|  
|**notify_level_page**|**int**|작업을 완료했을 때, 어떤 상황에서 호출을 해야 할지를 지정하는 비트 마스크입니다.<br /><br /> **0** = 안 함<br /><br /> **1** = 작업이 성공 하는 경우<br /><br /> **2** = 작업이 실패 하는 경우<br /><br /> **3** = 작업이 완료 될 때마다 (작업 결과에 관계 없음)|  
|**notify_email_operator_id**|**int**|정보를 알릴 운영자의 전자 메일 이름입니다.|  
|**notify_netsend_operator_id**|**int**|네트워크 메시지를 전달할 때 사용하는 컴퓨터 또는 사용자의 ID입니다.|  
|**notify_page_operator_id**|**int**|호출을 전달할 때 사용하는 컴퓨터 또는 사용자의 ID입니다.|  
|**delete_level**|**int**|작업이 완료 될 때 작업을 삭제 해야 하는 상황을 나타내는 **비트 마스크** 입니다.<br /><br /> **0** = 안 함<br /><br /> **1** = 작업이 성공 하는 경우<br /><br /> **2** = 작업이 실패 하는 경우<br /><br /> **3** = 작업이 완료 될 때마다 (작업 결과에 관계 없음)|  
|**date_created**|**datetime**|작업을 만든 날짜입니다.|  
|**date_modified**|**datetime**|작업을 마지막으로 수정한 날짜입니다.|  
|**version_number**|**int**|작업 버전입니다.|  
  
  
