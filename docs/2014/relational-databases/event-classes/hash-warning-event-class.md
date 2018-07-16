---
title: Hash Warning 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Hash Warning event class
ms.assetid: cb93c620-4be9-4362-8bf0-af3f2048bdaf
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b5ab99db22c29f6069f7b218b2a2c8d498da537
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209073"
---
# <a name="hash-warning-event-class"></a>Hash Warning 이벤트 클래스
  Hash Warning 이벤트 클래스는 해시 연산 중 해시 재귀 또는 해시 중단(해시 재귀 한도 초과) 발생을 모니터링하는데 사용할 수 있습니다.  
  
 해시 재귀는 빌드 입력이 사용할 수 있는 메모리를 초과하여 여러 개의 파티션으로 분할되어 개별적으로 처리되는 경우 발생합니다. 분할된 파티션 중 여전히 사용할 수 있는 메모리를 초과하는 파티션이 있으면 이는 다시 하위 파티션으로 분할되어 개별적으로 처리됩니다. 이러한 분할 프로세스는 각 파티션이 사용할 수 있는 메모리에 모두 맞거나 최대 재귀 수준에 도달할 때까지 계속됩니다(IntegerData 데이터 열에 표시됨).  
  
 해시 연산이 최대 재귀 수준에 도달하면 해시 재귀 한도 초과가 발생하며 대체 계획으로 변경하여 남은 파티션 데이터를 처리합니다. 해시 재귀 한도 초과는 보통 일치하지 않는 데이터로 인해 발생합니다.  
  
 해시 재귀 및 해시 재귀 한도 초과는 서버 성능을 저하시킵니다. 해시 재귀 및 해시 재귀 한도 초과를 제거하거나 빈도를 낮추려면 다음 중 하나를 실행하십시오.  
  
-   조인 또는 그룹화된 열에 통계가 있는지 확인합니다.  
  
-   열에 통계가 있으면 업데이트합니다.  
  
-   다른 형식의 조인을 사용합니다. 예를 들어 MERGE 또는 LOOP 조인을 대신 사용합니다(가능한 경우).  
  
-   컴퓨터에서 사용할 수 있는 메모리를 늘립니다. 해시 재귀 또는 해시 재귀 한도 초과는 쿼리를 적시에 처리할 메모리가 부족하여 디스크에 써야하는 경우 발생합니다.  
  
 해시 재귀 또는 해시 재귀 한도 초과가 발생하는 수를 줄이는 가장 효과적인 방법은 조인과 관련된 열의 통계를 만들거나 업데이트하는 것입니다.  
  
> [!NOTE]  
>  *유예 해시 조인* 및 *재귀 해시 조인* 도 해시 재귀 한도 초과와 관련이 있는 용어입니다.  
  
> [!IMPORTANT]  
>  쿼리 최적화 프로그램이 실행 계획을 생성할 때 Hash Warning 이벤트가 발생하는 위치를 확인하려면 추적에서 Showplan 이벤트 클래스도 수집해야 합니다. 노드 ID를 반환하지 않는 Showplan Text 및 Showplan Text (Unencoded) 이벤트 클래스를 제외한 모든 Showplan 이벤트 클래스를 선택할 수 있습니다. 실행 계획의 노드 ID는 쿼리 최적화 프로그램이 쿼리 실행 계획을 생성할 때 수행하는 각 연산을 식별합니다. 이러한 연산을 *연산자*라고 하며 실행 계획의 각 연산자에는 노드 ID가 있습니다. Hash Warning 이벤트의 ObjectID 열은 실행 계획의 노드 ID에 해당하므로 오류가 발생하는 연산자, 즉 연산을 확인할 수 있습니다.  
  
## <a name="hash-warning-event-class-data-columns"></a>Hash Warning 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|`int`|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|`int`|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|`nvarchar`|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|EventClass|`int`|이벤트 유형 = 55|27|아니요|  
|EventSequence|`int`|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|EventSubClass|`int`|이벤트 하위 클래스의 유형입니다.<br /><br /> 0=재귀<br /><br /> 1=한도 초과|21|예|  
|GroupID|`int`|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|`nvarchar`|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IntegerData|`int`|재귀 수준입니다(해시 재귀만 해당).|25|예|  
|IsSystem|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LoginName|`nvarchar`|사용자 로그인 이름(*\<DOMAIN>\\<username\>* 형식의 Windows 로그인 자격 증명 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 로그인)입니다.|11|예|  
|LoginSid|`image`|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|`nvarchar`|Windows 사용자 이름입니다.|6|예|  
|ObjectID|`int`|재분할에 관련된 해시 팀의 루트 노드 ID입니다. 실행 계획의 노드 ID와 일치합니다.|22|예|  
|RequestID|`int`|문을 포함하는 요청의 ID입니다.|49|예|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26||  
|SessionLoginName|`nvarchar`|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|`int`|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TransactionID|`bigint`|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|XactSequence|`bigint`|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>관련 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
