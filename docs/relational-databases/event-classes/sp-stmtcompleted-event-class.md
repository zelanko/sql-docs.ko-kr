---
description: SP:StmtCompleted 이벤트 클래스
title: SP:StmtCompleted 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SP:StmtCompleted event class
ms.assetid: 9e8147a4-aeeb-49a6-80f8-df753d0f34cc
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c24ab8d0656faaf69e09d42bf29febbc76a54f96
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494303"
---
# <a name="spstmtcompleted-event-class"></a>SP:StmtCompleted 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  SP:StmtCompleted 이벤트 클래스는 저장 프로시저 내의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 완료되었음을 나타냅니다.  
  
## <a name="spstmtcompleted-event-class-data-columns"></a>SP:StmtCompleted 이벤트 클래스 데이터 열  
  
|데이터 열 이름|**데이터 형식**|Description|열 ID|필터 가능|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|CPU|**int**|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|18|예|  
|DatabaseID|**int**|저장 프로시저가 실행되는 데이터베이스의 ID입니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|저장 프로시저가 실행되는 데이터베이스의 이름입니다.|35|예|  
|Duration|**bigint**|이벤트에 의해 사용된 시간(마이크로초)입니다.|13|예|  
|EndTime|**datetime**|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다.|15|예|  
|EventClass|**int**|이벤트 유형 = 45|27|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IntegerData|**int**|추적에서 캡처된 이벤트 클래스에 의존하는 정수 값입니다.|25|예|  
|IntegerData2|**int**|실행 중인 문의 종료 오프셋(바이트)입니다.|55|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LineNumber|**int**|실행 중인 문의 줄 번호입니다.|5|예|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NestLevel|**int**|@@NESTLEVEL에서 반환한 데이터를 나타내는 정수입니다.|29|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|ObjectID|**int**|시스템이 할당한 개체의 ID입니다.|22|예|  
|ObjectName|**nvarchar**|참조되는 개체의 이름입니다.|34|예|  
|ObjectType|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다. 이 값은 sys.objects 카탈로그 뷰의 유형 열과 일치합니다. 값은 [ObjectType 추적 이벤트 열](../../relational-databases/event-classes/objecttype-trace-event-column.md)을 참조하세요.|28|예|  
|Offset|**int**|저장 프로시저나 일괄 처리 내에 있는 문의 시작 오프셋입니다.|61|예|  
|읽기|**bigint**|이벤트 대신 서버에서 수행한 논리적 디스크 읽기 수입니다.|16|예|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|RowCounts|**bigint**|이벤트의 영향을 받은 행의 수입니다.|48|예|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SourceDatabaseID|**int**|개체가 있는 데이터베이스의 ID입니다.|62|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|추적에서 캡처된 이벤트 클래스에 따라 달라지는 텍스트 값입니다.|1|예|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|쓰기|**bigint**|이벤트 대신 서버에서 수행한 물리적 디스크 쓰기 수입니다.|17|예|  
|XactSequence|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
