---
title: sys.conversation_endpoints (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_endpoints_TSQL
- conversation_endpoints
- sys.conversation_endpoints
- sys.conversation_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_endpoints catalog view
ms.assetid: 2ed758bc-2a9d-4831-8da2-4b80e218f3ea
author: stevestein
ms.author: sstein
ms.openlocfilehash: 16d29272e4229ac93b3dd5b1eaf5502a07fb0a2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109539"
---
# <a name="sysconversationendpoints-transact-sql"></a>sys.conversation_endpoints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화의 각 상대는 대화 엔드포인트가 나타냅니다. 이 카탈로그 뷰에는 데이터베이스에 있는 각 대화 엔드포인트에 대한 행이 포함되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|conversation_handle|**uniqueidentifier**|이 대화 엔드포인트의 식별자입니다. NULL을 허용하지 않습니다.|  
|conversation_id|**uniqueidentifier**|대화의 식별자입니다. 이 식별자는 대화의 두 참가자가 모두 공유합니다. 이것은 is_initiator 열과 함께 데이터베이스 내에서 고유합니다. NULL을 허용하지 않습니다.|  
|is_initiator|**tinyint**|이 엔드포인트가 대화의 시작자인지 또는 대상인지를 나타냅니다.  NULL을 허용하지 않습니다.<br /><br /> 1 = 시작자<br /><br /> 0 = 대상|  
|service_contract_id|**int**|이 대화에 대한 계약의 식별자입니다. NULL을 허용하지 않습니다.|  
|conversation_group_id|**uniqueidentifier**|이 대화가 속하는 대화 그룹의 식별자입니다. NULL을 허용하지 않습니다.|  
|service_id|**int**|이 대화 상대에 대한 서비스 식별자입니다. NULL을 허용하지 않습니다.|  
|lifetime|**datetime**|이 대화의 만료 날짜/시간입니다. NULL을 허용하지 않습니다.|  
|state|**char(2)**|대화의 현재 상태입니다. NULL을 허용하지 않습니다. 다음 중 하나입니다.<br /><br /> 따라서 아웃 바운드가 시작 되었습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 대화에 대해 BEGIN CONVERSATION을 처리했지만 아직 보낸 메시지가 없습니다.<br /><br /> SI 인바운드가 시작 되었습니다. 다른 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 새 대화를 시작했지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 첫 번째 메시지를 완전히 받지 못했습니다. 첫 번째 메시지가 조각화되었거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 순서가 잘못된 메시지를 받는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 대화를 이 상태로 만들 수 있습니다. 하지만 대화에 대해 받은 첫 번째 전송에 첫 번째 메시지가 모두 포함된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 대화를 CO 상태로 만들 수 있습니다.<br /><br /> 대화를 CO 합니다. 대화가 설정되고 대화의 양쪽 모두 메시지를 보낼 수 있습니다. 일반 서비스에 대한 통신의 대부분은 대화가 이 상태일 때 수행됩니다.<br /><br /> 연결 끊김 DI 인바운드 합니다. 원격 대화 상대가 END CONVERSATION을 실행했습니다. 로컬 대화 상대가 END CONVERSATION을 실행할 때까지 대화는 이 상태로 유지됩니다. 응용 프로그램은 계속해서 대화 메시지를 받을 수 있습니다. 원격 대화 상대가 대화를 종료했기 때문에 애플리케이션에서 이 대화 메시지를 보낼 수는 없습니다. 응용 프로그램이 END CONVERSATION을 실행하면 대화가 CD(닫힘) 상태로 전환됩니다.<br /><br /> 아웃 바운드 연결 끊김을 수행 합니다. 로컬 대화 상대가 END CONVERSATION을 실행했습니다. 원격 대화 상대가 END CONVERSATION을 승인할 때까지 대화는 이 상태로 유지됩니다. 애플리케이션에서 대화 메시지를 보내거나 받을 수 없습니다. 원격 대화 상대가 END CONVERSATION을 승인하면 대화가 CD(닫힘) 상태로 전환됩니다.<br /><br /> ER 오류가 발생 했습니다. 이 엔드포인트에서 오류가 발생했습니다. 오류 메시지가 응용 프로그램 큐에 들어갑니다. 비어 있는 응용 프로그램 큐는 응용 프로그램이 이미 오류 메시지를 사용했음을 나타냅니다.<br /><br /> CD 닫힙니다. 대화 엔드포인트는 더 이상 사용되지 않습니다.|  
|state_desc|**nvarchar(60)**|끝점 대화 상태 설명입니다. 이 열은 NULL을 허용합니다. 다음 중 하나입니다.<br /><br /> **STARTED_OUTBOUND**<br /><br /> **STARTED_INBOUND**<br /><br /> **대화**<br /><br /> **DISCONNECTED_INBOUND**<br /><br /> **DISCONNECTED_OUTBOUND**<br /><br /> **CLOSED**<br /><br /> **ERROR**|  
|far_service|**nvarchar(256)**|원격 대화 상대에 있는 서비스의 이름입니다. NULL을 허용하지 않습니다.|  
|far_broker_instance|**nvarchar(128)**|원격 대화 상대에 대한 Broker 인스턴스입니다. NULL을 허용합니다.|  
|principal_id|**int**|로컬 대화 상대가 사용하는 인증서를 소유한 보안 주체의 식별자입니다. NULL을 허용하지 않습니다.|  
|far_principal_id|**int**|원격 대화 상대가 사용하는 인증서를 소유한 보안 주체의 식별자입니다. NULL을 허용하지 않습니다.|  
|outbound_session_key_identifier|**uniqueidentifier**|이 대화에 대한 아웃바운드 암호화 키의 식별자입니다. NULL을 허용하지 않습니다.|  
|inbound_session_key_identifier|**uniqueidentifier**|이 대화에 대한 인바운드 암호화 키의 식별자입니다. NULL을 허용하지 않습니다.|  
|security_timestamp|**datetime**|로컬 세션 키가 생성된 시간입니다. NULL을 허용하지 않습니다.|  
|dialog_timer|**datetime**|이 대화에 대한 대화 타이머가 DialogTimer 메시지를 보내는 시간입니다. NULL을 허용하지 않습니다.|  
|send_sequence|**bigint**|전송 시퀀스의 다음 메시지 번호입니다. NULL을 허용하지 않습니다.|  
|last_send_tran_id|**binary(6)**|메시지를 보내는 마지막 트랜잭션의 내부 트랜잭션 ID입니다. NULL을 허용하지 않습니다.|  
|end_dialog_sequence|**bigint**|종료 대화 메시지의 시퀀스 번호입니다. NULL을 허용하지 않습니다.|  
|receive_sequence|**bigint**|메시지 수신 시퀀스에서 예상되는 다음 메시지 번호입니다. NULL을 허용하지 않습니다.|  
|receive_sequence_frag|**int**|메시지 수신 시퀀스에서 예상되는 다음 메시지 조각 번호입니다. NULL을 허용하지 않습니다.|  
|system_sequence|**bigint**|이 대화에 대한 마지막 시스템 메시지의 시퀀스 번호입니다. NULL을 허용하지 않습니다.|  
|first_out_of_order_sequence|**bigint**|이 대화에 대한 순서가 잘못된 메시지에서 첫 번째 메시지의 시퀀스 번호입니다. NULL을 허용하지 않습니다.|  
|last_out_of_order_sequence|**bigint**|이 대화에 대한 순서가 잘못된 메시지에서 마지막 메시지의 시퀀스 번호입니다. NULL을 허용하지 않습니다.|  
|last_out_of_order_frag|**int**|이 대화에 대한 순서가 잘못된 조각에서 마지막 메시지의 시퀀스 번호입니다. NULL을 허용하지 않습니다.|  
|is_system|**bit**|시스템 대화일 경우 1입니다. NULL을 허용하지 않습니다.|  
|priority|**tinyint**|이 대화 엔드포인트에 할당된 대화 우선 순위입니다. NULL을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
  
