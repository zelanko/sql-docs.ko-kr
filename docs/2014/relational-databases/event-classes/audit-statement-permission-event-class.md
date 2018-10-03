---
title: Audit Statement Permission 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Statement Permission event class
ms.assetid: 84ababe0-166e-4b1e-903b-bee6c1f005e7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ee4da71b8abc31faea0dfbeee0dd98f5a781b4e0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140620"
---
# <a name="audit-statement-permission-event-class"></a>Audit Statement Permission 이벤트 클래스
  **Audit Statement Permission** 이벤트 클래스는 문 사용 권한(예: CREATE TABLE)이 사용될 때마다 발생합니다.  
  
 **Audit Statement Permission** 이벤트 클래스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서 제거될 수 있습니다. 대신 **Audit Schema Object Management** 이벤트 클래스를 사용하는 것이 좋습니다.  
  
## <a name="audit-statement-permission-event-class-data-columns"></a>Audit Statement Permission 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|사용자 계정 컨트롤|  
|**ClientProcessID**|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|사용자 계정 컨트롤|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|사용자 계정 컨트롤|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|사용자 계정 컨트롤|  
|**DBUserName**|**nvarchar**|데이터베이스에 있는 발급자의 사용자 이름입니다.|40|사용자 계정 컨트롤|  
|**EventClass**|**int**|이벤트 유형 = 113|27|아니요|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|사용자 계정 컨트롤|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|사용자 계정 컨트롤|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|사용자 계정 컨트롤|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|사용자 계정 컨트롤|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|사용자 계정 컨트롤|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|사용자 계정 컨트롤|  
|**사용 권한**|**bigint**|확인한 사용 권한의 유형을 나타내는 정수 값입니다.<br /><br /> 1=CREATE DATABASE(master 데이터베이스 전용)<br /><br /> 2=CREATE TABLE<br /><br /> 4=CREATE PROCEDURE<br /><br /> 8=CREATE VIEW<br /><br /> 16=CREATE RULE<br /><br /> 32=CREATE DEFAULT<br /><br /> 64=BACKUP DATABASE<br /><br /> 128=BACKUP LOG<br /><br /> 256=BACKUP TABLE<br /><br /> 512=CREATE FUNCTION|19|사용자 계정 컨트롤|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|사용자 계정 컨트롤|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|사용자 계정 컨트롤|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|사용자 계정 컨트롤|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|사용자 계정 컨트롤|  
|**성공**|**int**|1 = 성공, 0 = 실패. 예를 들어 값 1은 사용 권한 확인이 성공했음을 나타내고, 값 0은 확인이 실패했음을 나타냅니다.|23|사용자 계정 컨트롤|  
|**TextData**|**ntext**|문 사용 권한이 필요한 문의 SQL 텍스트입니다.|1|사용자 계정 컨트롤|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|사용자 계정 컨트롤|  
|**XactSequence**|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|사용자 계정 컨트롤|  
  
## <a name="see-also"></a>관련 항목  
 [확장 이벤트](../extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Audit Schema Object Management 이벤트 클래스](audit-schema-object-management-event-class.md)  
  
  
