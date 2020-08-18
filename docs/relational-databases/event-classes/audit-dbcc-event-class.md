---
description: Audit DBCC 이벤트 클래스
title: Audit DBCC 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Audit DBCC event class
ms.assetid: 73724190-d6b7-4f11-9446-78bcafa6c693
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 27ff72cfdf599e0e67000db2a73956d6fffb0dd2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88330839"
---
# <a name="audit-dbcc-event-class"></a>Audit DBCC 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  **Audit DBCC** 이벤트 클래스는 DBCC 명령이 실행될 때마다 발생합니다.  
  
## <a name="audit-dbcc-event-class-data-columns"></a>Audit DBCC 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**ColumnPermissions**|**int**|열 사용 권한이 설정되어 있는지 나타냅니다. 문 텍스트를 구문 분석하여 어떤 권한이 어떤 열에 적용되었는지 정확히 알 수 있습니다.|44|예|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|**DBUserName**|**nvarchar**|데이터베이스에 있는 발급자의 사용자 이름입니다.|40|예|  
||||||  
|**EventClass**|**int**|이벤트 유형 = 116|27|예|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LineNumber**|**int**|오류를 포함하는 줄 번호를 표시합니다.|5|예|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NestLevel**|**int**|@@NESTLEVEL에서 반환한 데이터를 나타내는 정수입니다.|29|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|**OwnerName**|**nvarchar**|개체 소유자의 데이터베이스 사용자 이름입니다.|37|예|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SessionLoginName**|**Nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**Success**|**int**|1 = 성공, 0 = 실패. 예를 들어 값 1은 사용 권한 확인이 성공했음을 나타내고, 값 0은 확인이 실패했음을 나타냅니다.|23|예|  
||||||  
||||||  
|**TextData**|**ntext**|DBCC 명령의 SQL 텍스트입니다.|1|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|**XactSequence**|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
  
  
