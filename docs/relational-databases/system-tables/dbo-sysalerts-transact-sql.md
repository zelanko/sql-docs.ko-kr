---
title: dbo.sysalerts (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7bad6fbd9229547318a060f08eeb102b21cda9bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470891"
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 경고에 대해 한 행을 포함합니다. 경고는 이벤트에 대한 응답으로 전달된 메시지입니다. 경고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경을 초월하여 메시지를 전달할 수 있으며 이때 경고는 전자 메일 또는 호출기 메시지가 될 수 있습니다. 경고 또한 태스크를 생성할 수 있습니다.  이 테이블에 저장 되는 **msdb** 데이터베이스입니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|경고 ID입니다.|  
|**name**|**sysname**|경고 이름입니다.|  
|**event_source**|**nvarchar(100)**|이벤트의 원본: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**event_category_id**|**int**|나중에 사용하도록 예약되어 있습니다.|  
|**event_id**|**int**|나중에 사용하도록 예약되어 있습니다.|  
|**message_id**|**int**|사용자 정의 메시지 ID 또는에 대 한 참조가 **sysmessages** 이 경고를 트리거하는 메시지입니다.|  
|**severity**|**int**|경고를 트리거한 심각도입니다.|  
|**enabled**|**tinyint**|경고의 상태입니다.<br /><br /> **0** = 사용 안 함.<br /><br /> **1** = 사용 하도록 설정 합니다.|  
|**delay_between_responses**|**int**|경고에 대한 알림 사이의 대기 시간을 초로 표시한 것입니다.|  
|**last_occurrence_date**|**int**|경고가 마지막으로 발생한 날짜입니다.|  
|**last_occurrence_time**|**int**|경고가 마지막으로 발생한 시간입니다.|  
|**last_response_date**|**int**|경고가 마지막으로 알려진 날짜입니다.|  
|**last_response_time**|**int**|경고가 마지막으로 알려진 시간입니다.|  
|**notification_message**|**nvarchar(512)**|경고와 함께 전달된 추가 정보입니다.|  
|**include_event_description**|**tinyint**|전자 메일, 호출기 또는 Net send 이벤트 설명 보낼지 여부를 나타내는 비트 마스크입니다. 값에 대 한 아래 차트를 참조 하세요.|  
|**database_name**|**nvarchar(512)**|해당 경고가 해당 경고를 트리거하기 위해 반드시 발생해야 하는 데이터베이스입니다.|  
|**event_description_keyword**|**nvarchar(100)**|경고를 트리거하기 위해 오류가 반드시 일치해야 하는 패턴입니다.|  
|**occurrence_count**|**int**|해당 경고의 발생 수입니다.|  
|**count_reset_date**|**int**|일 (날짜) 수가 다시 설정 됩니다 **0**합니다.|  
|**count_reset_time**|**int**|일의 시간 수가 다시 설정 됩니다 **0**합니다.|  
|**job_id**|**uniqueidentifier**|해당 경고가 발생할 때 실행되는 태스크의 ID입니다.|  
|**has_notification**|**int**|경고가 발생할 때 전자 메일 알림을 받는 운영자의 수입니다.|  
|**flags**|**int**|예약되어 있습니다.|  
|**performance_condition**|**nvarchar(512)**|예약되어 있습니다.|  
|**category_id**|**int**|예약되어 있습니다.|  
  
 ## <a name="remarks"></a>Remarks

다음 표에서 include_event_description 비트 마스크 값을 보여 줍니다. 10 진수 값 dbo.sysalerts에서 반환 됩니다. 

|Decimal | BINARY | 의미 |
|------|------|------|
|0 |0000 |메시지 없음 |
|1 |0001 |메일 주소 |
|2 |0010 |호출기(pager) |
|3 |0011 |호출기 및 전자 메일 |
|4 |0100 |Net Send |
|5 |0101 |Net send 및 전자 메일 |
|6 |0110 |Net send 및 호출기 |
|7 |0111 |Net send, 호출기 및 전자 메일 |
  
