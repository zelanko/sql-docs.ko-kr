---
title: SQL:StmtRecompile 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL:StmtRecompile event class
ms.assetid: 3a134751-3e93-4fe8-bf22-1e0561189293
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc05dfcfe9f332ca95f2836a2cf5400eed223776
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43081096"
---
# <a name="sqlstmtrecompile-event-class"></a>SQL:StmtRecompile 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQL:StmtRecompile 이벤트 클래스는 모든 유형의 일괄 처리로 인해 발생한 문 수준의 다시 컴파일을 나타냅니다. 여기에는 저장 프로시저, 트리거, 임시 일괄 처리 및 쿼리가 있습니다. sp_executesql, 동적 SQL, Prepare 메서드, Execute 메서드 또는 비슷한 인터페이스를 사용하여 쿼리를 제출할 수 있습니다. SP:Recompile 이벤트 클래스 대신 SQL:StmtRecompile 이벤트 클래스를 사용해야 합니다.  
  
## <a name="sqlstmtrecompile-event-class-data-columns"></a>SQL:StmtRecompile 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|사용자 계정 컨트롤|  
|ClientProcessID|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|사용자 계정 컨트롤|  
|DatabaseID|**int**|저장 프로시저가 실행되는 데이터베이스의 ID입니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|사용자 계정 컨트롤|  
|DatabaseName|**nvarchar**|저장 프로시저가 실행되는 데이터베이스의 이름입니다.|35|사용자 계정 컨트롤|  
|EventSequence|**int**|요청 내의 이벤트 시퀀스입니다.|51|아니오|  
|EventSubClass|**int**|다시 컴파일하는 원인을 설명합니다.<br /><br /> 1 = 스키마 변경<br /><br /> 2 = 통계 변경<br /><br /> 3 = 지연된 컴파일<br /><br /> 4 = SET 옵션 변경<br /><br /> 5 = 임시 테이블 변경<br /><br /> 6 = 원격 행 집합 변경<br /><br /> 7 = 찾아보기 권한 변경<br /><br /> 8 = 쿼리 알림 환경 변경<br /><br /> 9 = 분할 뷰 변경<br /><br /> 10 = 커서 옵션 변경<br /><br /> 11 = 옵션(recompile) 요청|21|사용자 계정 컨트롤|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|사용자 계정 컨트롤|  
|HostName|**nvarchar**|클라이언트에서 실행 중이며 해당 문을 제출한 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|사용자 계정 컨트롤|  
|IntegerData2|**int**|다시 컴파일이 발생한 저장 프로시저 또는 일괄 처리 내에 있는 문의 끝 오프셋입니다. 문이 일괄 처리의 마지막 문인 경우 끝 오프셋은 -1입니다.|55|사용자 계정 컨트롤|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> 1 = 시스템<br /><br /> 0 = 사용자|60|사용자 계정 컨트롤|  
|LineNumber|**int**|일괄 처리에서 해당 문의 시퀀스 번호입니다(해당될 경우).|5|사용자 계정 컨트롤|  
|LoginName|**nvarchar**|이 일괄 처리를 제출한 로그인 이름입니다.|11|사용자 계정 컨트롤|  
|LoginSid|**image**|현재 로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|사용자 계정 컨트롤|  
|NestLevel|**int**|저장 프로시저 호출의 중첩 수준입니다. 예를 들어 my_proc_a 저장 프로시저가 my_proc_b를 호출합니다. 이 경우 my_proc_a의 NestLevel은 1이고 my_proc_b의 NestLevel은 2입니다.|29|사용자 계정 컨트롤|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|사용자 계정 컨트롤|  
|NTUserName|**nvarchar**|연결된 사용자의 Windows 사용자 이름입니다.|6|사용자 계정 컨트롤|  
|ObjectID|**int**|다시 컴파일하도록 만든 문이 포함된 개체에 대해 시스템이 할당한 개체 ID입니다. 이 개체는 저장 프로시저, 트리거 또는 사용자 정의 함수일 수 있습니다. 임시 일괄 처리나 준비된 SQL의 경우 ObjectID 및 ObjectName에서 NULL 값이 반환됩니다.|22|사용자 계정 컨트롤|  
|ObjectName|**nvarchar**|ObjectID로 식별된 개체의 이름입니다.|34|사용자 계정 컨트롤|  
|ObjectType|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다. 자세한 내용은 [ObjectType Trace Event Column](../../relational-databases/event-classes/objecttype-trace-event-column.md)을(를) 참조하세요.|28|사용자 계정 컨트롤|  
|Offset|**int**|다시 컴파일이 발생한 저장 프로시저 또는 일괄 처리 내에 있는 문의 시작 오프셋입니다.|61|사용자 계정 컨트롤|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|사용자 계정 컨트롤|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|**nvarchar**|추적할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이름입니다.|26|아니오|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|사용자 계정 컨트롤|  
|SPID|**int**|연결의 서버 프로세스 ID입니다.|12|사용자 계정 컨트롤|  
|SqlHandle|**varbinary**|임시 쿼리 또는 데이터베이스의 텍스트 및 SQL 개체의 개체 ID를 기반으로 하는 64비트 해시입니다. 이 값을 sys.dm_exec_sql_text에 전달하여 연결된 SQL 텍스트를 검색할 수 있습니다.|63|아니오|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|사용자 계정 컨트롤|  
|TextData|**ntext**|다시 컴파일한 Transact-SQL 문의 텍스트입니다.|@shouldalert|사용자 계정 컨트롤|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|사용자 계정 컨트롤|  
|XactSequence|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|사용자 계정 컨트롤|  
  
## <a name="see-also"></a>참고 항목  
 [SP:Recompile 이벤트 클래스](../../relational-databases/event-classes/sp-recompile-event-class.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
