---
description: Execution Warnings 이벤트 클래스
title: Execution Warnings 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Execution Warnings event class
ms.assetid: 2c69e321-dc9a-4483-886d-81350adae2be
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d818d563d50643dcecc1fceb445fa37c8b0a82b2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469654"
---
# <a name="execution-warnings-event-class"></a>Execution Warnings 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  Execution Warnings 이벤트 클래스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문이나 저장 프로시저를 실행하는 동안 발생한 메모리 부여 경고를 나타냅니다. 이 이벤트 클래스를 모니터링하여 계속하기 전에 쿼리가 1초 이상 메모리를 기다려야 하는지 또는 메모리를 가져오려는 초기 시도가 실패했는지 여부를 확인할 수 있습니다. 쿼리 대기 기간에 대한 정보를 통해 성능에 영향을 미칠 수 있는 시스템이 경합 문제를 확인할 수 있습니다.  
  
## <a name="execution-warnings-event-class-data-columns"></a>Execution Warnings 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|Duration|**bigint**|쿼리가 필요한 메모리를 가져오기 위해 기다려야 했던 밀리초 단위의 시간입니다. EventSubClass = 1(쿼리 대기)일 경우에만 유효합니다.|13|예|  
|Error|**int**|사용되지 않습니다.|31|예|  
|EventClass|**int**|이벤트 유형 = 67|27|예|  
|EventSequence|**int**|추적 내의 지정된 이벤트 시퀀스입니다.|51|예|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 1=쿼리 대기<br /><br /> 2=쿼리 제한 시간|21|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, NULL = 사용자|60|예|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|XactSequence|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
