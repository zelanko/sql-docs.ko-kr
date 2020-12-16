---
description: SP:Recompile 이벤트 클래스
title: SP:Recompile 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SP:Recompile event class
ms.assetid: 526c8eae-a07b-4d0e-b91e-8e537835d77d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 43da69ae4f6404f0f5fca4b847acc32f95b6ff1b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467784"
---
# <a name="sprecompile-event-class"></a>SP:Recompile 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  SP:Recompile 이벤트 클래스는 저장 프로시저, 트리거 또는 사용자 정의 함수를 다시 컴파일했음을 나타냅니다. 이 이벤트 클래스가 보고하는 다시 컴파일은 문 수준에서 발생합니다.  
  
 SQL:StmtRecompile 이벤트 클래스를 사용하여 문 수준의 다시 컴파일을 추적하는 것이 좋습니다. SP:Recompile 이벤트 클래스는 더 이상 사용되지 않습니다. 자세한 내용은 [SQL:StmtRecompile Event Class](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md)을(를) 참조하세요.  
  
## <a name="sprecompile-event-class-data-columns"></a>SP:Recompile 이벤트 클래스 데이터 열  
  
|데이터 열 이름|**데이터 형식**|Description|열 ID|필터 가능|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**int**|저장 프로시저가 실행되는 데이터베이스의 ID입니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|저장 프로시저가 실행되는 데이터베이스의 이름입니다.|35|예|  
|EventClass|**int**|이벤트 유형 = 37|27|예|  
|EventSequence|**int**|요청 내의 지정된 이벤트 시퀀스입니다.|51|예|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다. 다시 컴파일하는 이유를 설명합니다.<br /><br /> 1 = 스키마 변경<br /><br /> 2 = 통계 변경<br /><br /> 3 = DNR 다시 컴파일<br /><br /> 4 = SET 옵션 변경<br /><br /> 5 = 임시 테이블 변경<br /><br /> 6 = 원격 행 집합 변경<br /><br /> 7 = 찾아보기 권한 변경<br /><br /> 8 = 쿼리 알림 환경 변경<br /><br /> 9 = MPI 뷰 변경<br /><br /> 10 = 커서 옵션 변경<br /><br /> 11 = 다시 컴파일 옵션 사용|21|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IntegerData2|**int**|다시 컴파일이 발생한 저장 프로시저 또는 일괄 처리 내에 있는 문의 끝 오프셋입니다. 문이 일괄 처리의 마지막 문인 경우 끝 오프셋은 -1입니다.|55|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NestLevel|**int**|저장 프로시저의 중첩 수준입니다.|29|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|ObjectID|**int**|시스템이 할당한 저장 프로시저의 ID입니다.|22|예|  
|ObjectName|**nvarchar**|다시 컴파일을 트리거한 개체의 이름입니다.|34|예|  
|ObjectType|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다. 자세한 내용은 [ObjectType Trace Event Column](../../relational-databases/event-classes/objecttype-trace-event-column.md)을(를) 참조하세요.|28|예|  
|Offset|**int**|다시 컴파일이 발생한 저장 프로시저 또는 일괄 처리 내에 있는 문의 시작 오프셋입니다.|61|예|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|SqlHandle|**varbinary**|임시 쿼리 또는 데이터베이스의 텍스트 및 SQL 개체의 개체 ID를 기반으로 하는 64비트 해시입니다. 이 값을 sys.dm_exec_sql_text에 전달하여 연결된 SQL 텍스트를 검색할 수 있습니다.|63|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|명령 수준의 다시 컴파일을 발생시킨 Transact-SQL 문의 텍스트입니다.|1|예|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|XactSequence|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL:StmtRecompile 이벤트 클래스](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md)  
  
  
