---
title: Lock:Acquired 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Acquired event class
ms.assetid: a6b1df2a-06ed-4fc3-8a84-f0becd5810d5
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 682e34a8ca9a265310cfb3d3fc99ce2064e800eb
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39563477"
---
# <a name="lockacquired-event-class"></a>Lock:Acquired 이벤트 클래스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Lock:Acquiredevent 클래스는 데이터 페이지와 같은 리소스에 대한 잠금 획득이 이루어졌음을 나타냅니다.  
  
 Lock:Acquired 및 Lock:Released 이벤트 클래스를 사용하여 개체 잠금 시기, 사용하는 잠금 유형 및 잠금 보유 기간을 모니터링할 수 있습니다. 장기간 보유되는 잠금은 경합 문제를 발생시킬 수 있으므로 면밀히 관찰해야 합니다. 예를 들어 응용 프로그램에서 테이블의 행에 대한 잠금을 획득하고 사용자 입력을 기다릴 수 있습니다. 사용자 입력 대기 시간이 길어지는 경우 이러한 잠금으로 인해 다른 사용자가 차단될 수 있습니다. 이런 경우 필요할 경우에만 잠금 요청을 하고 잠금이 획득된 경우 사용자 입력이 필요하지 않도록 응용 프로그램을 다시 디자인해야 합니다.  
  
## <a name="lockacquired-event-class-data-columns"></a>Lock:Acquired 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|사용자 계정 컨트롤|  
|BigintData1|**bigint**|잠금 리소스가 분할된 경우 파티션 ID입니다.|52|사용자 계정 컨트롤|  
|BinaryData|**image**|잠금 리소스 식별자입니다.|2|사용자 계정 컨트롤|  
|ClientProcessID|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|사용자 계정 컨트롤|  
|DatabaseID|**int**|잠금을 획득한 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|사용자 계정 컨트롤|  
|Duration|**bigint**|잠금 요청을 실행한 시간과 잠금을 획득한 시간 사이의 경과 시간(밀리초)입니다.|13|사용자 계정 컨트롤|  
|EndTime|**datetime**|이벤트가 종료된 시간입니다.|15|사용자 계정 컨트롤|  
|EventClass|**int**|이벤트 유형 = 24|27|아니오|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|사용자 계정 컨트롤|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|사용자 계정 컨트롤|  
|IntegerData2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|사용자 계정 컨트롤|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|사용자 계정 컨트롤|  
|LoginName|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 Windows 로그인 자격 증명 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 로그인)입니다.|11|사용자 계정 컨트롤|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|사용자 계정 컨트롤|  
|모드|**int**|잠금을 획득한 후의 결과 모드입니다.<br /><br /> 0=NULL - 모든 잠금 모드와 호환(LCK_M_NL)<br /><br /> 1=스키마 안정성 잠금(LCK_M_SCH_S)<br /><br /> 2=스키마 수정 잠금(LCK_M_SCH_M)<br /><br /> 3=공유 잠금(LCK_M_S)<br /><br /> 4=업데이트 잠금(LCK_M_U)<br /><br /> 5=배타 잠금(LCK_M_X)<br /><br /> 6=내재된 공유 잠금(LCK_M_IS)<br /><br /> 7=의도 업데이트 잠금(LCK_M_IU)<br /><br /> 8=의도 배타 잠금(LCK_M_IX)<br /><br /> 9=의도 업데이트 공유(LCK_M_SIU)<br /><br /> 10=의도 배타 공유(LCK_M_SIX)<br /><br /> 11=의도 배타 업데이트(LCK_M_UIX)<br /><br /> 12=대량 업데이트 잠금(LCK_M_BU)<br /><br /> 13=키 범위 공유/공유(LCK_M_RS_S)<br /><br /> 14=키 범위 공유/업데이트(LCK_M_RS_U)<br /><br /> 15=키 범위 삽입 NULL(LCK_M_RI_NL)<br /><br /> 16=키 범위 삽입 공유(LCK_M_RI_S)<br /><br /> 17=키 범위 삽입 업데이트(LCK_M_RI_U)<br /><br /> 18=키 범위 삽입 배타(LCK_M_RI_X)<br /><br /> 19=키 범위 배타 공유(LCK_M_RX_S)<br /><br /> 20=키 범위 배타 업데이트(LCK_M_RX_U)<br /><br /> 21=키 범위 배타 배타(LCK_M_RX_X)|32|사용자 계정 컨트롤|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|사용자 계정 컨트롤|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|사용자 계정 컨트롤|  
|ObjectID|**int**|잠금을 획득한 개체의 ID입니다(사용 및 적용 가능한 경우).|22|사용자 계정 컨트롤|  
|ObjectID2|**bigint**|관련 개체 또는 엔터티의 ID입니다(사용 및 적용 가능한 경우).|56|사용자 계정 컨트롤|  
|OwnerID|**int**|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|사용자 계정 컨트롤|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|사용자 계정 컨트롤|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니오|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|사용자 계정 컨트롤|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|사용자 계정 컨트롤|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|사용자 계정 컨트롤|  
|TextData|**ntext**|획득한 잠금 유형에 따라 달라지는 텍스트 값입니다. 이 값은 sys.dm_tran_locks의 resource_description 열과 같습니다.|@shouldalert|사용자 계정 컨트롤|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|사용자 계정 컨트롤|  
|형식|**int**|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|사용자 계정 컨트롤|  
  
## <a name="see-also"></a>참고 항목  
 [Lock:Released 이벤트 클래스](../../relational-databases/event-classes/lock-released-event-class.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.dm_tran_locks&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  
