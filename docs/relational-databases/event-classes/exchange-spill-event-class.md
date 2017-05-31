---
title: "Exchange Spill 이벤트 클래스 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Exchange Spill event class
ms.assetid: fb876cec-f88d-4975-b3fd-0fb85dc0a7ff
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5920469e3f0ff312ac155011300034b8d8f8de50
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="exchange-spill-event-class"></a>Exchange Spill 이벤트 클래스
  **Exchange Spill** 이벤트 클래스는 병렬 쿼리 계획의 통신 버퍼가 **tempdb** 데이터베이스에 임시적으로 기록되었음을 나타냅니다. 이는 매우 드물게 발생하며 쿼리 계획에 다중 범위 검색이 있는 경우에만 발생합니다.  
  
 일반적으로 이러한 다중 범위 검색은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리에 BETWEEN 연산자가 많이 사용되었을 때 발생하며 각 BETWEEN 연산자는 테이블 또는 인덱스에서 행 범위를 선택합니다. 또는 (T.a > 10 AND T.a < 20) OR (T.a > 100 AND T.a < 120)과 같은 식을 사용하여 다중 범위를 가져올 수도 있습니다. 또한 T.a에 ORDER BY 절이 있거나 계획 내의 반복자가 정렬된 튜플을 소비해야 하는 경우 쿼리 계획에서 이러한 범위가 순서대로 검색되어야 합니다.  
  
 이러한 쿼리의 쿼리 계획에 여러 **Parallelism** 연산자가 있는 경우 **Parallelism** 연산자가 사용하는 메모리 통신 버퍼는 꽉 차게 되고 쿼리 실행 진행이 중지되는 상황이 발생할 수 있습니다. 이런 경우에는 **Parallelism** 연산자 중 하나가 자신의 출력 버퍼를 **tempdb** 에 기록하여(이 연산을 *exchange spill*이라고 함) 일부 입력 버퍼에서 행을 사용할 수 있습니다. 결국 소비자가 이러한 행을 사용할 준비가 되면 기록된 행이 소비자에게 반환됩니다.  
  
 드문 경우지만 여러 exchange spill이 동일한 실행 계획 내에서 발생하여 쿼리 실행이 느려질 수 있습니다. 동일한 쿼리 계획 실행 내에서 6개 이상의 spill을 발견하면 기술 지원 전문가에게 문의하십시오.  
  
 Exchange spill은 임시적인 경우가 있으며 데이터 분산이 변경되면 사라질 수 있습니다.  
  
 Exchange Spill 이벤트를 방지하는 방법은 다음과 같이 여러 가지가 있습니다.  
  
-   결과 집합을 정렬할 필요가 없는 경우 ORDER BY 절을 생략합니다.  
  
-   ORDER BY가 필요한 경우에는 ORDER BY 절에서 다중 범위 검색에 참여하는 열(위의 예에 언급된 T.a)을 제거합니다.  
  
-   인덱스 힌트를 사용하여 최적화 프로그램이 해당 테이블의 다른 액세스 경로를 사용하도록 합니다.  
  
-   쿼리를 다시 작성하여 다른 쿼리 실행 계획을 생성합니다.  
  
-   쿼리 또는 인덱스 작업 끝에 MAXDOP = 1을 추가하여 쿼리를 강제로 직렬 실행합니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 및 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  쿼리 최적화 프로그램이 실행 계획을 생성할 때 **Exchange Spill** 이벤트가 발생하는 위치를 확인하려면 추적에서 Showplan 이벤트 클래스도 수집해야 합니다. 노드 ID를 반환하지 않는 **Showplan Text** 및 **Showplan Text(Unencoded)** 이벤트 클래스를 제외한 모든 Showplan 이벤트 클래스를 선택할 수 있습니다. 실행 계획의 노드 ID는 쿼리 최적화 프로그램이 쿼리 실행 계획을 생성할 때 수행하는 각 연산을 식별합니다. 이러한 연산을 연산자라고 하며 실행 계획의 각 연산자에는 노드 ID가 있습니다. **Exchange Spill** 이벤트의 **ObjectID** 열은 실행 계획의 노드 ID에 해당하므로 오류가 발생하는 연산자 또는 연산을 확인할 수 있습니다.  
  
## <a name="exchange-spill-event-class-data-columns"></a>Exchange Spill 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|**ClientProcessID**|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|**EventClass**|**int**|이벤트 유형 = 127|27|아니요|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|**EventSubClass**|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 1=Spill 시작<br /><br /> 2=Spill 종료|21|예|  
|**GroupID**|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(*\<DOMAIN>\\<username\>* 형식의 Windows 로그인 자격 증명 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 로그인)입니다.|11|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **master** 데이터베이스의 **syslogins** 테이블에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|**Exchange Spill**|**int**|시스템이 할당한 개체의 ID입니다. 실행 계획의 노드 ID와 일치합니다.|22|예|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|**XactSequence**|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [인덱스 옵션 설정](../../relational-databases/indexes/set-index-options.md)   
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  

