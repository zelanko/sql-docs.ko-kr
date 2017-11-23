---
title: sys.transmission_queue (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- transmission_queue
- sys.transmission_queue_TSQL
- sys.transmission_queue
- transmission_queue_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.transmission_queue catalog view
ms.assetid: f3515d1a-be8f-4a27-8058-8865f0919838
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c824744fab0b34685678471b045b360ee89c08b7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="systransmissionqueue-transact-sql"></a>sys.transmission_queue(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 카탈로그 뷰는 다음 표와 같이 전송 큐의 각 메시지에 대한 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**conversation_handle**|**uniqueidentifier**|이 메시지가 속하는 대화의 식별자입니다. NULL을 허용하지 않습니다.|  
|**to_service_name**|**nvarchar(256)**|이 메시지를 받을 서비스 이름입니다. NULL을 허용합니다.|  
|**to_broker_instance**|**nvarchar (128)**|이 메시지를 받을 서비스를 호스팅하는 Broker 식별자입니다. NULL을 허용합니다.|  
|**from_service_name**|**nvarchar(256)**|이 메시지를 보낸 서비스 이름입니다. NULL을 허용합니다.|  
|**service_contract_name**|**nvarchar(256)**|이 메시지의 대화가 준수하는 계약의 이름입니다. NULL을 허용합니다.|  
|**enqueue_time**|**datetime**|큐에 메시지가 입력된 시간입니다. 이 값은 인스턴스의 현지 표준 시간대에 관계없이 UTC를 사용합니다. NULL을 허용하지 않습니다.|  
|**message_sequence_number**|**bigint**|메시지의 시퀀스 번호입니다. NULL을 허용하지 않습니다.|  
|**message_type_name**|**nvarchar(256)**|메시지의 메시지 유형 이름입니다. NULL을 허용합니다.|  
|**is_conversation_error**|**bit**|이 메시지가 오류 메시지인지 여부를 나타냅니다.<br /><br /> 0 = 오류 메시지 아님<br /><br /> 1 = 오류 메시지<br /><br /> NULL을 허용하지 않습니다.|  
|**is_end_of_dialog**|**bit**|이 메시지가 대화 메시지의 끝인지 여부를 나타냅니다. NULL을 허용하지 않습니다.<br /><br /> 0 = 대화 메시지의 끝 아님<br /><br /> 1 = 대화 메시지의 끝<br /><br /> NULL을 허용하지 않습니다.|  
|**message_body**|**varbinary(max)**|이 메시지의 본문입니다. NULL을 허용합니다.|  
|**transmission_status**|**nvarchar(4000)**|이 메시지가 큐에 있는 이유입니다. 일반적으로 메시지 보내기가 실패한 이유를 설명하는 오류 메시지입니다. 비어 있으면 아직 메시지를 보내지 않은 것입니다. NULL을 허용합니다.|  
|**우선 순위**|**tinyint**|이 메시지에 할당된 우선 순위 수준입니다. NULL을 허용하지 않습니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
  
