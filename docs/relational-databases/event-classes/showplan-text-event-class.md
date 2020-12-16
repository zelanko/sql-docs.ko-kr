---
description: Showplan Text 이벤트 클래스
title: Showplan Text 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Showplan Text event class
ms.assetid: f36c73b2-a1d1-4513-9594-78818f3fcb0d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 865ed1dd3fd8f11a2ccf505f6e7e19f230c256a1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467794"
---
# <a name="showplan-text-event-class"></a>Showplan Text 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  Showplan Text 이벤트 클래스는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 SQL 문을 실행할 때 발생합니다. Showplan All, Showplan XML Statistics Profile 또는 Showplan XML 이벤트 클래스에서 사용할 수 있는 정보의 일부만 포함하고 있습니다.  
  
 추적에 Showplan Text 이벤트 클래스가 포함되면 오버헤드로 인해 성능이 크게 저하될 수 있습니다. 이 문제를 최소화하려면 단기간 동안 특정 문제를 모니터링하는 추적에서만 이 이벤트 클래스를 사용하십시오. Showplan Text는 다른 Showplan 이벤트 클래스만큼 많은 오버헤드를 발생시키지는 않습니다.  
  
 추적에 Showplan Text 이벤트 클래스가 포함되면 BinaryData 데이터 열을 선택해야 합니다. 그렇지 않을 경우 이 이벤트 클래스에 대한 정보가 추적에 표시되지 않습니다.  
  
## <a name="showplan-text-event-class-data-columns"></a>Showplan Text 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|BinaryData|**image**|Showplan 텍스트의 예상 비용입니다.|2|아니요|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|Event Class|**int**|이벤트 유형 = 96|27|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|Integer Data|**integer**|반환한 행의 예상 개수입니다.|25|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LineNumber|**int**|오류를 포함하는 줄 번호를 표시합니다.|5|예|  
|Login SID|**bitmap**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|아니요|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|NestLevel|**int**|@@NESTLEVEL에서 반환한 데이터를 나타내는 정수입니다.|29|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|ObjectID|**int**|시스템이 할당한 개체의 ID입니다.|22|예|  
|ObjectName|**nvarchar**|참조되는 개체의 이름입니다.|34|예|  
|ObjectType|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다. 이 값은 sys.objects의 유형 열과 일치합니다. 값은 [ObjectType 추적 이벤트 열](../../relational-databases/event-classes/objecttype-trace-event-column.md)을 참조하세요.|28|예|  
|RequestID|**int**|전체 텍스트 쿼리를 시작한 요청 ID입니다.|49|예|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|XactSequence|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [Showplan All 이벤트 클래스](../../relational-databases/event-classes/showplan-all-event-class.md)   
 [Showplan XML Statistics Profile 이벤트 클래스](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)   
 [Showplan XML 이벤트 클래스](../../relational-databases/event-classes/showplan-xml-event-class.md)  
  
  
