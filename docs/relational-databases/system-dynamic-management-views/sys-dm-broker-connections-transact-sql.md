---
title: sys.dm_broker_connections (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_connections
- dm_broker_connections
- sys.dm_broker_connections_TSQL
- dm_broker_connections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_connections dynamic management view
ms.assetid: d9e20433-67fe-4fcc-80e3-b94335b2daef
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 95acff9d1b80560294758045c449c1c6c6790c27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62759978"
---
# <a name="sysdmbrokerconnections-transact-sql"></a>sys.dm_broker_connections(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 네트워크 연결에 대해 한 행을 반환합니다. 다음 표에서는 보다 자세한 정보를 제공합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**connection_id**|**uniqueidentifier**|연결의 ID입니다. NULL을 허용합니다.|  
|**transport_stream_id**|**uniqueidentifier**|식별자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TCP/IP 통신에 대 한이 연결에서 사용 하는 네트워크 인터페이스 (SNI) 연결 합니다. NULL을 허용합니다.|  
|**state**|**smallint**|연결의 현재 상태입니다. NULL을 허용합니다. 가능한 값:<br /><br /> 1 = NEW<br /><br /> 2 = CONNECTING<br /><br /> 3 = CONNECTED<br /><br /> 4 = LOGGED_IN<br /><br /> 5 = CLOSED|  
|**state_desc**|**nvarchar(60)**|연결의 현재 상태입니다. NULL을 허용합니다. 가능한 값:<br /><br /> NEW<br /><br /> CONNECTING<br /><br /> CONNECTED<br /><br /> LOGGED_IN<br /><br /> CLOSED|  
|**connect_time**|**datetime**|연결을 연 날짜와 시간입니다. NULL을 허용합니다.|  
|**login_time**|**datetime**|연결에 대한 로그인이 성공한 날짜와 시간입니다. NULL을 허용합니다.|  
|**authentication_method**|**nvarchar(128)**|Windows 인증 방법의 이름(예: NTLM 또는 KERBEROS)입니다. 값은 Windows에서 가져옵니다. NULL을 허용합니다.|  
|**principal_name**|**nvarchar(128)**|연결 권한에 대해 확인된 로그인의 이름입니다. Windows 인증의 경우 이 값은 원격 사용자 이름입니다. 인증서 인증의 경우 이 값은 인증서 소유자입니다. NULL을 허용합니다.|  
|**remote_user_name**|**nvarchar(128)**|Windows 인증에서 사용하는 다른 데이터베이스의 피어 사용자 이름입니다. NULL을 허용합니다.|  
|**last_activity_time**|**datetime**|연결을 사용하여 마지막으로 정보를 보내거나 받은 날짜와 시간입니다. NULL을 허용합니다.|  
|**is_accept**|**bit**|연결이 원격측에서 시작되었는지 여부를 나타냅니다. NULL을 허용합니다.<br /><br /> 1 = 연결 요청을 원격 인스턴스에서 받아들였습니다.<br /><br /> 0 = 로컬 인스턴스에서 연결을 시작했습니다.|  
|**login_state**|**smallint**|이 연결에 대한 로그인 프로세스의 상태입니다. 가능한 값:<br /><br /> 0 = INITIAL<br /><br /> 1 = WAIT LOGIN NEGOTIATE<br /><br /> 2 = ONE ISC<br /><br /> 3 = ONE ASC<br /><br /> 4 = TWO ISC<br /><br /> 5 = TWO ASC<br /><br /> 6 = WAIT ISC Confirm<br /><br /> 7 = WAIT ASC Confirm<br /><br /> 8 = WAIT REJECT<br /><br /> 9 = WAIT PRE-MASTER SECRET<br /><br /> 10 = WAIT VALIDATION<br /><br /> 11 = WAIT ARBITRATION<br /><br /> 12 = ONLINE<br /><br /> 13 = ERROR|  
|**login_state_desc**|**nvarchar(60)**|원격 컴퓨터에서의 로그인의 현재 상태입니다. 가능한 값:<br /><br /> 연결 핸드셰이크가 초기화 중입니다.<br /><br /> 연결 핸드셰이크가 로그인 협상 메시지를 기다리고 있습니다.<br /><br /> 연결 핸드셰이크가 인증을 위한 보안 컨텍스트를 초기화하여 보냈습니다.<br /><br /> 연결 핸드셰이크가 인증을 위한 보안 컨텍스트를 받아 수락했습니다.<br /><br /> 연결 핸드셰이크가 인증을 위한 보안 컨텍스트를 초기화하여 보냈습니다. 피어를 인증하는 데 사용할 수 있는 선택적 메커니즘이 있습니다.<br /><br /> 연결 핸드셰이크가 인증을 위한 보안 컨텍스트를 받아 수락했습니다. 피어를 인증하는 데 사용할 수 있는 선택적 메커니즘이 있습니다.<br /><br /> 연결 핸드셰이크가 보안 컨텍스트 초기화 확인 메시지를 기다리고 있습니다.<br /><br /> 연결 핸드셰이크가 보안 컨텍스트 수락 확인 메시지를 기다리고 있습니다.<br /><br /> 연결 핸드셰이크가 실패한 인증에 대한 SSPI 거부 메시지를 기다리고 있습니다.<br /><br /> 연결 핸드셰이크가 Pre-Master Secret 메시지를 기다리고 있습니다.<br /><br /> 연결 핸드셰이크가 유효성 검사 메시지를 기다리고 있습니다.<br /><br /> 연결 핸드셰이크가 중재 메시지를 기다리고 있습니다.<br /><br /> 연결 핸드셰이크가 완료되었으며 메시지 교환을 위한 온라인(준비) 상태입니다.<br /><br /> 연결 오류입니다.|  
|**peer_certificate_id**|**int**|원격 인스턴스에서 인증을 위해 사용하는 인증서의 로컬 개체 ID입니다. 이 인증서의 소유자에게 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 엔드포인트에 대한 CONNECT 권한이 있어야 합니다. NULL을 허용합니다.|  
|**encryption_algorithm**|**smallint**|이 연결에 사용되는 암호화 알고리즘입니다. NULL을 허용합니다. 가능한 값:<br /><br /> **값 &#124; 설명 &#124; 해당 DDL 옵션**<br /><br /> 0 &#124; none &#124; 사용 안 함<br /><br /> 1 &AMP;#124; 만 서명<br /><br /> 2 &#124; -AES, RC4 &#124; 필요한 &#124; 필요한 알고리즘 RC4}<br /><br /> 3 &#124; AES &#124;필요한 알고리즘 AES<br /><br /> **참고:** RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|암호화 알고리즘을 텍스트로 표시한 것입니다. NULL을 허용합니다. 가능한 값은 다음과 같습니다.<br /><br /> **설명 &#124; 해당 DDL 옵션**<br /><br /> 없음 &#124; 사용 안 함<br /><br /> RC4 &#124; {필요한 &#124; 필요한 알고리즘 RC4}<br /><br /> AES &#124; 필요한 알고리즘 AES<br /><br /> -NONE, RC4 &#124; {지원 &#124; 지원 되는 알고리즘 RC4}<br /><br /> -NONE, AES &#124; 지원 되는 알고리즘 RC4<br /><br /> RC4, AES &#124; 필요한 알고리즘 RC4 AES<br /><br /> AES, RC4 &#124; 필요한 알고리즘 AES RC4<br /><br /> -NONE, RC4, AES &#124; 지원 되는 알고리즘 RC4 AES<br /><br /> -NONE, AES, RC4 &#124; 지원 되는 알고리즘 AES RC4|  
|**receives_posted**|**smallint**|이 연결에 대해 완료되지 않은 비동기 네트워크 받기 수입니다. NULL을 허용합니다.|  
|**is_receive_flow_controlled**|**bit**|네트워크 사용량이 많아 흐름 제어로 인해 네트워크 받기가 연기되었는지 여부를 나타냅니다. NULL을 허용합니다.<br /><br /> 1 = True|  
|**sends_posted**|**smallint**|이 연결에 대해 완료되지 않은 비동기 네트워크 보내기 수입니다. NULL을 허용합니다.|  
|**is_send_flow_controlled**|**bit**|네트워크 사용량이 많아 네트워크 흐름 제어로 인해 네트워크 보내기가 연기되었는지 여부를 나타냅니다. NULL을 허용합니다.<br /><br /> 1 = True|  
|**total_bytes_sent**|**bigint**|이 연결에서 보낸 총 바이트 수입니다. NULL을 허용합니다.|  
|**total_bytes_received**|**bigint**|이 연결에서 받은 총 바이트 수입니다. NULL을 허용합니다.|  
|**total_fragments_sent**|**bigint**|이 연결에서 보낸 총 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 조각 수입니다. NULL을 허용합니다.|  
|**total_fragments_received**|**bigint**|이 연결에서 받은 총 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 조각 수입니다. NULL을 허용합니다.|  
|**total_sends**|**bigint**|이 연결에서 수행한 총 네트워크 보내기 요청 수입니다. NULL을 허용합니다.|  
|**total_receives**|**bigint**|이 연결에서 수행한 총 네트워크 받기 요청 수입니다. NULL을 허용합니다.|  
|**peer_arbitration_id**|**uniqueidentifier**|엔드포인트의 내부 식별자입니다. NULL을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="physical-joins"></a>물리적 조인  
 ![Sys.dm_broker_connections에 대 한 조인](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-connections-1.gif "sys.dm_broker_connections에 대 한 조인")  
  
## <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|**dm_broker_connections.connection_id**|**dm_exec_connections.connection_id**|일 대 일|  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 관련 동적 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

