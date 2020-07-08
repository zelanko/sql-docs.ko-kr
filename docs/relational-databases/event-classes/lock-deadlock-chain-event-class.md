---
title: Lock:Deadlock Chain 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Deadlock Chain event class
ms.assetid: 9883127b-aa34-4235-88cc-c161cd2112cc
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6057c32842121f6d27649fe3f2b8e201d6c9695a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717928"
---
# <a name="lockdeadlock-chain-event-class"></a>Lock:Deadlock Chain 이벤트 클래스
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Lock:Deadlock Chain 이벤트 클래스는 교착 상태의 각 참가자에 대해 생성됩니다.  
  
 Lock:Deadlock Chain 이벤트 클래스를 사용하여 교착 상태 조건이 발생하는 시점을 모니터링할 수 있습니다. 이 정보는 교착 상태가 애플리케이션의 성능에 큰 영향을 미치는지 여부와 어떤 개체가 관련되어 있는지 확인하는 데 유용합니다. 이러한 개체를 수정하는 애플리케이션 코드를 검사하여 교착 상태를 최소화하도록 변경될 수 있는지 확인할 수 있습니다.  
  
## <a name="lockdeadlock-chain-event-class-data-columns"></a>Lock:Deadlock Chain 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BinaryData|**image**|잠금 리소스 식별자입니다.|2|yes|  
|DatabaseID|**int**|이 리소스가 속한 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|DatabaseName|**nvarchar**|리소스가 속한 데이터베이스의 이름입니다.|35|yes|  
|EventClass|**int**|이벤트 유형 = 59|27|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 101=리소스 유형 잠금<br /><br /> 102=리소스 유형 교환|21|yes|  
|IntegerData|**int**|교착 상태 번호입니다. 번호는 서버가 시작될 때 0부터 시작하도록 할당되고 교착 상태가 발생할 때마다 증가됩니다.|25|yes|  
|IntegerData2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|yes|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|yes|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|Mode|**int**|0=NULL - 모든 잠금 모드와 호환(LCK_M_NL)<br /><br /> 1=스키마 안정성 잠금(LCK_M_SCH_S)<br /><br /> 2=스키마 수정 잠금(LCK_M_SCH_M)<br /><br /> 3=공유 잠금(LCK_M_S)<br /><br /> 4=업데이트 잠금(LCK_M_U)<br /><br /> 5=배타 잠금(LCK_M_X)<br /><br /> 6=내재된 공유 잠금(LCK_M_IS)<br /><br /> 7=의도 업데이트 잠금(LCK_M_IU)<br /><br /> 8=의도 배타 잠금(LCK_M_IX)<br /><br /> 9=의도 업데이트 공유(LCK_M_SIU)<br /><br /> 10=의도 배타 공유(LCK_M_SIX)<br /><br /> 11=의도 배타 업데이트(LCK_M_UIX)<br /><br /> 12=대량 업데이트 잠금(LCK_M_BU)<br /><br /> 13=키 범위 공유/공유(LCK_M_RS_S)<br /><br /> 14=키 범위 공유/업데이트(LCK_M_RS_U)<br /><br /> 15=키 범위 삽입 NULL(LCK_M_RI_NL)<br /><br /> 16=키 범위 삽입 공유(LCK_M_RI_S)<br /><br /> 17=키 범위 삽입 업데이트(LCK_M_RI_U)<br /><br /> 18=키 범위 삽입 배타(LCK_M_RI_X)<br /><br /> 19=키 범위 배타 공유(LCK_M_RX_S)<br /><br /> 20=키 범위 배타 업데이트(LCK_M_RX_U)<br /><br /> 21=키 범위 배타 배타(LCK_M_RX_X)|32|yes|  
|ObjectID|**int**|잠긴 개체의 ID입니다(사용 및 적용 가능한 경우).|22|yes|  
|ObjectID2|**bigint**|관련 개체 또는 엔터티의 ID입니다(사용 및 적용 가능한 경우).|56|yes|  
|OwnerID|**int**|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|yes|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|yes|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 로그인이 모두 표시됩니다.|64|yes|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|TextData|**ntext**|리소스 유형에 따라 달라지는 텍스트 값입니다.|1|yes|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|yes|  
|Type|**int**|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|yes|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.dm_tran_locks&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  
