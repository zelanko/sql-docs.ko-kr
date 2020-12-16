---
title: RPC:Completed 이벤트 클래스 | Microsoft 문서
description: RPC:Completed 이벤트 클래스는 SQL Server에서 원격 프로시저 호출이 완료되었음을 나타냅니다.
ms.custom: ''
ms.date: 12/04/2015
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- RPC:Completed event class
ms.assetid: 0d526201-94c9-4e4c-afb1-4213df1815ba
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d1bca4deb6ef8396abff5ded129b5d23438a9ed2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483685"
---
# <a name="rpccompleted-event-class"></a>RPC:Completed 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  RPC:Completed 이벤트 클래스는 원격 프로시저 호출이 완료되었음을 나타냅니다.  
  
## <a name="rpccompleted-event-class-data-columns"></a>RPC:Completed 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|BinaryData|**image**|추적에서 캡처된 이벤트 클래스에 의존하는 이진 값입니다.|2|예|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|CPU|**int**|이벤트에서 사용한 CPU 시간입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 마이크로초 단위입니다. 이전 버전에서는 밀리초 단위입니다.|18|예|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|Duration|**bigint**|이벤트에서 사용한 시간입니다. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]부터 마이크로초 단위입니다. 이전 버전에서는 밀리초 단위입니다.|13|예|  
|EndTime|**datetime**|원격 프로시저 호출이 종료된 시간입니다.|15|예|  
|Error|**int**|지정된 이벤트의 오류 번호입니다.<br /><br /> 0=확인<br /><br /> 1=오류<br /><br /> 2=중단<br /><br /> 3=건너뜀|31|예|  
|EventClass|**int**|이벤트 유형 = 10|27|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|ObjectName|**nvarchar**|참조되는 개체의 이름입니다.|34|예|  
|읽기|**bigint**|원격 프로시저 호출로 실행된 페이지 읽기 수입니다.|16|예|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|RowCounts|**bigint**|RPC 일괄 처리의 행 수입니다.|48|예|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26||  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|원격 프로시저 호출의 텍스트입니다.|1|예|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|쓰기|**bigint**|원격 프로시저 호출로 실행된 페이지 쓰기 수입니다.|17|예|  
|XactSequence|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
