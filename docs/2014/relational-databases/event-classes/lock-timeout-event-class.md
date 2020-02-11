---
title: Lock:Timeout 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Timeout event class
ms.assetid: 8492f4be-4ea9-4059-80e0-9e7b71597da9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67f9d89897ef36d297dbeabfffcc02906677cb29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62663958"
---
# <a name="locktimeout-event-class"></a>Lock:Timeout 이벤트 클래스
  Lock:Timeout 이벤트 클래스는 페이지 등의 특정 리소스에 대해 다른 트랜잭션이 차단 잠금을 보유 중이기 때문에 해당 리소스에 대한 잠금 요청 시간이 초과되었음을 나타냅니다. 제한 시간은 @@LOCK_TIMEOUT 시스템 함수에 의해 결정되며 SET LOCK_TIMEOUT 문을 사용하여 설정할 수 있습니다.  
  
 Lock:Timeout 이벤트 클래스를 사용하여 제한 시간 조건이 발생하는 경우를 모니터링할 수 있습니다. 이 정보는 제한 시간이 애플리케이션 성능에 큰 영향을 주는지 여부와 관련 개체를 확인하는 데 유용하게 사용됩니다. 이러한 개체를 수정하는 애플리케이션 코드를 검사하여 제한 시간을 최소화하도록 변경할 수 있는지 확인할 수 있습니다.  
  
 지속 기간이 0인 Lock:Timeout 이벤트는 보통 내부 잠금 검색의 결과이며, 이는 반드시 문제를 나타내는 것은 아닙니다. Lock:Timeout (timeout > 0) 이벤트를 사용하면 지속 기간이 0인 제한 시간을 무시할 수 있습니다.  
  
## <a name="locktimeout-event-class-data-columns"></a>Lock:Timeout 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|BinaryData|`image`|잠금 리소스 식별자입니다.|2|yes|  
|ClientProcessID|`int`|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|DatabaseID|`int`|잠금 제한 시간을 초과한 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있는 경우 데이터베이스의 이름을 표시 합니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|DatabaseName|`nvarchar`|시간 초과가 발생한 데이터베이스의 이름입니다.|35|yes|  
|Duration|`bigint`|잠금 요청이 전달된 시간과 잠금 제한 시간이 초과된 시간 사이의 시간(밀리초)입니다.|13|yes|  
|EndTime|`datetime`|이벤트가 종료된 시간입니다.|15|yes|  
|EventClass|`int`|이벤트 유형 = 27|27|예|  
|EventSequence|`int`|요청 내의 지정된 이벤트 시퀀스입니다.|51|예|  
|GroupID|`int`|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|yes|  
|HostName|`nvarchar`|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|IntegerData2|`int`|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|yes|  
|IsSystem|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|yes|  
|LoginName|`nvarchar`|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|yes|  
|LoginSid|`image`|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|모드|`int`|제한 시간 초과 후의 결과 모드입니다.<br /><br /> 0=NULL - 모든 잠금 모드와 호환(LCK_M_NL)<br /><br /> 1=스키마 안정성 잠금(LCK_M_SCH_S)<br /><br /> 2=스키마 수정 잠금(LCK_M_SCH_M)<br /><br /> 3=공유 잠금(LCK_M_S)<br /><br /> 4=업데이트 잠금(LCK_M_U)<br /><br /> 5=배타 잠금(LCK_M_X)<br /><br /> 6=내재된 공유 잠금(LCK_M_IS)<br /><br /> 7=의도 업데이트 잠금(LCK_M_IU)<br /><br /> 8=의도 배타 잠금(LCK_M_IX)<br /><br /> 9=의도 업데이트 공유(LCK_M_SIU)<br /><br /> 10=의도 배타 공유(LCK_M_SIX)<br /><br /> 11=의도 배타 업데이트(LCK_M_UIX)<br /><br /> 12=대량 업데이트 잠금(LCK_M_BU)<br /><br /> 13=키 범위 공유/공유(LCK_M_RS_S)<br /><br /> 14=키 범위 공유/업데이트(LCK_M_RS_U)<br /><br /> 15=키 범위 삽입 NULL(LCK_M_RI_NL)<br /><br /> 16=키 범위 삽입 공유(LCK_M_RI_S)<br /><br /> 17=키 범위 삽입 업데이트(LCK_M_RI_U)<br /><br /> 18=키 범위 삽입 배타(LCK_M_RI_X)<br /><br /> 19=키 범위 배타 공유(LCK_M_RX_S)<br /><br /> 20=키 범위 배타 업데이트(LCK_M_RX_U)<br /><br /> 21=키 범위 배타 배타(LCK_M_RX_X)|32|yes|  
|NTDomainName|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|yes|  
|NTUserName|`nvarchar`|Windows 사용자 이름입니다.|6|yes|  
|ObjectID|`int`|제한 시간이 초과된 개체의 ID입니다(사용 및 적용 가능한 경우).|22|yes|  
|ObjectID2|`bigint`|관련 개체 또는 엔터티의 ID입니다(사용 및 적용 가능한 경우).|56|yes|  
|OwnerID|`int`|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|yes|  
|RequestID|`int`|문을 포함하는 요청의 ID입니다.|49|yes|  
|ServerName|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|`nvarchar`|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 사용자가 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행하는 경우 SessionLoginName은 Login1을, LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|yes|  
|SPID|`int`|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|StartTime|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|TextData|`ntext`|제한 시간이 초과될 때 획득한 잠금 유형에 따라 달라지는 텍스트 값입니다.|1|yes|  
|TransactionID|`bigint`|시스템이 할당한 트랜잭션의 ID입니다.|4|yes|  
|Type|`int`|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|yes|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Lock: Timeout &#40;timeout &#62; 0&#41; 이벤트 클래스](lock-timeout-timeout-0-event-class.md)   
 [sys.dm_tran_locks&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
  
