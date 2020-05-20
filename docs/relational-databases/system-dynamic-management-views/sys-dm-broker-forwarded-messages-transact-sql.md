---
title: sys. dm_broker_forwarded_messages (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_forwarded_messages
- dm_broker_forwarded_messages
- sys.dm_broker_forwarded_messages_TSQL
- dm_broker_forwarded_messages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_forwarded_messages dynamic management view
ms.assetid: 5576376d-6364-417a-8475-aa770e060845
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7142fd9482b3db72a356568b97beb4467a3fab31
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830882"
---
# <a name="sysdm_broker_forwarded_messages-transact-sql"></a>sys.dm_broker_forwarded_messages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 전달하고 있는 각 Service Broker 메시지에 대해 행을 반환합니다.  
  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**conversation_id**|**uniqueidentifier**|이 메시지가 속하는 대화의 ID입니다. NULL을 허용합니다.|  
|**is_initiator**|**bit**|이것이 대화 시작자가 보낸 메시지인지 여부를 나타냅니다.  NULL을 허용합니다.<br /><br /> 0 = 시작자가 보낸 메시지가 아닙니다.<br /><br /> 1 = 시작자가 보낸 메시지입니다.|  
|**to_service_name**|**nvarchar(512)**|이 메시지를 받는 서비스의 이름입니다. NULL을 허용합니다.|  
|**to_broker_instance**|**nvarchar(512)**|이 메시지를 받는 서비스를 호스팅하는 Broker의 식별자입니다. NULL을 허용합니다.|  
|**from_service_name**|**nvarchar(512)**|이 메시지를 보낸 서비스 이름입니다. NULL을 허용합니다.|  
|**from_broker_instance**|**nvarchar(512)**|이 메시지를 보낸 서비스를 호스팅하는 Broker의 식별자입니다. NULL을 허용합니다.|  
|**adjacent_broker_address**|**nvarchar(512)**|이 메시지를 받을 네트워크 주소입니다. NULL을 허용합니다.|  
|**message_sequence_number**|**bigint**|대화 상자에 있는 메시지의 시퀀스 번호입니다. NULL을 허용합니다.|  
|**message_fragment_number**|**int**|대화 메시지가 조각화된 경우 이 전송 메시지가 포함하는 조각 번호입니다. NULL을 허용합니다.|  
|**hops_remaining**|**tinyint**|최종 대상에 도달하기 전에 메시지를 재전송할 수 있는 횟수입니다. 메시지가 전달될 때마다 이 숫자는 1씩 감소합니다. NULL을 허용합니다.|  
|**time_to_live**|**int**|메시지가 활성 상태로 유지되는 최대 시간입니다. 0에 도달하면 메시지가 삭제됩니다. NULL을 허용합니다.|  
|**time_consumed**|**int**|메시지가 활성화되어 있는 시간입니다. 메시지가 전달될 때마다 이 숫자는 메시지를 전달하는 데 걸린 시간만큼 증가합니다. NULL을 허용하지 않습니다.|  
|**message_id**|**uniqueidentifier**|메시지의 ID입니다. NULL을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 관련 동적 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

