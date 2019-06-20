---
title: Lock:Timeout(timeout &gt; 0) 이벤트 클래스 | Microsoft 문서
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
ms.assetid: d755833a-d7eb-4973-9352-67a2fba2442a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 312cda4fd588336d8be42c82a20392c8d0b80664
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023497"
---
# <a name="locktimeout-timeout-gt-0-event-class"></a>Lock:Timeout(timeout &gt; 0) 이벤트 클래스
  **Lock:Timeout(timeout > 0)** 이벤트 클래스는 페이지 등의 특정 리소스에 대해 다른 트랜잭션이 차단 잠금을 보유 중이기 때문에 해당 리소스에 대한 잠금 요청 시간이 초과되었음을 나타냅니다. 이 이벤트 클래스는 제한 시간 값이 0인 이벤트를 포함하지 않는다는 점만 제외하면 **Lock:Timeout** 이벤트 클래스와 동일하게 동작합니다.  
  
 제한 시간 값이 0인 잠금 검색 및 다른 프로세스를 사용하는 추적에 **Lock:Timeout(timeout > 0)** 이벤트 클래스를 포함하세요. 이렇게 하면 제한 시간 값이 0인 경우를 제외하고 실제 시간 초과가 발생한 부분을 확인할 수 있습니다.  
  
## <a name="locktimeout-timeout--0-event-class-data-columns"></a>Lock:Timeout (timeout > 0) 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|사용자 계정 컨트롤|  
|BinaryData|`image`|잠금 리소스 식별자입니다.|2|사용자 계정 컨트롤|  
|ClientProcessID|`int`|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|사용자 계정 컨트롤|  
|DatabaseID|`int`|시간 초과가 발생한 데이터베이스의 ID입니다. `ServerName` 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|사용자 계정 컨트롤|  
|DatabaseName|`nvarchar`|시간 초과가 발생한 데이터베이스의 이름입니다.|35|사용자 계정 컨트롤|  
|Duration|`bigint`|이벤트에 의해 사용된 시간(마이크로초)입니다.|13|사용자 계정 컨트롤|  
|EndTime|`datetime`|이벤트가 종료된 시간입니다. 이 열은 **SQL:BatchStarting** 또는 **SP:Starting**과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다.|15|사용자 계정 컨트롤|  
|EventClass|`int`|이벤트 유형 = 189|27|아니요|  
|EventSequence|`int`|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|GroupID|`int`|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|사용자 계정 컨트롤|  
|HostName|`nvarchar`|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|사용자 계정 컨트롤|  
|IntegerData2|`int`|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|사용자 계정 컨트롤|  
|IsSystem|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|사용자 계정 컨트롤|  
|LoginName|`nvarchar`|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|사용자 계정 컨트롤|  
|LoginSid|`image`|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|사용자 계정 컨트롤|  
|모드|`int`|이벤트가 받거나 요청한 상태입니다.<br /><br /> 0=NULL<br /><br /> 1=Sch-S<br /><br /> 2=Sch-M<br /><br /> 3=S<br /><br /> 4=U<br /><br /> 5=X<br /><br /> 6=IS<br /><br /> 7=IU<br /><br /> 8=IX<br /><br /> 9=SIU<br /><br /> 10=SIX<br /><br /> 11=UIX<br /><br /> 12=BU<br /><br /> 13=RangeS-S<br /><br /> 14=RangeS-U<br /><br /> 15=RangeI-N<br /><br /> 16=RangeI-S<br /><br /> 17=RangeI-U<br /><br /> 18=RangeI-X<br /><br /> 19=RangeX-S<br /><br /> 20=RangeX-U<br /><br /> 21=RangeX-X|32|사용자 계정 컨트롤|  
|NTDomainName|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|사용자 계정 컨트롤|  
|NTUserName|`nvarchar`|Windows 사용자 이름입니다.|6|사용자 계정 컨트롤|  
|ObjectID|`int`|개체의 ID입니다(사용 및 적용 가능한 경우).|22|사용자 계정 컨트롤|  
|ObjectID2|`bigint`|관련 개체 또는 엔터티의 ID입니다(사용 및 적용 가능한 경우).|56|사용자 계정 컨트롤|  
|OwnerID|`int`|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|사용자 계정 컨트롤|  
|RequestID|`int`|문을 포함하는 요청의 ID입니다.|49|사용자 계정 컨트롤|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|SessionLoginName|`nvarchar`|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하고 Login2로 문을 실행할 경우 `SessionLoginName`은 Login1을 표시하고 `LoginName`은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|사용자 계정 컨트롤|  
|SPID|`int`|이벤트가 발생한 세션의 ID입니다.|12|사용자 계정 컨트롤|  
|StartTime|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|사용자 계정 컨트롤|  
|TextData|`ntext`|추적에서 캡처된 이벤트 클래스에 따라 달라지는 텍스트 값입니다.|1|사용자 계정 컨트롤|  
|TransactionID|`bigint`|시스템이 할당한 트랜잭션의 ID입니다.|4|사용자 계정 컨트롤|  
|형식|`int`|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|사용자 계정 컨트롤|  
  
## <a name="see-also"></a>관련 항목  
 [Lock:Timeout 이벤트 클래스](lock-timeout-event-class.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sys.dm_tran_locks&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
  
